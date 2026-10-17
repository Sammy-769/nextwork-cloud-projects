<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Testing VPC Connectivity

**Project Link:** [View Project](https://nextwork.ai/projects/da091986-ef01-5973-a070-b15e174f59d8)

**Author:** Sammy Shah Saleh  
**Email:** sammysaleh769@gmail.com

---

![Image](https://nextwork.ai/sammy769/uploads/da091986-ef01-5973-a070-b15e174f59d8_8ee57662)

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC (Virtual Private Cloud) allows me to create an isolated virtual network within AWS, giving me control over IP address ranges, subnets, route tables and network security.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to test connectivity between my public and private EC2 instances. I used tools such as ping and curl to check network communication and internet access, and configured security groups and network ACLs to allow the required traffic.

### One thing I didn't expect in this project was...

One thing I didn't expect was how easily I could connect to my EC2 instance directly through the AWS Management Console using EC2 Instance Connect, without needing a separate SSH client on my computer.

### This project took me...

This project took me more than two hours to complete because I wanted to understand the networking concepts and how the different AWS settings affected connectivity.

## Connecting to an EC2 Instance

In AWS, connectivity means the ability of resources, such as EC2 instances, to communicate with each other or with other networks. It depends on factors such as routing, security groups, network ACLs and network configuration.

My first connectivity test was to check whether I could connect to my public EC2 instance.

![Image](https://nextwork.ai/sammy769/uploads/da091986-ef01-5973-a070-b15e174f59d8_88727bef)

## EC2 Instance Connect

EC2 Instance Connect is an AWS service that allows me to connect securely to my EC2 instance using SSH through the AWS Management Console, without needing to use a separate SSH client on my computer.

My first connection attempt failed because my public security group's inbound rules allowed HTTP traffic but did not allow SSH traffic. As a result, the SSH connection required to access my Linux instance was blocked.

I fixed the connection error by adding an inbound rule to my public security group to allow SSH traffic on port 22. This allowed me to connect to my EC2 instance using EC2 Instance Connect.

![Image](https://nextwork.ai/sammy769/uploads/da091986-ef01-5973-a070-b15e174f59d8_1cbb1b88)

## Connectivity Between Servers

Ping is a network utility that I used to test connectivity between my public and private EC2 instances. It sends ICMP Echo Request packets to the target IP address and checks whether it responds, helping me identify potential network connectivity issues.

The command I ran was `ping 10.0.1.119` This IP address belonged to my private EC2 instance, and I ran the command from my public EC2 instance to check whether they could communicate.

My first ping attempt displayed the target IP address and the message `56(84) bytes of data`, but I did not receive any replies. This suggested that the target had not responded to my ICMP requests yet. I investigated the network security rules to find out why the traffic was not getting through.

![Image](https://nextwork.ai/sammy769/uploads/da091986-ef01-5973-a070-b15e174f59d8_defghijk)

## Troubleshooting Connectivity

I resolved the issue by updating the relevant security group and network ACL rules to allow ICMP traffic between my public and private EC2 instances. Because network ACLs are stateless, I needed to ensure that the necessary traffic was allowed in both directions. This allowed the ping requests and their replies to pass between the instances.

![Image](https://nextwork.ai/sammy769/uploads/da091986-ef01-5973-a070-b15e174f59d8_4a9e8014)

## Connectivity to the Internet

Curl is a command-line tool that allows me to transfer data to and from a server using protocols such as HTTP and HTTPS. 

I used it to check whether my public EC2 instance could reach an external website over the internet.

### Ping vs Curl

Ping and curl serve different purposes. Ping uses ICMP to test whether a target responds to network requests, while curl tests communication using application protocols such as HTTP or HTTPS. This means ping can help me check basic network connectivity, whereas curl can help me check whether my instance can reach a web server

## Connectivity to the Internet

The command I ran was `curl mail.google.com`. It sent an HTTP request to Google's mail website and allowed me to check whether my public EC2 instance could reach an external web server. For a more direct test of HTTPS connectivity, I could use `curl -I https://mail.google.com` to request the response headers. This helps me check whether the web server responds over HTTPS.

![Image](https://nextwork.ai/sammy769/uploads/da091986-ef01-5973-a070-b15e174f59d8_8ee57662)

---

*Built with [NextWork](https://nextwork.ai) - [View this project](https://nextwork.ai/projects/da091986-ef01-5973-a070-b15e174f59d8)*
