# cloudlaunch-aws

CloudLaunch AWS Deployment
📌 Project Overview

This project demonstrates deploying a lightweight product, CloudLaunch, on AWS. It consists of:

Task 1: Hosting a static website on S3.

Task 2: Designing a secure VPC layout with strict IAM permissions.

The goal was to show AWS fundamentals in action — S3, IAM, and VPC — with restricted access controls.

📝 Task 1 – S3 Static Website Hosting

Created an S3 bucket (cloudlaunch-site-buckettt) with static website hosting enabled.

Uploaded static files (HTML, CSS, JS).

Configured bucket policy for public read access (only for website content).

🔗 S3 Website URL: http://cloudlaunch-site-buckettt.s3-website-eu-west-1.amazonaws.com

🔗 CloudFront URL: d2uqgs7muxm3jf.cloudfront.net

📝 Task 2 – VPC Network Setup

VPC with CIDR 10.0.0.0/16.

Subnets: 1 Public + 1 Private.

Route Table: Public subnet routes internet traffic via Internet Gateway.

Security Group Rule Example:

Inbound HTTP (80) allowed from within VPC CIDR 10.0.0.0/16.

🔐 IAM Configuration

Created IAM user: cloudlaunch-user

Permissions: Read-only access to VPC components only (VPCs, Subnets, Route Tables, Security Groups).

Enforced password reset on first login.

📄 IAM Policy File: cloudlaunch-user-policy.json

Policy allows:

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "ec2:DescribeVpcs",
        "ec2:DescribeVpcAttribute",
        "ec2:DescribeSubnets",
        "ec2:DescribeRouteTables",
        "ec2:DescribeSecurityGroups"
      ],
      "Resource": "*"
    }
  ]
}

🔑 Console Access Details

Console URL:  https://samuel232.signin.aws.amazon.com/console

Account ID / Alias: samuel232

IAM Username: cloudlaunch-user

Password: 

