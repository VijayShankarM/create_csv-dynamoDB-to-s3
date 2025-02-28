# DynamoDB to S3 Data Export

## Overview
This project sets up an AWS pipeline that automatically exports data from DynamoDB to an S3 bucket in CSV format using AWS Lambda and DynamoDB Streams.

## Step 1: Setup AWS Services
- **DynamoDB** → Stores structured data
- **DynamoDB Streams** → Triggers Lambda on new records
- **AWS Lambda** → Converts data to CSV and uploads to S3
- **S3** → Stores the generated CSV files

## Step 2: Create an S3 Bucket
1. Go to AWS S3 Console → Click **Create Bucket**
2. Enter a unique **Bucket Name** (e.g., `dynamodb-to-s3-bucket`)
3. Select **Region** (close to your location)
4. **Block Public Access** → Keep all options enabled (for security)
5. Click **Create bucket**

## Step 3: Create a DynamoDB Table
1. Go to AWS DynamoDB Console → Click **Create Table**
2. Enter the following details:
   - **Table Name**: `CSVData`
   - **Partition Key**: `id` (String)
3. Click **Create table**

## Step 4: Enable DynamoDB Streams
1. Open **CSVData Table** → Click **Exports and streams**
2. Under **DynamoDB Streams**, click **Enable Stream**
3. Select **New and Old Images**
4. Copy the **Stream ARN** (needed for later steps)

## Step 5: Create an AWS Lambda Function
1. Go to **AWS Lambda Console** → Click **Create function**
2. Select **Author from scratch**
3. Enter:
   - **Function Name**: `DynamoDBToS3Processor`
   - **Runtime**: Python 3.x
   - **Permissions**: Create a new role with basic Lambda permissions
4. Click **Create function**

## Step 6: Attach DynamoDB Stream as Lambda Trigger
1. Open **DynamoDBToS3Processor** function → Go to **Triggers**
2. Click **Add trigger**
3. Select **DynamoDB**
4. Choose **CSVData Table**
5. Paste the **Stream ARN** (copied earlier)
6. Set **Batch size**: `100`
7. Click **Add**

## Step 7: Write and Deploy the Lambda Function
1. Open **DynamoDBToS3Processor** → Go to **Code**
2. Replace existing code with the Python script
3. Click **Deploy**

## Step 8: Update IAM Role for Lambda
1. Go to **AWS IAM Console** → Click **Roles**
2. Find the **Lambda Execution Role**
3. Click **Attach Policies** → Search and attach:
   - `AmazonDynamoDBFullAccess`
   - `AmazonS3FullAccess`
4. Click **Save changes**

## Step 9: Test the Process
1. **Insert Data into DynamoDB**
   - Go to **DynamoDB Console** → Open **CSVData Table**
   - Click **Explore Table Items** → **Create Item**
   - Add sample data
   - Click **Save**

## Step 10: Verify the CSV File in S3
1. Go to **AWS S3 Console** → Open `dynamodb-to-s3-bucket`
2. Check for the CSV file

✅ **The pipeline is now fully functional!** 🎉

