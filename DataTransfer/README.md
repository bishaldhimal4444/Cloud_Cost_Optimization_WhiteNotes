## Data Transfer: 
An overview of techniques for managing and optimizing data transfer costs across AWS services and regions.

#### Types of Data Transfer (DT):

###### 1.	DT Internet 
-	cost for DT-OUT to the internet depends on the AWS regions(from which region, data is out).
-	up to 100 Gb of DT-OUT per month is free (under Free Tier)
-	DT-IN from the internet is free.

###### 2.	DT between AWS Regions
-	DT-OUT pricing to another AWS region depends on the originating region.
-	DT-IN from another AWS region is free.

###### 3.	DT within as AWS Region
-	When resources in different AZ’s of the same AWS region communicate, you are charged for both DT-IN and DT-OUT.
-	When resources within the same AZ communicate while using Private IP, then DT is free.
-	When resources within the same AZ communicate while using Public IP, you are charged for DT.

#### Data Transfer in Amazon CloudFront

 DT for CloudFront is charged as follows:
-	Up to 1Tb of DT-OUT per month is free (under Free Tier)
-	DT from the origin/aws-region to edge location is free
-	DT from CloudFront edge location to the origin/aws-region (aws backend resource) is charged depending on the location

#### Data Transfer in AWS Direct Connect
DT for AWS Direct Connect is charged as follows:
-	DT Out from AWS Region to AWS Direct Connect location is charged depending on the region and location
-	DT In from AWS Direct Connect location into AWS is free

#### Data Transfer/DT Optimization Ways:

###### 1.	DT Internet
-	Amazon CloudFront 
  
o	If you need to transfer data externally, CloudFront can be a secure and cost-efficient solution. Evaluate your DT traffic patterns and volume to determine if it's the right choice for your scenario 

o	CloudFront Security Savings bundle: you can save up to 30% on your CloudFront bill in exchange for a set monthly spend commitment over a one-year term. 

o	If you have a public-facing service that delivers content like videos or audio files, utilizing CloudFront can be beneficial 

-	AWS PrivateLink
o	With AWS PrivateLink you can establish private connection between your VPCs, or even with the VPC in another AWS account, without using internet gateway.

o	Gateway VPC endpoints allow communication to Amazon S3 and Amazon DynamoDB without requiring an internet gateway or a NAT device. There is no additional charge for using gateway endpoints.

o	Interface VPC endpoints allow private and secure access to AWS services, your internal applications, or SaaS services that are running outside of your VPC. Interface endpoints incur hourly service charges and data transfer charges.

-	AWS Direct Connect
o	Use Direct Connect when sending data to on-premises networks. AWS Direct Connect can reduce network costs, increase bandwidth throughput, and provide a more consistent network experience than internet-based connections.

###### 2.	DT between AWS Region/Inter-Region
-	Avoid cross-region data transfer unless your business case requires it.
-	Place your S3 buckets in a region where most of your other resources are located to minimize unnecessary data movements across the global network.


###### 3.	DT within an AWS Regioin/Inter-AZ
-	DT between resources within the same AZ is free when using private IPs.
-	DT between Application Load Balancers (ALB) and backend resources (e.g. EC2 instances) within the same AWS Region is free.
-	Use resources within the same AZ where possible.
-	DT over a VPC peering connection that stays within an AZ is free.
-	Some multi-AZ configurations for replication purposes are exempt from charges when replicating data across AZs. These include: Amazon Aurora, Amazon Neptune, and Amazon RDS. Use private IPs where possible for resources when sending traffic between them.
-	Use Gateway VPC Endpoints for S3 and DynamoDB.
-	Place NAT Gateway in the same AZ with the backend instances where possible



