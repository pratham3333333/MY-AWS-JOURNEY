# AWS-EC2-SETUP-NGINX

---

# 🚀 Hosting a Website on Nginx Server on AWS EC2 (Amazon Linux)

This guide will walk you through the process of setting up an **Nginx** web server on an **Amazon EC2 instance** running **Amazon Linux**. By the end, you'll have a simple website hosted and accessible via your public IP address.

---

**
**![fjnef](https://github.com/user-attachments/assets/432628ea-13bd-47ba-acbd-ad63844eee5e)


![AWS-EC2-NGINX](https://github.com/user-attachments/assets/826e41f8-e877-4072-bd96-4ed64316ca97)

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

# AWS-EC2-SETUP-APACHE

---

# 🚀 Hosting a Website on Apache Server on AWS EC2 (Amazon Linux)

This guide will help you set up an **Apache** web server on an **Amazon EC2 instance** running **Amazon Linux**. By the end of this tutorial, you’ll have a simple website hosted and accessible via your public IP address.

---
![AWS-EC2-APACHE](https://github.com/user-attachments/assets/09f55d79-57c6-4338-baeb-50ad0933b37f)

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

### Step 3: Install Apache

Install **Apache** with the following commands:

```bash
sudo yum install httpd -y
```

---

### Step 4: Start Apache

Start and enable the **Apache** service:

```bash
sudo systemctl start httpd
sudo systemctl enable httpd
```

---

### Step 5: Verify Apache is Running

Check the Apache status:

```bash
sudo systemctl status httpd
```

You should see `Active: active (running)` if Apache is running correctly.

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

Apache serves content from `/var/www/html`. Replace the default content:

1. Navigate to the HTML directory:

   ```bash
   cd /var/www/html
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
     <title>My Apache Website</title>
   </head>
   <body>
     <h1>Welcome to My Website Hosted on Apache! 🚀</h1>
     <p>This is a simple webpage hosted on an Amazon EC2 instance with Apache.</p>
   </body>
   </html>
   ```

4. Press `Esc` to exit insert mode.
5. Save changes and exit by typing `:wq` and pressing **Enter**.

---

### Step 8: Restart Apache

Apply the changes by restarting Apache:

```bash
sudo systemctl restart httpd
```

---

### Step 9: Access Your Website

1. Open your web browser.
2. Enter your EC2 instance’s **public IP address**:

   ```text
   http://your-ec2-public-ip
   ```

You should see the message "Welcome to My Website Hosted on Apache! 🚀".

---

## ✅ Conclusion

🎉 **Congratulations!** You've successfully set up an **Apache web server** on your **Amazon Linux EC2 instance**. Your website is now live and accessible via the internet.

---

### 🚨 Troubleshooting Tips

- **Apache isn’t working:** Ensure your EC2 instance’s Security Group allows **port 80 (HTTP)** and **port 443 (HTTPS)** traffic.
- **Can’t connect via SSH:** Verify your **.pem file** permissions (`chmod 400 your-key.pem`).
- **Website doesn’t load over HTTPS:** This guide covers HTTP traffic only. For HTTPS, set up SSL certificates using tools like Let's Encrypt.

---


# 🚀 Hosting a Website on Apache Server on AWS EC2 (Amazon Linux and Ubuntu)

This guide will help you set up an **Apache** web server on an **Amazon EC2 instance** running **Amazon Linux** or **Ubuntu**. By the end of this tutorial, you’ll have a simple website hosted and accessible via your public IP address.

---
![02_AWS-EC2--UBUNTU-APACHE](https://github.com/user-attachments/assets/c286efc9-954b-4e32-ac33-dae6166256b1)

## 🖊️ Prerequisites

Ensure you have the following:
1. ✅ An **AWS account** and access to the **AWS Management Console**.
2. ✅ A **running EC2 instance** (either **Amazon Linux 2** or **Ubuntu**).
3. ✅ SSH access to the EC2 instance using a **.pem private key**.
4. ✅ **Default VPC** and **Security Group** configured.
5. ✅ A **Security Group** allowing **HTTP (port 80)** and **HTTPS (port 443)** inbound traffic.

If you don't have an EC2 instance, create one using the appropriate AMI within the **default VPC**.

---

## 🛠️ Step-by-Step Guide

### Step 1: Connect to Your EC2 Instance via SSH

1. Open a terminal.
2. Use the following command to connect to your EC2 instance:
   
   For **Amazon Linux**:
   ```bash
   ssh -i "your-key.pem" ec2-user@your-ec2-public-ip
   ```

   For **Ubuntu**:
   ```bash
   ssh -i "your-key.pem" ubuntu@your-ec2-public-ip
   ```

---

### Step 2: Update Your EC2 Instance

Update the instance’s package list:

For **Amazon Linux**:
```bash
sudo yum update -y
```

For **Ubuntu**:
```bash
sudo apt update && sudo apt upgrade -y
```

---

### Step 3: Install Apache

Install **Apache** using the package manager:

For **Amazon Linux**:
```bash
sudo yum install httpd -y
```

For **Ubuntu**:
```bash
sudo apt install apache2 -y
```

---

### Step 4: Start Apache

Start and enable the **Apache** service:

For **Amazon Linux**:
```bash
sudo systemctl start httpd
sudo systemctl enable httpd
```

For **Ubuntu**:
```bash
sudo systemctl start apache2
sudo systemctl enable apache2
```

---

### Step 5: Verify Apache is Running

Check the Apache status:

For **Amazon Linux**:
```bash
sudo systemctl status httpd
```

For **Ubuntu**:
```bash
sudo systemctl status apache2
```

You should see `Active: active (running)` if Apache is running correctly.

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

Apache serves content from:
- **Amazon Linux**: `/var/www/html`
- **Ubuntu**: `/var/www/html`

Replace the default content:

1. Navigate to the HTML directory:
   ```bash
   cd /var/www/html
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
     <title>My Apache Website</title>
   </head>
   <body>
     <h1>Welcome to My Website Hosted on Apache! 🚀</h1>
     <p>This is a simple webpage hosted on an Amazon EC2 instance with Apache.</p>
   </body>
   </html>
   ```

4. Press `Esc` to exit insert mode.
5. Save changes and exit by typing `:wq` and pressing **Enter**.

---

### Step 8: Restart Apache

Apply the changes by restarting Apache:

For **Amazon Linux**:
```bash
sudo systemctl restart httpd
```

For **Ubuntu**:
```bash
sudo systemctl restart apache2
```

---

### Step 9: Access Your Website

1. Open your web browser.
2. Enter your EC2 instance’s **public IP address**:

   ```text
   http://your-ec2-public-ip
   ```

You should see the message "Welcome to My Website Hosted on Apache! 🚀".

---

## ✅ Conclusion

🎉 **Congratulations!** You've successfully set up an **Apache web server** on your **Amazon Linux or Ubuntu EC2 instance**. Your website is now live and accessible via the internet.

---

### 🚨 Troubleshooting Tips

- **Apache isn’t working:** Ensure your EC2 instance’s Security Group allows **port 80 (HTTP)** and **port 443 (HTTPS)** traffic.
- **Can’t connect via SSH:** Verify your **.pem file** permissions (`chmod 400 your-key.pem`).
- **Website doesn’t load over HTTPS:** This guide covers HTTP traffic only. For HTTPS, set up SSL certificates using tools like Let's Encrypt.

---

# AWS-EC2-SETUP-WEBSERVER-WINDOWS

---

# 🚀 Hosting a Website on a Windows EC2 Instance

This guide will help you set up a **web server** on an **Amazon EC2 Windows instance** using **IIS (Internet Information Services)**. By the end of this tutorial, you’ll have a simple website hosted and accessible via your instance’s public IP address.

---


## 🖊️ Prerequisites

Ensure you have the following:

1. ✅ An **AWS account** and access to the **AWS Management Console**.
2. ✅ A **running EC2 instance** with **Windows Server** (e.g., Windows Server 2019/2022).
3. ✅ **RDP access** to your EC2 instance using the private key and administrator credentials.
4. ✅ A **Security Group** allowing **HTTP (port 80)** and **RDP (port 3389)** traffic.

If you don't have an EC2 instance yet, create one with the **Windows Server AMI** in the **default VPC**.

---

## 🛠️ Step-by-Step Guide

### Step 1: Connect to Your Windows EC2 Instance via RDP

1. In the **AWS Management Console**, navigate to **EC2** > **Instances**.
2. Select your Windows instance and click **Connect**.
3. Under the **RDP Client** tab, download the **Remote Desktop File** and note down the public IP address.
4. Decrypt the **administrator password** using your private key file.
5. Open the downloaded RDP file, enter the administrator credentials, and connect to the instance.

---

### Step 2: Install IIS (Internet Information Services)

Once connected to the instance:

1. Open **Server Manager** from the **Start Menu**.
2. Click on **Manage** > **Add Roles and Features**.
3. In the **Add Roles and Features Wizard**:
   - **Installation Type**: Select **Role-based or feature-based installation**.
   - **Server Selection**: Select your EC2 instance.
   - **Server Roles**: Check **Web Server (IIS)** and click **Next**.
4. Click **Next** until you reach the **Confirmation** page, then click **Install**.
5. Wait for the installation to complete and close the wizard.

---

### Step 3: Start IIS and Test the Default Website

1. Open a web browser within the Windows instance.
2. Enter `http://localhost` in the address bar.
3. You should see the default IIS welcome page, indicating that IIS is running.

---

### Step 4: Adjust Security Group Rules for HTTP Traffic

Allow **HTTP (port 80)** traffic by modifying your instance’s **Security Group**:

1. In the **AWS Management Console**, navigate to **EC2** > **Security Groups**.
2. Select the Security Group associated with your EC2 instance.
3. Click **Inbound rules** > **Edit inbound rules**.
4. Add the following rule:
   - **Type**: HTTP
   - **Port Range**: 80
   - **Source**: Anywhere (0.0.0.0/0)
5. Save the rules.

---

### Step 5: Upload Your Website Files

To replace the default IIS webpage with your own content:

1. Open **File Explorer** and navigate to the IIS root directory:
   ```text
   C:\inetpub\wwwroot
   ```
2. Delete or rename the default `iisstart.html` file.
3. Copy your website files (e.g., `index.html`) into this directory.

---

### Step 6: Test Your Website

1. Open your web browser on your local machine.
2. Enter your EC2 instance’s **public IP address** in the address bar:

   ```text
   http://your-ec2-public-ip
   ```

3. You should see your custom webpage.

---

## ✅ Conclusion

🎉 **Congratulations!** You’ve successfully set up a **web server** on your **Windows EC2 instance** using IIS. Your website is now accessible via the instance’s public IP address.

---

### 🚨 Troubleshooting Tips

- **Website not loading?** Ensure port **80** is open in the instance’s Security Group.
- **Can’t connect via RDP?** Verify that port **3389** (RDP) is open and that you’re using the correct private key and administrator password.
- **Custom website not displaying?** Check that your website files are in the `C:\inetpub\wwwroot` directory.

---


