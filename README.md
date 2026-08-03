
# 🔒 Linux Web Server Deployment with Firewall Configuration and HTTPS using Self-Signed SSL Certificate

![Linux](https://img.shields.io/badge/Linux-CentOS%20Stream-red)
![Apache](https://img.shields.io/badge/Apache-httpd-orange)
![Firewall](https://img.shields.io/badge/firewalld-Enabled-success)
![HTTPS](https://img.shields.io/badge/HTTPS-Self--Signed%20SSL-blue)
![License](https://img.shields.io/badge/License-MIT-green)

## 📌 Project Overview

This project demonstrates the deployment of a secure Apache Web Server on a Linux (Fedora) system. The objective is to understand the fundamentals of Linux server administration by hosting a static website while implementing network security using **firewalld** and secure communication using **HTTPS with a Self-Signed SSL Certificate**.

The project simulates the responsibilities of a Linux System Administrator by configuring and securing a web server for local network access.

---

# 🎯 Objectives

- Deploy a static website using Apache HTTP Server.
- Configure Linux Firewall (`firewalld`) to allow only required services.
- Enable HTTPS using a Self-Signed SSL Certificate.
- Understand HTTP and HTTPS communication.
- Learn basic Linux server administration.
- Demonstrate secure web server deployment.

---

# 🛠 Technologies Used

| Category | Technology |
|-----------|------------|
| Operating System | Fedora |
| Web Server | Apache HTTP Server (httpd) |
| Firewall | firewalld |
| Security | OpenSSL |
| Protocols | HTTP, HTTPS |
| Website | HTML, CSS |

---

# 📂 Project Structure

```
Linux-Web-Server-Deployment/
│
├── website/
│   ├── index.html
|
├── README.md

```

---

# ⚙️ Project Architecture Diagram

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

# 🚀 Features

- Apache HTTP Server Deployment
- Static Website Hosting
- HTTP Support
- HTTPS Support using Self-Signed SSL Certificate
- Firewall Configuration using firewalld
- Secure Communication using SSL/TLS
- Local Network Website Access
- Linux Service Management using systemd

---

# 🔥 Firewall Configuration

The firewall is configured using **firewalld** to control incoming network traffic.

Allowed Services:

- HTTP (Port 80)
- HTTPS (Port 443)

The firewall ensures that only required services are accessible while reducing unnecessary network exposure.

---

# 🔐 HTTPS Implementation

HTTPS is enabled using a Self-Signed SSL Certificate generated with OpenSSL.

This provides:

- Encrypted communication
- SSL/TLS handshake
- Secure browser-server communication
- Practical understanding of HTTPS deployment

Since the certificate is self-signed, browsers display a warning, which is expected in local development environments.

---

# 📦 Installation

## Update the System

```bash
sudo dnf update -y
```

---

## Install Apache

```bash
sudo dnf install httpd -y
```

---

## Start Apache

```bash
sudo systemctl enable httpd
sudo systemctl start httpd
```

---

## Install SSL Module

```bash
sudo dnf install mod_ssl -y
```

---

## Generate Self-Signed Certificate

```bash
sudo openssl req -x509 -nodes -days 365 \
-newkey rsa:2048 \
-keyout /etc/pki/tls/private/server.key \
-out /etc/pki/tls/certs/server.crt
```

---

## Configure Firewall

```bash
sudo firewall-cmd --permanent --add-service=http
sudo firewall-cmd --permanent --add-service=https
sudo firewall-cmd --reload
```

---

## Restart Apache

```bash
sudo systemctl restart httpd
```

---

# 🌐 Access the Website

HTTP

```
http://SERVER-IP
```

HTTPS

```
https://SERVER-IP
```

---

# 🔍 Verification Commands

Check Apache Status

```bash
sudo systemctl status httpd
```

Check Listening Ports

```bash
sudo ss -tulpn
```

Check Firewall Rules

```bash
sudo firewall-cmd --list-services
```

Check Server IP

```bash
hostname -I
```

---

# 📚 Key Concepts Learned

- Linux Server Administration
- Apache Web Server Deployment
- Service Management with systemd
- Network Ports
- HTTP vs HTTPS
- SSL/TLS Encryption
- Self-Signed Certificates
- Linux Firewall Configuration
- Web Server Security
- Local Network Hosting

---

# 💡 Learning Outcome

Through this project, I gained hands-on experience in deploying and securing a Linux web server. I learned how web servers communicate over HTTP and HTTPS, how firewalld controls network access, and how SSL/TLS encrypts client-server communication using a self-signed certificate.

---



