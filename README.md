![image](https://github.com/user-attachments/assets/b3ace866-fd66-4fb7-8327-f26d1717cc62)# Automated-Image-Resizer

## Project Description
This project focuses on building an automated system for image processing and management within the AWS ecosystem. The goal is to streamline the handling of images by automatically resizing them and transferring them to a designated storage location while keeping stakeholders informed through notifications. Key AWS services, such as Lambda, S3, and SNS, are used to orchestrate this workflow.

## Key Features
1. **Image processing automation**: Automatically resize and optimize images upon upload.
2. **Secure storage**: Store processed images in a secure and reliable S3 bucket.
3. **Real-time notifications**: Receive immediate updates about image processing via SNS.
4. **Scalable architecture**: Designed for scalability to handle image processing demands.
5. **Cost-efficient solution**: Leverage AWS serverless technologies to minimize operational costs.

## Overview
![image](https://github.com/user-attachments/assets/135cb1f9-171a-40bd-9a46-747b5755351a)

## Steps

### Step 1: Creating Source and Destination S3 Buckets
1. Navigate to the S3 Console.
   ![image](https://github.com/user-attachments/assets/d4286e39-7df1-466a-9ff8-d9c285f8d37e)
   ![image](https://github.com/user-attachments/assets/b51ce11e-ffc3-4ea7-815a-70f40dd6142c)
   Don't change any other settings, just scroll down and click `Create Bucket`.
   ![image](https://github.com/user-attachments/assets/5b7441f9-ac01-4eeb-bcf9-0455b0010f26)
   ![image](https://github.com/user-attachments/assets/fb9dbbb9-3939-48d4-8c63-9e8d2bc9e24d)

2. Create the destination bucket using the same steps and give it a unique name.
   ![image](https://github.com/user-attachments/assets/f3566e35-985f-4e0c-8028-b0e97c2368c8)

3. As you can see above, I created two buckets: one is the Source bucket, and the other is the Destination bucket.

### Step 2: Creating SNS Topic and Subscription
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

### Step 3: Creating the Lambda Function
1. Navigate to the Lambda Console.
   ![image](https://github.com/user-attachments/assets/956d7f01-bd85-49a7-81fd-7e36ed3a78de)

2. Select "Author from scratch," give the function a name, select Python 3.9, and create the function.
   ![image](https://github.com/user-attachments/assets/10eeb1cd-d528-4317-a298-490fda6517e9)
   ![image](https://github.com/user-attachments/assets/3f7fd0f5-9cbe-4036-af31-7b93b13be80d)

3. Replace the default code with `image-resizing-s3.py` and deploy the changes. Don't test the code now; we have more actions before testing.
   ![image](https://github.com/user-attachments/assets/fa83cb29-f74c-464e-b57f-9fd203221fb4)

4. To grant the Lambda function necessary permissions for resizing, navigate to the IAM Console and follow these steps:
   - Click `Create Policy`
     ![image](https://github.com/user-attachments/assets/9ec622a4-6f1c-4992-bd16-a2fa4a150051)
   - Search for `S3`, check 'All S3 actions', and specify resource ARNs for these actions: `ALL`
     ![image](https://github.com/user-attachments/assets/9fc610d0-d94e-4f03-80cb-d30885435fae)
     ![image](https://github.com/user-attachments/assets/f4c24a4a-743e-4ace-b6e3-dc6a53102ab2)

   - Click `Add more Permissions`
     - Choose `SNS`, check 'All SNS actions', and specify resource ARNs for these actions: `ALL`
       ![image](https://github.com/user-attachments/assets/e9101130-542a-444a-a305-2a1a5e15d02b)

   - Click `Add more Permissions`
     - Choose `Lambda`, actions allowed: `GetLayerVersion`, specify resource ARNs for these actions: `ALL`, and click `Next`
       ![image](https://github.com/user-attachments/assets/0b722092-2632-40ac-bfc6-8f05bf2d1c0b)

   - Add `Policy name` and click `Create Policy`
     ![image](https://github.com/user-attachments/assets/2aaec4ab-f8c7-4193-beaa-72dd5cd3a6c1)

5. Navigate to the Lambda Console and follow these steps:
   - Go to `Configuration` -> `Permissions` and click on the `Role Name`
     ![image](https://github.com/user-attachments/assets/af40f840-d07a-406e-a68a-1111206b624c)
   - Click `Add permission` -> `Attach policies`
     ![image](https://github.com/user-attachments/assets/1e7b95ec-6ee3-4c1a-a1c5-a068894e8a2a)
   - Search for the created policy
     ![image](https://github.com/user-attachments/assets/c9618d63-b444-4a21-9797-4fb770d1232b)
   - Click `Add permission`
     ![image](https://github.com/user-attachments/assets/3a534b4d-2e84-46ed-8e77-dd33b6e905ae)

6. Configure the trigger for the Lambda function:
   - Go to Lambda Console -> `Configuration` -> `Trigger` -> `Add trigger`
     ![image](https://github.com/user-attachments/assets/63a3f342-0be2-46cd-b473-6a4de861d778)
   - Search for `S3`, choose the source bucket, acknowledge, and click `Add`
     ![image](https://github.com/user-attachments/assets/37ac1cb3-0c46-4e1b-a05c-e86186447f7e)
     ![image](https://github.com/user-attachments/assets/966390f6-4270-4a36-8108-ef0f22585f00)

7. Go to the code section, scroll down to `Layers`, and add the layer.
   - Click `Add Layer`
     ![image](https://github.com/user-attachments/assets/c737b764-d5a2-455a-bbc5-37d281961909)
   - Click `Specify an ARN: arn:aws:lambda:us-east-1:770693421928:layer:Klayers-p39-pillow:1`
     ![image](https://github.com/user-attachments/assets/883b566d-7597-4b1e-8676-7f3cb881000f)

8. After done all the actions above , now we can test our code.
   - Lambda -> Functions -> image-resize-function
     ![image](https://github.com/user-attachments/assets/15bb19cf-47a0-4e15-b8c9-cb4d3ed3cba2)
   - Give Event name and Click `Save`
     ![image](https://github.com/user-attachments/assets/6be330c2-22c6-48ed-919b-9853add72f54)
   - It will show some results like below , It runs successfully but return some error because we still not upload the images in S3 yet.
     ![image](https://github.com/user-attachments/assets/6f53c493-c3c8-4e82-8aaa-4221cd3bfe9a)

### Step 4:
 1. Navigate to the S3 Console.
    ![image](https://github.com/user-attachments/assets/224cced9-9e5d-43db-b07d-e9e7d8f11885)
 2. Upload Some images in Source Bucket.
    ![image](https://github.com/user-attachments/assets/30e9cfeb-67ae-4e8c-bd0e-8cc10e790caf)
    ![image](https://github.com/user-attachments/assets/7b848ec0-a15d-40aa-82a8-931200acf67d)

 3. 









