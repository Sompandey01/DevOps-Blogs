---
title: "Project 2: Host a static website using AWS S3 bucket."
datePublished: Thu Feb 15 2024 10:04:37 GMT+0000 (Coordinated Universal Time)
cuid: clsn20ygi00040alchh28g8u1
slug: project-2-host-a-static-website-using-aws-s3-bucket
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1707991416921/2ddf2efb-d9fd-4b42-9d3e-6bf8a59fb4be.jpeg
tags: aws, projects, devops, 90daysofdevops, trainwithshubham

---

The project aims to host a static website using AWS S3, an object storage service known for its simplicity and scalability. Website files will be uploaded to an S3 bucket and configured for static website functionality. With appropriate permissions and a unique domain name, the website becomes publicly accessible. Leveraging AWS S3 ensures a cost-effective and scalable solution for hosting static websites. 🌐🚀

* In the AWS management console, Create an Amazon S3 bucket service.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1707989847867/bf636c2a-6fb7-4175-ac92-ed8731571b0c.png align="center")

* Now, Choose a unique bucket name and select a region
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1707990211466/f6efac0b-ef92-4a6a-bc22-dd8bfd89be8a.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1707989993428/b8066232-cfe4-4459-b375-f9cee38ac2f9.png align="center")

* Enable the Bucket versioning
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1707990032188/d38477e5-d143-492c-b6d1-42ade8a34aa6.png align="center")

* Click on Create a bucket
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1707990095979/275c6a80-6d40-4e21-93cf-017df3a3abd7.png align="center")

* The bucket is successfully created.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1707990227609/a1402813-f6db-44bc-b6b2-c83b7f39ad0f.png align="center")

* Once your bucket is created, upload your website files to the bucket. Click on ‘Upload’
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1707990267082/9d67a434-4b5a-4c1f-a168-234d04613212.png align="center")

* Click on ‘Add files’ to add website files.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1707990297192/cb5db14c-17b3-4cf3-8888-f954c3c59ed3.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1707990758859/7f23d181-0d68-47bf-b2db-f980dc6af328.png align="center")

* Go to the “Properties” tab and Scroll down to the bottom and Edit “Static Website Hosting”.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1707990827493/294571fc-6cc1-4878-a7b4-6a86de23f635.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1707990856365/8ee56798-8bc6-4ff0-b3cf-d69ef9417ce5.png align="center")

* Enable Static website hosting. Set the “Index Document” to “index.html”
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1707990940072/4c5b12a3-9775-44d1-9d30-01c98ea55625.png align="center")

* Save the changes
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1707990981845/1d198282-9f9d-442d-a41a-15c22e876009.png align="center")

* Set the bucket permissions to allow public access to your website. Go to the “Permissions” tab and click on “Bucket Policy” and edit
    

```yaml
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": [
                "s3:GetObject"
            ],
            "Resource": [
                "arn:aws:s3:::Bucket-Name/*"
            ]
        }
    ]
}
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1707991150357/aed77f20-cff0-44e2-8079-dc960345673c.png align="center")

* Browse the bucket website URL. You should now be able to access your static website using the bucket’s URL.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1707991210716/7a5b7189-d0a0-42ea-8cb7-fff57e1c21f6.png align="center")

---

Thank you for enjoying my DevOps blog! Your positive response fuels my passion to dive deeper into technology and innovation.

Stay tuned for more captivating DevOps articles, where we'll explore this dynamic field together. Follow me on **Hashnode** and connect on **LinkedIn** ([https://www.linkedin.com/in/som-shanker-pandey/](https://www.linkedin.com/in/som-shanker-pandey-a76b41251/)) for the latest updates and discussions.