# Security Documentation

This document outlines the security posture, access decisions, and isolation mechanisms implemented for the AWS DevOps assignment.

## 1. Security Groups (`WebServerSecurityGroup`)
- **Inbound Rules:** Restricted strictly to necessary traffic vectors. Port `80` (HTTP) is opened for public web traffic access, and Port `22` (SSH) is permitted for administrative maintenance.
- **Outbound Rules:** Retains default unrestricted egress (`0.0.0.0/0`) to allow package updates and software installations via Amazon Linux repositories.

## 2. Identity and Access Management (IAM) & Least Privilege
- **No Hardcoded Credentials:** Credentials (AWS Access Keys) are completely omitted from application code and repository files to prevent credential leakage.
- **Instance Profile & Role:** The EC2 instance utilizes an attached IAM role (`WebServerRole`) that assumes permission boundaries dynamically.
- **Least Privilege Enforced:** The role is scoped strictly to `AmazonS3ReadOnlyAccess`, ensuring the application can read or list required bucket contents without having write, delete, or administrative control over the broader AWS account.

## 3. S3 Access Decisions
- Public direct access is restricted. 
- The S3 bucket is accessed securely from within AWS boundaries by the EC2 instance using its assigned IAM role, minimizing exposure surface to the public internet.

## 4. Secret-Handling Practices
- Secrets and sensitive keys are excluded from version control. 
- Environment variables and dynamic IAM roles replace static secrets, adhering to cloud security best practices.