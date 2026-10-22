<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Access S3 from a VPC

**Project Link:** [View Project](https://nextwork.ai/projects/36d7dc8f-3a9f-51ff-91ae-662077ea9920)

**Author:** Sammy Shah Saleh  
**Email:** sammysaleh769@gmail.com

---

![Image](https://nextwork.ai/sammy769/uploads/36d7dc8f-3a9f-51ff-91ae-662077ea9920_3e1e79a2)

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC (Virtual Private Cloud) allows me to create an isolated virtual network in AWS where I can launch and manage resources such as EC2 instances. 

### How I used Amazon VPC in this project

In this project, I created a VPC with a public subnet and an Internet Gateway, then launched an EC2 instance inside it to interact with my Amazon S3 bucket using the AWS CLI.

### One thing I didn't expect in this project was...

One thing I didn't expect was how powerful access keys are. I learnt that they work like credentials for applications and can allow access to AWS resources, depending on the permissions associated with them. I also realised how important it is to keep secret access keys private and secure.

### This project took me...

This project took me about one hour or slightly longer to complete.

## In the first part of my project...

### Step 1 - Architecture set up

In this step, I created a VPC from scratch and launched an EC2 instance inside it to prepare the network environment for interacting with Amazon S3.

### Step 2 - Connect to my EC2 instance

In this step, I connected to my EC2 instance and tested whether I could access AWS services from the instance.

### Step 3 - Set up access keys

In this step, I configured AWS access keys so that my EC2 instance could authenticate with AWS services and interact with my AWS environment through the AWS CLI.

## Architecture set up

I created a VPC with one public subnet and an Internet Gateway in a single Availability Zone. I also launched an EC2 instance in the VPC to prepare for interacting with Amazon S3. The EC2 instance used the AWS CLI to communicate with Amazon S3. Because I did not configure an S3 VPC endpoint in this project, the instance accessed S3 through the service's public endpoint using its available network connectivity.

I uploaded two JPEG image files to my Amazon S3 bucket so that I could practise accessing and listing the stored objects from my EC2 instance using the AWS CLI.

![Image](https://nextwork.ai/sammy769/uploads/36d7dc8f-3a9f-51ff-91ae-662077ea9920_4334d777)

## Running CLI commands

AWS CLI (Command Line Interface) is a tool that allows me to interact with AWS services by running commands in a terminal. It was pre-installed on my EC2 instance.



The first command I ran was `aws s3 ls`. This command lists the Amazon S3 buckets that my current AWS credentials have permission to list.

The second command I ran was `aws configure`. This command allowed me to configure my AWS access key ID, secret access key, default AWS Region and output format. The AWS CLI then used the configured credentials when making requests to AWS services.

![Image](https://nextwork.ai/sammy769/uploads/36d7dc8f-3a9f-51ff-91ae-662077ea9920_e7fa8776)

## Access keys

### Credentials

The `aws configure` command stored my AWS CLI settings and credentials so that the CLI could use them when making requests to AWS services, such as Amazon S3.

AWS access keys are credentials used by the AWS CLI and applications to authenticate programmatic requests to AWS. They consist of an access key ID and a secret access key. The access key ID identifies the credentials, while the secret access key is used to sign requests. The permissions associated with the IAM user or other identity determine which AWS resources those credentials can access.

A secret access key must be kept private and secure. If someone obtains it, they may be able to access AWS resources using the associated identity's permissions. I should never share it publicly or commit it to a GitHub repository.

### Best practice

Although I used access keys in this project, the recommended approach for an EC2 instance is to attach an IAM role through an instance profile. The instance can then obtain temporary security credentials automatically, without requiring me to store long-term access keys on it. I should also follow the principle of least privilege by granting only the permissions the instance needs.

## In the second part of my project...

### Step 4 - Set up an S3 bucket

In this step, I created an Amazon S3 bucket and uploaded two JPEG image files so that I could practise accessing the bucket from my EC2 instance.


### Step 5 - Connecting to my S3 bucket

In this step, I returned to my EC2 instance and used the AWS CLI to access my Amazon S3 bucket and list its stored objects.

## Connecting to my S3 bucket

The first command I ran was `aws s3 ls`. This command lists the Amazon S3 buckets that my current AWS credentials have permission to list.

When I ran the `aws s3 ls` command again, the terminal displayed a list of the S3 buckets in my AWS account that my credentials had permission to access. This indicated that the AWS CLI was successfully authenticated and could access my Amazon S3 resources.

![Image](https://nextwork.ai/sammy769/uploads/36d7dc8f-3a9f-51ff-91ae-662077ea9920_4334d778)

## Connecting to my S3 bucket

Another command I ran was `aws s3 ls s3://s3-vpc-project-bucket`. It listed the two JPEG files, `cloud.jpeg` and `image.jpeg`, stored in my S3 bucket, along with their last-modified dates and file sizes. This confirmed that my EC2 instance could successfully access the bucket and list its objects using the AWS CLI.

![Image](https://nextwork.ai/sammy769/uploads/36d7dc8f-3a9f-51ff-91ae-662077ea9920_4334d779)

## Uploading objects to S3

I created an empty text file named `main.txt` on my EC2 instance using the `sudo touch main.txt` command.

I then used `aws s3 cp main.txt s3://s3-vpc-project-bucket ` to upload the file to my S3 bucket. The terminal confirmed that the upload was successful.

Finally, I ran `aws s3 ls` to list my S3 buckets and `aws s3 ls s3://s3-vpc-project-bucket` to check the objects inside my project bucket. The output showed `main.txt` alongside the two JPEG images, confirming that my EC2 instance could upload files to Amazon S3 successfully.

![Image](https://nextwork.ai/sammy769/uploads/36d7dc8f-3a9f-51ff-91ae-662077ea9920_3e1e79a2)

---

*Built with [NextWork](https://nextwork.ai) - [View this project](https://nextwork.ai/projects/36d7dc8f-3a9f-51ff-91ae-662077ea9920)*
