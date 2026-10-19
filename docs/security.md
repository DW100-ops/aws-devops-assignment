# Security Documentation - AWS DevOps Assignment

## Why IAM Roles Are Preferable to Hard-Coded Access Keys

Hard-coding AWS access keys (Access Key ID and Secret Access Key) directly into application code, configuration files, or user data scripts presents severe security risks. IAM roles solve these risks through several architectural advantages:

1. **No Stored Credentials on Disk:** IAM roles leverage temporary, automatically rotating security tokens managed securely behind the scenes by the AWS Security Token Service (STS). No permanent credentials are saved on the EC2 instance's file system where they could potentially be compromised.
2. **Reduced Blast Radius & Principle of Least Privilege:** If an application or instance is compromised, an attacker with hard-coded keys gains permanent, long-term access to your AWS account. With IAM roles, permissions are scoped specifically to the resources the workload requires (e.g., S3 read-only access), limiting potential exposure.
3. **No Manual Key Rotation:** Hard-coded keys require manual rotation and retirement schedules to maintain security compliance, creating administrative overhead and human error risks. IAM roles handle credential lifecycle management and rotation completely automatically.