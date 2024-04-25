# How to Setup a aws Three Tier Application
***


## Prerequesties
  * Knowledge of AWS EC2 Service
  * Knowledge of AWS S3 Bucket
  * Knowledge of AWS IAM Service
  * Knowledge of AWS VPC Service
  * Knowledge of AWS RDS

## Concept of AWS Three Tier Architecture

### Need of AWS Three Tier Web Architecture

By separating your application into distinct tiers for presentation, application, and data, you can improve scalability, reliability, security, and maintainability. With the wide range of AWS services and tools available, it's easy to set up and manage a 3-tier architecture in the cloud.

![Three Tier Architecture](https://miro.medium.com/v2/resize:fit:828/format:webp/1*r4vO86K8M9n5WZkqvTfPvg.png)

As show in the Above Picture There are three Layers.
  * Web Tier: This is the outer layer or the internet facing layer.
  * App Tier: This Layer will connect to the Database which is in layer 3
  * Database Tier: This layer contains the database for the application.


### Step 1

In this Example we are creatina a web app using React App. To get the code we need to download the code from the github link.
You can save that repo anywhere as of now in your system.

[Github repo link](https://github.com/aws-samples/aws-three-tier-web-architecture-workshop)

### Step 2

 * Login to your AWS console and Navigate to the VPC Service. Now in the VPC service create a Vpc using **Your VPCs** option.
 * After creating VPC we need to create Subnets. The subnets we will create will be in across two different AZs. There will be total 6 Subnets. **Public-Subnet-AZ1, Privte-Subnet-AZ1, Private-DB-Subnet-AZ1** and so on for the other AZ.
 * Attaching the Internet Gateway
 * Attaching the NAT Gateways to the Private Subnets
 * Creating Route Tables for the Subnets.There will be three route tables. One for the Public Subnets which will have both the public subnets and other two will be for the Private subnets. After creating tables edit the routes of the table and subnet associations according to the Subnets.

### Step 3
* Create a IAM role for the EC2 Instance and Attach the **AmazonSSMManagedInstanceCore** and **AmazonS3ReadOnlyAccess** policies to it.

### Step 4

* Now Navigate to RDS service and create a Subnet Group create a subnet group and add the **Private-Subnet-AZ1** and **Private-Subnet-AZ2** to it.
* Navigate to the Databases Section and Create a Mysql/Aurora Database with Aurora Replica Reader Node to it.


### Step 5
* Navigate to the EC2 service and setup a EC2 instance with Private Subent that is App tier.

* After creating Private App Tier instances Setup load Balancer and Auto Scaling Groups to it.

* Crate EC2 instances for the Public Web Tier Application with Public Subnet. 

* Setting up a External load balancer that will connected with a Auto Scaling group Attached to it.


