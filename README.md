# Route-53-Web-Hosting-Architecture

## Route 53 using S3 and EC2
In this project, we will design a Route 53 with s3 bucket & ec2 server using Domain name: patilenterprises.shop
***
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

***
## Important Tips

- **Elastic IP**: If you reboot your EC2 instance without an Elastic IP, its public IP might change. Always use an Elastic IP to avoid DNS mismatch.
- **Propagation Time**: After updating DNS records, changes may take a few minutes to a few hours to propagate globally.
- **Alias Records**: Alias records allow AWS to map DNS to AWS services like S3 buckets easily (no IP address needed).

***
## Example Scenario
* A user accesses www.patilenterprises.shop

* Route 53 resolves the domain to the EC2 instance IP where the application is hosted.

* The EC2 application loads static files (images, CSS) directly from the S3 bucket.
***
## Best Practices
* Use an Elastic IP for your EC2 instance to avoid IP address changes.

* Restrict S3 bucket access using bucket policies if static website hosting is enabled.

* Set up SSL/TLS certificates using AWS Certificate Manager.

* (Optional) Use CloudFront CDN for faster content delivery and improved security.

*** 
## Notes

* For HTTPS (SSL/TLS), consider using AWS Certificate Manager (ACM) with CloudFront or Load Balancer.

* Ensure your S3 bucket policy allows public access if you want your static site visible.

* Use Elastic IP for your EC2 instance to avoid IP changes on reboot.
  
* DNS propagation after updating route53 or any nameservers may take up to 24 hours.

***
## License
This project is licensed under the MIT License.
