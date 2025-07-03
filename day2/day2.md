🧠 Day 2 – AWS Core Services (EC2, S3, IAM)
💡 What is EC2?
✍️ 
EC2 is like a virtual computer in the cloud that I can rent anytime. I can choose the operating system and install software, just like on my own laptop. But the best part is that I don’t have to own or maintain any hardware — AWS handles it. I can scale resources up or down easily based on my needs.

### 🧪 What I Did:
- Launched a **t2.micro** EC2 instance using Amazon Linux 2
- Created a **key pair** and downloaded `.pem` file
- Connected to instance via **SSH**
- Installed **Apache Web Server** and hosted a basic `index.html`


💡 What is S3?
✍️ 

S3 is like AWS’s version of Google Drive. I can upload and store any type of file (images, documents, backups) inside buckets. It’s highly reliable, accessible from anywhere, and I only pay for the space I use. It’s perfect for storing static website files, user uploads, and backup data.

### 🧪 What I Did:
- Created a unique **S3 bucket**
- Uploaded an image and accessed it via public link
- Used the S3 object in my EC2-hosted webpage

💡 What is IAM?
✍️ 

IAM helps me control who can access what in my AWS account. I can create users, assign them to groups, and give permissions using policies. It’s like a digital security system where only authorized people or services can enter certain rooms.

### 🧪 What I Did:
- Created a new **IAM user**
- Created a **group** and attached `AmazonS3ReadOnlyAccess`
- Created an **IAM Role** for EC2 with S3 access
- Attached that role to the EC2 instance to let it access S3

🧩 EC2 / S3 / IAM Table Summary
Service	Purpose	Real World Analogy	Example Use Case
EC2	Virtual servers to run apps	Renting a powerful laptop	Host backend of web app
S3	File/object storage	Google Drive or Dropbox	Store images/backups
IAM	User and access management	Office security system	Give devs access to S3 only

📌 Real World Analogies 
✅ Real World Analogies
🔹 EC2 (Elastic Compute Cloud)
Analogy: Like renting a car when you need to travel
You don’t buy the car (physical server), you rent it for as long as you need. EC2 gives you a virtual server (computer) on demand. You can choose the size, type, and operating system, and stop it when you're done.

🔹 S3 (Simple Storage Service)
Analogy: Like using a digital locker or Dropbox
Imagine you have a cloud-based storage locker where you can safely store and retrieve files (documents, images, videos) anytime from anywhere. That’s what S3 does—secure, scalable object storage over the internet.

🔹 IAM (Identity and Access Management)
Analogy: Like giving different keys and permissions to rooms in an office building
IAM controls who can enter which room (access what service), and what they can do inside (read, write, delete). You define roles, permissions, and users to securely manage access to AWS resources.

🧠 5 Reasons Why EC2/S3/IAM are Core AWS Services
✔️ Scalable compute power (EC2)
✔️ Durable and cheap storage (S3)
✔️ Fine-grained access control (IAM)
✔️ All are building blocks for modern cloud apps
✔️ They work together securely and efficiently

🎯 What I Learned Today

 I learned how to launch a virtual machine (EC2) and connect via SSH.

I uploaded a file to S3 and tested public access.

I created an IAM user with restricted access and understood permission boundaries.

