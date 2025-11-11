![Alt text](/Host_a_Static_Website_on_AWS.png)
 
 
 Hosting a Static Website on AWS

Project Overview

This project demonstrates how to host a static HTML web application on AWS using a fully automated and scalable cloud infrastructure.
The deployment leverages multiple AWS services to ensure high availability, fault tolerance, scalability, and security.

Architecture Summary
Below is an overview of the infrastructure components and configurations used in this project:

Virtual Private Cloud (VPC): Configured with public and private subnets across two Availability Zones (AZs) for high availability.

Internet Gateway (IGW): Enables connectivity between instances in the VPC and the internet.

Security Groups: Act as virtual firewalls controlling inbound and outbound traffic.

Availability Zones: Two AZs are used to improve reliability and fault tolerance.

Public Subnets: Used for internet-facing components such as the NAT Gateway and Application Load Balancer (ALB).

EC2 Instance Connect Endpoint: Allows secure connections to both public and private subnet resources.

Private Subnets: Host EC2 instances running the static web application for enhanced security.

NAT Gateway: Enables private instances to securely access the internet for updates and package installations.

EC2 Instances: Serve the static website content.

Application Load Balancer (ALB): Distributes incoming web traffic evenly across EC2 instances in multiple AZs.

Auto Scaling Group (ASG): Automatically scales the number of EC2 instances based on traffic load and health checks.

GitHub: Used for storing and version-controlling web files.

AWS Certificate Manager (ACM): Provides SSL/TLS certificates to secure web communications.

Simple Notification Service (SNS): Sends alerts about Auto Scaling Group activities.

Amazon Route 53: Manages domain registration and DNS configuration.

 Deployment Script

Below is the user data script used to configure and deploy the web server automatically during EC2 instance launch:

#!/bin/bash
# Switch to root
sudo su

# Update all installed packages
yum update -y

# Install Apache HTTP Server
yum install -y httpd

# Change directory to the Apache web root
cd /var/www/html

# Install Git
yum install git -y

# Clone the project GitHub repository
git clone https://github.com/Dee-code-bar/host-a-static-website-on-aws.git

# Copy all files (including hidden ones) to the web root
cp -R host-a-static-website-on-aws/. /var/www/html/

# Remove the cloned repository directory to clean up
rm -rf host-a-static-website-on-aws

# Enable Apache to start at boot
systemctl enable httpd

# Start Apache web server
systemctl start httpd


🧩 How It Works

The VPC provides a secure and isolated environment for the web infrastructure.

The Load Balancer routes incoming traffic to available EC2 instances across AZs.

The Auto Scaling Group ensures application resilience by automatically launching or terminating instances based on demand.

The NAT Gateway allows instances in private subnets to reach the internet for updates.

The Route 53 domain setup ensures user-friendly access to the website using a custom domain name.

HTTPS is enforced using an SSL/TLS certificate issued by AWS Certificate Manager.
