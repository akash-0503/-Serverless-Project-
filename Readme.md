🟦 Mini Project: S3 Event Trigger → Lambda → DynamoDB 
=
🎯 Objective
=
 
 Build a fully serverless, event-driven data pipeline on AWS that automatically responds to file uploads in an S3 bucket by triggering a Lambda function, which extracts and stores relevant file metadata into a DynamoDB table for logging, tracking, or further processing — all without managing any servers.
## 🧱 Architecture Overview

### 📌 Flow:

1. **User uploads a file** → S3 Bucket  
2. **S3 Event Notification** → Triggers Lambda Function  
3. **Lambda Function** → Extracts metadata and writes to DynamoDB  

---

### 🖼️ Diagram:


<img width="1115" height="416" alt="image" src="https://github.com/user-attachments/assets/7bf56833-e04e-4210-88aa-f23a2c135a2b" />

🎯Benefits of This Architecture 
=
• Serverless – no servers to manage.

• Event-driven – reacts in real time to file uploads.

• Scalable – DynamoDB scales automatically.

• Extensible – you can add file processing logic in Lambda (e.g., virus scan, metadata 
extraction). 


Prerequisites 
=
• AWS account with IAM permissions to create S3, Lambda, and DynamoDB resources.

• Basic knowledge of Python and AWS Lambda. 

