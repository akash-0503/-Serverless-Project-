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

![Architecture Diagram](./c6cb2ebb-9527-4b54-8db7-67e18b881ade.png)
