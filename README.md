# NGINX-Configuration-on-Amazon-EC2
This guide walks you through the process of setting up an NGINX web server on an Amazon EC2 instance, configuring a custom HTML page, and troubleshooting connectivity issues.

# NGINX Configuration on Amazon EC2

## Overview
This project sets up an NGINX web server on an Amazon EC2 instance, configures a custom HTML page, and ensures accessibility via HTTP.

## Prerequisites
- AWS account with access to EC2.
- Git Bash or another SSH client.
- Basic knowledge of Linux commands.

## Setup Instructions

### 1. **Launch an EC2 Instance**
1. Log in to AWS and go to the EC2 Dashboard.
2. Click **Launch Instances** and select an Amazon Linux 2 or Ubuntu AMI.
3. Choose **t2.micro** (free-tier eligible).
4. Select/Create a key pair (RSA or ED25519) and download the `.pem` file.
5. Configure security groups:
   - Allow **HTTP (port 80)** from `0.0.0.0/0`.
   - Allow **SSH (port 22)** from your IP.
6. Launch the instance and wait for initialization.

### 2. **Connect to the Instance**
1. Open Git Bash and navigate to the `.pem` file location.
2. Run the SSH command:
   ```bash
   ssh -i "my-key.pem" ec2-user@<your-ec2-public-ip>
   ```

### 3. **Install and Start NGINX**
```bash
sudo apt update && sudo apt upgrade -y  # For Ubuntu
sudo yum update -y                      # For Amazon Linux
sudo apt install nginx -y  # Ubuntu
sudo yum install nginx -y  # Amazon Linux
sudo systemctl start nginx
sudo systemctl enable nginx
```

### 4. **Configure the Custom HTML Page**
1. Open the default web page:
   ```bash
   sudo nano /var/www/html/index.html
   ```
2. Replace the content with:
   ```html
   <!DOCTYPE html>
   <html>
   <head>
       <title>DevOps Stage 0</title>
   </head>
   <body>
       <h1>Welcome to DevOps Stage 0 - [Your Name]/[SlackName]</h1>
   </body>
   </html>
   ```
3. Save and exit (`CTRL+O`, `Enter`, `CTRL+X`).
4. Reload NGINX:
   ```bash
   sudo systemctl reload nginx
   ```

### 5. **Test the Web Server**
1. Find your public IPv4 address from the EC2 Dashboard.
2. Open a web browser and go to:
   ```
   http://<your-ec2-public-ip>
   ```
3. The custom message should be displayed.

### 6. **Troubleshooting**
- Check NGINX status: `sudo systemctl status nginx`
- Verify security group rules in AWS.
- Check firewall settings (`sudo ufw status`).
- Use `curl http://<your-ec2-public-ip>` to debug response.

## License
This project is open-source and free to use.

## View blogpost here
https://medium.com/@johannesvanderpuije/setting-up-and-testing-nginx-on-amazon-ec2-5716eaac768b

