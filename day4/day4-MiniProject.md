# 🛠️ Day 4 – Mini Project: Host Static Website + EBS Setup

---

## 🎯 Objective

Today’s project focuses on:

✅ Hosting a static website on S3  
✅ Attaching and mounting EBS on EC2  
✅ Applying lifecycle rules to manage storage  


## ✅ Project 1: S3 Bucket – `day4-cloud-bucket`



### Step 1 – Create S3 Bucket

1. Navigate to **Services → S3**
2. Click **Create bucket**
3. Configure:

   * **Bucket name:** `day4-cloud-bucket` 
   * **Region:** e.g., `ap-south-1` 
   * Leave other settings default
4. Click **Create bucket**

### Step 2 – Enable Versioning

1. Go to your bucket → **Properties**
2. Scroll to **Bucket Versioning** → Click **Edit**
3. Select **Enable** → Save changes

### Step 3 – Upload Files

1. Open your bucket
2. Click **Upload**
3. Add image, PDF, and code files
4. Click **Upload** to finish

### Step 4 – Make a File Public

1. Click on a file (e.g., `demo.txt`)
2. Go to **Permissions**
3. Edit and disable "Block all public access" for the object
4. Click **Object URL** to access it publicly

### Step 5 – Apply Lifecycle Rule

1. Go to **Management → Lifecycle rules**
2. Click **Create lifecycle rule**
3. Name: `Glacier-Then-Delete`
4. Actions:

   * Transition to Glacier after 30 days
   * Expire/delete after 90 days
5. Save the rule

---

## ✅ Project 2: EC2 + EBS Volume

### Step 0 – Sign In to AWS

Already completed above.

### Step 1 – Launch EC2 Instance

1. Go to **EC2 → Instances → Launch Instance**
2. Configuration:

   * **AMI:** Amazon Linux 2023
   * **Instance type:** `t2.micro`
   * **Key pair:** Create/download `.pem`
   * **Security Group:** Allow SSH (22) and HTTP (80)
3. Launch instance

### Step 2 – Create New EBS Volume

1. Navigate to **Volumes → Create Volume**
2. Configure:

   * **Size:** 5 GB
   * **AZ:** Same as EC2 (e.g., `ap-south-1a`)
3. Click **Create Volume**

### Step 3 – Attach EBS Volume

1. Go to volume → **Actions → Attach Volume**
2. Select instance and device name (`/dev/xvdf`)

### Step 4 – SSH into EC2

```bash
ssh -i ec2key.pem ec2-user@<your-ec2-public-ip>
```

### Step 5 – Format EBS Volume

```bash
lsblk
sudo mkfs -t ext4 /dev/xvdf
```

### Step 6 – Mount EBS Volume

```bash
sudo mkdir /data
sudo mount /dev/xvdf /data
```

### Step 7 – Store Test Files

```bash
echo "Hello Cloud!" | sudo tee /data/hello.txt
cat /data/hello.txt
```

---