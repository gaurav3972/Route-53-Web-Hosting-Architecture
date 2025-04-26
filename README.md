# Route-53-Web-Hosting-Architecture
## Route 53 using S3 and EC2
In this project, we will design a Route 53 with s3 bucket & ec2 server using Domain name: patilenterprises.shop
## Learning Objectives
Upon completion of this project we will be able to create, configure and test the following:

* configure Amazon Route 53 for DNS management.

* launch and manage an Amazon EC2 instance.

* create and configure an Amazon S3 bucket for static file hosting.

* connect a domain name to an EC2 instance using Route 53.

* serve static content (images, CSS) from an S3 bucket.

## Prerequisites

* active AWS account.

* Basic knowledge of AWS services (EC2, S3, Route 53).

* AWS CLI installed and configured on your local machine.

* A registered domain name (either within Route 53 or another registrar).

* Understanding of basic networking concepts (IP addresses, DNS).

* A basic web application or HTML page to deploy (optional for testing).
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

## 3. Configure Route 53
* Open the Route 53 console.

* Create or use an existing Hosted Zone for your domain.

* Create Record Sets:

* A Record: Point your domain to your EC2 instance’s public IP address.

* CNAME Record (optional): Map a subdomain (like static.example.com) to your S3 static website endpoint.

## Example Scenario
* A user accesses www.patilenterprises.shop

* Route 53 resolves the domain to the EC2 instance IP where the application is hosted.

* The EC2 application loads static files (images, CSS) directly from the S3 bucket.
## Best Practices
* Use an Elastic IP for your EC2 instance to avoid IP address changes.

* Restrict S3 bucket access using bucket policies if static website hosting is enabled.

* Set up SSL/TLS certificates using AWS Certificate Manager.

* (Optional) Use CloudFront CDN for faster content delivery and improved security.
