# Route-53-Web-Hosting-Architecture

## Route 53 using S3 and EC2
In this project, demonstrates how to use Amazon Route 53 to host a website by integrating both Amazon EC2 (for dynamic content) and Amazon S3 (for static files), connected through a custom domain name like patilenterprises.shop. It combines DNS management, web server hosting, and cloud storage to build a complete, scalable web hosting architecture on AWS.
***
![](https://github.com/gaurav3972/Route-53-Web-Hosting-Architecture/blob/main/route%2053/.....png)
## 🎯 What This Project Does
* Hosts a dynamic web application using Amazon EC2.

* Hosts static content (HTML/CSS/JS/images) using an S3 bucket.

* Uses Amazon Route 53 to manage DNS for both EC2 and S3 resources.

* Maps a custom domain (patilenterprises.shop) to:

1. The EC2 instance for the root domain (patilenterprises.shop)

2. The S3 bucket for the www.patilenterprises.shop subdomain
## Learning Objectives

Upon completion of this project we will be able to create, configure and test the following:

* configure Amazon Route 53 for DNS management.

* launch and manage an Amazon EC2 instance.

* create and configure an Amazon S3 bucket for static file hosting.

* connect a domain name to an EC2 instance using Route 53.

* serve static content (images, CSS) from an S3 bucket.
***
## Prerequisites

* active AWS account.

* Basic knowledge of AWS services (EC2, S3, Route 53).

* AWS CLI installed and configured on your local machine.

* A registered domain name (either within Route 53 or another registrar).

* Understanding of basic networking concepts (IP addresses, DNS).

* A basic web application or HTML page to deploy (optional for testing).
* You have to purchase domain name from any where or using route 53 
***
## Setup Instructions
### 1. Set Up EC2 Instance

* Launch an EC2 instance (Amazon Linux 2 or Ubuntu).


* Open inbound ports for HTTP (80) and SSH (22) in the Security Group.

* SSH into the instance and install a web server:(image)

* Deploy a sample application or static website

## 2. Set Up S3 Bucket
* Create a new S3 bucket.

* Upload your static files (e.g., images, CSS, JS).


* Enable public access settings if needed 

* (Optional) Enable Static Website Hosting:
![](https://github.com/gaurav3972/Route-53-Web-Hosting-Architecture/blob/main/route%2053/Screenshot%202025-04-26%20092645.png)
## Step 3: Configure Route 53 DNS Records

After setting up your Hosted Zone and linking your Hostinger domain to AWS nameservers, configure the DNS records in Route 53 as follows:

### 1. Create an A Record for the Root Domain (`yourdomain.com`)

- **Record Type**: A (Alias)
- **Name**: `yourdomain.com`
- **Value**: Public IP Address (or Elastic IP) of your EC2 instance
- **Routing Policy**: Simple

This will make `yourdomain.com` point directly to your EC2-hosted website.

### 2. Create an A Record for the Subdomain (`www.yourdomain.com`)

- **Record Type**: c name(IPv4 address)
- **Name**: `www.yourdomain.com`
- **Alias Target**: S3 Bucket Static Website Endpoint (alias record)
- **Routing Policy**: Simple

This will make `www.yourdomain.com` load your static website from S3.

### Example DNS Table

| Record Type | Name             | Value                                      | Routing Policy |
|-------------|------------------|-------------------------------------------|----------------|
| A           | yourdomain.com    | EC2 Elastic IP address                    | Simple         |
| A (Alias)   | www.yourdomain.com| S3 Static Website Endpoint (Alias Target) | Simple         |
![](https://github.com/gaurav3972/Route-53-Web-Hosting-Architecture/blob/main/route%2053/Screenshot%202025-04-26%20093529.png)

## Important Tips

- **Elastic IP**: If you reboot your EC2 instance without an Elastic IP, its public IP might change. Always use an Elastic IP to avoid DNS mismatch.
- **Propagation Time**: After updating DNS records, changes may take a few minutes to a few hours to propagate globally.
- **Alias Records**: Alias records allow AWS to map DNS to AWS services like S3 buckets easily (no IP address needed).

***
## Best Practices
* Use an Elastic IP for your EC2 instance to avoid IP address changes.

* Restrict S3 bucket access using bucket policies if static website hosting is enabled.

* Set up SSL/TLS certificates using AWS Certificate Manager.

* (Optional) Use CloudFront CDN for faster content delivery and improved security.

*** 
![](https://github.com/gaurav3972/Route-53-Web-Hosting-Architecture/blob/main/route%2053/Screenshot%202025-04-26%20092955.png)
## Notes

* For HTTPS (SSL/TLS), consider using AWS Certificate Manager (ACM) with CloudFront or Load Balancer.

* Ensure your S3 bucket policy allows public access if you want your static site visible.

* Use Elastic IP for your EC2 instance to avoid IP changes on reboot.
  
* DNS propagation after updating route53 or any nameservers may take up to 24 hours.

***
![](https://github.com/gaurav3972/AutoScale-Load-Balancer-with-Route-53-Project/blob/main/images/Screenshot%202025-06-08%20192946.png)
## Summmary
 
Amazon Route 53 is a scalable and highly available Domain Name System (DNS) web service used to route traffic to various AWS services like S3 and EC2. When used with Amazon S3, Route 53 enables you to host static websites by pointing a domain name (such as `www.patilenterprises.shop`) to an S3 bucket configured for static website hosting. The S3 bucket must be named exactly like the domain and have public access enabled or be served through CloudFront. This setup is ideal for websites made with only HTML, CSS, and JavaScript.

In contrast, when working with Amazon EC2, Route 53 can direct domain traffic to an EC2 instance running a dynamic web application using software like Apache, Nginx, or Node.js. By associating an Elastic IP with the EC2 instance, Route 53 can use an A record to map your domain to this IP, ensuring that the site remains reachable even if the instance is restarted. This approach is suitable for more complex, server-side applications that require computing power.

In summary, Route 53 acts as a bridge between your domain name and AWS services like S3 for static websites or EC2 for dynamic ones, offering flexible routing, reliability, and easy integration with the AWS ecosystem.

***
## 🔐 License
This project is licensed under the MIT License — meaning it's open-source and free to use, modify, and distribute.