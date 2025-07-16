# 🧠 Day 4 – AWS Storage: S3, EBS, Glacier & Lifecycle Rules

---

## 🎯 Goals for Today

By the end of Day 4, I’ve learned:

✅ What is S3, EBS, and Glacier in AWS  
✅ The differences between **object, block, and archive storage**  
✅ How to create & manage S3 buckets  
✅ How to attach and use EBS volumes with EC2  
✅ How lifecycle rules help reduce storage cost  
✅ Quiz and Mini Project to reinforce learning

---

## 📦 AWS Storage Services

| Service | Type | Description | Real World Analogy |
|--------|------|-------------|--------------------|
| **S3** | Object Storage | Stores files, images, logs, backups | Dropbox or Google Drive |
| **EBS** | Block Storage | Disk volume attached to EC2 (like HDD) | USB hard drive attached to PC |
| **Glacier** | Archival Storage | Long-term, infrequent access storage | Offsite tape backup or warehouse storage |
| **EFS** | File Storage | Shared filesystem for multiple EC2 | Network Drive (shared folder)

---

## ☁️ Amazon S3 (Simple Storage Service)

### ✅ Features
- Stores **objects** (files) in **buckets**
- **Unlimited** storage
- High durability (11 9s)
- Can host static websites
- Access via Console, CLI, SDK
- Lifecycle rules to manage storage cost

### 🧪 Hands-On

- Created S3 bucket: `day5-cloud-bucket`
- Uploaded multiple files (image, PDF, text)
- Set one file **public**
- Enabled **versioning**
- Added **lifecycle rule**:
  - Move to Glacier after 30 days
  - Delete after 90 days

---

## 💾 Amazon EBS (Elastic Block Store)

### ✅ Features
- Persistent **block storage** attached to EC2
- Must be in **same AZ** as EC2
- Automatically replicated in zone
- Types:
  - **gp3** – General purpose (default)
  - **io2** – High-performance IOPS
  - **sc1** – Throughput-optimized

### 🧪 Hands-On

- Created EBS volume (8 GB gp3)
- Attached to EC2 instance
- SSH into EC2:
```bash
lsblk                        # View volume
sudo mkfs -t ext4 /dev/xvdf  # Format
sudo mkdir /data
sudo mount /dev/xvdf /data   # Mount
df -h                        # Check mounted space
🧊 Amazon Glacier
✅ Features
Used for archival (cold) storage

Very low-cost

Retrieval takes time (minutes to hours)

Ideal for logs, compliance data

🧪 Applied S3 lifecycle rule to move data to Glacier class automatically

🔄 Lifecycle Rules (S3)
Help automate storage cost management

Example:

After 30 days → move to Glacier

After 90 days → delete the object

Useful for log files, temporary uploads, backups

🗂️ File Types and Use Cases
File Type	Use	Service
Image uploads	User-generated media	S3
Application files	EC2 OS, app binaries	EBS
Monthly logs	Audit, backups	Glacier
Shared Configs	Shared across EC2	EFS

🧠 Key Takeaways
S3: Great for storing files, backups, and hosting static content

EBS: Acts like a hard drive for EC2 instances

Glacier: Cold storage for data you rarely access

Use lifecycle rules to move data automatically and save costs

You must format and mount EBS volumes to use them