# Cloud & Infrastructure as a Service – Demo Project

## Overview

This project demonstrates how to create and configure a cloud server and deploy a Java application using Infrastructure as a Service (IaaS) on **AWS EC2**.

---

## Technologies Used

* AWS EC2
* Linux (Ubuntu)
* Java
* Gradle
* SSH

---

## Project Features

* Provision and configure an EC2 instance on AWS
* Secure server access using SSH keys
* Create and manage a new Linux user (best practice)
* Build the application locally using Gradle
* Deploy and run the application on the server

---

## Architecture

* Cloud Provider: AWS
* Instance Type: EC2 (Ubuntu)
* Access: SSH using private key
* Deployment: Manual using SCP + SSH

---

## Setup & Deployment Steps

### 1. Launch EC2 Instance

* Create a new EC2 instance (Ubuntu)
* Download `.pem` key
* Allow SSH (port 22) in Security Group

---

### 2. Connect to Server

```bash
ssh -i your-key.pem ubuntu@your-ec2-public-ip
```

---

### 3. Create New User

```bash
sudo adduser hassan
sudo usermod -aG sudo hassan
```

---

### 4. Copy SSH Access to New User

```bash
sudo mkdir -p /home/hassan/.ssh
sudo cp /home/ubuntu/.ssh/authorized_keys /home/hassan/.ssh/
sudo chown -R hassan:hassan /home/hassan/.ssh
sudo chmod 700 /home/hassan/.ssh
sudo chmod 600 /home/hassan/.ssh/authorized_keys
```

---

### 5. Build Application Locally

```bash
gradle build
```

---

### 6. Upload Application

```bash
scp -i ~/your-key.pem build/libs/app.jar hassan@your-ip:/home/hassan
```

---

### 7. Run Application

```bash
ssh -i your-key.pem hassan@your-ip
java -jar app.jar
```

---

## Security Best Practices

* Avoid using root user
* Use SSH key authentication instead of passwords
* Assign sudo privileges only when needed
* Restrict permissions on `.pem` files

---

## Notes

* Ensure correct Java version is installed on server
* Make sure `.pem` file has correct permissions:

```bash
chmod 400 your-key.pem
```

---

## Author

Hassan Ali Salama

---

## Status

Completed – Basic IaaS deployment using AWS EC2
