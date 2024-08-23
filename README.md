# VPC Endpoints
## What is Amazon VPC?
Amazon Virtual Private Cloud (Amazon VPC) is a service that gives you full control over your virtual networking environment. It allows you to manage the configuration of your network, including the placement of resources, the connectivity between them, and the security measures you put in place.

## How I Used Amazon VPC in This Project
I used Amazon VPC to create my own network with a public subnet inside it. I also launched an EC2 instance inside it which I used to access other aws resource such as S3 bucket.

## Unexpected Learnings
One thing I didn’t expect was that VPC endpoints can be configured using policies too. This feature provided additional flexibility and control over how my resources communicated within the VPC.

## Project Duration
This project took me approximately **1 hour and 15 minutes** to complete.

## Project Steps

### Step 1: Architecture Set Up

In this step, I created a **VPC** and launched an **EC2 instance** inside it. This setup allowed me to access other AWS resources from the EC2 instance. 

### Step 2: Connect to EC2 Instance

I connected to my EC2 instance and accessed the **S3** service through the public internet, ensuring the instance was correctly configured within the VPC.

### Step 3: Set Up Access Keys

Since the EC2 instance needs an access key to verify my identity and grant permissions to view and use other AWS resources, I created the necessary access keys.

### Step 4: Interact with S3 Bucket

With the access keys set up, I used the EC2 instance to view and interact with files stored in an S3 bucket.

## Architecture set up
I started my project by launching an EC2 instance named "Instance - NextWork VPC Endpoints" inside a VPC. I also set up a S3 bucket named "nextwork-vpc-endpoints-nis" and uploaded few files.

## Access keys
### Credentials
To set up my EC2 instance to interact with my AWS environment, I configured access keys. Through that access key I can use/view aws resources through an EC2 instace. Access keys are the credentials which is use to validate us and help to use other aws resources from an EC2 instance. secret access key are like the password that pairs with access key ID. Both of them are required to access AWS services.
### Best practice
Although I'm using access keys in this project, a best practice alternative is touse to create an IAM role with the necessary permissions and then attaching that role to your EC2 instance.

## Connecting to my S3 bucket
The command I ran was "aws s3 ls". This command is used to list all the files inside a S3 bucket. The terminal responded with the name of my S3 bucket I created. This indicated that the access keys I set up worked correctly. I also tested the command "aws s3 ls s3://nextwork-vpc-endpoints-nis" which returned all the files inside the S3 bucket. 

## Uploading objects to S3
To upload a new file to my bucket, I first ran the command sudo touch /tmp/nextwork.txt. This command creates file named nextwork which is a text file. The second command I ran was 'aws s3 cp /tmp/nextwork.txt s3://nextworkvpcproject-nis'. This command will copy file to the path mentioned. The third command I ran was 'aws s3 ls s3://nextwork-vpc-project-nis' whichvalidated that I sucessfully copied the file to the path 
 mentioned.

## In the second part of my project...
### Step 5  Set up a Gateway
In this step I am going to create a VPC endpoint which allows an EC2 instance to connect to S3 bucket or any other aws resources directly without using the traffic through public internet.

### Step 6  Bucket policies
In this step I am going to block off S3 bucket from ALL traffic except traffic coming from the endpoint. 

### Step 7  Update route tables
In this step I am going to check whether my configurations has worked or not.

### Step 8  Validate endpoint conection
As I have modified the route table I am again going to validate the EC2 instance to interact with the S3 bucket.

## Setting up a Gateway
I set up an S3 Gateway, which is particularly created for a VPC to connect with S3.

## What are endpoints?
An endpoint in AWS is a service that allows private connections between your VPC and other AWS services without needing the traffic to go over the internet.

## Bucket policies
A bucket policy is a type of IAM policy designed for setting access permissions to an S3 bucket. Using bucket policies, you get to decide who can access the bucket and what actions they can perform with it My bucket policy will block all the traffic except traffic coming from the VPC endpoint.
Right after saving my bucket policy, my S3 bucket page showed 'denied access' warnings. This was because attempt to access the bucket from othersources, including the AWS Management Console, is blocked. I also had to update my route table because route table doesn't have a route that directs traffic bound for S3 to the VPC endpoint. So, traffic from EC2 instance is actually trying to get to the S3 bucket through the public internet. 

## Route table updates
To update my route table, I modified the route tables of endpoints. After updating my public subnet's route table, my terminal could return all the files inside my S3 bucket.

## Endpoint policies
An endpoint policy is a quicker way to give/deny away access to your AWS services. I updated my endpoint's policy by chainging Effect: Allow to Effect : Deny. I could see the effect of this right away, because I could not acces S3 bucket from the EC2 instance. 








