# create_csv-dynamoDB-to-s3
This project automates the process of exporting data from an AWS DynamoDB table to an S3 bucket in CSV format using AWS Lambda and DynamoDB Streams. Whenever a new record is inserted into DynamoDB, a Lambda function is triggered to process the data, convert it into CSV format, and upload the file to an S3 bucket.
