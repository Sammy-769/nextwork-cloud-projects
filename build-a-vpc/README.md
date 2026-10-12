<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Build a Virtual Private Cloud

**Project Link:** [View Project](https://nextwork.ai/projects/7f907ac7-2473-5c15-a8be-edb36581cdba)

**Author:** Sammy Shah Saleh  
**Email:** sammysaleh769@gmail.com

---

![Image](https://nextwork.ai/soothed_pink_vibrant_kangaroo/uploads/aws-networks-vpc_2facf927)

## Introducing Today's Project!

This project demonstrates how to build and configure an isolated virtual network on Amazon Web Services (AWS). The primary goal of this project is to gain a practical, hands-on understanding of cloud networking fundamentals. /n In this implementation, I built a custom Virtual Private Cloud (VPC) and integrated two critical networking components: -**Public Subnets:** To segment the network and allocate IP addresses for cloud resources. -**Internet Gateway (IGW):** To connect the virtual network to the public internet.

## Virtual Private Clouds (VPCs)

### What I did in this step

In this step, I navigated to the Amazon VPC console in the eu-north-1 region to create a custom Virtual Private Cloud from scratch. I defined the network's boundary by assigning a specific IPv4 CIDR block (such as 10.0.0.0/16). This established an isolated, private IP space that will house all the subnets and cloud resources for this project.

### How VPCs work

A Virtual Private Cloud (VPC) works as a dedicated software-defined network inside the AWS cloud. It mimics a traditional physical network but runs on AWS's scalable infrastructure.

### Why there is a default VPC in AWS accounts

AWS automatically includes a default VPC in every region when a new account is created. This default network comes pre-configured with public subnets and  an attached internet gateway.

![Image](https://nextwork.ai/soothed_pink_vibrant_kangaroo/uploads/aws-networks-vpc_2facf927)

### Defining IPv4 CIDR blocks

To set up my VPC, I had to define an IPv4 Classless Inter-Domain Routing (CIDR) block, which is a standardized method used to allocate IP addresses and route data packets across a network. It consists of a base IP address followed by a forward slash and a number (for example, 10.0.0.0/16). -Network Prefix: The number after the slash (e.g., /16) tells the cloud how many bits are locked for the network identity. -IP Allocation: A lower slash number gives you a larger pool of available IP addresses, while a higher number narrows down the pool. -Custom Sizing: For this project, using a /16 block provided a massive range of 65,536 private IP addresses, giving the custom VPC plenty of room to expand.

## Subnets

### What I did in this step

In this step, I created custom subnets within my VPC to segment the overall network into smaller, manageable sections. I did this because different cloud resources have different security and accessibility needs. By dividing the VPC, I can isolate public-facing resources from private internal systems.

### Creating and configuring subnets

Subnets (short for sub-networks) are smaller subdivisions of a VPC's larger IP address range. AWS automatically creates default subnets in every default VPC—typically one for each **Availability Zone (AZ)** in that region. This default setup ensures that your applications can achieve high availability across separate, physical data centers right out of the box.

### Public vs private subnets

The core difference between public and private subnets lies in how they connect to the outside world: -**Public Subnets:** These host resources that must be accessible from the public internet (such as web servers or load balancers). For a subnet to be considered public, it must have a route in its route table that directs external traffic to an Internet Gateway. -**Private Subnets:** These host isolated resources that should never be directly accessed from the internet (such as backend databases or internal application logic). They lack a direct route to an internet gateway, keeping them secure from external threats.

![Image](https://nextwork.ai/soothed_pink_vibrant_kangaroo/uploads/aws-networks-vpc_157c4219)

### Auto-assigning public IPv4 addresses

Once I created my subnet, I enabled the "Enable auto-assign public IPv4 address" setting in the subnet configuration properties. /n This setting ensures that any new AWS resources—such as Amazon EC2 instances—launched inside this specific subnet automatically receive a public IPv4 address alongside their private IP address.By automating this process, resources can immediately communicate with external networks and the public internet upon startup, saving me from having to manually assign public IP addresses to every new instance.

## Internet gateways

### What I did in this step

In this step, I created an Internet Gateway and attached it to my custom VPC. I did this because a VPC is completely isolated by default. Without a gateway, resources inside the VPC have no way to send or receive traffic from the public internet.

### Setting up internet gateways

An Internet Gateway is a horizontally scaled, redundant, and highly available AWS component. It acts as a virtual bridge between your VPC and the outside internet. It performs network address translation (NAT) for your instances, allowing them to communicate externally without exposing their private IP addresses.

Attaching an Internet Gateway to a VPC means linking that gateway to your specific virtual network perimeter.If I missed this step, the VPC would remain a closed loop. Even if my subnet settings were correct and instances had public IP addresses, they would remain completely unreachable from the outside world, and they would not be able to download software updates or connect to external services.

![Image](https://nextwork.ai/soothed_pink_vibrant_kangaroo/uploads/aws-networks-vpc_4ae90410)

## Using the AWS CLI

### What I'm doing in this extension

In this project extension, I will use CloudShell to launch a VPC, add a subnet, and then configure an internet gateway. I am doing this in CloudShell because it allows for automation and scripting, making it much faster and more efficient for managing cloud infrastructure compared to clicking through the console GUI.

### Exploring CloudShell and CLI

A CLI (Command Line Interface) is a tool installed directly on your laptop where you type text commands to manage files or cloud systems instead of clicking buttons. 
A CloudShell is an identical command line tool that opens inside your internet browser without installing anything, running instantly on a remote cloud server with all software pre-configured.

### Debugging my setup

The command failed because I haven't included the mandatory --cidr-block parameter, which specifies the IP address range for the new subnet. Without this information, the AWS CLI cannot create the subnet because it doesn't know which IP addresses to allocate for the network.

![Image](https://nextwork.ai/soothed_pink_vibrant_kangaroo/uploads/7f907ac7-2473-5c15-a8be-edb36581cdba_9b2465411)

### Comparing CloudShell vs AWS Console

Compared to using the AWS Console, an advantage of using commands is speed and automation, as typing text into CloudShell allows for quick scripting and repeatable infrastructure deployment without repetitive manual steps. An advantage of using the Console is visual clarity, providing an intuitive graphical interface that helps you easily see how networks map out and catch configuration details without memorising exact command syntax. Overall, I preferred using CloudShell because running commands allows for efficient, code-driven management that builds real-world cloud engineering skills.

---

*Built with [NextWork](https://nextwork.ai) - [View this project](https://nextwork.ai/projects/7f907ac7-2473-5c15-a8be-edb36581cdba)*
