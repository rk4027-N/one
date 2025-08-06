# Java Web App Deployment with Jenkins, Maven, Git, and Apache Tomcat

## 🚀 Overview
This project demonstrates how to build and deploy a Java web application using:
- **Maven** for build automation
- **Git** for version control
- **Jenkins** for CI/CD
- **Apache Tomcat** for hosting
- **NGINX** (optional) as a reverse proxy

---

## 📦 Prerequisites

- Amazon Linux 2 or Ubuntu server
- Java 17 (Amazon Corretto or OpenJDK)
- Apache Tomcat 9
- Jenkins installed and configured
- GitHub repository for source code
- NGINX (optional)
## 🌐 NGINX Reverse Proxy Setup

This section explains how to configure NGINX to act as a reverse proxy for Apache Tomcat.

### ✅ 1. Install NGINX

**Amazon Linux:**
```bash
sudo amazon-linux-extras install nginx1 -y
sudo systemctl start nginx
sudo systemctl enable nginx

⚙️ 2. Configure NGINX
Edit the NGINX configuration file:

bash
sudo nano /etc/nginx/nginx.conf
Add or update the server block:

nginx
server {
    listen 80;
    server_name your_domain_or_ip;

    location / {
        proxy_pass http://localhost:8080;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
Replace your_domain_or_ip with your actual domain name or public IP.

🔄 3. Restart NGINX
bash
sudo systemctl restart nginx
🧪 4. Verify
Open a browser and visit:

http://your_domain_or_ip
You should see your Tomcat-hosted application served through NGINX.
