# Automated-Image-Resizer-
## Project Description:
This project focuses on building an automated system for image processing and management within the AWS ecosystem. The goal is to streamline the handling of images by automatically resizing them and transferring them to a designated storage location while keeping stakeholders informed through notifications. Key AWS services, such as Lambda, S3, and SNS, are used to orchestrate this workflow.
## Key Features:
1. Image processing automation: Automatically resize and optimize images upon upload.
2. Secure storage: Store processed images in a secure and reliable S3 bucket.
3. Real-time notifications: Receive immediate updates about image processing via SNS.
4. Scalable architecture: Design for scalability to handle image processing demands.
5. Cost-efficient solution: Leverage AWS serverless technologies to minimize operational costs.
## Overview
![image](https://github.com/user-attachments/assets/135cb1f9-171a-40bd-9a46-747b5755351a)
## Steps
### Step 1
Creating Source and Designation s3 Buckets :
  1. Navigate to the S3 Console.
  2. Create Bucket
![image](https://github.com/user-attachments/assets/d4286e39-7df1-466a-9ff8-d9c285f8d37e)
![image](https://github.com/user-attachments/assets/b51ce11e-ffc3-4ea7-815a-70f40dd6142c)
Don't change any other settings, just scroll down and click `Create Bucket`.
![image](https://github.com/user-attachments/assets/5b7441f9-ac01-4eeb-bcf9-0455b0010f26)
![image](https://github.com/user-attachments/assets/fb9dbbb9-3939-48d4-8c63-9e8d2bc9e24d)
  3.Create the destination bucket using the same steps and name it with a unique name.
![image](https://github.com/user-attachments/assets/f3566e35-985f-4e0c-8028-b0e97c2368c8)
  4.As you can see above , I created two buckets one is Source bucket and another one is Destination bucket.


