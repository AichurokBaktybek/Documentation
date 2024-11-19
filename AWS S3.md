--- For open Bucket we need to follow a few steps:
    1. Go to S3 Service in AWS and create a Bucket.
    2. upload an “Hello World” index.html file
    3. for Allow public access only to specific website assets like HTML do next:
     a. Go to Permissions and uncheck Block all public access.
     b. Add a Bucket Policy that only allows public access
     Example: 
     {
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::aichurokbucket/*.html"
    }
  ]
}
    4. Add an Error Document
       -In the bucket settings, go to Properties > Static website hosting.
	   •	Enter error.html in the Error document field.
  	   •	Upload an error.html file in your bucket 
    5. Set Up Security with Bucket Policies and IAM Roles
    6. Create an IAM Role for Restricted Upload/Delete Permissions

	•	Go to IAM > Roles and create a new role.
	•	Attach a policy that allows restricted access, like uploading or deleting only in the /uploads folder.
	•	Example policy for limited access:

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:PutObject",
        "s3:DeleteObject"
      ],
      "Resource": "arn:aws:s3:::aichurokbacket/uploads/*"
    }
  ]
}
    7. Set Up Cross-Region Replication:

	•	Enable Versioning on both the source and destination buckets.
	•	Go to the Management tab in the source bucket and configure Replication to sync objects to the target bucket.
	•	Choose to replicate only specific folders if needed (e.g., /uploads).

8. Implement a Lifecycle Policy for Cost Optimization:
	•	In Management, create a Lifecycle rule.
	•	Set it to move objects to Infrequent Access after 30 days, then to Glacier after 90 days.
	•	Optionally, configure automatic deletion for objects older than 365 days.

9. Integrate CloudFront for HTTPS and CDN:
	•	Go to the CloudFront Console and create a Distribution.
	•	Set your S3 bucket as the Origin.
	•	Enable HTTPS by adding an SSL certificate if needed.
