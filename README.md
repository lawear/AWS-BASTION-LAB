# AWS Bastion Host Project

## Overview
This project demonstrates how to set up a secure AWS environment using a **Bastion Host** to access private EC2 instances within a **Virtual Private Cloud (VPC)**.

The configuration ensures that private instances are **not directly accessible from the internet**, improving overall security and control.

---

## Architecture Components

- **VPC** – Custom virtual network for isolated cloud resources.  
- **Public Subnet** – Hosts the Bastion Host (jump box) with internet access.  
- **Private Subnet** – Hosts backend EC2 instances that are not directly accessible from the internet.  
- **Internet Gateway (IGW)** – Enables internet connectivity for the public subnet.  
- **Route Tables** – Define routing for both public and private subnets.  
- **Security Groups (SG)** – Control inbound and outbound traffic to EC2 instances.  
- **Network ACLs (NACLs)** – Provide an additional layer of network traffic control.

---

## Step-by-Step Setup

### 1. Create a VPC
- Specify a CIDR block, e.g. `10.0.0.0/16`.  
- ![Create VPC](./screenshots/create-vpc.png)

---

### 2. Create a Public Subnet
- Example CIDR: `10.0.1.0/24`.  
- ![Create Public Subnet](./screenshots/create-public-subnet.png)

---

### 3. Attach an Internet Gateway
- Create an **Internet Gateway (IGW)**.  
- Attach it to your VPC.  
- ![Attach IGW](./screenshots/attach-igw.png)

---

### 4. Create a Route Table for the Public Subnet
- Add a route to the Internet Gateway:  


- Associate the route table with your public subnet.  
- ![Public Route Table](./screenshots/public-route-table.png)

---

### 5. Create a Security Group
- Allow **SSH (port 22)** from your trusted IP (e.g. your home or office).  
- Optionally allow **HTTP (port 80)** and **HTTPS (port 443)** if needed.  
- ![Security Group](./screenshots/security-group.png)

---

### 6. Create a Network ACL for the Public Subnet
- Allow inbound and outbound traffic for SSH and HTTP/HTTPS.  
- ![Public NACL](./screenshots/public-nacl.png)

---

### 7. Create a Private Subnet
- Example CIDR: `10.0.2.0/24`.  
- ![Create Private Subnet](./screenshots/create-private-subnet.png)

---

### 8. Create a Route Table for the Private Subnet
- Do **not** add a route to the internet.  
- Associate it with the private subnet.  
- ![Private Route Table](./screenshots/private-route-table.png)

---

### 9. Create a Private Network ACL
- Restrict inbound/outbound traffic to internal IP ranges only.  
- ![Private NACL](./screenshots/private-nacl.png)

---

### 10. Launch EC2 Instances
- **Public EC2 (Bastion Host)** → Launch in the **public subnet**.  
- **Private EC2 (Target Instance)** → Launch in the **private subnet**.  
- Assign appropriate security groups.  
- ![Launch EC2](./screenshots/launch-ec2.png)

---


