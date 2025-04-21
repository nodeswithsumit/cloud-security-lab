# Practical 1: Set Up a Virtual Private Cloud (VPC) and Configure Network Security on AWS

## Objective

To create a **Virtual Private Cloud (VPC)** in AWS, configure **public and private subnets**, and manage access using **Security Groups** and **Route Tables**.

This simulates a secure cloud environment setup for IoT devices.

---

## Tools & Services Used

- AWS Management Console
- Amazon VPC
- Amazon EC2
- Internet Gateway
- Security Groups

---

## Steps to Follow

### Step 1: Login to AWS Console

- Visit: [https://aws.amazon.com](https://aws.amazon.com)
- Log in to your **AWS Free Tier** account.

---

### Step 2: Create a New VPC

1. Navigate to **VPC Dashboard**
2. Click on **Create VPC**
3. Choose **VPC only** option
4. Set:
   - **Name tag:** `iot-secure-vpc`
   - **IPv4 CIDR block:** `10.0.0.0/16`
   - Leave IPv6 unchecked
   - Tenancy: Default
5. Click **Create VPC**

---

### Step 3: Create Subnets

Create two subnets:
- **Public Subnet**: For internet-facing IoT devices
- **Private Subnet**: For internal processing servers

1. Go to **Subnets** → Click **Create Subnet**
2. Choose VPC: `iot-secure-vpc`
3. Create:
   - **Public Subnet**
     - Subnet name: `public-subnet`
     - Availability Zone: (any)
     - CIDR: `10.0.1.0/24`
   - **Private Subnet**
     - Subnet name: `private-subnet`
     - CIDR: `10.0.2.0/24`

---

### Step 4: Create and Attach an Internet Gateway

1. Go to **Internet Gateways** → Click **Create**
   - Name tag: `iot-igw`
2. Click **Create**
3. Select the gateway and click **Attach to VPC**
   - Choose: `iot-secure-vpc`

---

### Step 5: Configure Route Tables

1. Go to **Route Tables** → Click **Create**
   - Name tag: `public-route-table`
   - VPC: `iot-secure-vpc`
2. Add a route:
   - Destination: `0.0.0.0/0`
   - Target: Internet Gateway (`iot-igw`)
3. Associate this route table to **public-subnet** only.

Now, only your public subnet has internet access.

---

### Step 6: Launch EC2 Instance in Public Subnet

1. Go to **EC2 Dashboard** → Click **Launch Instance**
2. Choose:
   - AMI: Amazon Linux 2
   - Instance type: `t2.micro` (free tier)
   - Network: `iot-secure-vpc`
   - Subnet: `public-subnet`
   - Enable: **Auto-assign public IP**
3. Add storage (leave default)
4. Configure **Security Group**:
   - Name: `iot-sg`
   - Inbound rules:
     - SSH (22) → My IP
     - HTTP (80) → Anywhere
     - HTTPS (443) → Anywhere
   - Outbound: Allow all (default)
5. Launch instance using a new key pair or existing one

---

### Step 7: Test the Setup

- SSH into the instance using the `.pem` key:
  ```bash
  ssh -i "your-key.pem" ec2-user@<public-ip>


# Recap: VPC Setup & Network Security Basics

## What You Learned

In this practical, you successfully:

1. Created a **Virtual Private Cloud (VPC)** with a custom IP range.
2. Designed **Public and Private Subnets** within the VPC.
3. Attached an **Internet Gateway (IGW)** to allow internet access for public resources.
4. Configured **Route Tables** to control traffic flow.
5. Launched and accessed an **EC2 Instance** via SSH in the public subnet.
6. Applied **Security Groups** to allow specific traffic (like SSH, HTTP, HTTPS).
7. Understood **network isolation** by testing access differences between subnets.

---

## Understanding Route Table Association

| Subnet Type      | Route Table Target            | Internet Access | Use Case                          |
|------------------|-------------------------------|------------------|-----------------------------------|
| `public-subnet`  | `0.0.0.0/0 → Internet Gateway`| ✅ Yes            | Hosts public-facing services      |
| `private-subnet` | No explicit internet route    | ❌ No             | Hosts internal systems (databases, backend apps)

**Key Point:** Only the **public subnet** was associated with the route table that has a route to the Internet Gateway. This ensures that instances in the private subnet **stay isolated** and cannot directly access the internet.

---

## Glossary of Key Components

| Component | Description |
|----------|-------------|
| **VPC (Virtual Private Cloud)** | A logically isolated network within AWS where you can deploy resources. |
| **Subnet** | A segment of a VPC's IP address range. Helps isolate workloads. |
| **Internet Gateway (IGW)** | Connects the VPC to the internet. Needed for outbound traffic. |
| **Route Table** | A set of rules used to determine network traffic flow. |
| **Security Group** | Acts like a firewall; controls inbound/outbound traffic for instances. |
| **EC2 (Elastic Compute Cloud)** | Virtual servers that run your apps in the AWS cloud. |
| **CIDR Block** | IP address range in the form `10.0.0.0/16` used to define VPCs and subnets. |
| **SSH (Secure Shell)** | Protocol for securely connecting to remote systems using key authentication. |

---

## Cleanup Reminder

To avoid charges:
- Terminate your EC2 instances
- Delete Subnets
- Detach & delete the Internet Gateway
- Delete the Route Table and VPC

---

## References

- [AWS VPC Documentation](https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html)
- [AWS Route Tables](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Route_Tables.html)
