# MY-AWS-JOURNEY
# AWS-EC2-SETUP-NGINX

---

# 🚀 Hosting a Website on Nginx Server on AWS EC2 (Amazon Linux)

This guide will walk you through the process of setting up an **Nginx** web server on an **Amazon EC2 instance** running **Amazon Linux**. By the end, you'll have a simple website hosted and accessible via your public IP address.

---

## 🖊️ Prerequisites

Ensure you have the following:
1. ✅ An **AWS account** and access to the **AWS Management Console**.
2. ✅ A **running EC2 instance** (preferably **Amazon Linux 2**).
3. ✅ SSH access to the EC2 instance using a **.pem private key**.
4. ✅ **Default VPC** and **Security Group** configured.
5. ✅ A **Security Group** allowing **HTTP (port 80)** and **HTTPS (port 443)** inbound traffic.

If you don't have an EC2 instance, create one using the **Amazon Linux 2** AMI within the **default VPC**.

---

## 🛠️ Step-by-Step Guide

### Step 1: Connect to Your EC2 Instance via SSH

1. Open a terminal.
2. Use the following command to connect to your EC2 instance (replace `your-key.pem` with your private key file and `your-ec2-public-ip` with your instance's public IP):

   ```bash
   ssh -i "your-key.pem" ec2-user@your-ec2-public-ip
   ```

   For **Ubuntu**-based instances, replace `ec2-user` with `ubuntu`:

   ```bash
   ssh -i "your-key.pem" ubuntu@your-ec2-public-ip
   ```

---

### Step 2: Update Your EC2 Instance

Update the instance’s package list:

```bash
sudo yum update -y
```

---

### Step 3: Install Nginx

Install **Nginx** with the following commands:

```bash
sudo amazon-linux-extras install nginx1 -y
sudo yum install nginx -y
```

---

### Step 4: Start Nginx

Start and enable the **Nginx** service:

```bash
sudo systemctl start nginx
sudo systemctl enable nginx
```

---

### Step 5: Verify Nginx is Running

Check the Nginx status:

```bash
sudo systemctl status nginx
```

You should see `Active: active (running)` if Nginx is running correctly.

---

### Step 6: Configure Security Group Rules

Allow **HTTP (port 80)** and **HTTPS (port 443)** traffic by editing your EC2 instance's **Security Group**:

1. Navigate to **EC2** > **Security Groups** in the **AWS Management Console**.
2. Select the **Security Group** associated with your EC2 instance.
3. Click **Inbound rules**, then **Edit inbound rules**.
4. Add the following:
   - **Type**: HTTP, **Port Range**: 80, **Source**: Anywhere (0.0.0.0/0)
   - **Type**: HTTPS, **Port Range**: 443, **Source**: Anywhere (0.0.0.0/0)

5. Remove any unnecessary inbound rules, such as **SSH (port 22)**, if no longer needed.
6. Save the rules.

**Note:** Keep port 22 open if you still require SSH access.

---

### Step 7: Edit the Default `index.html`

Nginx serves content from `/usr/share/nginx/html`. Replace the default content:

1. Navigate to the HTML directory:

   ```bash
   cd /usr/share/nginx/html
   ```

2. Edit the `index.html` file:

   ```bash
   sudo vi index.html
   ```

3. Press `i` to enter **insert mode**, and replace the content with:

   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
     <meta charset="UTF-8">
     <meta name="viewport" content="width=device-width, initial-scale=1.0">
     <title>My Awesome Website</title>
   </head>
   <body>
     <h1>Welcome to My Website Hosted on Nginx! 🚀</h1>
     <p>This is a simple webpage hosted on an Amazon EC2 instance with Nginx.</p>
   </body>
   </html>
   ```

4. Press `Esc` to exit insert mode.
5. Save changes and exit by typing `:wq` and pressing **Enter**.

---

### Step 8: Restart Nginx

Apply the changes by restarting Nginx:

```bash
sudo systemctl restart nginx
```

---

### Step 9: Access Your Website

1. Open your web browser.
2. Enter your EC2 instance’s **public IP address**:

   ```text
   http://your-ec2-public-ip
   ```

You should see the message "Welcome to My Website Hosted on Nginx! 🚀".

---

## ✅ Conclusion

🎉 **Congratulations!** You've successfully set up an **Nginx web server** on your **Amazon Linux EC2 instance**. Your website is now live and accessible via the internet.

---

### 🚨 Troubleshooting Tips

- **Nginx isn’t working:** Ensure your EC2 instance’s Security Group allows **port 80 (HTTP)** and **port 443 (HTTPS)** traffic.
- **Can’t connect via SSH:** Verify your **.pem file** permissions (`chmod 400 your-key.pem`).
- **Website doesn’t load over HTTPS:** This guide covers HTTP traffic only. For HTTPS, set up SSL certificates using tools like Let's Encrypt.

---

