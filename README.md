
# Linux Web Server Deployment with Firewall Configuration and HTTPS using Self-Signed SSL Certificate

---

# 📌 Project Overview

This project demonstrates the deployment of a **Secure Linux Web Server** using **Apache HTTP Server** on **Fedora**. The primary objective is to understand how a Linux System Administrator deploys, manages, and secures a web server using Linux administration tools.

The project includes:

- Apache Web Server Installation
- Static Website Deployment
- Linux File Permissions
- Firewall Configuration using **firewalld**
- HTTPS Configuration using a **Self-Signed SSL Certificate**
- Linux Service Management using **systemctl**

Instead of simply hosting a website, this project focuses on understanding **how a Linux server receives, processes, secures, and serves web requests**.

---

# 🎯 Project Objectives

- Deploy a static website using Apache HTTP Server.
- Learn Linux service management.
- Configure Linux Firewall (`firewalld`).
- Allow only required network ports.
- Secure web communication using HTTPS.
- Generate and configure a Self-Signed SSL Certificate.
- Understand Linux file permissions.
- Learn how Apache serves website files.
- Simulate a real-world Linux System Administration task.

---

# 🚀 Features

- ✅ Apache HTTP Server Deployment
- ✅ Static Website Hosting
- ✅ HTTP Configuration (Port 80)
- ✅ HTTPS Configuration (Port 443)
- ✅ Self-Signed SSL Certificate
- ✅ Firewall Configuration using firewalld
- ✅ Linux File Permission Management
- ✅ Service Management using systemctl
- ✅ Secure Local Network Hosting

---

# 🛠 Technologies Used

| Category | Technology |
|-----------|------------|
| Operating System | CentOS Stream |
| Web Server | Apache HTTP Server (httpd) |
| Firewall | firewalld |
| SSL | OpenSSL |
| Service Manager | systemd |
| Protocols | HTTP / HTTPS |
| Frontend | HTML, CSS |

---

# 📂 Project Directory Structure

```
linux-web-server-deployment/
│
├── website/
│   ├── index.html
│
├── README.md

```

---

# 🏗 Project Architecture

The following architecture illustrates the complete request flow from the client browser to the Apache Web Server.

> **Replace the image below with your hand-drawn architecture diagram.**

---

## 📖 Project Architecture Diagram
```


                             +-------------+
                             |    USER     |
                             +-------------+
                                    |
                                    |
                          https://<Server-IP>
                                    |
                                    ▼
                 +----------------------------------+
                 | Network Interface (ens160/ens192)|
                 +----------------------------------+
                                    |
                                    ▼
                  +--------------------------------+
                  |   firewalld checks whether     |
                  |      Port 80/443 is allowed    |
                  +--------------------------------+
                         /                     \
                        /                       \
              Allowed                          Not Allowed
                 |                                  |
                 ▼                                  ▼
      +---------------------+           +----------------------+
      | Apache Web Server   |           |  Request Blocked     |
      |      (httpd)        |           +----------------------+
      +---------------------+
                 |
                 ▼
      +-----------------------------+
      | SSL/TLS Handshake           |
      | (Self-Signed Certificate)   |
      +-----------------------------+
                 |
                 ▼
      +-----------------------------+
      | Linux File Permission Check |
      +-----------------------------+
             /                 \
            /                   \
      Allowed               Not Allowed
         |                       |
         ▼                       ▼
 +----------------+      +----------------------+
 | Display Website|      |  Request Blocked     |
 +----------------+      +----------------------+

```

---

# 🔄 Project Workflow

The project follows the below workflow:

1. User enters the server IP address in the browser.
2. The browser sends an HTTP/HTTPS request.
3. The request reaches the Linux network interface.
4. firewalld checks whether the requested port is allowed.
5. If the port is blocked, the request is rejected.
6. If allowed, Apache HTTP Server receives the request.
7. During HTTPS, Apache performs the SSL/TLS handshake.
8. Apache attempts to access the requested website files.
9. Linux verifies the file permissions.
10. Apache reads the files.
11. The webpage is sent back to the browser.

---

# 🎓 Learning Outcomes

By completing this project, I learned:

- Linux Server Administration
- Apache Web Server Configuration
- Linux Service Management
- Static Website Deployment
- Linux File Permissions
- Firewall Configuration
- HTTP vs HTTPS
- SSL/TLS Basics
- Self-Signed SSL Certificates
- Web Server Security
- Linux Networking Basics

---

# 📋 Prerequisites

Before starting this project, ensure that you have:

- Fedora installed
- Internet Connection
- Root or sudo privileges
- A static website (HTML/CSS/JavaScript)
- Basic Linux command-line knowledge

---

# 📥 Clone this Repository

```bash
git clone https://github.com/anindita8671/linux-web-server-deployment.git
```

```bash
cd linux-web-server-deployment
```

---

# ⚙️ Installation & Configuration

Follow the steps below to deploy the web server from scratch.

# 🚀 Step 1: Update the System

Before installing any packages, update the system to ensure all repositories and installed packages are up to date.

```bash
sudo dnf update -y
```

---

# 🖥 Step 2: Check the Hostname

Verify the hostname of your Linux machine.

```bash
hostnamectl
```

Example Output

```
Operating System: Fedora
Kernel: Linux
Architecture: x86-64
```

---

# 🌐 Step 3: Check the Server IP Address

To access the web server from another device on the same network, determine the server's IP address.

```bash
hostname -I
```

Example

```
192.168.1.10
```

This IP will be used later to access the hosted website.

---

# 📦 Step 4: Install Apache HTTP Server

Install Apache using the DNF package manager.

```bash
sudo dnf install httpd -y
```

Verify the installation

```bash
httpd -v
```

Expected Output

```
Server version: Apache/2.4.x
```

---

# ▶ Step 5: Start Apache Service

Start the Apache web server.

```bash
sudo systemctl start httpd
```

---

# 🔄 Step 6: Enable Apache at Boot

Configure Apache to start automatically whenever the server boots.

```bash
sudo systemctl enable httpd
```

---

# ✅ Step 7: Verify Apache Status

Check whether Apache is running successfully.

```bash
sudo systemctl status httpd
```

Expected Status

```
Active: active (running)
```

---

# 🌍 Step 8: Verify Apache is Listening on Port 80

Apache should now be listening on HTTP Port 80.

```bash
sudo ss -tulpn | grep :80
```

Expected Output

```
LISTEN 0 511 *:80
```

This confirms that Apache is ready to accept HTTP requests.

---

# 📂 Step 9: Verify the Default Web Directory

Apache serves web pages from

```text
/var/www/html
```

Check the directory

```bash
ls /var/www/
```

Expected Output

```
html
```

---

# 📁 Step 10: Copy Website Files

Copy your website into Apache's document root.

Example

```bash
sudo cp -r ~/web-server-project/* /var/www/html/
```

Verify

```bash
ls /var/www/html
```

Example Output

```
index.html
style.css
script.js
images/
```

---

# 👤 Step 11: Change Ownership

Assign ownership of the website files to Apache.

```bash
sudo chown -R apache:apache /var/www/html
```

### Why?

Apache runs using the **apache** user.

Changing ownership ensures Apache has ownership of all website files and directories.

The **-R** option applies the ownership recursively to every file and folder.

Verify

```bash
ls -l /var/www/html
```

---

# 🔐 Step 12: Set File Permissions

Configure the required permissions for the website.

```bash
sudo chmod -R 755 /var/www/html
```

### Why?

755 means

| User | Permission |
|------|------------|
| Owner | Read, Write, Execute |
| Group | Read, Execute |
| Others | Read, Execute |

This allows Apache to read website files while preventing unauthorized modifications.

Verify

```bash
ls -l /var/www/html
```

---

# 🛡 Step 13: Check SELinux Status

Verify whether SELinux is enabled.

```bash
getenforce
```

Example

```
Enforcing
```

This indicates that SELinux is active.

---

# 🔥 Step 14: Check Firewall Status

Verify whether firewalld is running.

```bash
sudo systemctl status firewalld
```

If inactive, start it.

---

# ▶ Step 15: Start Firewall

```bash
sudo systemctl start firewalld
```

---

# 🔄 Step 16: Enable Firewall at Boot

```bash
sudo systemctl enable firewalld
```

---

# ✅ Step 17: Verify Firewall Status

```bash
sudo systemctl status firewalld
```

Expected Output

```
Active: active (running)
```

---

# 🌍 Step 18: Check Active Firewall Zone

```bash
sudo firewall-cmd --get-active-zones
```

Example

```
public
interfaces: ens192
```

---

# 📋 Step 19: View Allowed Services

```bash
sudo firewall-cmd --list-services
```

Initially, the output may look like

```
cockpit dhcpv6-client ssh
```

Notice that HTTP is not yet allowed.

---

# ➕ Step 20: Allow HTTP Traffic

Permit incoming HTTP traffic through the firewall.

```bash
sudo firewall-cmd --permanent --add-service=http
```

---

# 🔄 Step 21: Reload Firewall Rules

Apply the changes.

```bash
sudo firewall-cmd --reload
```

---

# ✅ Step 22: Verify HTTP Service

```bash
sudo firewall-cmd --list-services
```

Expected Output

```
http ssh dhcpv6-client
```

Now Port **80** is accessible.

---

# 🌐 Step 23: Access the Website

Open any browser on another device connected to the same network.

Enter

```
http://SERVER-IP
```

Example

```
http://192.168.1.10
```

If everything is configured correctly, your website should load successfully.

---

# 🔍 Verification Commands

Apache Status

```bash
sudo systemctl status httpd
```

Apache Listening Port

```bash
sudo ss -tulpn | grep :80
```

Firewall Services

```bash
sudo firewall-cmd --list-services
```

Server IP

```bash
hostname -I
```

SELinux Status

```bash
getenforce
```

---

# 📌 What We Achieved So Far

At this stage, we have successfully:

- Installed Apache HTTP Server
- Started and enabled Apache
- Hosted a static website
- Configured file ownership
- Configured Linux file permissions
- Verified SELinux status
- Configured firewalld
- Allowed HTTP traffic
- Successfully accessed the website using HTTP

The next step is to secure the web server by enabling HTTPS using a Self-Signed SSL Certificate.

# 🔐 Step 24: Install SSL Module for Apache

Apache requires the **mod_ssl** package to support HTTPS connections.

Install the SSL module:

```bash
sudo dnf install mod_ssl -y
```

Verify the installation

```bash
rpm -q mod_ssl
```

Expected Output

```
mod_ssl-<version>
```

---

# 📁 Step 25: Generate a Self-Signed SSL Certificate

Generate a new Self-Signed SSL Certificate using OpenSSL.

```bash
sudo openssl req -x509 -nodes -days 365 \
-newkey rsa:2048 \
-keyout /etc/pki/tls/private/server.key \
-out /etc/pki/tls/certs/server.crt
```

During the process, provide the requested information.

Example:

```
Country Name: IN
State: West Bengal
Locality: Kolkata
Organization: Project
Organizational Unit: IT
Common Name: YOUR_SERVER_IP
Email Address: example@email.com
```

**Note:** For the **Common Name**, enter your server's IP address if you are accessing the website using the IP.

---

# 📂 Step 26: Verify Certificate Files

Certificate

```bash
ls /etc/pki/tls/certs/
```

Expected Output

```
server.crt
```

Private Key

```bash
ls /etc/pki/tls/private/
```

Expected Output

```
server.key
```

---

# ⚙ Step 27: Configure Apache SSL

Open the SSL configuration file.

```bash
sudo vim /etc/httpd/conf.d/ssl.conf
```

Locate the following directives.

```apache
SSLCertificateFile
```

and

```apache
SSLCertificateKeyFile
```

Update them as follows.

```apache
SSLCertificateFile /etc/pki/tls/certs/server.crt

SSLCertificateKeyFile /etc/pki/tls/private/server.key
```

Save the file.

---

# ✅ Step 28: Verify Apache Configuration

Before restarting Apache, verify that the configuration contains no syntax errors.

```bash
sudo apachectl configtest
```

Expected Output

```
Syntax OK
```

---

# 🔄 Step 29: Restart Apache

Restart Apache to apply the SSL configuration.

```bash
sudo systemctl restart httpd
```

Verify

```bash
sudo systemctl status httpd
```

Expected Output

```
Active: active (running)
```

---

# 🔥 Step 30: Allow HTTPS through Firewall

Allow HTTPS traffic.

```bash
sudo firewall-cmd --permanent --add-service=https
```

Reload the firewall.

```bash
sudo firewall-cmd --reload
```

Verify.

```bash
sudo firewall-cmd --list-services
```

Expected Output

```
http https ssh
```

---

# 🌐 Step 31: Verify Apache is Listening on Port 443

```bash
sudo ss -tulpn | grep :443
```

Expected Output

```
LISTEN 0 511 *:443
```

Apache is now listening for HTTPS connections.

---

# 🌍 Step 32: Access the Website using HTTPS

Open your browser.

Visit

```
https://SERVER-IP
```

Example

```
https://192.168.1.10
```

Since this is a Self-Signed Certificate, your browser will display a warning.

Click

```
Advanced

↓

Proceed to Website
```

Your website should now load securely over HTTPS.

---

# 🔒 How Security Works in this Project

## Firewall (firewalld)

The firewall controls incoming network traffic.

Its responsibilities include:

- Allow HTTP traffic on Port 80.
- Allow HTTPS traffic on Port 443.
- Block unwanted network connections.
- Reduce the server's attack surface.

Request Flow

```
Browser

↓

Firewall

↓

Apache
```

If HTTP/HTTPS is blocked, Apache never receives the request.

---

## HTTPS (SSL/TLS)

HTTPS encrypts communication between the browser and the web server.

During connection:

```
Browser

↓

SSL/TLS Handshake

↓

Encrypted Connection

↓

Apache

↓

Website
```

The data exchanged between the client and server cannot be read by unauthorized users.

---

## Linux File Permissions

Apache must have permission to access website files.

Ownership

```bash
sudo chown -R apache:apache /var/www/html
```

Permissions

```bash
sudo chmod -R 755 /var/www/html
```

These commands ensure that Apache can read the website files while maintaining secure access permissions.

---

# 🔍 Verification Commands

Check Apache Status

```bash
sudo systemctl status httpd
```

Check Firewall

```bash
sudo firewall-cmd --list-services
```

Check HTTP Port

```bash
sudo ss -tulpn | grep :80
```

Check HTTPS Port

```bash
sudo ss -tulpn | grep :443
```

Check Server IP

```bash
hostname -I
```

Check SELinux Status

```bash
getenforce
```

---


# 🛠 Troubleshooting

## Apache Service Not Running

```bash
sudo systemctl status httpd
```

Check logs

```bash
journalctl -xeu httpd
```

---

## Firewall Blocking Website

Verify services

```bash
sudo firewall-cmd --list-services
```

Allow HTTP

```bash
sudo firewall-cmd --permanent --add-service=http
```

Allow HTTPS

```bash
sudo firewall-cmd --permanent --add-service=https
```

Reload

```bash
sudo firewall-cmd --reload
```

---

## SSL Configuration Error

Verify configuration

```bash
sudo apachectl configtest
```

---

## Website Not Loading

Verify Apache

```bash
sudo systemctl status httpd
```

Verify ports

```bash
sudo ss -tulpn
```

Verify website files

```bash
ls /var/www/html
```

Verify permissions

```bash
ls -l /var/www/html
```

---

# 📚 Learning Outcomes

Through this project, I gained practical knowledge of:

- Linux System Administration
- Apache HTTP Server
- Linux Networking
- Service Management using systemctl
- Firewall Configuration using firewalld
- HTTP & HTTPS Communication
- SSL/TLS Encryption
- Self-Signed SSL Certificates
- Linux File Permissions
- Web Server Deployment
- Linux Security Fundamentals
