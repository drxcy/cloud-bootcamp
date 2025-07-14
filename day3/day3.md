# 🧠 Day 3 – Cloud Networking: VPC, Subnets, IPs, Gateways

---

## 🎯 What You’ll Learn Today

By the end of **Day 3**, you will:

- ✅ Understand how **AWS Virtual Private Cloud (VPC)** works
- ✅ Learn about **subnets** (public vs private), **IP addresses**, and **route tables**
- ✅ Understand how **NAT Gateways** and **Internet Gateways** function
- ✅ Practice creating your own VPC manually (no wizard!)
- ✅ Deploy an **EC2 instance** in a public subnet and verify internet access
- ✅ Complete a quiz and mini-project for hands-on practice

---

## 🌐 What is a VPC?

- **VPC** stands for **Virtual Private Cloud**.
- It’s your own **isolated network space** inside AWS where you can launch resources (like EC2 instances, databases, etc.).
- You decide:
  - IP address ranges
  - Subnets
  - Security settings
  - Routing rules

**Analogy:**  
> A VPC is like your own office building. You control who enters, how rooms are divided, and how people move around inside.

---

## 🗂️ What are Subnets?

- A **subnet** divides your VPC into smaller, logical segments.
- Each subnet is associated with a **CIDR block** (a range of IP addresses).
- Subnets help you separate resources into:
  - **Public subnet** → has internet access via an Internet Gateway
  - **Private subnet** → no direct internet access

**Analogy:**  
> Subnets are like floors inside your office building. You might keep your reception and meeting rooms on the ground floor (public), and your secure server room on another floor (private).

---

## 📡 Internet Gateway (IGW)

- An **Internet Gateway** allows resources in your VPC to connect directly to the internet.
- Required if you want your public subnet to:
  - Host web servers
  - Be reachable from outside AWS

**Analogy:**  
> The Internet Gateway is like the main door of your building where people can enter and exit freely (if allowed).

---

## 🔒 NAT Gateway

- A **NAT Gateway** allows resources in a private subnet to:
  - **Access the internet for outbound traffic** (e.g. updates, external APIs)
  - **Remain inaccessible from the internet** for inbound traffic
- Placed in a public subnet.

**Analogy:**  
> Think of it like a one-way mirror room: people inside can look out, but outsiders can’t look in.

---

## 🗺️ Route Tables

- A **Route Table** defines how network traffic travels within your VPC.
- Tells AWS:
  - Which subnet routes traffic where
  - Where internet-bound traffic should go (IGW or NAT)
- Each subnet must be associated with a route table.

**Analogy:**  
> A route table is like a building floor plan showing which doors lead to which rooms or exits.

---

## 🌍 Public vs Private Subnets

| **Feature**         | **Public Subnet**                             | **Private Subnet**                     |
|----------------------|-----------------------------------------------|-----------------------------------------|
| Internet Access      | Has direct internet access via IGW           | No direct internet access               |
| Use Case             | Web servers, load balancers, bastion hosts   | Databases, app servers, internal tools  |
| Route Table          | Route to IGW                                  | No direct route to IGW                  |
| IPs                  | Often use public IPs                         | Private IPs only                        |

---

## 🔢 What is a CIDR Block?

- **CIDR** → Classless Inter-Domain Routing
- Defines a **range of IP addresses**.
- Example:
  - `10.0.0.0/16` → can have ~65,536 IP addresses
- Helps split networks into smaller subnets.

**Analogy:**  
> Like assigning address numbers to rooms in your building so every room has a unique location.

---

## ✅ Example Workflow

**Goal:** Launch a web server reachable on the internet.

### 1. Create a VPC
- CIDR block: `10.0.0.0/16`

### 2. Create subnets:
- Public Subnet → `10.0.1.0/24`
- Private Subnet → `10.0.2.0/24`

### 3. Create Internet Gateway (IGW)
- Attach IGW to VPC

### 4. Create Route Table for Public Subnet
- Add route:
  - Destination: `0.0.0.0/0`
  - Target: Internet Gateway

### 5. Launch EC2 Instance in Public Subnet
- Assign public IP
- Install web server (e.g. Apache)

### 6. Test Connectivity
- Access your EC2’s public IP in a browser.

---

## 📝 Mini Quiz

1. What does a VPC do?
2. What’s the purpose of an Internet Gateway?
3. Why would you use a NAT Gateway?
4. How does a route table work?
5. True or False: Private subnets have direct internet access.

---

## 💡 Mini Project

✅ **Deploy a public web server:**

- Create a new VPC
- Set up a public subnet
- Attach an Internet Gateway
- Launch an EC2 instance
- Install Apache or NGINX
- Test by accessing your public IP in a browser

---

