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

## 🔌 Step 1: Connect to Instance via AWS Console

1. Go to **EC2 > Instances**
2. Select the instance named `myserver1`
3. Click the **"Connect"** button at the top
4. In the **Connect to instance** panel:
   - Choose **"EC2 Instance Connect (browser-based SSH)"**
   - Click **"Connect"**

You will now see a terminal inside your browser connected to your instance.

---

## ⚙️ Step 2: Install Python, pip, Flask, and Gunicorn

Depending on your instance OS, run the following commands **in the browser terminal**:

### ✅ For Amazon Linux 2:

```bash
sudo su
mkdir myproject
cd myproject
mkdir myflaskapp
cd myflaskapp
sudo yum update -y
sudo yum install python3 -y
python3 -m venv venv
source venv/bin/activate
python3 -m pip install --upgrade pip

pip3 install flask gunicorn

```
---
### In the terminal 
- Use **vim app.py** to create flask app.
- press **Insert** in your keyboard.
- paste this code in it
  
```python
from flask import Flask
app = Flask(__name__)
@app.route('/')
def home():
    return "Hello from Flask on myserver1 (via User Data)"
```
- Press **ESC** in your keyboard
- type **:wq**
- Then run the command

```bash
gunicorn --bind 0.0.0.0:80 app:app
```
You should see 

- Starting gunicorn 23.0.0.
- Listening at: http://0.0.0.0:80
- Using worker: sync
- Booting worker with pid: 7777

Open your browser and type:
**http://your_Public-IP:80**

You should see ***Hello from Flask on myserver1 (via User Data)**

If not, recheck your settings 


