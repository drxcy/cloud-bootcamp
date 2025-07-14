
# 🛠️ Day 3 – Mini Project: Manual VPC Setup + EC2 in Public Subnet

---

## 🎯 Objective

Create a custom VPC environment with public and private subnets, launch an EC2 instance, and test internet access manually — no wizard.

---

## ✅ STEP 1 — Create a VPC

1. Go to **VPC Dashboard** → **Your VPCs**
2. Click **Create VPC**
3. Choose:
   - **Name tag** → `my-vpc`
   - **IPv4 CIDR block** → `10.0.0.0/16`
   - Leave IPv6 as **No IPv6 CIDR Block**
4. Click **Create VPC**

✅ **Done! Your VPC exists.**

---

## ✅ STEP 2 — Create Public Subnet

1. Go to **Subnets** → Click **Create subnet**
2. Choose:
   - **VPC** → Select `my-vpc`
   - **Subnet name** → `public-subnet-1`
   - **Availability Zone** → `us-east-1a`
   - **IPv4 CIDR block** → `10.0.1.0/24`
3. Click **Create subnet**

✅ **Public subnet created!**

---

## ✅ STEP 3 — Create Private Subnet

1. Repeat previous steps, but use:
   - **Subnet name** → `private-subnet-1`
   - **CIDR block** → `10.0.2.0/24`

✅ **Private subnet created!**

---

## ✅ STEP 4 — Create and Attach Internet Gateway

1. Go to **Internet Gateways** → Click **Create internet gateway**
2. Enter:
   - **Name tag** → `my-igw`
3. Click **Create internet gateway**

### Attach it:

1. Select `my-igw`
2. Click **Actions** → **Attach to VPC**
3. Select `my-vpc` → **Attach**

✅ **Internet Gateway is now connected.**

---

## ✅ STEP 5 — Create Public Route Table

1. Go to **Route Tables** → Click **Create route table**
2. Enter:
   - **Name tag** → `public-route-table`
   - **VPC** → Select `my-vpc`
3. Click **Create route table**

### Add Route for Internet:

1. Select `public-route-table`
2. Go to **Routes** tab → **Edit routes** → **Add route**:
   - **Destination** → `0.0.0.0/0`
   - **Target** → Select `my-igw`
3. Click **Save changes**

### Associate Route Table with Public Subnet:

1. Select `public-route-table`
2. Go to **Subnet Associations** → **Edit subnet associations**
3. Check `public-subnet-1`
4. Click **Save**

✅ **Public subnet can now reach the internet!**

---

## ✅ STEP 6 — Launch EC2 in Public Subnet

1. Go to **EC2 Dashboard** → Click **Launch instance**

### Configure EC2:

- **Name** → `my-webserver`
- **Amazon Machine Image** → Amazon Linux 2
- **Instance type** → `t2.micro` (Free Tier eligible)
- **Key pair** → Create or use existing (save your `.pem` file!)

### Network:

- **VPC** → `my-vpc`
- **Subnet** → `public-subnet-1`
- **Auto-assign public IP** → **Enable**

### Configure Security Group:

- Create new security group:
  - **Allow SSH (TCP 22)** → your IP
  - **Allow HTTP (TCP 80)** → Anywhere (`0.0.0.0/0`)

Click **Launch**!

✅ **EC2 instance running in your public subnet.**

---

## ✅ STEP 7 — Connect and Install Apache

### Connect via SSH:

```bash
ssh -i your-key.pem ec2-user@<public-ip>

# Install Apache:

- ** sudo yum update -y
- ** sudo yum install httpd -y
- ** sudo systemctl start httpd
- ** sudo systemctl enable httpd

### Test it!
- ** Go to browser → http://<public-ip>