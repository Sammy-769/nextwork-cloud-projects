<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Creating a Private Subnet

**Project Link:** [View Project](https://nextwork.ai/projects/4e96e29d-98b8-551e-ae93-da39c36e30fd)

**Author:** Sammy Shah Saleh  
**Email:** sammysaleh769@gmail.com

---

![Image](https://nextwork.ai/soothed_pink_vibrant_kangaroo/uploads/4e96e29d-98b8-551e-ae93-da39c36e30fd_afe1fdbd)

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC (Virtual Private Cloud) allows me to create an isolated virtual network within AWS, giving me control over IP address ranges, subnets, route tables and network security. 

### How I used Amazon VPC in this project

In today's project, I used my VPC to create a private subnet and configure a separate route table and network ACL to control its network traffic.

### One thing I didn't expect in this project was...

One thing I didn't expect was that every subnet is automatically associated with a network ACL, even when I haven't configured one myself. I learnt that a new subnet is associated with the VPC's default network ACL unless I associate it with a different one.

### This project took me...

This project took me around one and a half hours to complete, including creating the private subnet and configuring its networking and security settings.

## Private vs Public Subnets

A public subnet has a route to an internet gateway, allowing resources with public IP addresses and appropriate security settings to communicate directly with the public internet. A private subnet does not have a direct route to an internet gateway, helping to protect resources such as databases from direct access from the internet.

Private subnets are useful for hosting resources such as databases and internal applications that should not be directly accessible from the public internet. Their route tables do not provide a direct route to an internet gateway. This reduces their exposure to external traffic, while resources can still communicate within the VPC when routing and security rules permit it.

My public and private subnets cannot share the same CIDR block because their IP address ranges must not overlap. Each subnet needs its own unique range of IP addresses within the VPC so that AWS can identify and route traffic to the correct subnet.

![Image](https://nextwork.ai/soothed_pink_vibrant_kangaroo/uploads/4e96e29d-98b8-551e-ae93-da39c36e30fd_afe1fdbd)

## A dedicated route table

When I created my private subnet, it was initially associated with the main route table of my VPC, sam-vpc. I then created a separate route table and associated it with my private subnet so that I could manage its routing independently of my public subnet, public-1.



My private subnet's route table currently contains only a local route for traffic within the VPC. It has no route to an internet gateway, so resources in the subnet cannot access the public internet directly. Security groups and network ACLs separately control which traffic is permitted.

![Image](https://nextwork.ai/soothed_pink_vibrant_kangaroo/uploads/4e96e29d-98b8-551e-ae93-da39c36e30fd_b4b904b5)

## A new network ACL

By default, my private subnet is associated with the default network ACL of my VPC, which allows all inbound and outbound traffic.

I created a new network ACL to isolate the security rules for my private subnet from those of my other subnets, giving me separate control over its inbound and outbound traffic.

My new network ACL has no inbound or outbound allow rules, so traffic is denied by default. I would need to add rules to allow the traffic required by my private resources. I can also use explicit deny rules to block particular types of traffic.

![Image](https://nextwork.ai/soothed_pink_vibrant_kangaroo/uploads/4e96e29d-98b8-551e-ae93-da39c36e30fd_1ed2cb07)

---

*Built with [NextWork](https://nextwork.ai) - [View this project](https://nextwork.ai/projects/4e96e29d-98b8-551e-ae93-da39c36e30fd)*
