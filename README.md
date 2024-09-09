# Automated-Image-Resizer-
## Project Description:
This project focuses on building an automated system for image processing and management within the AWS ecosystem. The goal is to streamline the handling of images by automatically resizing them and transferring them to a designated storage location while keeping stakeholders informed through notifications. Key AWS services, such as Lambda, S3, and SNS, are used to orchestrate this workflow.

## Key Features:
1. Image processing automation: Automatically resize and optimize images upon upload.
2. Secure storage: Store processed images in a secure and reliable S3 bucket.
3. Real-time notifications: Receive immediate updates about image processing via SNS.
4. Scalable architecture: Designed for scalability to handle image processing demands.
5. Cost-efficient solution: Leverage AWS serverless technologies to minimize operational costs.

## Overview
![image](https://github.com/user-attachments/assets/135cb1f9-171a-40bd-9a46-747b5755351a)

## Steps
### Step 1
Creating Source and Destination S3 Buckets:
1. Navigate to the S3 Console.
2. Click `Create Bucket`.
   ![image](https://github.com/user-attachments/assets/d4286e39-7df1-466a-9ff8-d9c285f8d37e)
   ![image](https://github.com/user-attachments/assets/b51ce11e-ffc3-4ea7-815a-70f40dd6142c)
   Don't change any other settings, just scroll down and click `Create Bucket`.
   ![image](https://github.com/user-attachments/assets/5b7441f9-ac01-4eeb-bcf9-0455b0010f26)
   ![image](https://github.com/user-attachments/assets/fb9dbbb9-3939-48d4-8c63-9e8d2bc9e24d)

3. Create the destination bucket using the same steps and give it a unique name.
   ![image](https://github.com/user-attachments/assets/f3566e35-985f-4e0c-8028-b0e97c2368c8)

4. As you can see above, I created two buckets: one is the Source bucket, and the other is the Destination bucket.

### Step 2
1. Navigate to the SNS console.  
   ![image](https://github.com/user-attachments/assets/a07b7398-de8a-4469-af3a-e2b93b9da7b3)
   
2. Click `Create Topic`.  
   ![image](https://github.com/user-attachments/assets/5214c7cd-90aa-4641-b736-32fcd75d0ceb)  
   Don't change any other settings, just scroll down and click `Create Topic`.  
   ![image](https://github.com/user-attachments/assets/82b752f8-6eeb-4c35-8270-fbfb526fbd24)
   
3. Click `Create subscription`.  
   ![image](https://github.com/user-attachments/assets/46ea4fc9-8f2e-4b9d-8260-77909ec80d07)  
   Click on `Select Protocol` and choose `Email`.  
   ![image](https://github.com/user-attachments/assets/db3d47cf-673c-4dea-8e65-bc4a2f415c65)  
   Use your email address in the endpoint field.  
   ![image](https://github.com/user-attachments/assets/8c47e1a3-05c7-4e49-b41d-b718b3db6186)  
   Subscription created.  
   ![image](https://github.com/user-attachments/assets/fece93ba-4e0f-4149-9ca3-5392320bd1bb)

4. Scroll down and click `Create subscription`.

5. After this, you will receive an email for subscription confirmation. Make sure to confirm the subscription.

6. You can use other protocols like SQS, HTTP, SMS, etc.  
   ![image](https://github.com/user-attachments/assets/d98296cc-41c1-4649-84dd-a91ba8a2532f)  
   ![image](https://github.com/user-attachments/assets/6bdca488-ae03-4ebc-b1aa-7ca7a23c0d2d)








   
