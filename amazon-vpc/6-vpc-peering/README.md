<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# VPC Peering

**Project Link:** [View Project](https://nextwork.ai/projects/fd75209e-d2a1-5bdd-90e8-bdb9ee49de16)

**Author:** Sammy Shah Saleh  
**Email:** sammysaleh769@gmail.com

---

![Image](https://nextwork.ai/sammy769/uploads/fd75209e-d2a1-5bdd-90e8-bdb9ee49de16_88727bef)

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC (Virtual Private Cloud) allows me to create an isolated virtual network in AWS where I can control IP address ranges, subnets, route tables and network security. It is useful because it gives me control over how my AWS resources communicate with each other and with other networks.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to create two VPCs and connect them using a VPC peering connection, allowing resources in both VPCs to communicate using private IP addresses.

### One thing I didn't expect in this project was...

One thing I did not expect in this project was that I could establish a private connection between two separate VPCs, allowing their resources to communicate without using the public internet.

### This project took me...

This project took me a little over two hours to complete because I needed extra time to troubleshoot connection errors and configure the networking rules correctly.

## In the first part of my project...

### Step 1 - Set up my VPC

In this step, I used the VPC and more option to create two VPCs and their associated networking components. I then used the visual VPC resource map to review the resources and understand how they were connected.

### Step 2 - Create a Peering Connection

In this step, I set up a VPC peering connection between my two VPCs so that resources in both networks could communicate using private IP addresses.

### Step 3 - Update Route Tables

In this step, I updated the route tables in both VPCs to direct traffic to the other VPC through the VPC peering connection, allowing traffic to travel in both directions.

### Step 4 - Launch EC2 Instances

In this step, I launched an EC2 instance in each VPC so that I could use them to test connectivity between the two VPCs and verify that the VPC peering connection was working correctly.

## Multi-VPC Architecture

I created two VPCs, each with one public subnet. I used the VPC and more option to create the VPCs and their associated networking components, including route tables and internet gateways.

The IPv4 CIDR blocks of my two VPCs are `10.1.0.0/16` and `10.2.0.0/16`. These ranges do not overlap, which allows me to connect the VPCs through VPC peering without conflicting IP address ranges.

### I also launched 2 EC2 instances

I chose not to create my own key pairs because I used EC2 Instance Connect to access my EC2 instances through the AWS Console. EC2 Instance Connect temporarily provides an SSH public key for authentication, so I did not need to manage my own SSH key pair for this connection method.

![Image](https://nextwork.ai/sammy769/uploads/fd75209e-d2a1-5bdd-90e8-bdb9ee49de16_11111111)

## VPC Peering

A VPC peering connection allows two VPCs to communicate with each other using private IPv4 or IPv6 addresses.

Peering connections exist so that resources in separate VPCs can exchange traffic without needing to use the public internet. The VPCs must have non-overlapping IP address ranges.

The Requester is the VPC that initiates the peering connection `sam-vpc1`, while the Accepter is the VPC that receives the request `sam-vpc2`. The Accepter must accept the request before the peering connection becomes active.

![Image](https://nextwork.ai/sammy769/uploads/fd75209e-d2a1-5bdd-90e8-bdb9ee49de16_1cbb1b88)

## Updating route tables

After accepting a peering connection, I needed to update my VPCs' route tables so that traffic destined for the other VPC's IP address range would be routed through the VPC peering connection. This allows resources in both VPCs to communicate with each other using private IP addresses.

I added a new route to each VPC's route table, using the other VPC's IPv4 CIDR block as the destination and setting the target to the VPC peering connection. The route in VPC 2's route table used `10.1.0.0/16` as the destination, while the route in VPC 1's route table used `10.2.0.0/16`. 

![Image](https://nextwork.ai/sammy769/uploads/fd75209e-d2a1-5bdd-90e8-bdb9ee49de16_4a9e8014)

## In the second part of my project...

### Step 5 - Use EC2 Instance Connect

In this step, I tried to connect to my first EC2 instance using EC2 Instance Connect, but I received an error stating that no public IPv4 address was assigned. Since I was using the browser-based connection method, I allocated an Elastic IP address and associated it with my instance to resolve the issue.

### Step 6 - Connect to EC2 Instance 1

In this step, I tried connecting to my first EC2 instance again, but the connection failed because I had not allowed SSH traffic in the security group associated with `sam-ec2-vpc2` in `sam-vpc2`. I resolved the issue by adding an inbound rule to allow SSH traffic on port 22.

### Step 7 - Test VPC Peering

In this step, I tested communication between my two EC2 instances by using the `ping` command to send ICMP requests from Instance 1 to Instance 2. The test initially failed because I had not allowed ICMP - IPv4 traffic in the security group associated with the instance in `sam-vpc2`. I fixed this by adding an inbound rule to allow ICMP - IPv4 traffic from `sam-vpc1`'s CIDR block, enabling the instances to communicate through the VPC peering connection.

## Troubleshooting Instance Connect

Next I used EC2 Instance Connect because it provides an easy way to access my EC2 instances through the AWS Console. This allowed me to test connectivity between my two VPCs and check whether the VPC peering connection was working correctly.

I ran into a connection error with EC2 Instance Connect because I had not enabled the auto-assign public IP setting when launching my EC2 instances. As a result, my instances did not have public IP addresses, which prevented me from connecting to them through the usual public connectivity method.

![Image](https://nextwork.ai/sammy769/uploads/fd75209e-d2a1-5bdd-90e8-bdb9ee49de16_7685490c)

## Elastic IP addresses

I encountered a connection error because I had not enabled the auto-assign public IP setting when launching my EC2 instances. As I was using the browser-based EC2 Instance Connect method, I needed to provide public connectivity to the instances.

An Elastic IP address is a static public IPv4 address that I can allocate to my AWS account and associate with an EC2 instance. To resolve the connection issue, I allocated Elastic IP addresses and associated them with my instances. This provided the public IP addresses I needed to connect through EC2 Instance Connect, alongside the appropriate routing and security rules.

![Image](https://nextwork.ai/sammy769/uploads/fd75209e-d2a1-5bdd-90e8-bdb9ee49de16_45663498)

## Troubleshooting ping issues

I used the `ping` command to test connectivity between my two VPCs by sending ICMP echo requests from an EC2 instance in one VPC to the private IP address of an instance in the other VPC.

My first attempt to reach `10.2.3.119` did not receive any replies; the terminal only displayed `PING 10.2.3.119 (10.2.3.119) 56(84) bytes of data`. This output was not itself an error, but the lack of replies suggested that I needed to investigate the network configuration, including the security group rules.

I updated the inbound rules of the target instance's security group to allow ICMP traffic from `10.1.0.0/16`, the CIDR block of `sam-vpc1`. This allowed the instance in VPC 1 to send ping requests to the target instance in VPC 2, provided the route tables and network ACLs also allowed the traffic.

![Image](https://nextwork.ai/sammy769/uploads/fd75209e-d2a1-5bdd-90e8-bdb9ee49de16_7a29d352)

---

*Built with [NextWork](https://nextwork.ai) - [View this project](https://nextwork.ai/projects/fd75209e-d2a1-5bdd-90e8-bdb9ee49de16)*
