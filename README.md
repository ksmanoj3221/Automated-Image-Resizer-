# Project Description
This project focuses on building an automated system for image processing and management within the AWS ecosystem. The goal is to streamline the handling of images by automatically resizing them and transferring them to a designated storage location while keeping stakeholders informed through notifications. Key AWS services, such as Lambda, S3, and SNS, are used to orchestrate this workflow.

## Key Features
1. **Image Processing Automation**: Automatically resize and optimize images upon upload.
2. **Secure Storage**: Store processed images in a secure and reliable S3 bucket.
3. **Real-Time Notifications**: Receive immediate updates about image processing via SNS.
4. **Scalable Architecture**: Designed for scalability to handle image processing demands.
5. **Cost-Efficient Solution**: Leverage AWS serverless technologies to minimize operational costs.

## Overview
![Project Overview](https://github.com/user-attachments/assets/135cb1f9-171a-40bd-9a46-747b5755351a)

## Steps

### Step 1: Creating Source and Destination S3 Buckets
1. Navigate to the S3 Console.
   ![S3 Console](https://github.com/user-attachments/assets/d4286e39-7df1-466a-9ff8-d9c285f8d37e)
   ![Create Bucket](https://github.com/user-attachments/assets/ecf3976e-ae5e-4af0-98bd-1c80fdf1e2f3)   
   Don't change any other settings, just scroll down and click `Create Bucket`.
   ![Bucket Created](https://github.com/user-attachments/assets/5b7441f9-ac01-4eeb-bcf9-0455b0010f26)
   ![Bucket Settings](https://github.com/user-attachments/assets/fb9dbbb9-3939-48d4-8c63-9e8d2bc9e24d)

2. Create the destination bucket using the same steps and give it a unique name.
   ![Destination Bucket](https://github.com/user-attachments/assets/ab04b2fa-1c9f-4b22-ad31-1be3efb11c85)

3. As shown above, I created two buckets: one as the Source bucket and the other as the Destination bucket.

### Step 2: Creating SNS Topic and Subscription
1. Navigate to the SNS console.
   ![SNS Console](https://github.com/user-attachments/assets/a07b7398-de8a-4469-af3a-e2b93b9da7b3)

2. Click `Create Topic`.
   ![Create Topic](https://github.com/user-attachments/assets/5214c7cd-90aa-4641-b736-32fcd75d0ceb)
   Don't change any other settings, just scroll down and click `Create Topic`.
   ![Topic Created](https://github.com/user-attachments/assets/82b752f8-6eeb-4c35-8270-fbfb526fbd24)

3. Click `Create Subscription`.
   ![Create Subscription](https://github.com/user-attachments/assets/46ea4fc9-8f2e-4b9d-8260-77909ec80d07)
   Select `Email` from `Select Protocol` and enter your email address in the endpoint field.
   ![Email Subscription](https://github.com/user-attachments/assets/db3d47cf-673c-4dea-8e65-bc4a2f415c65)
   Subscription created.
   ![Subscription Confirmation](https://github.com/user-attachments/assets/8c47e1a3-05c7-4e49-b41d-b718b3db6186)

4. Scroll down and click `Create subscription`.

5. You will receive an email to confirm the subscription. Make sure to confirm it.

6. You can use other protocols like SQS, HTTP, SMS, etc.
   ![Other Protocols](https://github.com/user-attachments/assets/d98296cc-41c1-4649-84dd-a91ba8a2532f)
   ![Subscription Options](https://github.com/user-attachments/assets/6bdca488-ae03-4ebc-b1aa-7ca7a23c0d2d)

### Step 3: Creating the Lambda Function
1. Navigate to the Lambda Console.
   ![Lambda Console](https://github.com/user-attachments/assets/956d7f01-bd85-49a7-81fd-7e36ed3a78de)

2. Select "Author from scratch," give the function a name, select Python 3.9, and create the function.
   ![Author from Scratch](https://github.com/user-attachments/assets/10eeb1cd-d528-4317-a298-490fda6517e9)
   ![Function Created](https://github.com/user-attachments/assets/3f7fd0f5-9cbe-4036-af31-7b93b13be80d)

3. Replace the default code with `image-resizing-s3.py` and deploy the changes. We will test the code after completing the remaining steps.
   ![Replace Code](https://github.com/user-attachments/assets/fa83cb29-f74c-464e-b57f-9fd203221fb4)

4. To grant the Lambda function necessary permissions for resizing, navigate to the IAM Console and follow these steps:
   - Click `Create Policy`
     ![Create Policy](https://github.com/user-attachments/assets/9ec622a4-6f1c-4992-bd16-a2fa4a150051)
   - Search for `S3`, check 'All S3 actions', and specify resource ARNs for these actions: `ALL`
     ![S3 Permissions](https://github.com/user-attachments/assets/9fc610d0-d94e-4f03-80cb-d30885435fae)
     ![Add More Permissions](https://github.com/user-attachments/assets/f4c24a4a-743e-4ace-b6e3-dc6a53102ab2)

   - Click `Add more Permissions`
     - Choose `SNS`, check 'All SNS actions', and specify resource ARNs for these actions: `ALL`
       ![SNS Permissions](https://github.com/user-attachments/assets/e9101130-542a-444a-a305-2a1a5e15d02b)

   - Click `Add more Permissions`
     - Choose `Lambda`, actions allowed: `GetLayerVersion`, specify resource ARNs for these actions: `ALL`, and click `Next`
       ![Lambda Permissions](https://github.com/user-attachments/assets/0b722092-2632-40ac-bfc6-8f05bf2d1c0b)

   - Add a `Policy name` and click `Create Policy`
     ![Policy Created](https://github.com/user-attachments/assets/2aaec4ab-f8c7-4193-beaa-72dd5cd3a6c1)

5. Navigate to the Lambda Console and follow these steps:
   - Go to `Configuration` -> `Permissions` and click on the `Role Name`
     ![Role Name](https://github.com/user-attachments/assets/af40f840-d07a-406e-a68a-1111206b624c)
   - Click `Add permission` -> `Attach policies`
     ![Attach Policies](https://github.com/user-attachments/assets/1e7b95ec-6ee3-4c1a-a1c5-a068894e8a2a)
   - Search for the created policy
     ![Search Policy](https://github.com/user-attachments/assets/c9618d63-b444-4a21-9797-4fb770d1232b)
   - Click `Add permission`
     ![Add Permission](https://github.com/user-attachments/assets/3a534b4d-2e84-46ed-8e77-dd33b6e905ae)

6. Configure the trigger for the Lambda function:
   - Go to Lambda Console -> `Configuration` -> `Trigger` -> `Add trigger`
     ![Add Trigger](https://github.com/user-attachments/assets/63a3f342-0be2-46cd-b473-6a4de861d778)
   - Search for `S3`, choose the source bucket, acknowledge, and click `Add`
     ![Configure Trigger](https://github.com/user-attachments/assets/37ac1cb3-0c46-4e1b-a05c-e86186447f7e)
     ![Trigger Added](https://github.com/user-attachments/assets/966390f6-4270-4a36-8108-ef0f22585f00)

7. Go to the code section, scroll down to `Layers`, and add the layer.
   - Click `Add Layer`
     ![Add Layer](https://github.com/user-attachments/assets/c737b764-d5a2-455a-bbc5-37d281961909)
   - Click `Specify an ARN: arn:aws:lambda:us-east-1:770693421928:layer:Klayers-p39-pillow:1`
     ![Layer ARN](https://github.com/user-attachments/assets/883b566d-7597-4b1e-8676-7f3cb881000f)

8. After done all the actions above , now we can test our code.
   - Lambda -> Functions -> image-resize-function
     ![image](https://github.com/user-attachments/assets/15bb19cf-47a0-4e15-b8c9-cb4d3ed3cba2)
   - Give Event name and Click `Save`
     ![image](https://github.com/user-attachments/assets/6be330c2-22c6-48ed-919b-9853add72f54)
   - It will show some results like below , It runs successfully but return some error because we still not upload the images in S3 yet.
     ![image](https://github.com/user-attachments/assets/6f53c493-c3c8-4e82-8aaa-4221cd3bfe9a)

### Step 4: Testing the Workflow
1. Navigate to the S3 Console.
    ![image](https://github.com/user-attachments/assets/224cced9-9e5d-43db-b07d-e9e7d8f11885)
 2. Upload Some images in Source Bucket.
    ![image](https://github.com/user-attachments/assets/30e9cfeb-67ae-4e8c-bd0e-8cc10e790caf)
    ![image](https://github.com/user-attachments/assets/7b848ec0-a15d-40aa-82a8-931200acf67d)

 3. Open Destination Bucket
    - You can see that automatically new folder is created and inside this folder we can find our resized image
      ![image](https://github.com/user-attachments/assets/4e3c2a4b-f218-4ce6-aa2b-5b67b149b4d1)

    - Initially size was 108.4 kb
      ![image](https://github.com/user-attachments/assets/5b1671bd-2fd0-4e6b-be2a-f27a6661419f)
   
    - It changed to 77.1 kb
      ![image](https://github.com/user-attachments/assets/0933350e-b4be-47f1-9e8d-be772bc01310)


4. Confirm that you receive an email notification about the processing event.
   ![Email Notification](https://github.com/user-attachments/assets/7ea0f209-6580-44e6-b251-1121070551ad)

## Conclusion
The AWS-based image processing and management system has been successfully implemented. This setup ensures automated handling, secure storage, real-time notifications, and scalability. Ensure to test the workflow thoroughly and adjust the configurations as needed for your specific use case.

