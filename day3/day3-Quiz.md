# 📋 Day 3 – AWS Networking Quiz ✅

---

### 1. ❓ What is a VPC?

A **Virtual Private Cloud (VPC)** is a logically isolated virtual network in AWS that you control. It allows you to launch AWS resources (like EC2) in a secure, private network.

---

### 2. ❓ What is the difference between a Public and Private Subnet?

- **Public Subnet**: Connected to the internet via Internet Gateway (IGW)  
- **Private Subnet**: No direct internet access (used for secure backend resources)

---

### 3. ❓ What is the purpose of an Internet Gateway (IGW)?

An **IGW** allows traffic from the internet to reach your VPC (for EC2 in public subnets), and vice versa. It enables internet communication for public subnets.

---

### 4. ❓ What is a NAT Gateway used for?

A **NAT Gateway** lets instances in a private subnet access the internet **outbound**, but it blocks all inbound connections from the internet.

---

### 5. ❓ What does a Route Table do?

A **Route Table** defines rules (routes) that determine where traffic is directed from your subnets. It’s how AWS knows how to route packets inside your VPC.

---

### 6. ❓ What does the CIDR block `10.0.0.0/16` represent?

It defines an IP range with **65,536 IP addresses** (from 10.0.0.0 to 10.0.255.255), which can be used to create subnets inside the VPC.

---

### 7. ❓ How do you make a subnet public?

1. Create an Internet Gateway and attach to VPC  
2. Create a route in Route Table → `0.0.0.0/0` → IGW  
3. Associate that route table with the subnet

---

### 8. ❓ What happens if a subnet has no route to 0.0.0.0/0?

It has **no internet access**, even if the instance has a public IP.

---

### 9. ❓ Why should private subnets be used?

To securely host backend systems (databases, internal services) that shouldn't be exposed to the internet directly.

---

### 10. ❓ What is the difference between Elastic IP and Private IP?

- **Elastic IP**: A static, public IP address reachable from the internet  
- **Private IP**: Used for communication inside the VPC (not accessible from internet)

---
✅ Why use a VPC instead of default VPC?
✅ Simple Answer:

Because you want full control over your own network instead of using AWS’s pre-made one.

✅ Technical Answer:

Default VPC:

Automatically exists in every AWS region

Has pre-configured subnets, route tables, etc.

All subnets can reach the internet by default

Your own VPC:

Lets you:

Choose your own IP ranges

Separate private/public networks

Control routing and security

Necessary for strict security or network designs

In interviews, mention security, compliance, and custom architecture as reasons for building your own VPC.

✅ Why split into public and private subnets?
✅ Simple Answer:

To keep sensitive stuff hidden from the internet while letting public services be reachable.

✅ Technical Answer:

Public subnet:

Resources get public IPs

Can talk directly to the internet via Internet Gateway

Private subnet:

No direct internet access

Used for databases, application servers, backend services

This improves:
✅ Security
✅ Cost control
✅ Architecture best practices

Example:

Web server → public subnet

Database → private subnet

✅ What’s the purpose of an Internet Gateway?
✅ Simple Answer:

It’s the door that lets your network talk to the internet.

✅ Technical Answer:

An Internet Gateway (IGW):

Connects your VPC to the public internet

Needed for:

Inbound internet traffic to public resources

Outbound internet traffic from resources with public IPs

Without an IGW, your VPC is fully isolated.

✅ What’s a NAT Gateway vs NAT Instance?
✅ Simple Answer:

Both let private resources connect out to the internet, but the NAT Gateway is managed by AWS, while a NAT Instance is a DIY solution.

✅ Technical Answer:

Feature	NAT Gateway	NAT Instance
Managed	Fully managed by AWS	You manage it yourself
High availability	Yes (in AZ)	You must configure it
Cost	More expensive	Cheaper EC2 pricing
Scalability	Automatically scales	Must resize instance
Performance	High throughput	Depends on instance size

Both:

Let private subnet instances outbound-connect to the internet

Block inbound traffic from internet

NAT Gateway = simpler, pay more
NAT Instance = cheaper, more admin work

✅ How does a route table affect subnet traffic?
✅ Simple Answer:

It decides where your network traffic goes.

✅ Technical Answer:

A route table defines:

Which traffic stays inside the VPC

Which traffic goes to the internet

Or goes to a VPN, NAT, Transit Gateway, etc.

Example routes:

10.0.0.0/16 → local → internal VPC traffic

0.0.0.0/0 → IGW → public internet traffic

Subnets must be associated with route tables to direct traffic properly.

✅ Why open only certain ports in Security Groups?
✅ Simple Answer:

To keep hackers out and only allow necessary connections.

✅ Technical Answer:

Security Groups are virtual firewalls for EC2 and other resources.

If you open:

Port 22 → SSH

Port 80 → HTTP

Port 443 → HTTPS

You’re limiting exposure.
Opening all ports (0-65535) is dangerous → attackers can exploit services.

Principle of least privilege:

Only allow what your app needs

✅ What’s the difference between a Security Group and a Network ACL?
✅ Simple Answer:

Security Group protects servers. Network ACL protects entire subnets.

✅ Technical Answer:

Feature	Security Group	Network ACL
Scope	Resource-level (instance)	Subnet-level
Stateful	Yes (return traffic allowed automatically)	No (need rules for inbound & outbound separately)
Rules evaluated	All rules evaluated together (allow rules only)	Rules evaluated in order (allow & deny rules)
Typical Use	Protecting EC2 instances	Extra subnet-wide rules

Examples:

Security Group → “allow HTTP to web server”

NACL → “block certain IP ranges from entire subnet”