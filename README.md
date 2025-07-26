# url-shortener-project
Serverless URL Shortener with Click Analytics
 # A Recorded video demonstrating the deployed solution :
https://drive.google.com/drive/folders/1vyt-YTwuDNBvcfJoVCl5OlisZ30Bb22r?usp=sharing

# Project Description:
A fully serverless URL shortener built with AWS Lambda, API Gateway, DynamoDB, and S3. It allows users to generate shortened links and track click activity with logs.

# Key Features:
✅ Shorten any valid URL

📊 Tracks number of clicks

🗂 Logs IP address, user-agent, timestamp

☁️ Uses S3 to host redirect pages and optionally store logs

🔐 Fully serverless and scalable with IAM-based security

# AWS Services Used:
Service	Purpose
Lambda	Backend logic
API Gateway	Expose RESTful endpoints
DynamoDB	Store URL mappings and click logs
S3	Host HTML redirect & log JSON files
IAM	Grant least-privilege access
CloudWatch	Log monitoring for Lambdas

Lambda Code:
ShortURLDB (shorten URL):
Validates input

Generates short ID

Uploads redirect HTML to S3

Saves mapping in UrlShortener

HitCount (track clicks):
Looks up long URL from UrlShortener

Increments clicks atomically

Logs access to UrlClickLogs and S3

Redirects user to long URL

Deployment Steps:
Create the required DynamoDB tables

Deploy Lambda functions

Create API Gateway routes

Configure S3 bucket with public access for redirect
