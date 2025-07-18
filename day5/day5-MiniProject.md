# 🚀 Day 5 Mini Project – Git + Jenkins + AWS S3 Deploy

---

## 🎯 Objective:
Automate code deployment to S3 using GitHub and Jenkins.

---

## 📂 Steps:

### 1️⃣ Create Simple Website Repo
- Repo structure:
## index.html
## index.css


### 2️⃣ Push to GitHub
```bash
git init
git add .
git commit -m "Initial site"
git remote add origin <your-repo-url>
git push -u origin main

### Step 3: Launch EC2 Instance (Free Tier)
Type: t2.micro

AMI: Amazon Linux 2

Key pair: create or use existing

Security Group:

Port 22 → SSH

Port 8080 → Jenkins

Port 80 → (Optional, if running site locally)

Storage: default (8GB, SSD)

## Step 3 Install Dependencies on EC2 
sudo yum update -y
sudo yum install git -y
sudo yum search java-11
sudo yum install java-11-openjdk-devel -y or java-11-corretto-devel -y

## Step 4 Install Jenkins

sudo wget -O /etc/yum.repos.d/jenkins.repo \
  https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
sudo yum install jenkins -y
sudo systemctl enable jenkins
sudo systemctl start jenkins

## Step 5 Install aws cli 
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
## Step 6 Configure AWS CLI (IAM User with S3FullAccess)
aws configure
 Enter Access Key, Secret Key, Region (ap-south-1), output format (json)
## Step 7 Unlock Jenkins
Visit: http://<EC2-Public-IP>:8080
Get password:
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
## Step 8 Install Jenkins Plugins
AWS CLI

Git

Pipeline

GitHub integration
##Step 9 Create Pipeline Job
-- Go to Jenkins ➝ New Item ➝ “DeployToS3” ➝ Type: Pipeline

Pipeline script:
pipeline {
    agent any
    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/YOUR_USERNAME/YOUR_REPO.git'
            }
        }
        stage('Deploy to S3') {
            steps {
                sh 'aws s3 cp index.html s3://your-s3-bucket-name/ --acl public-read'
                sh 'aws s3 cp index.css s3://your-s3-bucket-name/ --acl public-read'
            }
        }
    }
}
--
## Step 10 Create S3 Bucket
aws s3 mb s3://day8-jenkins-site-bucket

## Step 11 Make it Website Enabled
Go to S3 → Properties → Static Website Hosting → Enable

Set index document: index.html
## Step 12 Set Bucket Policy (Public Read)
{
  "Version":"2012-10-17",
  "Statement":[
    {
      "Sid":"PublicReadGetObject",
      "Effect":"Allow",
      "Principal": "*",
      "Action":["s3:GetObject"],
      "Resource":["arn:aws:s3:::day8-jenkins-site-bucket/*"]
    }
  ]
}

## Step 13 Test Deployment
Push a change to GitHub

Jenkins pulls → uploads to S3

Visit: http://day8-jenkins-site-bucket.s3-website.ap-south-1.amazonaws.com/

screenshots 


![alt text](<Screenshot 2025-07-17 205829.png>)


![alt text](<Screenshot 2025-07-17 201530.png>)