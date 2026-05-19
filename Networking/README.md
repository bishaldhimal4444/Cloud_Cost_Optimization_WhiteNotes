## Networking:
Best practice guidance for monitoring and optimizing cost of commonly used core networking services and features.

#### 1. Amazon VPC:
**-	Gateway VPC endpoints:** Provide reliable connectivity to Amazon S3 or Amazon DynamoDB without requiring an internet gateway or a NAT device for your VPC. Gateway endpoints do not use AWS PrivateLink, unlike other types of VPC endpoints. There is no additional charge for using gateway endpoints.
**-	Interface VPC endpoints:** You can use interface endpoints to privately and securely access AWS services, internal application services or SaaS services that are running outside of your VPC.

###### Amazon VPC Optimization Techniques
-	For workloads within the same region, if your destination service is either S3 or DynamoDB, utilize Gateway endpoints if possible.
-	Check for idle VPC Endpoints to find out if they are needed based on each use case given that they could be deleted if no traffic is going through them.
-	As the number of VPCs in your account grows, centralizing the interface endpoints might be more cost-efficient (please note this does not work with gateway endpoints).

#### 2. Network Address Translation (NAT) Gateway
NAT Gateways have the following pricing dimensions:

-	Price per NAT Gateway ($/hour): Each hour that your NAT Gateway is provisioned and available.
-	Price per GB data processed ($/GB): Each gigabyte of data that it processed, regardless of the traffic’s source or destination.
-	Data Transfer charges ($/GB-month): There’s an additional indirect factor, which is Data Transfer charges.

###### NAT Gateway Optimization Techniques
-	Determine whether the majority of your NAT Gateway charges are from traffic to AWS regional services (Amazon S3, Amazon DynamoDB, Amazon Kinesis, Amazon SQS, Amazon CloudWatch, etc.) and route that traffic to and from those services using VPC endpoints.
-	Determine whether the resources sending most of the traffic to NAT Gateway are in the same Availability Zone as the NAT Gateway. If they are not, then route the traffic to a NAT Gateway in the same AZ to reduce cross-AZ data transfer charges.
-	Identify top contributors to traffic charges going through NAT Gateways. Consider enabling VPC Flow Logs, and then leverage CloudWatch Log Insights.
-	Inter-AZ Traffic:
  
          o	Resources sending traffic to NAT Gateways can be placed in the same AZs as their NAT Gateway to avoid traffic crossing AZs and incurring costs.
          o	It's recommended to check the route tables of the subnets in which those resources are created, and ensure that NAT Gateways in those route tables are in the same AZ. The ultimate goal is to get the traffic from private subnets flow "vertically" where possible.
-	Data Transfer Out:
  
          o Evaluate if there is a legitimate use case and business reason for the traffic that your instances are sending out to the internet.
          o It's recommended to place resources in private subnets where possible, including resources sending legitimate traffic out to the internet. Depending on the destination of the traffic (for example, if the destination for your traffic is within AWS), consider using PrivateLink, so the traffic wouldn't cross a NAT Gateway or Internet Gateway to reach its target. After carefully checking on security and compliance implications, you can then evaluate placing those resources in a public subnet.
-	Idle NAT Gateways:
  
        o	Consider checking unused NAT Gateways.
        o	Discover whether they are needed based on each use case given that they could be deleted if no traffic is going through them.

-	NAT Gateway data processing cost:
  
        o	An important cost component for NAT Gateways is the amount of traffic they process.
        o	If the workload running in your private subnet is reaching S3 or DynamoDB in the same region through NAT Gateway, then set up a gateway VPC endpoint and modify the corresponding VPC route table to route traffic to and from the AWS resource through the gateway VPC endpoint, rather than through the NAT Gateway.


#### 3. Amazon VPC IP Address Manager (IPAM)
With Amazon VPC IP Address Manager (IPAM) you pay an hourly rate for each active IP address that you manage using IPAM.
###### IPAM Optimization Techniques
- Consider employing IPAM only in production environments, where a tighter control or management of CIDRs is needed.
- IPAM only in select operating regions.
- Monitor IPAM costs to ensure business value is being delivered for the proportionate cost.
- Use IP prefix allocation - VPC allows you to assign IPv4 and IPv6 prefixes to your EC2 instances, enabling you to scale and simplify the management of your container and networking applications that require multiple IP addresses on an instance. IPAM counts the whole delegation (16 IP addresses) as a single IP address, thus optimizing cost.

#### 4. Network Analysis
**Traffic Mirroring:**

If you choose to enable traffic mirroring on Amazon EC2 Instance elastic network interfaces (ENIs), ENI owner pays hourly for each ENI that is enabled with traffic mirroring. If you no longer wish to be charged for traffic mirroring, delete the traffic mirroring session associated to the instance/ENI using the AWS Management Console, command line interface, or API.

Note: You'll continue to be charged for Traffic Mirroring until you delete all active traffic mirroring sessions. For example, you'll still be charged in the following scenarios:

- You detached the network interface from the mirror source but do not delete the relevant traffic mirroring session.
- You stopped or terminated the mirror source but do not delete the relevant traffic mirroring session.
- You changed the instance type of the mirror source to an unsupported instance type but do not delete the relevant traffic mirroring session.

**Reachability Analyzer**

Reachability Analyzer is a configuration analysis tool that enables you to perform connectivity testing between traffic source and destination in your VPC. When the destination is reachable, Reachability Analyzer produces hop-by-hop details of the virtual network path between the source and the destination. When the destination is not reachable, Reachability Analyzer identifies the blocking component. For example, paths can be blocked by configuration issues in a security group, network ACL, route table, or load balancer.

You pay for each time you analyze connectivity between a given source and destination using Reachability Analyzer.

It’s recommended to limit reachability analyzer runs.


**Network Access Analyzer**

Network Access Analyzer is a feature that identifies unintended network access to your resources on AWS. You can use Network Access Analyzer to specify your network access requirements and to identify potential network paths that do not meet your specified requirements.

You pay for the number of Amazon EC2 Instance elastic network interfaces (ENIs) analyzed when you run a network assessment using Network Access Analyzer.

It’s recommended to limit network analyzer runs.

**VPC Flow logs**

VPC Flow Logs is a feature that enables you to capture information about the IP traffic going to and from network interfaces in your VPC. Flow log data can be published to the following locations: Amazon CloudWatch Logs, Amazon S3, or Amazon Data Firehose. After you create a flow log, you can retrieve and view the records in the log group, S3 bucket, or delivery stream that you configured.

Flow logs can help you with tasks, such as:
- Diagnosing overly restrictive security group rules
- Monitoring the traffic that is reaching your instance
- Determining the direction of the traffic to and from the network interfaces

Flow log data is collected outside of the path of your network traffic, and therefore does not affect network throughput or latency. You can create or delete flow logs without any risk of impact to network performance.

Data ingestion and archival charges for vended logs apply when you publish flow logs to either CloudWatch or S3. There is no Data Transfer IN charges for CloudWatch logs. Make sure to setup appropariate log retention to avoid being charges for old loga unnecessarily.

##### Optimization Techniques for Network Analysis
- Turn on VPC flow logs only when you need them (e.g. for troubleshooting or investigating an issue).
-  logs sent to Amazon CloudWatch, reduce the log group retention period.
- If sending VPC flow logs to S3, consider using lifecycle rules to transition logs to cheaper storage classes.
- Limit the scope of VPC flow logs to only what you are interested in capturing. You can enable VPC flow logs at the ENI, subnet or VPC level. The more resources covered by the capture, the higher the cost. Additionally, use the default 10-min aggregation interval. Flow logs with an aggregation interval of 1 minute produce a higher volume of flow log records than flow logs with an aggregation interval of 10 minutes.
- Turn on flow logs for REJECT or ACCEPT. Capturing traffic in both directions implies higher volume of logs & cost.
- For S3 VPC flows logs delivery, use the default text format. Parquet format comes with an additional charge per GB.
- Consider checking idle VPC endpoints and discover whether they are needed based on each use case given that they could be deleted if no traffic is going through them.

#### Public IPv4
When you launch an instance in a default VPC, AWS assigns it a public IP address by default. When you launch an instance into a non-default VPC, the subnet has an attribute that determines whether instances launched into that subnet receive a public IP address from the public IPv4 address pool. By default, a public IP address is not assigned to instances launched in a non-default subnet. There is a charge per IP per hour for all public IPv4 addresses.

##### Public IPv4 Optimization Techniques

- Assess which resources must be deployed in public subnets and require individual public IPv4 addresses. Resources like databases or container services can be deployed in private subnets, without being exposed directly to the Internet. This will help you optimize the number of public IPv4 addresses associated with your resources.
- For remote access to resources within your VPCs, consider using EC2 Instance Connect (EIC) Endpoints instead of assigning public IPv4 addresses to each resource. This will help you optimize the number of public IPv4 addresses associated with your resources and improve your security posture.
- For inbound internet traffic, consider using Elastic Load Balancers or AWS Global Accelerator. These services help you increase the availability and performance of your workloads while optimizing public IPv4 utilization. When assessing the use of ELBs or AWS Global Accelerator, consider your architecture and traffic profiles.
- Consider disabling the auto-assignment of public IPv4 addresses on default subnets.
- For outbound internet traffic, NAT Gateways can help you optimize public IPv4 address utilization. NAT gateway offers you the capability to perform source address translation at scale, in each Availability Zone. When assessing the use of NAT Gateway, consider your architecture and traffic profiles.
