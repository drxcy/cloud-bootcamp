This is my Project contains :- 

EC2 public IP link :- http://3.110.54.20/

Screenshot of running web page

![alt text](<Screenshot 2025-07-13 073817.png>)

S3 bucket name and object URL
bucket name : ra-1456-buck
index.css : http://ra-1456-buct.s3.ap-south-1.amazonaws.com/index.css
image : https://ra-1456-buct.s3.ap-south-1.amazonaws.com/banner-2.webp

Role name and attached policy
Role name : access_to_ec2_backend 
attached policy : AmazonS3ReadOnlyAccess , AmazonS3FullAccess

Commands used
ssh -i my-key.pem ec2-user@<your-ec2-public-ip> // which shown in when click connect to initialise your instance
# For install apache server 

sudo yum update -y  //update apache
# Install Apache Web Server
sudo yum install httpd -y 
# Start Apache service
sudo systemctl start httpd  
# Enable Apache on boot
sudo systemctl enable httpd 

# Prepare Website Files
cd /var/www/html             # Navigate to the Apache web root
sudo nano index.html          # Create your basic HTML file 

# Test if Apache serves your file correctly
curl http://localhost/index.html  
# Test from browser
http://<your-ec2-public-ip>

# Make S3 bucket
aws s3 mb s3://your-bucket-name

# Upload files to S3 bucket
aws s3 cp file.html s3://your-bucket-name/
aws s3 cp image.jpg s3://your-bucket-name/

# List S3 buckets and objects
aws s3 ls
aws s3 ls s3://your-bucket-name/

# more basic command I used in this

pwd          # Show current directory path
ls -la       # List files with details
mkdir        # Make directory
rm -rf       # Delete files/folders
cat          # View contents of file
nano         # Open file for editing
# 🔨 Part 2: Mini Project – Static Website with EC2 + S3 + IAM

## ✅ Objective:
Deploy a static HTML page from an EC2 server that pulls an image hosted on S3, with secure access managed via IAM.


# Steps for this mini project

Step 1 – Create EC2 Instance
Launch EC2:

Amazon Linux 2

t2.micro

Allow SSH (port 22) in security group

# Connect via SSH:

ssh -i your-key.pem ec2-user@EC2_PUBLIC_IP
Step 2 – Install Apache

sudo yum update -y
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
# Step 3 – Create HTML Page

sudo nano /var/www/html/index.html
# Step 4 – Create S3 Bucket
Create S3 bucket in console or via AWS CLI:

aws s3 mb s3://your-unique-bucket-name
# Upload a file:

aws s3 cp myimage.jpg s3://your-unique-bucket-name/
# Optional public access:

Set bucket policy or object ACL to public-read for testing.

# Step 5 – IAM Role for EC2
Go to IAM → Roles → Create role

# Trusted entity: EC2

Attach policy: AmazonS3FullAccess

Example policy:

json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::your-unique-bucket-name/*"
    }
  ]
}
# Attach role to EC2 instance via console.

# Step 6 – Test
Visit:

cpp
http://YOUR_EC2_PUBLIC_IP
You should see your page and the image from S3.
# To Create Bucket via console
aws s3 mb s3://bucketname
aws s3 cp file s3://bucketname/
# Create bucket policy to restrict access only to your IAM role:
Example bucket policy:

{
  "Version":"2012-10-17",
  "Statement":[
    {
      "Effect":"Allow",
      "Principal": {
        "AWS": "arn:aws:iam::YOUR_ACCOUNT_ID:role/YOUR_EC2_ROLE_NAME"
      },
      "Action":"s3:GetObject",
      "Resource":"arn:aws:s3:::your-unique-bucket-name/*"
    }
  ]
}
