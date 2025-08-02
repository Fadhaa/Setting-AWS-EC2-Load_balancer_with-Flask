# Step 1: Launch an VPC dashboard via AWS Console (No Bash Required)-Updated 02 Aug 2025

This guide walks you through Creating VPC using the AWS Management Console.

---

## ✅ Prerequisites

- You have an [AWS account](https://aws.amazon.com/)
- You are signed in to the [AWS Console](https://console.aws.amazon.com/)
- You have a region selected (e.g., `us-east-1`, `eu-west-2`)

---
## 1️⃣ Under **Virtual private cloud**
1. Click **Your VPCs** and then click on **Create VPC**
2. Under **VPC settings** select **VPC only**
3. In **Name tag - optional**, enter **myvpc1**
4. For **IPv4 CIDR block**, select **IPv4 CIDR manual input**
5. For **IPv4 CIDR**, use **10.0.0.0/16**
6. Under **IPv6 CIDR block**, select **No IPv6 CIDR block**
7. Leave **Tenancy** as **Default** and click **creat vpc**


---
## 2️⃣ Create Two Public Subnets
### Go to **Subnets → Create subnet**
1. Under **VPC ID**, select your created vpc name. In this example, it's **myvpc1**
2. In **Subnet name**, enter **mysubnet1**
3. For **Availability Zone**, select **us-east-1a** (or as you like depending on selected region).
4. In **IPv4 subnet CIDR block**, enter **10.0.1.0/24**
5. Click **create Subnet**
6. Create another on by repeating the above steps 1-5, with the following changes
   - Name: **mysubnet2**
   - Availability Zone: **us-east-1b**
   - IPv4 subnet CIDR block: **10.0.2.0/24**
   - Click on **create Subnet**
  

  ---

  
