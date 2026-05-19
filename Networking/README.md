## Networking:
Best practice guidance for monitoring and optimizing cost of commonly used core networking services and features.

#### Amazon VPC:
**-	Gateway VPC endpoints:** Provide reliable connectivity to Amazon S3 or Amazon DynamoDB without requiring an internet gateway or a NAT device for your VPC. Gateway endpoints do not use AWS PrivateLink, unlike other types of VPC endpoints. There is no additional charge for using gateway endpoints.
**-	Interface VPC endpoints:** You can use interface endpoints to privately and securely access AWS services, internal application services or SaaS services that are running outside of your VPC.

#### Amazon VPC Optimization Techniques
-	For workloads within the same region, if your destination service is either S3 or DynamoDB, utilize Gateway endpoints if possible.
-	Check for idle VPC Endpoints to find out if they are needed based on each use case given that they could be deleted if no traffic is going through them.
-	As the number of VPCs in your account grows, centralizing the interface endpoints might be more cost-efficient (please note this does not work with gateway endpoints).

#### Network Address Translation (NAT) Gateway
NAT Gateways have the following pricing dimensions:

-	Price per NAT Gateway ($/hour): Each hour that your NAT Gateway is provisioned and available.
-	Price per GB data processed ($/GB): Each gigabyte of data that it processed, regardless of the traffic’s source or destination.
-	Data Transfer charges ($/GB-month): There’s an additional indirect factor, which is Data Transfer charges.

#### NAT Gateway Optimization Techniques
-	Determine whether the majority of your NAT Gateway charges are from traffic to AWS regional services (Amazon S3, Amazon DynamoDB, Amazon Kinesis, Amazon SQS, Amazon CloudWatch, etc.) and route that traffic to and from those services using VPC endpoints.
-	Determine whether the resources sending most of the traffic to NAT Gateway are in the same Availability Zone as the NAT Gateway. If they are not, then route the traffic to a NAT Gateway in the same AZ to reduce cross-AZ data transfer charges.
-	Identify top contributors to traffic charges going through NAT Gateways. Consider enabling VPC Flow Logs, and then leverage CloudWatch Log Insights.
-	Inter-AZ Traffic:
  
              o	Resources sending traffic to NAT Gateways can be placed in the same AZs as their NAT Gateway to avoid traffic crossing AZs and incurring costs.
              o	It's recommended to check the route tables of the subnets in which those resources are created, and ensure that NAT Gateways in those route tables are in the same AZ. The ultimate goal is to get the traffic from private subnets flow "vertically" where possible.
-	Data Transfer Out:
                o	Evaluate if there is a legitimate use case and business reason for the traffic that your instances are sending out to the internet.
                o	It's recommended to place resources in private subnets where possible, including resources sending legitimate traffic out to the internet. Depending on the destination of the traffic (for example, if the destination for your traffic is within AWS), consider using PrivateLink, so the traffic wouldn't cross a NAT Gateway or Internet Gateway to reach its target. After carefully checking on security and compliance implications, you can then evaluate placing those resources in a public subnet.
-	Idle NAT Gateways:
        o	Consider checking unused NAT Gateways.
        o	Discover whether they are needed based on each use case given that they could be deleted if no traffic is going through them.

-	NAT Gateway data processing cost:
      o	An important cost component for NAT Gateways is the amount of traffic they process.
      o	If the workload running in your private subnet is reaching S3 or DynamoDB in the same region through NAT Gateway, then set up a gateway VPC endpoint and modify the corresponding VPC route table to route traffic to and from the AWS resource through the gateway VPC endpoint, rather than through the NAT Gateway.
