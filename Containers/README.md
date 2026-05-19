## Containers:
Cost monitoring and optimization for container-based architectures using Amazon ECS and Amazon EKS.

### 1. Amazon Elastic Kubernetes Service (EKS)
Amazon Elastic Kubernetes Service (Amazon EKS) is a managed service that eliminates the need to install, operate, and maintain your own Kubernetes control plane on AWS. Kubernetes is an open-source system that automates the management, scaling, and deployment of containerized applications.

#### Terminology
1. Node:

A node may be a virtual or physical machine, depending on the cluster. Typically, you have several nodes in a cluster.

2. Cluster:

Combine several nodes to form a more powerful machine.

3. Container:

Each container that you run is repeatable; the standardization from having dependencies included means that you get the same behavior wherever you run it. Containers decouple applications from the underlying host infrastructure.

4. Pod:

One or more containers into a higher-level structure are called a pod. Any containers in the same pod will share the same resources and local network. Containers can easily communicate with other containers in the same pod as though they were on the same machine while maintaining a degree of isolation from others.

###### Amazon EKS Pricing

You can use a single EKS cluster to run multiple applications by taking advantage of Kubernetes namespaces and IAM security policies. You can run EKS on AWS using either Amazon EC2 or AWS Fargate, and on-premises using AWS Outposts.

If you are using Amazon EC2 (including with Amazon EKS managed node groups), you pay for AWS resources (e.g., EC2 instances, EBS volumes, Outposts capacity) you create to run your Kubernetes worker nodes. You only pay for what you use, as you use it; there are no minimum fees and no upfront commitments. See detailed pricing information on the Amazon EC2 pricing page and AWS Outposts rack pricing page.

#### Amazon EKS Optimization Techniques
- Underutilized resources: Identify Low Utilization Amazon EC2 Instances, from AWS Trusted Advisor, consider stopping or terminating instances that have low utilization, or scale the number of instances by using Auto Scaling.
  
- Tagging: Tag your EKS clusters and activate relevant tags for cost allocation. This will help you identify how your cost is spread across the different AWS services/resources (EKS, EC2, EBS, ELB, EFS and more). When using managed node groups, the EC2 instances created in the node group will be automatically tagged.
  
- EKS Split Cost Allocation Data: With EKS Split Cost Allocation Data (SCAD), you can receive granular cost visibility for EKS in the AWS Cost and Usage Reports (CUR) and Data Exports (CURv2.0), enabling you to analyze, optimize, and chargeback cost and usage for your Kubernetes applications. It enabled you to allocate application costs to individual business units and teams based on how Kubernetes applications consume shared EC2 CPU and memory resources.
  
- Auto Scaling: EKS supports two autoscaling products - Cluster Autoscaler and Karpenter. With autoscaling, you can automatically scale your EC2 resources to meet the required capacity.
  
- Rightsizing:
Right-size your EC2 nodes to fit the required capacity. The following tools can help you identify rightsizing opportunities:
```
- Amazon CloudWatch lets you observe CPU utilization, network throughput, and disk I/O.
- AWS Compute Optimizer helps avoid overprovisioning and underprovisioning of your resources based on your utilization metrics.
- AWS Cost Explorer is a free tool that lets you dive deeper into your cost and usage data to identify trends, pinpoint cost drivers, and detect anomalies.
```
AWS Compute Optimizer delivers actionable recommendations and also quantifies the cost impact of adopting these recommendations, so that you can prioritize your optimization efforts based on the size of the saving opportunity.
- Modernization
- Purchase Option Optimization (Spot & Savings Plans)


