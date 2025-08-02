
# 🧭 Setting Up an AWS Load Balancer with HTTPS Support

This guide walks you through creating an **Application Load Balancer (ALB)** in AWS to enable **secure HTTPS** access to your EC2 instance.

---

## ✅ Prerequisites

- A running EC2 instance in a public subnet.
- A valid domain name (e.g., from Route 53, GoDaddy, or another registrar).
- A public hosted zone in Route 53 (if using Route 53).
- A security group allowing inbound traffic on ports **80** and **443**.

---

## 🚀 Step-by-Step Instructions

### 1. Request an SSL Certificate (ACM)

1. Go to **AWS Certificate Manager (ACM)**.
2. Click **Request a certificate**.
3. Choose **Request a public certificate**.
4. Enter your domain name (e.g., `www.example.com` and `example.com`).
5. Choose **DNS validation** (recommended).
6. Complete the validation by adding CNAME records to your DNS provider or Route 53.
7. Wait for the certificate status to become **Issued**.

---

### 2. Modify Existing Security Group (Add HTTPS Rule)

1. Go to **EC2 > Security Groups**.
2. Select the security group used by your EC2 instance.
3. Edit **Inbound rules** and add:
   - Type: HTTPS
   - Port: 443
   - Source: `0.0.0.0/0`

---

### 3. Create Target group

1. For **Default action**, create a new **Target Group**:
   - Name: `mytarget1`
   - Target type: `Instance`
   - Protocol: `HTTP`
   - Port: `80`
  2. Select your VPC. In my case, it's **myvpc1**
  3. Leave **Health checks** as default for now
  4. Click **Next**
  5. In the **Available instances**. Select your instance of interest. In this example, my instance is **myserver1**.
  6. Click on **Include as pending below**
  7. Click on **Create target group**



### 3. Create the Application Load Balancer

1. Go to **EC2 > Load Balancers**.
2. Click **Create Load Balancer** → select **Application Load Balancer**.
3. Set:
   - **Name**: `myapl1`
   - **Scheme**: `Internet-facing`
   - **IP address type**: `IPv4`
4. Select your **VPC** and **at least two public subnets**. In my example, they are **mysubnet1** and **mysubnet2**
5. Assign your existing **Security Group** (now with HTTPS allowed). If you didn't see the existing security group, create new one and add **Inbound rules**: SSH, HTTP, HTTPS. All with source **0.0.0.0/0**

---

### 4. Configure Listeners and Target Group

1. Add a **listener** for **HTTPS (443)** and **HTTP (80)**. Also select your target group for each listener.
2. Choose the **SSL certificate** you created in ACM.
3. 
4. Click on **Create Load Balancer** .

---

### 5. Update DNS Settings

Point your domain to the Load Balancer’s **DNS name**, such as:
```
my-app-lb-1234567890.us-east-1.elb.amazonaws.com
```

- If using Route 53:
  - Create an **A record** (Alias) pointing to the ALB (you just created).
- If using another DNS provider:
  - Create a **CNAME** pointing to the ALB's DNS name.

---

## ✅ Done!

#### Go to your instance terminal and enter the directory where your app.py exist and run
**gunicorn --bind 0.0.0.0:80 app:app**

You can now securely access your application at `https://yourdomain_name/`.
