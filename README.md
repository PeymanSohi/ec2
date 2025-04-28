# 🚀 Deploy a Static Website on AWS EC2

## 📖 Project Overview

This project will guide you through:
- Creating and setting up an AWS account
- Launching a Linux server using AWS EC2
- Configuring server access and security
- Installing a web server (Nginx)
- Deploying a simple static HTML website
- (Optional Stretch Goals) Setting up a custom domain and HTTPS

You will gain real-world experience working with AWS, Linux, networking, and website deployment.

---

## 🛠️ Technologies Used
- Amazon Web Services (AWS)
- EC2 (Elastic Compute Cloud)
- Ubuntu Server 22.04
- Nginx Web Server
- SSH

---

## 📋 Prerequisites
- AWS account (sign up [here](https://aws.amazon.com/))
- SSH client (Terminal, PuTTY, etc.)
- Basic familiarity with Linux commands
- A public/private SSH key pair

---

## 🚀 Step-by-Step Guide

### 1. Create an AWS Account
- Visit [AWS](https://aws.amazon.com/) and sign up for a free account.
- Complete the verification and sign in to the AWS Management Console.

---

### 2. Launch an EC2 Instance

- Go to the EC2 Dashboard and click **Launch Instance**.
- **Name**: `static-website-server`
- **AMI**: Choose **Ubuntu Server 22.04 LTS** (or latest available)
- **Instance Type**: Select **t2.micro** (Free Tier eligible)
- **Key Pair**: 
  - Create a new key pair (type: RSA, format: `.pem`) 
  - Download and save it securely.
- **Network Settings**:
  - Allow inbound SSH (port 22)
  - Allow inbound HTTP (port 80)
- **Storage**:
  - Default 8 GB is sufficient.
- **Public IP**: Ensure **Auto-assign Public IP** is enabled.

Click **Launch Instance**.

---

### 3. Connect to Your EC2 Instance

- After launch, go to **Instances**, select your instance.
- Click **Connect** → **SSH Client** tab.
- Example SSH Command:

```bash
chmod 400 your-key.pem
ssh -i your-key.pem ubuntu@your-public-ip
```

---

### 4. Install Nginx Web Server

SSH into your instance and run:

```bash
sudo apt update
sudo apt install nginx -y
```

Start and enable Nginx:

```bash
sudo systemctl start nginx
sudo systemctl enable nginx
```

You can now visit your public IP in a browser and see the default Nginx page.

---

### 5. Create and Deploy Your Static Website

#### Create a simple HTML file:

```bash
echo "<h1>Hello from AWS EC2!</h1>" > index.html
```

#### Move it to Nginx web root:

```bash
sudo mv index.html /var/www/html/index.html
```

(Optional: remove Nginx default page)

```bash
sudo rm /var/www/html/index.nginx-debian.html
```

#### Restart Nginx:

```bash
sudo systemctl restart nginx
```

---

### 6. Access Your Website

- Open a browser and go to:  
  `http://your-public-ip`

You should see your custom "Hello from AWS EC2!" page.

---

## 🎯 Stretch Goals (Optional)

### 1. Set up a Custom Domain (Amazon Route 53)

- Register a domain via AWS Route 53 or any domain registrar.
- Create a hosted zone in Route 53.
- Point your domain’s DNS A Record to your EC2 public IP.

### 2. Set up HTTPS with Let's Encrypt

- Install Certbot:

```bash
sudo apt install certbot python3-certbot-nginx -y
```

- Run Certbot:

```bash
sudo certbot --nginx
```

- Follow the prompts to generate and apply SSL certificates.
- Your website will now be available via HTTPS.

### 3. Create a CI/CD Pipeline (AWS CodePipeline)

- Use AWS CodePipeline and CodeDeploy.
- Connect your GitHub repository.
- Automate deployment of website changes to your EC2 server.

---

## 🛠️ Useful EC2 Commands

| Command | Purpose |
|:--------|:--------|
| `sudo systemctl status nginx` | Check if Nginx is running |
| `sudo systemctl restart nginx` | Restart Nginx |
| `sudo ufw allow 'Nginx Full'` | Allow Nginx through UFW firewall |
| `curl http://localhost` | Check the website from inside the server |

---

## 📈 Learning Outcomes

By completing this project, you will have learned:
- How to create and configure AWS EC2 instances
- How to SSH into a remote Linux server
- How to install and configure a web server (Nginx)
- How to deploy a static website to AWS
- Basic cloud networking (VPCs, subnets, security groups)

---

## 🏁 Final Result

You will have a fully functional static website hosted on an AWS EC2 server, accessible through the public internet.

---

# 🏴‍☠️ Quick Architecture Overview

```
[ Local SSH Client ] --> [ AWS EC2 Instance ]
                                 ↓
                        [ Nginx Web Server ]
                                 ↓
                    [ Static Website Deployment ]
```

---

## 📚 References

- [AWS Free Tier](https://aws.amazon.com/free/)
- [AWS EC2 Documentation](https://docs.aws.amazon.com/ec2/)
- [Nginx Documentation](https://nginx.org/en/docs/)
- [Let's Encrypt](https://letsencrypt.org/)

---
https://roadmap.sh/projects/ec2-instance
