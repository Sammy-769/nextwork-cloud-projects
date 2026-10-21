<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# VPC Monitoring with Flow Logs

**Project Link:** [View Project](https://nextwork.ai/projects/6954a600-a89e-56b0-886b-7054da118a3b)

**Author:** Sammy Shah Saleh  
**Email:** sammysaleh769@gmail.com

---

![Image](https://nextwork.ai/sammy769/uploads/6954a600-a89e-56b0-886b-7054da118a3b_3e1e79a1)

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC (Virtual Private Cloud) allows me to create an isolated virtual network in AWS where I can control IP addresses, subnets, route tables and network security. It is useful because it gives me control over how my AWS resources communicate with each other and the internet.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to create two VPCs and connect them using a VPC peering connection. I updated their route tables to allow communication between EC2 instances using private IP addresses. I also configured VPC Flow Logs and Amazon CloudWatch to record and analyse network traffic, helping me understand how to monitor traffic and troubleshoot connectivity issues.



### One thing I didn't expect in this project was...

One thing I did not expect was that CloudWatch Logs Insights had been renamed or moved under Log Analytics in the AWS console. I had to recognise the updated interface to continue analysing my flow logs.

### This project took me...

This project took me more than two hours to complete.

## In the first part of my project...

### Step 1 - Set up VPCs

In this step, I created two VPCs to prepare the network environment for configuring VPC Flow Logs and monitoring network traffic using Amazon CloudWatch.

### Step 2 - Launch EC2 instances

In this step, I launched an EC2 instance in each VPC so that I could generate network traffic and use VPC Flow Logs to monitor and analyse the traffic in Amazon CloudWatch.

### Step 3 - Set up Logs

In this step, I configured VPC Flow Logs to record inbound and outbound network traffic and set up an Amazon CloudWatch log group to store and analyse these records.

### Step 4 - Set IAM permissions for Logs

In this step, I gave VPC Flow Logs the necessary IAM permissions to publish flow log records to Amazon CloudWatch Logs and finished configuring the flow log for my subnet.

## Multi-VPC Architecture

I had already created one VPC, and in this step, I created a second VPC with one public subnet and its associated networking components.

I used unique, non-overlapping IPv4 CIDR blocks for VPCs 1 and 2 to give each VPC its own IP address range and prevent IP address conflicts when connecting them through VPC peering.

### I also launched EC2 instances in each subnet

The security group `sec-1`, attached to the EC2 instance in `sam-1-vpc`, allowed inbound traffic from resources associated with the same security group on all ports and protocols. It also allowed inbound SSH traffic over TCP port 22 from any IPv4 address (`0.0.0.0/0`) so that I could connect to the instance. However, this rule is broad and should be restricted to trusted IP addresses where possible.

The security group `sec-2`, attached to the EC2 instance in `sam-2-vpc`, allowed inbound traffic from resources associated with the same security group on all ports and protocols. It also allowed ICMP traffic from the `10.1.0.0/16` CIDR block so that the instance could receive ping requests from VPC 1. Its outbound rules allowed all traffic to any destination.

![Image](https://nextwork.ai/sammy769/uploads/6954a600-a89e-56b0-886b-7054da118a3b_e7fa8775)

## Logs

Logs are records of events that happen in a system or application. They help me understand what happened, identify errors, troubleshoot problems and monitor activity.

Log groups are collections of log streams in Amazon CloudWatch Logs. They help me organise and manage logs from different applications or AWS resources in one place.

![Image](https://nextwork.ai/sammy769/uploads/6954a600-a89e-56b0-886b-7054da118a3b_e8398869)

## IAM Policy and Roles

I created an IAM policy to grant VPC Flow Logs the necessary permissions to publish log data to my Amazon CloudWatch log group. Without the required permissions, VPC Flow Logs cannot deliver log records to CloudWatch.

I also created an IAM role because VPC Flow Logs needs a role to assume so that it can publish log data to my Amazon CloudWatch log group. I attached the necessary IAM policy to grant the role permission to deliver the flow log records.

A custom trust policy defines which service can assume an IAM role. I used it to allow only VPC Flow Logs, through `vpc-flow-logs.amazonaws.com`, to assume the role and publish logs to CloudWatch.

![Image](https://nextwork.ai/sammy769/uploads/6954a600-a89e-56b0-886b-7054da118a3b_4334d777)

## In the second part of my project...

### Step 5 - Ping testing and troubleshooting

In this step, I sent test traffic from Instance 1 to Instance 2 to test VPC peering and used VPC Flow Logs to monitor the network traffic between them.

### Step 6 - Set up a peering connection

In this step, I created a VPC peering connection between my two VPCs and updated their route tables to allow resources in both VPCs to communicate using private IP addresses.

### Step 7 - Analyze flow logs

In this step, I analysed the flow logs recorded for VPC 1's public subnet to understand network traffic, identify accepted and rejected connections, and investigate how traffic flowed through my VPC.

## Connectivity troubleshooting

The ping test was unsuccessful because I did not receive any replies from the EC2 instance at `10.0.1.119`. This indicated that the instances could not communicate successfully, so I needed to troubleshoot the VPC peering connection, route tables and security group rules.

![Image](https://nextwork.ai/sammy769/uploads/6954a600-a89e-56b0-886b-7054da118a3b_99d4ba42)

I could receive ping replies when I used the instance's public IP address, but not when I used its private IP address (`10.0.1.119`). This showed that communication through the public IP address was working, but communication through the private IP address was unsuccessful. I needed to investigate the VPC peering connection, route tables and security group rules to identify the cause.

## Connectivity troubleshooting

I identified that the ping test failed because I had not yet created a VPC peering connection between VPC 1 and VPC 2. Without this connection, I could not establish direct communication between the instances using their private IP addresses.

### To solve this, I set up a peering connection between my VPCs

I updated both VPCs' route tables because accepting a VPC peering connection does not automatically configure routes between them. I added a route to each route table with the other VPC's CIDR block as the destination and the VPC peering connection as the target, allowing traffic to reach resources in both VPCs using private IP addresses.

![Image](https://nextwork.ai/sammy769/uploads/6954a600-a89e-56b0-886b-7054da118a3b_7316a13d)

## Connectivity troubleshooting

I received successful ping replies from Instance 2's private IP address, which confirmed that the two instances could communicate using private IP addresses through the VPC peering connection. This showed that the peering connection and route table configuration were working correctly, and the security group rules allowed the ICMP traffic.

![Image](https://nextwork.ai/sammy769/uploads/6954a600-a89e-56b0-886b-7054da118a3b_4ec7821f)

## Analyzing flow logs

A VPC Flow Log records information about IP traffic going to and from network interfaces in my VPC. Each record can include the source and destination IP addresses, ports, protocol, number of packets and bytes, timestamps, and the traffic action.

In this example, the action is `REJECT`, which means the traffic was rejected according to the applicable network rules. These records help me investigate network activity and troubleshoot connectivity issues, although flow logs do not capture the actual contents of network packets.

![Image](https://nextwork.ai/sammy769/uploads/6954a600-a89e-56b0-886b-7054da118a3b_d116818e)

## Logs Insights

Amazon CloudWatch Logs Insights allows me to search, filter and analyse log data using queries. In the AWS console, this experience is now available under Log Analytics. I can use it to identify patterns in VPC Flow Logs, investigate rejected traffic and troubleshoot network connectivity issues.

I ran the following CloudWatch Logs Insights query to analyse the flow logs from the last three hours:

```
SOURCE "arn:aws:logs:eu-north-1:958125727288:log-group:sam-vpcflow" START=-3h END=0s
| stats sum(bytes) as bytesTransferred by srcAddr, dstAddr
| sort bytesTransferred desc
| limit 10
```

The query calculates the total number of bytes transferred for each source and destination IP address pair, sorts the results from highest to lowest data transfer, and displays the top 10 results. This helps me identify which IP address pairs transferred the most data through my VPC.

![Image](https://nextwork.ai/sammy769/uploads/6954a600-a89e-56b0-886b-7054da118a3b_3e1e79a1)

---

*Built with [NextWork](https://nextwork.ai) - [View this project](https://nextwork.ai/projects/6954a600-a89e-56b0-886b-7054da118a3b)*
