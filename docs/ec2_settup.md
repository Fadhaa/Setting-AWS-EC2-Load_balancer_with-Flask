
# Step 1: Launch EC2 Instances inside Custom VPC (`myvpc1`)

This guide walks you through launching EC2 instances in your custom VPC (`myvpc1`) using the AWS Console.

---

## ✅ Prerequisites

Before launching EC2 instances, make sure you've already created:

- A **VPC** named `myvpc1`
- Two **public subnets**: `mysubnet1` and `mysubnet2` in different Availability Zones
- A **Route Table** named `mytable1` (associated with both subnets)
- An **Internet Gateway** named `myiqw1` (attached to `myvpc1`)

### see https://github.com/Fadhaa/Setting-AWS-EC2-Load_balancer_with-Flask/blob/main/docs/vpc-requirements.md
---


## 🚀 Launch an EC2 Instance

### 1. Go to EC2 Dashboard
- From AWS Console, search for and select **"EC2"**
- Click on **"Instances"** in the left menu
- Click **"Launch instance"**

---

### 2. Configure Basic Settings

| Field                           | Value Example                |
|---------------------------------|------------------------------|
| **Name**                        | `flask-server-1`             |
| **Application & OS**            | Amazon Linux 2 or Ubuntu 22.04|
| **Amazon Machine Image (AMI)**  | Amazon Linux Kernel- 6.12 AMI  |
| **Instance type**               | `t2.micro`                   |
| **Key pair**                    | Choose existing or create new|

---

### 3. Configure Network Settings

Click on **"Edit"** under Network Settings:

| Option              | Value            |
|---------------------|------------------|
| **VPC**             | `myvpc1`         |
| **Subnet**          | `mysubnet1`      |
| **Auto-assign IP**  | **Enable**       |
| **Firewall**        | Add Security Group or create default one|

#### Add Inbound Rules:
- Under **Inbound Security Group Rules**
- ✅ **SSH** — Port 22 — Source: **Anywhere (0.0.0.0/0)**
- ✅ **HTTP** — Port 80 — Source: **Anywhere (0.0.0.0/0)**



### 4. Add Storage (Optional)

- Leave the default 8 GiB (General Purpose SSD)

---

### 5. Launch Instance

- Click "Launch instance"
- After a few seconds, click "View all instances"
- Make sure the instance State is Running














