# Deploy Flask on EC2 Instance `myserver1` via AWS Console Only

This guide explains how to install and run a simple Flask app on your EC2 instance (`myserver1`) **without using the terminal**, by using the **User Data** field in the AWS Console.

---

## ✅ Prerequisites

- You have already launched an EC2 instance named `myserver1`
- The instance is in VPC `myvpc1`, subnet `mysubnet1`
- You selected Amazon Linux 2 or Ubuntu 22.04 as the OS
- The security group allows **inbound HTTP (port 80)** access
- The instance has **auto-assigned public IP**

---

## 




### 🧾 Step 2: Paste the User Data Script

#### For Amazon Linux 2:

```bash
#!/bin/bash
yum update -y
yum install python3 -y
pip3 install flask gunicorn

mkdir -p /home/ec2-user/flask-app
cat > /home/ec2-user/flask-app/app.py << EOF
from flask import Flask
app = Flask(__name__)

@app.route('/')
def home():
    return "Hello from Flask on myserver1 (via User Data)"
EOF

cd /home/ec2-user/flask-app
gunicorn --bind 0.0.0.0:80 app:app
