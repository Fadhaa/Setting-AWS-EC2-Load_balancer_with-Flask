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
  

##For both subnets, do the following

### update your subnets

  1. Go to **subnets**, select your subnet. In my example, it's **mysubnet1**
  2. Click on **Network ACL** in the middle of the page
  3. Click on your **Network ACL Name** next to **Network ACL** (e.g. acl-0d59dcvfdggt455)
  4. Select the ACL from the list above.
  5. in the middle of the page, click on **Inbound rules**
  6. Then click **Edit inbound rules**
  7. Add a new rule for SSH with source 0.0.0.0/0 and another for HTTP with source 0.0.0.0/0.
  9. Click **save changes**
      
 

---

## 3️⃣ Create an Internet Gateway
1. Go to **Internet Gateways → Create internet gateway**
2. In **Name**, enter **myigw1**
3. Click **Create internet gateway**
   - Select it and click **Actions → Attach to VPC**
   - Choose `myvpc1`

---

## 4️⃣ Create a Route Table
1. Go to **Route Tables → Create route table**
2. In **Name**, use **mytable1**
3. In **VPC**, select your vpc **myvpc1**
4. Click on **create route table**

---

## 5️⃣ Add Route to the Internet:
-Select the route table
1. Go to **Routes tab → Edit routes → Add route**
  - Destination: `0.0.0.0/0`
  - Target: Select the Internet Gateway (`myigw1`)
- Click **Save routes**


## 6️⃣ Associate Subnets with Route Table
- Go to **Subnet Associations → Edit subnet associations**
- Select `mysubnet1`
- From **Action** click on **Edit route table association**
- In **Route table ID**, select **mytable1**
- Click **Save**
- Repeate these steps with the other **mysubnet2**
- Click **Save**

---

✅ Done! Your custom VPC is now ready.

You can now launch EC2 instances inside these subnets and ensure they have public internet access.

---





















  
