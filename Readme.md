#  SmartScale: Intelligent EC2 Auto Scaling and Alerting Platform

##  Project Overview

SmartScale is an enterprise-style AWS automation project that demonstrates intelligent infrastructure scaling based on real-time CPU utilization. The system continuously monitors EC2 performance and automatically launches new EC2 instances when CPU usage exceeds the defined threshold, ensuring high availability and performance stability.
In addition, real-time email notifications are sent to administrators during scaling events using Amazon SNS.
This project simulates real-world production architecture and follows AWS best practices for monitoring, scaling, and alerting.

---
![alt text](<WhatsApp Image 2026-03-01 at 16.29.34.jpeg>)
##  Problem Statement

Traditional server-based systems suffer from:

- Fixed infrastructure capacity  
- Manual scaling delays  
- Risk of downtime during traffic spikes  
- Inefficient resource utilization  

SmartScale solves these problems through automated, event-driven scaling.

---

## Project Objectives

- Automate EC2 scaling based on CPU utilization  
- Maintain identical configuration across instances  
- Implement proactive alerting via email  
- Achieve high availability and fault tolerance  
- Reduce manual operational overhead  

---

##  AWS Services Used

- Amazon EC2  
- Amazon Machine Image (AMI)  
- Launch Template  
- Auto Scaling Group (ASG)  
- Amazon CloudWatch  
- Amazon SNS  
- Amazon VPC  
- Security Groups  
- Nginx  

---

##  Architecture Flow

1. User accesses the application hosted on EC2 via Nginx  
2. CloudWatch continuously monitors CPU utilization  
3. When CPU exceeds 50%, CloudWatch alarm triggers  
4. Auto Scaling policy executes  
5. Auto Scaling Group launches a new EC2 instance  
6. Launch Template uses custom AMI for identical configuration  
7. New instance becomes healthy and serves traffic  
8. SNS sends real-time email notification  

---

##  Step-by-Step Implementation

##  Step 1 : EC2 Setup and Web Server Configuration

- Launch EC2 instance (Amazon Linux)  
![alt text](<Screenshot 2026-02-23 173056.png>)
* open linux terminal : Enter below command
* ssh -i ./downloads/key.pem ec2-user@ip
* Install and configure Nginx 
* sudo yum update -y
* sudo yum install nginx -y
* sudo systemctl start nginx
* sudo systemctl enable nginx
* Verify application via public IP  
---

## Step 2 : Create Custom AMI

- Select configured EC2 instance  
- Create AMI to preserve configuration  
- Wait until AMI status is available  

![alt text](<Screenshot 2026-02-23 183615.png>)

---

##  Step 3 : Configure Launch Template

- Select custom AMI  
- Choose instance type (t2.micro)  
- Attach security group and key pair  
- Create launch template

![alt text](<Screenshot 2026-02-23 184049.png>)  

## Step 4 : Create Auto Scaling Group

Configuration:

- Minimum capacity: 1  
- Desired capacity: 1  
- Maximum capacity: 3  
- Select multiple subnets  
- Enable health checks  

![alt text](<Screenshot 2026-02-23 184249.png>)

---

## Step 5 : Configure SNS Email Alerts

- Create SNS topic  
- Create email subscription  
- Confirm subscription from email  

![alt text](<Screenshot 2026-02-23 185127.png>)

![alt text](<Screenshot 2026-02-23 185931.png>)

---

## Step 6 : CloudWatch Alarm Configuration

- Monitor EC2 CPUUtilization  
- Threshold: > 50%  
- Attach SNS topic for notifications  

![alt text](<Screenshot 2026-02-23 190408.png>)
---

###  Step 7 : Create Dynamic Scaling Policy

- Policy type: Target tracking  
- Metric: Average CPU utilization  
- Target value: 50%  
- Instance warmup: 300 seconds  

![alt text](<Screenshot 2026-02-23 191444.png>)

---

## Step 8 : Testing and Validation

- Generate artificial CPU load using stress tool 

**Test Command:**

* sudo yum install stress -y
* tress --cpu 2 --timeout 300


![alt text](<Screenshot 2026-02-23 193234.png>)
- Observe automatic EC2 launch 

![alt text](<Screenshot 2026-02-23 192837.png>) 
- Verify email notification
- Confirm identical application output   

![alt text](<Screenshot 2026-02-23 193903.png>)

## Summary : 
SmartScale is an AWS-based automation project that demonstrates intelligent EC2 auto scaling driven by real-time CPU monitoring. An EC2 instance running Nginx is continuously monitored using Amazon CloudWatch, and when CPU utilization exceeds the defined threshold, an Auto Scaling Group automatically launches a new instance using a custom AMI to maintain performance and availability. The system also integrates Amazon SNS to send real-time email alerts during scaling events. This project showcases a production-style, self-healing cloud architecture that improves reliability, scalability, and operational efficiency.
