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

