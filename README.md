# 🚀 Deploying a Static Website on AWS with Docker, Amazon ECR, and Amazon ECS

This project demonstrates how to deploy a **static website** on **AWS** using **Docker, Amazon ECR, and Amazon ECS**, automating containerization, image storage, and scalable deployment.

---

## 📂 Project Files

- **Dockerfile** – Defines the container image for the static website using **Amazon Linux** and **Apache (httpd)**.

---

## 🛠️ Deployment Process

### 1️⃣ Set up AWS infrastructure

- Create **VPC, Subnets, Internet Gateway, NAT Gateway, Route Tables, and Security Groups**.

### 2️⃣ Install Docker

- Set up **Docker** and build the container image for the static website.

### 3️⃣ Create Dockerfile & Build Image

Use the following **Dockerfile** to build the container image:

```dockerfile
FROM amazonlinux:latest

# Install dependencies
RUN yum update -y && \
    yum install -y httpd && \
    yum search wget && \
    yum install wget -y && \
    yum install unzip -y

# Change directory
WORKDIR /var/www/html

# Download webfiles
RUN wget https://github.com/azeezsalu/jupiter/archive/refs/heads/main.zip

# Unzip folder
RUN unzip main.zip

# Copy files into HTML directory
RUN cp -r jupiter-main/* /var/www/html/

# Remove unwanted files
RUN rm -rf jupiter-main main.zip

# Expose port 80 on the container
EXPOSE 80

# Set the default application to start when the container runs
ENTRYPOINT ["/usr/sbin/httpd", "-D", "FOREGROUND"]
```

### 4️⃣ Push Image to ECR

- Store the container image in **Amazon Elastic Container Registry (ECR)**.

### 5️⃣ Deploy to Amazon ECS

- Create an **ECS cluster**, register the task definition, and launch the service with **AWS Fargate**.

### 6️⃣ Configure Load Balancer & Domain Name

- Use **AWS ALB** and **Route 53** for traffic management and domain mapping.

### 7️⃣ Enable SSL/TLS

- Secure the website with **AWS Certificate Manager**.

---

## 📖 Step-by-Step Guide

For detailed steps, check out the **Medium Article**:\
📌 [Deploying a Static Website on AWS with Docker, Amazon ECR, and Amazon ECS](https://medium.com/@smaddy799/587d8f9041a1)

---

## 💡 Key Features

✅ **Automated Deployment** – Fully automated using Docker and AWS services.\
✅ **Scalable & Secure** – ECS with Fargate, ALB for load balancing, Route 53 for domain mapping, and SSL encryption.\
✅ **Serverless Infrastructure** – No need to manage EC2 instances, fully managed AWS container service.

---
