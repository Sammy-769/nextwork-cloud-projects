<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Launching VPC Resources

**Project Link:** [View Project](https://nextwork.ai/projects/8f49d756-9e51-58c0-856a-e71e54f064ab)

**Author:** Sammy Shah Saleh  
**Email:** sammysaleh769@gmail.com

---

![Image](https://nextwork.ai/sammy769/uploads/8f49d756-9e51-58c0-856a-e71e54f064ab_8ee57662)

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC (Virtual Private Cloud) allows me to create an isolated virtual network within AWS, giving me control over IP address ranges, subnets, route tables and network security.

### How I used Amazon VPC in this project

In today's project, I used the VPC and more option to create a VPC and its related networking resources, including subnets, route tables and an internet gateway, all in one go. This made the setup quicker and more convenient than creating each resource separately.

### One thing I didn't expect in this project was...

One thing I didn't expect was the VPC Resource Map, which provides a visual diagram of my VPC architecture and shows how its networking resources are connected. I found this particularly useful because it makes the network easier to understand. I also learnt that this feature was introduced in 2023.

### This project took me...

This project took me around one and a half hours, including the time I spent learning and understanding the different features.

## Setting Up Direct VM Access

Directly accessing my EC2 instance means connecting to it remotely, usually through SSH for a Linux instance. This allows me to interact with the instance's operating system and run commands from my own computer, provided the network and security settings allow the connection.

### SSH is a key method for directly accessing a VM

SSH stands for Secure Shell. It is a network protocol that allows me to connect securely to a remote server, such as a Linux EC2 instance, and execute commands over an encrypted connection.

### To enable direct access, I set up key pairs

An EC2 key pair consists of a public key and a private key. AWS stores the public key on the EC2 instance, while I keep the private key to authenticate my connection to the instance. This allows me to connect securely without relying on a password alone.

A private key can be provided in different file formats, depending on how it was created or converted. My private key was in the .pem format, which is commonly used for SSH access to Linux EC2 instances. I need to keep this file secure because anyone who obtains it may be able to authenticate as me if the other access requirements are met.

## Launching a public server

When launching my EC2 instance, I selected my custom VPC, sam-vpc, chose the public-1 subnet, and assigned the appropriate security group. These settings determine which network the instance belongs to and help control its network traffic.

![Image](https://nextwork.ai/sammy769/uploads/8f49d756-9e51-58c0-856a-e71e54f064ab_88727bef)

## Launching a private server

My private server uses a different security group from my public server so that I can manage access to each instance separately. This allows me to apply different security rules depending on each server's role and limit unnecessary access to my private server.

My new security group's source is the security group attached to my public server. This means I can configure the private server to accept traffic from resources associated with the public security group, rather than allowing access from any source. The actual access still depends on the inbound rules, the traffic protocol and port, and the network configuration.

![Image](https://nextwork.ai/sammy769/uploads/8f49d756-9e51-58c0-856a-e71e54f064ab_4a9e8014)

## Speeding up VPC creation

After setting up my public and private EC2 instances in sam-vpc, I created a separate VPC using the VPC and more option. This allowed me to explore a quicker way to create a VPC and its related networking resources.

The VPC Resource Map provides a visual representation of my VPC architecture, showing resources such as subnets, route tables and internet gateways, along with their relationships. It helps me understand how my network is structured and review how traffic is intended to flow through it.

My new VPC can have the same IPv4 CIDR block as my previous VPC, sam-vpc, because each VPC is a separate, logically isolated network. However, overlapping CIDR blocks can cause routing problems if I later want to connect the VPCs using VPC peering or other network connections.

![Image](https://nextwork.ai/sammy769/uploads/8f49d756-9e51-58c0-856a-e71e54f064ab_1cbb1b88)

## Speeding up VPC creation

### Tips for using the VPC resource map

Using the VPC and more option, I can configure up to 2 public subnets through the creation wizard. The number I choose determines how many public subnets AWS creates, subject to the available Availability Zones and suitable, non-overlapping IP address ranges.

NAT gateways allow resources in a private subnet to initiate connections to external networks, such as the public internet, without allowing unsolicited connections from the internet directly to those resources. For example, a private EC2 instance can use a public NAT gateway to download software updates while remaining inaccessible through a direct inbound internet connection. NAT gateways can incur additional charges, so I need to consider the cost when using them.

![Image](https://nextwork.ai/sammy769/uploads/8f49d756-9e51-58c0-856a-e71e54f064ab_8ee57662)

---

*Built with [NextWork](https://nextwork.ai) - [View this project](https://nextwork.ai/projects/8f49d756-9e51-58c0-856a-e71e54f064ab)*
