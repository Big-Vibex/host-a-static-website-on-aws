![Alt text](/Host_a_Static_Website_on_AWS.png)
````
# Host a Static Website on AWS

This DevOps project demonstrates how to host a static HTML website on AWS using a secure and scalable architecture. The web application is deployed on EC2 instances in private subnets, behind an Application Load Balancer (ALB), and managed via an Auto Scaling Group to ensure high availability and fault tolerance.


## 🛠️ Infrastructure Overview

The following AWS services and resources were utilized:

1. **Virtual Private Cloud (VPC)**  
   - Configured with both public and private subnets across two Availability Zones for high availability.

2. **Internet Gateway**  
   - Enables communication between instances in the VPC and the internet.

3. **Security Groups**  
   - Act as virtual firewalls to control traffic to EC2 instances and other services.

4. **Availability Zones (AZs)**  
   - Leveraged two AZs for improved redundancy and fault tolerance.

5. **Public Subnets**  
   - Hosted NAT Gateway and Application Load Balancer.

6. **Private Subnets**  
   - Deployed EC2 web servers securely within private subnets.

7. **EC2 Instance Connect Endpoint**  
   - Secure SSH access to instances in both public and private subnets without exposing them to the internet.

8. **NAT Gateway**  
   - Allowed instances in private subnets to access the internet for updates and package installations.

9. **EC2 Instances**  
   - Hosted the Apache HTTP server and served the static website.

10. **Application Load Balancer (ALB)**  
    - Distributed incoming traffic evenly across EC2 instances in different AZs.

11. **Auto Scaling Group (ASG)**  
    - Automatically adjusted the number of EC2 instances based on demand.

12. **GitHub**  
    - Used for storing and version-controlling web content and deployment scripts.

13. **AWS Certificate Manager**  
    - Provided SSL/TLS certificates for securing application traffic.

14. **Amazon SNS**  
    - Configured to send alerts and notifications related to the Auto Scaling Group.

15. **Route 53**  
    - Managed domain registration and DNS configuration for the web application.

## 🚀 Deployment Script

Below is the Bash script used to initialize and deploy the static site on EC2 instances:

```bash
#!/bin/bash

# Switch to root user
sudo su

# Update packages
yum update -y

# Install Apache HTTP Server (corrected from 'htpd')
yum install -y httpd

# Move to Apache web root
cd /var/www/html

# Install Git
yum install git -y

# Clone project repository
git clone https://github.com/aosnotes77/host-a-static-website-on-aws.git

# Copy web files to Apache root
cp -R host-a-static-website-on-aws/. /var/www/html/

# Clean up
rm -rf host-a-static-website-on-aws

# Enable and start Apache
systemctl enable httpd
systemctl start httpd
````

⚠️ **Note**: Ensure the package name `httpd` is spelled correctly (not `htpd`).

**Repository Link**
The project is available on GitHub: [host-a-static-website-on-aws](https://github.com/Big-Vibex/host-a-static-website-on-aws
)
## 🧩 Key Features

* Secure VPC design with private web servers
* Highly available across multiple AZs
* Scalable using Auto Scaling Groups
* Git-integrated deployment workflow
* SSL-enabled and DNS-configured
