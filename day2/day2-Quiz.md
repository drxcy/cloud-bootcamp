# 📋 Day 2 – AWS Core Services Quiz ✅

---

### 1. ❓ What is an Amazon EC2 instance, and what does AMI stand for?

An EC2 instance is a virtual server that you can rent from AWS to run applications.  
**AMI** stands for **Amazon Machine Image**, which is a pre-configured template (OS + software) used to launch an instance.

---

### 2. ❓ What does a security group do in EC2?

A **security group** acts like a virtual firewall for your EC2 instance.  
It controls **inbound and outbound traffic** using rules that allow or deny access to specific ports (like SSH or HTTP).

---

### 3. ❓ What are the steps to SSH into an EC2 instance?

1. Launch EC2 and download your `.pem` key pair.
2. Open terminal and run:
```bash
chmod 400 my-key.pem
ssh -i "my-key.pem" ec2-user@<public-ip>
3. Ensure port 22 (SSH) is open in the security group.

4. ❓ What is the maximum size of a single object you can store in S3?
The maximum size of a single object in S3 is 5 terabytes (TB).
For uploads over 5 GB, AWS recommends using Multipart Upload.

5. ❓ What’s the difference between S3 and EBS?
S3 is object storage — stores files in buckets and is accessible over HTTP.

EBS is block storage — acts like a hard drive for EC2 and requires it to be attached to an instance.

6. ❓ Why must S3 bucket names be globally unique?
Because S3 bucket names become part of the public URL (like a website), AWS enforces global uniqueness across all regions and accounts to avoid conflicts.

7. ❓ What is an IAM policy, and what language is it written in?
An IAM policy is a JSON document that defines permissions (what actions are allowed or denied) on AWS resources for users, groups, or roles.

8. ❓ What’s the difference between an IAM user and an IAM role?
IAM User: A real person or developer with permanent credentials.

IAM Role: A temporary identity used by AWS services (like EC2) or federated users — it assumes permissions based on trust relationships.

9. ❓ Can EC2 access S3 directly? If yes, how?
Yes. You attach an IAM Role with S3 permissions (e.g., AmazonS3ReadOnlyAccess) to the EC2 instance.
This lets the instance access S3 without needing access keys.

10. ❓ Why should you avoid using the root AWS account regularly?
The root account has full access to everything and is a security risk if compromised.
Best practice is to create IAM users/roles for daily tasks and keep root access locked down (with MFA enabled).

