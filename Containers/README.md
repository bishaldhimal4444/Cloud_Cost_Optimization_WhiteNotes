## Containers:
Cost monitoring and optimization for container-based architectures using Amazon ECS and Amazon EKS.

### 1. Amazon Elastic Kubernetes Service (EKS)
Amazon Elastic Kubernetes Service (Amazon EKS) is a managed service that eliminates the need to install, operate, and maintain your own Kubernetes control plane on AWS. Kubernetes is an open-source system that automates the management, scaling, and deployment of containerized applications.

#### Terminology
1. Node: A node may be a virtual or physical machine, depending on the cluster. Typically, you have several nodes in a cluster.

2. Cluster: Combine several nodes to form a more powerful machine.

3. Container: Each container that you run is repeatable; the standardization from having dependencies included means that you get the same behavior wherever you run it. Containers decouple applications from the underlying host infrastructure.

4. Pod: One or more containers into a higher-level structure are called a pod. Any containers in the same pod will share the same resources and local network. Containers can easily communicate with other containers in the same pod as though they were on the same machine while maintaining a degree of isolation from others.

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
- Modernization: Use latest generation family or AMD and Graviton for better price-performance: Use latest generation family or AMD and Graviton for better price-performance.
- Purchase Option Optimization (Spot & Savings Plans): You can save EC2 instances costs by covering your EC2 On-Demand costs with Savings Plans (for 24/7 usage), or using Spot instances for workloads that can tolerate interruptions.

### 2. Amazon Elastic Container Service (ECS)
Amazon Elastic Container Service (Amazon ECS) is a highly scalable, high-performance container orchestration service that supports Docker containers and allows you to easily run and scale containerized applications on AWS.

Modern application (say Microservices) architecture recommends to split your applications into individual units, and Amazon ECS is optimized for this pattern. Tasks are the smallest unit of compute in Amazon ECS and allow you to define a set of containers you would like to place together, their properties, and how they may be linked. Tasks include all the information Amazon ECS needs to make the placement decision. To launch a single container, your task definition should only include one container definition.

###### Terminology
**Container:** Provide a standard way to package your application’s code, configurations, and dependencies into a single object. Containers share an operating system installed on the server and run as resource-isolated processes, ensuring quick, reliable, and consistent deployments, regardless of environment.

**Cluster:** A grouping of container instances.

**Task:** The instantiation of a task definition within a cluster. After you create a task definition for your application ECS, you can specify the number of tasks to run on your cluster. An ECS service runs and maintains your desired number of tasks simultaneously in a cluster.

###### Amazon ECS Pricing

There are two different charge models for Amazon ECS:

- Amazon EC2 Launch Type Model - There is no additional charge for Amazon EC2 launch type. You pay for AWS resources (such as Amazon EC2 instances or Amazon EBS volumes) you create to store and run your application. You only pay for what you use, as you use it; there are no minimum fees and no upfront commitments.

- AWS Fargate Launch Type Model (serverless) - With AWS Fargate, you pay for the amount of vCPU and memory resources that your containerized application requests. vCPU and memory resources are calculated from the time your container images are pulled until the Amazon ECS Task terminates, rounded up to the nearest second. A minimum charge of one minute applies.

#### Amazon ECS Optimization Techniques

**- Underutilized Resources:** Identify Low Utilization Amazon EC2 Instances, from AWS Trusted Advisor, consider stopping or terminating instances that have low utilization, or scale the number of instances by using Auto Scaling.

**- Tagging:** Tag your Amazon ECS and AWS Fargate resources such as services, task definitions, tasks, clusters, and container instances. Then, activating relevant tags for cost allocation will enable you to better allocate costs, improve visibility into your workloads, and search and identify your containerized applications.

**- ECS Split Cost Allocation Data:** With Split Cost Allocation Data (SCAD) feature it's possible to monitor how containerized applications consume shared compute and memory resources in CUR. So, you can allocate costs to individual applications, business units, or teams. To enable SCAD, you need to complete a simple two-step opt-in process. First, as a payer account owner, you need to opt-in SCAD from your AWS Billing and Cost Management preferences page. Then, enable SCAD for a new or existing CUR report from the Data Export page in the AWS Billing and Cost Management Console. Once enabled, the report will automatically scan for ECS tasks for the entire Consolidated Billing family (all clusters belonging to member accounts across all regions) and start preparing the granular cost data for the current month.

**- Rightsizing:** Over-provisioning an Amazon ECS task's CPU and memory results in unnecessary spending while under-provisioning can lead to poor application performance. AWS Compute Optimizer delivers actionable recommendations so you can optimize your task CPU and memory allocation for your Amazon ECS services running on Fargate. AWS Compute Optimizer also quantifies the cost impact of adopting these recommendations, so that you can prioritize your optimization efforts based on the size of the saving opportunity.

**- Auto Scaling:** Optimizing auto-scaling policies for ECS and Fargate services is an effective strategy for cost reduction. Ensuring that a cluster service is not scaling unnecessarily will lead to cost efficiency. To fine-tune auto-scaling in ECS and Fargate service configuration, it’s important to learn the baseline performance of the application and then the performance of the application under load.

**- Savings Plans:** Use Compute Savings Plan to cover your ECS and Fargate cost. AWS Fargate pricing is based on the vCPU and memory resources used from the time you start to download your container image until the Amazon ECS task terminates, rounded up to the nearest second. Savings Plans offer savings of up to 50% on your AWS Fargate usage in exchange for a commitment to use a specific amount of compute usage (measured in dollars per hour) for a one or three year term. The AWS Cost Explorer will help you to choose a Savings Plan, and will guide you through the purchase process.

**- Spot:** By utilizing Fargate Spot, you can save up to 70% of the on-demand pricing to run fault tolerant Fargate tasks. It’s not only a great option for parallelizable tasks, but also for websites and API tasks, which require high availability. When configuring your service auto-scaling policy, you can specify the minimum number of regular tasks that should run at all times and then add tasks running on Fargate Spot to improve service performance in a cost-efficient way.

### Note's:
**1. Your organization uses ECS for periodic data pipelines tasks, which purchase option will be the most cost effective?**
- Spot

**2. Your organization uses ECS and would like to allocate container costs to individual business units and teams, based on how the container workloads consume shared compute and memory resources. They would like to do this at the task level. What service should they use to achieve this?**
- Enable split cost allocation data feature

**3. What is the best way to see EKS total cost, including EC2 instance, EBS volume and EKS cluster cost?**
- Filter by the cost allocation tag in AWS Cost Explorer

**4. What is the best tool to review rightisizng opportunities for your EKS nodes?**
- AWS Compute Optimizer

