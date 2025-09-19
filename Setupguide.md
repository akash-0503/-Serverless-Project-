step 1 : first we should have the AWS account created or with IAM User you can login.
=
<img width="1920" height="949" alt="Screenshot (11)" src="https://github.com/user-attachments/assets/a3b64a1e-e46e-435b-94e7-15fb8fd83d44" />

Step 2: Create DynamoDB Table 
=

1. Go to DynamoDB → Create Table 
2. Table name: Table-1 
3. Partition key: key-1 (String) 
(You can also add Sort Key if needed) 
4. Keep other settings as default and create table. 
<img width="1892" height="912" alt="image" src="https://github.com/user-attachments/assets/2ea1f685-5a01-46e3-97ee-e647c57a013c" />

Step 3: Create S3 Bucket 
=
1. Go to S3 → Create Bucket 
2. Bucket name: s3-lambda-demo-serverless
3. Block public access → Keep default (enabled) 
4. Create bucket. 
<img width="1895" height="912" alt="image" src="https://github.com/user-attachments/assets/128e21a0-9dcd-4ab0-af9c-3648f42d2592" />

Step 4: Create IAM Role for Lambda 
=
1. Go to IAM → Roles → Create role 
2. Trusted entity: Lambda-role
3. Attach policies: 
   o AmazonS3ReadOnlyAccess 
   o AmazonDynamoDBFullAccess
4. Name role: lambda-role 
<img width="1876" height="925" alt="image" src="https://github.com/user-attachments/assets/2eda0baf-0a07-4982-b329-59e22706d27f" />

Step 5: Create Lambda Function 
=
1. Go to Lambda → Create function 
2. Runtime: Python 3.12 (or latest available) 
3. Execution Role: Select lambda-role
4. Add the following code:
   
    import boto3
   
from uuid import uuid4

def lambda_handler(event, context):

 dynamodb = boto3.resource("dynamodb")
 
dynamo_table = dynamodb.Table("Table-1") # Replace with your DynamoDB table name
 
 for record in event["Records"]:
 
 bucket_name = record["s3"]["bucket"]["s3-lambda-demo-serverless"]
 
 object_key = record["s3"]["object"]["key-1"]
 
 size = record["s3"]["object"].get("size", -1)
 
 event_name = record["eventName"]
 
 event_time = record["eventTime"]
 
 # Insert item into DynamoDB
 
 dynamo_table.put_item(
 
 Item={
 
 "key-1": str(uuid4()), # Ensure this matches DynamoDB PK
 
 "Bucket": s3-lambda-demo-serverless,
 
 "Object": object_key,
 
 "Size": size,
 
 "Event": event_name,
 
 "EventTime": event_time
 
 }
 
 )
 <img width="1892" height="912" alt="image" src="https://github.com/user-attachments/assets/19e1f19f-4a22-4416-8203-0d44179f5886" />

Step 5: Configure S3 Event Notification
=
1. Go to your S3 bucket → Properties 
2. Scroll to Event Notifications → Create event notification 
3. Name: s3-to-lambda 
4. Event types: All object create events (s3:ObjectCreated:*) 
5. Destination: Lambda Function → Select your function 
6. Save changes. 
<img width="1900" height="917" alt="image" src="https://github.com/user-attachments/assets/40a95f90-2150-4998-a257-4379422df4e2" />
<img width="1881" height="907" alt="image" src="https://github.com/user-attachments/assets/1ca9d7ab-62b5-4704-9224-263932b8a9f6" />
<img width="1878" height="911" alt="image" src="https://github.com/user-attachments/assets/0bafbdd2-2a83-4d1b-9512-617b2e3269b4" />
<img width="1872" height="912" alt="image" src="https://github.com/user-attachments/assets/86beff8b-b3c1-41cf-a59e-ac9b37b03bb3" />

Step 6: Test the Setup 
=
1. Upload a file (e.g., test.txt) into your S3 bucket. 
<img width="1897" height="917" alt="image" src="https://github.com/user-attachments/assets/5c4a6ed6-2af9-442f-b0d9-4e71375082d6" />

2. Open DynamoDB → Table-1 → Explore items 

o You should see an entry with file  



