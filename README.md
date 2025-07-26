<img width="1536" height="1024" alt="ChatGPT Image Jul 26, 2025, 10_24_57 AM" src="https://github.com/user-attachments/assets/5c332807-6ec6-4eb4-8002-4214417a6388" /><img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/e027212f-aeee-40d4-807f-6c0c1003dade" /># url-shortener-project
Serverless URL Shortener with Click Analytics
 # A Recorded video demonstrating the deployed solution :
https://drive.google.com/drive/folders/1vyt-YTwuDNBvcfJoVCl5OlisZ30Bb22r?usp=sharing

# Project Description:
A fully serverless URL shortener built with AWS Lambda, API Gateway, DynamoDB, and S3. It allows users to generate shortened links and track click activity with logs.

# Architecture Diagram
<img width="1536" height="1024" alt="diagram" src="https://github.com/user-attachments/assets/5fb13569-a76c-4d45-a5fa-c49670de408c" />

# 📌 Overview:
The architecture allows users to:

Generate a short URL from a long one.

Track clicks, IPs, user agents, and timestamps.

Store everything in DynamoDB and S3.

Use only serverless AWS services (cost-effective, scalable).

# 🔁 1. /shorten – Create Short URL Flow
Step-by-step:

Client sends a POST request to POST /shorten via API Gateway.

API Gateway triggers the Lambda function (ShortURLDB) for URL shortening.

The Lambda function:

Generates a short_id (e.g., abc123)

Creates a redirect HTML file

Saves this file to an S3 bucket (e.g., buraq-shorten-url) using the short_id as the filename.

Stores the mapping (short_id, long_url, clicks) in DynamoDB table UrlShortener.

It returns a JSON response with:

short_url (to S3 redirect)

click_url (tracks clicks and redirects)

debug_url (raw HTML on S3)

# 📥 2. /{short_id} – Redirect and Track Flow
When someone clicks a shortened URL:

Client visits a GET route like GET /abc123 → sent to API Gateway.

API Gateway triggers another Lambda function (HitCount).

That Lambda function:

Looks up the short_id in DynamoDB (UrlShortener)

Increments the clicks count

Collects metadata (IP address, User-Agent, timestamp)

Writes a click log entry to a second table: UrlClickLogs

Also uploads the log file to S3 for redundancy and inspection

Finally, it sends a 302 redirect response to the original long URL.

# 🧱 AWS Services Used
Service	Purpose
API Gateway	Exposes HTTP endpoints for URL actions
Lambda	Stateless backend logic for create/track
DynamoDB	NoSQL database to store URLs and logs
S3	Hosts redirect HTML files & optional logs
IAM	Secures access between services

# Key Features:
✅ Shorten any valid URL

📊 Tracks number of clicks

🗂 Logs IP address, user-agent, timestamp

☁️ Uses S3 to host redirect pages and optionally store logs

🔐 Fully serverless and scalable with IAM-based security

Logs and S3

Redirects user to long URL

Deployment Steps:
Create the required DynamoDB tables

Deploy Lambda functions

Create API Gateway routes

Configure S3 bucket with public access for redirect
