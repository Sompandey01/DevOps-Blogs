---
title: "Automating Alerts for Manually Created AWS Resources Using Lambda, CloudTrail, and SNS"
datePublished: Thu Jan 30 2025 12:13:45 GMT+0000 (Coordinated Universal Time)
cuid: cm6jar6fm000d09kvhd5x5de4
slug: automating-alerts-for-manually-created-aws-resources-using-lambda-cloudtrail-and-sns
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1738223187861/9dec1284-e9ed-4459-bf19-4293ed3dde6d.png
tags: cloud, aws, projects, devops, devops-articles

---

## **Project Overview:**

Scenario: Your organization decided to only use terraform for the resource creation and if someone manually creates an AWS resource, we want the admins to know about it right away.

In this project, the goal was to notify admins when AWS resources are created manually. I used AWS Lambda, CloudWatch, CloudTrail and SNS to monitor infrastructure and to send real time notiffications when resource are manually created. When a manual creation is detected, admins receive an instant notification. This way, we catch any manual changes and keep everything under control, ensuring our Terraform setup stays intact while admins stay informed.

## Step 1: Set Up CloudTrail to Log Events

1. **Create a Trail**:
    
    * Go to the AWS Management Console → **CloudTrail**.
        
    * Click **Create trail**.
        
    * Name the trail (e.g. `ResourceCreationTrail`).
        
    * Create a new S3 bucket or use the existing one to store the logs.
        
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738237060272/46c02c2e-7f84-491e-adcf-6a809e168c08.png align="center")
    
    * Enable CloudWatch logs.
        
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738237118007/29928b94-18ae-43d3-8e9d-69a44c3cebfe.png align="center")
    
    * Enable both **Management events** and **Data events** for full logging.
        
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738236852998/24d86d04-3f45-45d1-b8c8-95b768193d88.png align="center")
    
2. **Verify Logging**:
    
    * After a few minutes, check the S3 bucket for log files. They will be in JSON format.
        
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738237237417/6bbe0a6c-65b5-4818-bed8-0876a4167f1f.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738237345391/1c1b70f5-18a9-4b39-b90f-fd3442a71291.png align="center")
    

## Step 2: Create an SNS Topic

Amazon SNS (Simple Notification Service) will be used to send notifications to recipients when events occur.

1. Open the **SNS** console.
    
2. Click on **Create topic**.
    
3. Select **Standard** for the topic type.
    
4. Give it a name (e.g. `EC2-Event-Notifications`).
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738237539683/4cadb574-0289-446e-bfe2-5b135ba7b8bf.png align="center")
    
5. Select the topic and create a subscription. choose email and give the email which you wanna use to notify.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738237636618/eb3231c6-67bf-4400-bac2-68a68b91947d.png align="center")
    
6. After creating the topic, note down the ARN (Amazon Resource Name) of the SNS topic.
    

## Step 3: Create a Lambda Function to Handle Events

The core logic of this project lies in an AWS Lambda function that listens for CloudTrail events and sends notifications.

1. Go to the **Lambda** console.
    
2. Click on **Create function** and choose **Author from scratch**.
    
3. Name your function (e.g., `Notify-EC2-Changes`).
    
4. Set the runtime to **Python 3.13**.
    

### Lambda Function Code

```yaml
import boto3
import json

sns_client = boto3.client('sns')
SNS_TOPIC_ARN = 'arn:aws:sns:us-east-1:YOUR_ACCOUNT_ID:EC2-Event-Notifications'  # Replace with your SNS topic ARN

def lambda_handler(event, context):
    try:
        # Parse CloudTrail event
        detail = event['detail']
        event_name = detail.get('eventName', 'Unknown')
        user_agent = detail.get('userAgent', '')
        user = detail.get('userIdentity', {}).get('arn', 'Unknown')
        
        # Check if the event is related to EC2 creation or deletion
        if "RunInstances" in event_name:  # EC2 instance creation
            subject = f"Manual EC2 Creation Detected: {event_name}"
        elif "TerminateInstances" in event_name:  # EC2 instance deletion
            subject = f"Manual EC2 Deletion Detected: {event_name}"
        else:
            subject = f"Manual AWS Event Detected: {event_name}"
        
        body = f"""
        A manual resource event occurred in your AWS account:
        
        - **Event Type**: {event_name}
        - **User**: {user}
        - **UserAgent**: {user_agent}
        - **Time**: {detail.get('eventTime')}
        - **Region**: {detail.get('awsRegion')}
        """
        
        # Send notification via SNS
        sns_client.publish(
            TopicArn=SNS_TOPIC_ARN,
            Message=body,
            Subject=subject,
        )
    except Exception as e:
        print(f"Error: {e}")
        raise e
```

### Explanation of the Code:

1. **SNS Client:** This connects to the SNS service to send notifications.
    
2. **Event Parsing:** We retrieve the event details from CloudTrail and extract critical information like the event name, user agent, and time of the event.
    
3. **Event Type Check:** We check if the event type is related to EC2 instance creation (`RunInstances`) or deletion (`TerminateInstances`).
    
4. **Send SNS Message:** If an event matches, we send an SNS message with details of the event to our previously created SNS topic.
    

## Step 4: Set Up EventBridge to Trigger Lambda

We need to link CloudTrail to our Lambda function. We’ll use **EventBridge** (formerly CloudWatch Events) to trigger our Lambda function based on specific CloudTrail events.

1. Open the **EventBridge** console.
    
2. Create a new **Rule**:
    
    * **Event Source:** Choose `others.`
        
    * **Event Pattern:** Choose **Custom Pattern** and add the following pattern to capture EC2 creation and deletion events:
        

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738237937259/27ba6646-d313-4ccf-bedf-53442598f27e.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738237963435/211efb91-50d3-45ed-b1f8-ecf3db5a65b4.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738238038436/f0063005-fe20-49ba-876f-97dc45b6bc1b.png align="center")

```yaml
{
  "source": ["aws.ec2", "aws.s3", "aws.iam", "aws.dynamodb"],
  "detail": {
    "eventName": ["RunInstances", "CreateBucket", "CreateTable", "CreateUser", "TerminateInstances", "DeleteBucket", "DeleteUser", "DeleteTable"]
  }
}
```

3. In the **Targets** section, choose **Lambda function** and select the Lambda function (`Notify-EC2-Changes`).
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738238100701/ca411079-a636-4370-a3b4-94f673d6e753.png align="center")

3. Enable the rule.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738238157979/70db1e8f-4fac-414a-ae42-4e2f8c6b2cb8.png align="center")

## Step 5: Add Permissions to Lambda

Lambda needs permissions to be triggered by EventBridge and send notifications via SNS. To do this:

1. Open the Lambda function
    
2. Go to **Configuration**, then **permission** and Click on the **Role Name** and add the following permissions:
    
    * **AmazonSNSFullAccess** (for publishing to SNS).
        
    * **AWSLambdaBasicExecutionRole** (for basic Lambda execution permissions).
        
    * **CloudWatchLogsReadOnlyAccess** (for reading CloudTrail logs).
        

## Step 6: Test the Setup

To test the setup:

1. Manually create or terminate an EC2 instance from the AWS console.
    
2. After a few moments, check the SNS topic subscribers (like an email address) to see if you’ve received the notification.
    
3. Let’s test the setup
    

**RunInstances :-**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738238573722/3e5879cc-175b-49db-a2f3-8f3e18982bd4.png align="center")

**TerminateInstances :-**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738238651805/167e34c7-231e-402a-9670-e2d4bd5f0e37.png align="center")

## Conclusion

Congratulations! You've successfully set up an automated notification system to monitor Resource creation and deletion events. To check if this setup is working fine with terraform also, I created a EC2 instance using terraform and as expected, I did not receive any notifications. This confirms that the monitoring solution works perfectly, detecting only manually created resources while allowing Terraform to function as intended.