<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# VPC Traffic Flow and Security

**Project Link:** [View Project](https://nextwork.ai/projects/fe5ed473-5874-57e1-a58f-d9b3d652330c)

**Author:** Sammy Shah Saleh  
**Email:** sammysaleh769@gmail.com

---

![Image](https://nextwork.ai/soothed_pink_vibrant_kangaroo/uploads/fe5ed473-5874-57e1-a58f-d9b3d652330c_92b0b0b4)

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC (Virtual Private Cloud) allows me to create an isolated virtual network within AWS. It is useful because it gives me control over my network configuration, including IP address ranges, subnets, route tables and security settings. This allows me to organise my AWS resources, control how they communicate with each other and manage their access to the internet.

### How I used Amazon VPC in this project

In today's project, I created an Amazon VPC to provide an isolated virtual network for my AWS environment. I then created a subnet within the VPC and configured other networking components, including an internet gateway, a route table, a security group and a network ACL. Although I did not launch an EC2 instance in this VPC, I learnt how these components work together to manage network traffic and control access to AWS resources.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was discovering AWS Global View. I learnt that I can view my AWS resources across different Regions in one place, without having to switch between Regions individually.

### This project took me...

This project took me around two hours to complete, including creating the AWS resources and learning how the different networking components work together.

## Route tables

Route tables are used to control where network traffic goes within a VPC. They contain a set of rules called routes that determine where traffic should be sent based on its destination. For example, I can add a route that directs traffic intended for the public internet to an internet gateway. By associating a route table with a subnet, I can control how traffic leaving that subnet is routed.

I need a route table to make a subnet public because it tells network traffic where to go when it needs to reach the internet. By adding a route that directs internet-bound traffic (0.0.0.0/0) to an internet gateway and associating the route table with my subnet, I allow resources in that subnet to send traffic to the public internet. However, the resources also need public IP addresses and appropriate security settings to communicate with the internet.

![Image](https://nextwork.ai/soothed_pink_vibrant_kangaroo/uploads/fe5ed473-5874-57e1-a58f-d9b3d652330c_0a07b191)

## Route destination and target

A route's destination specifies where the network traffic needs to go, while the target specifies where AWS should send that traffic. For example, if I set the destination to 0.0.0.0/0, it means the route applies to traffic going to any IPv4 address. If I set the target to my internet gateway, AWS will direct that traffic to the internet gateway so it can reach the public internet.

My route's destination is 0.0.0.0/0, which represents all IPv4 addresses. The target is my internet gateway, which allows internet-bound traffic to travel from my VPC to the public internet.

![Image](https://nextwork.ai/soothed_pink_vibrant_kangaroo/uploads/fe5ed473-5874-57e1-a58f-d9b3d652330c_0a07b191)

## Security groups

Security groups act as virtual firewalls for my AWS resources, such as EC2 instances. They control inbound and outbound traffic by using rules that specify which connections are allowed. By configuring these rules, I can control which network connections are allowed to reach my resources and which connections my resources can make, helping to protect my cloud environment from unwanted traffic.

### Inbound vs Outbound rules

An inbound rule controls the traffic allowed to enter my AWS resources. My security group's inbound rules determine which types of connections can reach my resources, based on settings such as the protocol, port number and source IP address.

An outbound rule controls the traffic allowed to leave my AWS resources. My security group's outbound rules determine where my resources can send traffic. By default, my security group allows all outbound traffic to any destination.

![Image](https://nextwork.ai/soothed_pink_vibrant_kangaroo/uploads/fe5ed473-5874-57e1-a58f-d9b3d652330c_92b0b0b4)

## Network ACLs

Network ACLs are firewalls that control inbound and outbound traffic at the subnet level in my VPC. They use rules to allow or deny traffic based on factors such as IP addresses and port numbers, providing an additional layer of security for my cloud environment.

### Security groups vs. network ACLs

Security groups act as firewalls at the resource level, controlling traffic allowed to reach or leave resources such as EC2 instances. Network ACLs act at the subnet level and can allow or deny traffic. Security groups are stateful, meaning they automatically allow response traffic, while network ACLs are stateless, meaning I must configure rules for both inbound and outbound traffic.

## Default vs Custom Network ACLs

### Similar to security groups, network ACLs use inbound and outbound rules

By default, a network ACL allows all inbound and outbound traffic. This means all traffic is permitted to enter and leave the subnet unless I change the rules. Unlike security groups, network ACLs are stateless, so inbound and outbound traffic are evaluated separately.

A custom network ACL denies all inbound and outbound traffic by default. I must add rules to specify which traffic is allowed or denied, giving me control over the connections entering and leaving my subnet.

![Image](https://nextwork.ai/soothed_pink_vibrant_kangaroo/uploads/fe5ed473-5874-57e1-a58f-d9b3d652330c_4faeb056)

## Tracking VPC Resources

I deployed three AWS resources in the US East (N. Virginia) region: a Virtual Private Cloud (VPC) named new-region-VPC to create an isolated network, an internet gateway named new-region-IG to enable communication with the internet, and a security group named new-region-sg to control inbound and outbound traffic to my AWS resources.

AWS Global View allows me to see and manage my AWS resources across different AWS Regions from one place. I can use it to check which resources I have created in each Region, such as VPCs, EC2 instances, internet gateways and security groups, without switching between Regions individually.

I would use AWS Global View again when I want to check and manage my AWS resources across multiple Regions from one place. It helps me quickly see where my resources are deployed and keep track of my cloud infrastructure without switching between Regions individually.

![Image](https://nextwork.ai/soothed_pink_vibrant_kangaroo/uploads/fe5ed473-5874-57e1-a58f-d9b3d652330c_b03ea6162)

---

*Built with [NextWork](https://nextwork.ai) - [View this project](https://nextwork.ai/projects/fe5ed473-5874-57e1-a58f-d9b3d652330c)*
