# **cloudlaunch-aws**

CloudLaunch AWS Deployment

📌 Project Overview

This project demonstrates deploying a lightweight product, CloudLaunch, on AWS. It consists of:

**Task 1: Static Website Hosting Using S3 + IAM User with Limited Permissions**

S3 Buckets

**cloudlaunch-site-buckettt**

Hosts a simple static website (index.html, styles.css, script.js).

Enabled static website hosting.

Configured for public read-only access.

CloudFront for HTTPS and caching.

**cloudlaunch-private-buckettt**

Private bucket.

IAM user (cloudlaunch-user) has GetObject/PutObject permissions only (no delete).

**cloudlaunch-visible-only-buckettt**

Private bucket.

IAM user can ListBucket, but cannot read objects.

IAM User – cloudlaunch-user

Permissions:

ListBucket on all three buckets.

GetObject on cloudlaunch-site-buckettt.

GetObject + PutObject on cloudlaunch-private-buckettt.

No delete permission anywhere.

No object access to cloudlaunch-visible-only-buckettt.



Custom IAM Policy:
cloudlaunch-user
<img width="1912" height="864" alt="image" src="https://github.com/user-attachments/assets/b4c61a11-71fc-4081-8107-ceff1285f935" />



{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "s3:ListAllMyBuckets"
            ],
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "s3:ListBucket"
            ],
            "Resource": [
                "arn:aws:s3:::cloudlaunch-site-buckettt",
                "arn:aws:s3:::cloudlaunch-private-buckettt",
                "arn:aws:s3:::cloudlaunch-visible-only-buckettt"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "s3:GetObject"
            ],
            "Resource": "arn:aws:s3:::cloudlaunch-site-buckettt/*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "s3:GetObject",
                "s3:PutObject"
            ],
            "Resource": "arn:aws:s3:::cloudlaunch-private-buckettt/*"
        },
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

Static Website Link

S3 Website URL:
http://cloudlaunch-site-buckettt.s3-website-eu-west-1.amazonaws.com


 CloudFront URL:
https://d2uqgs7muxm3jf.cloudfront.net


**Task 2: VPC Design for CloudLaunch**

VPC

Name: cloudlaunch-vpc



CIDR Block: 10.0.0.0/16

Subnets

Public Subnet (10.0.1.0/24) → For load balancers/future public services.

Application Subnet (10.0.2.0/24) → For private app servers.

Database Subnet (10.0.3.0/28) → For private DB services (e.g., RDS).

Internet Gateway (IGW)

Name: cloudlaunch-igw

Attached to cloudlaunch-vpc.

Route Tables

Public Route Table – cloudlaunch-public-rt

Associated with Public Subnet.

Has route 0.0.0.0/0 → cloudlaunch-igw.

Private Route Tables

cloudlaunch-app-rt (App Subnet).

cloudlaunch-db-rt (DB Subnet).

No route to IGW (fully private).



Security Groups

cloudlaunch-app-sg



Allows HTTP (80) traffic within the VPC only.

cloudlaunch-db-sg



Allows MySQL (3306) traffic only from app subnet.

IAM Permissions

cloudlaunch-user has read-only access to VPC components:

VPC, Subnets, Route Tables, Security Groups.

No ability to modify/delete.

📄 IAM Policy File: CloudLaunchVPCReadOnly
<img width="1593" height="688" alt="image" src="https://github.com/user-attachments/assets/99c404cf-5653-4df0-8261-8c8e07cb35df" />


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

Console Access Details (submitted in the google form)

Console URL:

Account Alias :

IAM Username:

Password: (password will require a reset upon first login)






