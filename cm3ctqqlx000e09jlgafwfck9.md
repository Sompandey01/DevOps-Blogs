---
title: "A Complete Guide to Automating AWS Key Rotation and GitLab Integration Using Lambda"
datePublished: Mon Nov 11 2024 09:31:47 GMT+0000 (Coordinated Universal Time)
cuid: cm3ctqqlx000e09jlgafwfck9
slug: a-complete-guide-to-automating-aws-key-rotation-and-gitlab-integration-using-lambda
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1731317426327/1e43a3cb-1474-4a51-afe8-c6cb08da96b2.png
tags: aws, devops, gitlab, aws-lambda, devops-articles

---

### Introduction:

When managing the AWS Credentials for project in Gitlab, keeping them secure is very important. One way to improve security is by regularly rotating (changing) the keys. However, doing it manually can be time consuming. What if I tell you we can automate this, sounds interesting right? This guide will show you how to automate AWS access keys using AWS lambda and update it automatically in Gitlab. This setup will create new keys, update it directly in Gitlab and delete the old keys regularly.

### Step 1: Set Up an IAM User in AWS

1. **Log in to the AWS Management Console** and navigate to **IAM (Identity and Access Management)**.
    
2. Create a **new IAM user** with **programmatic access** (or use an existing one).
    
3. **Attach Policies:**
    
    * **IAM Policy:** Grants permissions such as `iam:CreateAccessKey`, `iam:DeleteAccessKey`, `iam:ListAccessKeys`, and `iam:UpdateAccessKey` to make it more easy just use `IAMFullAccess`.
        
    * **Secrets Manager Policy:** Grants permissions like
        
        `SecretsManagerReadWrite` for accessing the stored secrets.
        
4. **Create the Access Keys** using Third-party service.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1731309280017/805ab250-f297-4460-b40e-39452f145b6e.png align="center")
    
5. **Save the Access Keys (Access Key ID and Secret Access Key)** temporarily; these will be replaced through automation later.
    
6. **Setup the variables in Group or Project Level in Gitlab** will update the keys automatically later.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1731308838567/2bc78a21-5c27-4067-9c68-e72151752b43.png align="center")

<mark>Note:-</mark> If you already have an IAM user whose access keys you have defined in your Gitlab variables then attach the policies to that user only.

### Step 2: Create a GitLab API Token

1. Go to **GitLab Profile Settings &gt; Access Tokens**.
    
2. **Create a personal access token** with the **API scope** so it can update group-level variables.
    
3. **Copy the token** and save it in AWS Secrets Manager (it will be needed for the Lambda function).
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1731309027303/1dded489-e738-47f9-8c56-75f5e7793db9.png align="center")

### Step 3: Store Secrets in AWS Secrets Manager

1. Go to **AWS Secrets Manager** and create a new secret with the following key-value pairs:
    
    * `GITLAB_TOKEN`: Your GitLab API token with permissions to update group-level variables.
        
    * `GITLAB_GROUP_ID`: The ID of the GitLab group where AWS keys will be stored.
        
    * `AWS_IAM_USER`: The IAM username whose access keys will be rotated.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1731309616527/92812720-0483-4546-bfcf-019b5bea0ee7.png align="center")
        
2. Name the secret (e.g., `gitlab-key-rotation-secrets`) and save it. This name will be used in the Lambda function.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1731310498332/a8ec807d-d798-4574-a4a2-ae0dc71e6103.png align="center")
    

### Step 4: Set Up AWS Lambda

* 1. Go to **AWS Lambda** and create a new function:
        
        * **Runtime:** Python 3.9 or later.
            
        * **Permissions:** Attach an execution role to the Lambda function that includes:
            
            * IAM permissions to rotate keys.
                
            * Secrets Manager permissions to access secrets.
                
    2. **Name the function** (e.g., `rotate-aws-keys`).
        

### Step 5: Write the Lambda Function Code

Replace the Lambda function code with the following script. This code automates AWS key creation, updates GitLab’s group-level environment variables, and deletes old keys.

```yaml
import boto3
import requests
import json

# Initialize AWS clients
iam = boto3.client('iam')
secrets_client = boto3.client('secretsmanager')

# Function to retrieve secrets from Secrets Manager
def get_secret():
    secret_name = "gitlab-key-rotation-secrets"  # Replace with your actual secret name
    response = secrets_client.get_secret_value(SecretId=secret_name)
    secret = json.loads(response['SecretString'])
    return secret

# Main function to rotate AWS access keys
def rotate_aws_keys(event, context):
    # Retrieve GitLab secrets from Secrets Manager
    secrets = get_secret()
    GITLAB_TOKEN = secrets['GITLAB_TOKEN']
    GITLAB_GROUP_ID = secrets['GITLAB_GROUP_ID']
    AWS_IAM_USER = secrets['AWS_IAM_USER']
    
    # Step 1: Create a new access key for the IAM user
    new_key = iam.create_access_key(UserName=AWS_IAM_USER)['AccessKey']
    new_access_key = new_key['AccessKeyId']
    new_secret_key = new_key['SecretAccessKey']
    print("New AWS Access Key Created.")

    # Step 2: Update GitLab group-level variables with the new access key
    gitlab_api_url = f"https://gitlab.com/api/v4/groups/{GITLAB_GROUP_ID}/variables"
    
    # Update AWS_ACCESS_KEY_ID in GitLab group variables
    requests.put(
        f"{gitlab_api_url}/AWS_ACCESS_KEY_ID",
        headers={'PRIVATE-TOKEN': GITLAB_TOKEN},
        data={'value': new_access_key}
    )

    # Update AWS_SECRET_ACCESS_KEY in GitLab group variables
    requests.put(
        f"{gitlab_api_url}/AWS_SECRET_ACCESS_KEY",
        headers={'PRIVATE-TOKEN': GITLAB_TOKEN},
        data={'value': new_secret_key}
    )
    print("Updated GitLab group-level variables with new AWS keys.")

    # Step 3: List existing keys and delete the old key
    access_keys = iam.list_access_keys(UserName=AWS_IAM_USER)['AccessKeyMetadata']
    for key in access_keys:
        if key['AccessKeyId'] != new_access_key:
            iam.update_access_key(
                UserName=AWS_IAM_USER,
                AccessKeyId=key['AccessKeyId'],
                Status='Icnative'
            )
            iam.delete_access_key(UserName=AWS_IAM_USER, AccessKeyId=key['AccessKeyId'])
            print(f"Old AWS Access Key {key['AccessKeyId']} has been deleted.")

# Entry point for AWS Lambda
def lambda_handler(event, context):
    rotate_aws_keys(event, context)
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1731311198695/31e53861-eeff-46f2-9a2a-1fc64a37ed69.png align="center")

### Step 6: Add Dependencies (Optional)

If the **requests** library is not available in Lambda by default, package it as a Lambda Layer or include it in a deployment package alongside the Lambda function code.

In my case I faced the error regarding the requests module, Lambda was not able to find the `requests` module. How I solved it?? Created new dir installed the python requests in it and zip it.

```yaml
mkdir python
pip install requests -t python/
zip -r requests_layer.zip python
```

Then created a new layer in Lambda and uploaded the zip file and it solved the problem.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1731311068237/8ebb4e20-705d-4b0a-9320-516aefccb4ce.png align="center")

### Step 7: Test the Lambda Function

1. Create a sample test event in **AWS Lambda** with default settings.
    
2. **Run the function** and check:
    
    * **CloudWatch Logs** for any errors or messages confirming that AWS access keys were rotated.
        
    * **GitLab group-level CI/CD variables** page to ensure `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` were updated correctly.
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1731312802285/8226cb1a-0359-4822-b481-7273292a4c62.png align="center")
        
    * Old AWS Access Key `AKIA23WHUE7PVQDM4R43` has been deleted and new keys are created as well as automatically updated in the Gitlab Variables.
        
3. ### Previous Access and Secret Access Keys :-
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1731312624993/8865a21c-aae6-4aae-9085-107adaa105fc.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1731312920463/c93f477f-38df-45c4-8a4c-504f9c7915aa.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1731312967934/c0a10a35-7e6f-4364-9b2a-00380b1e57a8.png align="center")
    
4. ### New Access and Secret Access Keys :-
    
    Refresh the IAM and Gitlab variables page and see the magic.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1731313096440/db8cb34b-95fc-4383-8e00-cd17ad6aee0a.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1731313161655/f9f7fbf0-61e7-4870-8461-6de894779a46.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1731313198563/520280f3-5ea7-4416-9b69-0e4e8732c92c.png align="center")
    
    **Let’s delete it and update it again**
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1731313293728/eb150d53-b23a-4bbd-bf16-1eeacfffa63d.png align="center")
    
    Old AWS Access Key `AKIA23WHUE7PWS5DMVRZ` has been deleted. There’s a problem we still haven’t automated it fully yet there’s still manual work of starting the test case. So, let’s automate it also using AWS CloudWatch Events. Let’s gooooooo
    

### Step 8: Automate with AWS CloudWatch Events

1. Go to **CloudWatch Events** and create a rule to trigger the Lambda function periodically (e.g., every month).
    
2. Choose **Cron expression** and specify the frequency.
    
3. Select **Lambda function** as the target and choose the Lambda function you created.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1731313827004/b7a6170f-9a45-4bb8-890d-9b20610da6f9.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1731314200800/8d07ca3f-1736-4419-8f91-7fda5459b191.png align="center")

Set the Cron according to your need I set up for every 3 mins just for demo.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1731314610154/fa163028-43ff-43e9-854f-883c26d41e11.png align="center")

### Test and Monitor the Automation

Monitor the Lambda function’s CloudWatch logs to confirm that it runs successfully on the schedule you set.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1731315071285/d2275386-0eff-4ce7-8488-22eac516471c.png align="center")

It successfully created new keys and updated it in the GitlabVariables.

### Summary

This setup automatically rotates AWS IAM keys and updates the group-level GitLab environment variables regularly, ensuring all projects within the GitLab group have access to up-to-date credentials. Automating this process enhances security by rotating sensitive access keys periodically and reduces the need for manual updates.