## Analytics:
Strategies for optimizing costs in analytics workloads powered by Amazon Athena, Amazon EMR, and Amazon Redshift.

### 1. Amazon Athena
Amazon Athena is a serverless, interactive analytics service built on open-source frameworks, supporting open-table and file formats. Athena provides a simplified, flexible way to analyze petabytes of data where it lives. You can analyze data or build applications from an Amazon Simple Storage Service (S3) data lake and 30 data sources, including on-premises data sources or other cloud systems using SQL or Python.

###### Amazon Athena Pricing
With per query billing, you can get started quickly and pay only for the data scanned by queries you run. You are charged for the number of bytes scanned per query, rounded up to the nearest megabyte, with a 10 MB minimum per query

#### Amazon Athena Optimization Techniques
**- Partition your data:** Partitioning divides your table into parts and keeps the related data together based on column values such as date, country, and region. You can restrict the amount of data scanned by a query by specifying filters based on the partition

**- Use compression:** Compressing your data can speed up your queries significantly. Smaller chunks of data reduce the data scanned from Amazon S3, resulting in lower costs of running queries. It also reduces the network traffic from Amazon S3 to Athena. Parquet and ORC files are splittable because these formats compress sections of the files separately, and have metadata that contains the locations within the files for the different sections. The GZIP format provides good compression ratios and has a wide range support across other tools and services.

**- Query tuning:** The Athena SQL engine is built on the open source distributed query engines Trino and Presto. Understanding how it works provides insight into how you can optimize queries when running them. Recommended best practices are:
- Optimize 'ORDER BY '
- Optimize joins
- Optimize 'GROUP BY '
- Use approximate functions
- Only include the columns that you need

### 2. Amazon Elastic Map Reduce (EMR)
Amazon EMR is the industry-leading cloud big data solution for petabyte-scale data processing, interactive analytics, and machine learning using open-source frameworks such as Apache Spark, Apache Hive, and Presto.

###### Amazon EMR Pricing
EMR price is added to the Amazon EC2 cost - the price for the underlying instances and Amazon EBS volumes. There is a variety of EC2 pricing options you can choose from, including On-Demand, Reserved Instances, Savings Plans, and Spot instances. Spot Instances are a spare EC2 capacity available at a discounted rate. See Spot Instance price savings versus On Demand by filtering for "Instance types supported by EMR" on the Spot Instance Advisor page.

#### Amazon EMR Optimization
**- Reserved Instances:** Reserved Instances are a cost-saving option that offers you to commit to running a certain amount of resources (such as instances) for one or three years, in return for a discounted rate. When you launch an EMR cluster, you can benefit from RI discount if the attributes of the underlying EC2 instances match the attributes of your active RIs. Keep in mind that RI discounts only apply to the EC2 instances, and not to other resources like EBS or S3.

**- Saving Plans:** Saving Plans provide flexible pricing that is based on a commitment to use a specific amount of compute resources over a period of one or three years. To use Saving Plans with EMR, you can purchase a Saving Plan that matches the compute usage of your EMR cluster, and the discount will apply automatically. Keep in mind that Saving Plans require careful consideration of usage patterns. You should monitor your usage and adjust your Saving Plans as needed to ensure that you are getting the best possible savings.

**- Transient Clusters vs. Long Running Clusters:** EMR clusters can be configured to run as either transient or long-running clusters. Transient clusters are created and terminated for a specific job or set of jobs, while long-running clusters are maintained for ongoing data processing tasks. Transient clusters can help save on costs by only running when needed, and can be terminated once the job is complete. Long-running clusters, on the other hand, can provide more predictable and consistent processing power but require ongoing maintenance costs.

**- Instance Fleets:** The instance fleet configuration for Amazon EMR clusters lets you select a wide variety of provisioning options for Amazon EC2 instances, and helps you develop a flexible and elastic resourcing strategy for each node type in your cluster. In an instance fleet configuration, you specify a target capacity for On-Demand Instances and Spot Instances within each fleet. When Amazon EC2 reclaims a Spot Instance in a running cluster because of a price increase or instance failure, Amazon EMR tries to replace the instance with any of the instance types that you specify. This makes it easier to regain capacity during a spike in Spot pricing.

**- Partitioning and File Compression on S3:** Partitioning your data on S3 can help optimize your EMR costs by reducing the amount of data read and processed during each query. This can be especially important for large datasets. File compression can also help reduce the amount of data read and processed during queries. Common compression formats include GZIP and snappy.

### 3. Amazon Redshift
Customers use Amazon Redshift to modernize their data analytics workloads and deliver insights for their businesses. With a fully managed, AI powered, massively parallel processing (MPP) architecture, Amazon Redshift drives business decision making quickly and cost effectively.

###### Amazon Redshift Pricing

- Amazon Redshift node types: Choose the best cluster configuration and node type for your needs, and pay for capacity by the hour with Amazon Redshift on-demand pricing. When you choose on-demand pricing, you can use the pause and resume feature to suspend on-demand billing when a cluster is not in use.
- You can also choose Reserved nodes instead of on-demand instances for steady-state workloads and get significant discounts over on-demand pricing.
- Amazon Redshift Spectrum pricing: Run SQL queries directly against the data in your Amazon S3 data lake, out to exabytes -- you simply pay for the number of bytes scanned.
- Concurrency Scaling pricing: Each cluster earns up to one hour of free Concurrency Scaling credits per day, which is sufficient for 97% of customers. This enables you to provide consistently fast performance, even with thousands of concurrent queries and users. You simply pay a per-second on-demand rate for usage that exceeds the free credits.
- RMS pricing: Pay only for the data you store in RA3 clusters, independent of the number of compute nodes provisioned. You simply pay hourly for the total amount of data in managed storage. RMS is also used with Amazon Redshift Serverless.
- Redshift ML: Use SQL to create, train, and deploy machine learning (ML) models. After you exhaust the free tier for Amazon SageMaker, you will incur costs for creating your model and storage. Redshift ML is also available for use with Amazon Redshift Serverless.

##### Amazon Redshift Optimization
**- Amazon Redshift Managed Storage:** (Relevant when using RA3 nodes or Serverless) Managed storage comes exclusively with RA3 node types, and you pay the same low rate for Redshift managed storage regardless of data size. Usage of managed storage is calculated hourly based on the total data present in the managed storage. You can monitor the amount of data in your RA3 cluster via Amazon CloudWatch or the AWS Management Console. You do not pay for any data transfer charges between RA3 nodes and managed storage. Managed storage charges do not include back up storage charges due to automated and manual snapshots (see more information in the documentation on Backup Storage). Once the cluster is terminated, you will continue to be charged for the retention of your manual backups. Example for RMS cost calculation can be found on the Redshift pricing page.

**- Pause and Resume Amazon Redshift:** Pause clusters which do not need to be up 24x7. Shut down underutilized or development workloads on weekends/weeknights. This feature is available through the console or Redshift API.

**- Underutilized Amazon Redshift Clusters:** Review underutilized Redshift clusters in AWS Trusted Advisor and terminate if not required. Depending on your analysis of the cluster utilization metrics, you can either shut it down after taking a final snapshot, or downsize it.

**- Redshift Spectrum:** Redshift Spectrum allows you to directly run SQL queries against exabytes of data in Amazon S3. This is charged per terabyte of data scanned. You can control your Spectrum costs by configuring usage limits.

**- Amazon Redshift Serverless:** Easily run analytics workloads of any size without managing data warehouse infrastructure. Developers, data scientists, and data analysts can work across data warehouses and data lakes to build reporting and dashboarding applications, perform real-time analytics, collaborate on data, and build and train machine learning (ML) models. You pay only for what you use. Redshift Serverless offers flexibility to support a diverse set of workloads of varying complexity, starting at a low price point.

**- Amazon Redshift Reserved Nodes:** If you intend to keep your Redshift cluster running continuously for a prolonged period, you should consider purchasing reserved node offering. These offerings provide significant savings over on-demand pricing, but they require you to commit to paying for a certain amount of usage for either a one-year or three-year duration in return for a discount. Reserved nodes are a billing concept that is used to determine the rate at which you are charged for nodes. Reserving a node does not actually create any nodes for you. You are charged for reserved nodes regardless of usage, which means that you must pay for each node that you reserve for the whole duration of the term, whether or not you have any Redshift nodes in a running cluster to which the discounted rate applies.


### 4. Amazon Managed Streaming for Apache Kafka
Amazon Managed Streaming for Apache Kafka (Amazon MSK) makes it easy to ingest and process streaming data in real time with fully managed Apache Kafka. It is good for ingesting and processing log and event streams, running centralized state or data buses and to power your event-driven systems.

##### Amazon Managed Streaming for Apache Kafka Pricing

You pay an hourly rate for Apache Kafka broker instance usage (billed at one-second resolution), with varying fees depending on the size of the broker instance and active brokers in your Amazon MSK clusters. You also pay for the amount of storage you provision in your cluster. You are not charged for data transfer between brokers or between Apache ZooKeeper nodes and brokers. You will pay standard AWS data transfer charges for data transferred in and out of Amazon MSK clusters.

#### Amazon Managed Streaming for Apache Kafka Optimization
**Rightsizing your cluster:** You can size your clusters to meet your throughput, availability, and latency requirements. For the implementation details, can out the Best practices for right-sizing your Apache Kafka clusters to optimize performance and cost blog post, which also provides answers to questions such as when you should scale up versus scale out, and guidance on how to continuously verify the size of your production clusters.

**Manage Data retention:** You can use different data retention strategies to reduce your storage costs by using data retention parameters on a cluster or topic level. Adjust log data retention parameters:
- Log data retention on Provisioned MSK Clusters at the cluster level
- Topic retention parameters

**Configure tiered storage on Provisioned MSK Clusters:** You can create an Amazon MSK cluster configured with tiered storage that balances performance and cost. Amazon MSK stores streaming data in a performance-optimized primary storage tier until it reaches the Apache Kafka topic retention limits. Then, Amazon MSK automatically moves data into the new low-cost storage.

**Reduce network traffic costs:** 
- By default, Amazon MSK sets the brocker.rack parameter automatically according to the Availability Zone in which it is deployed. For example, when you deploy a three-node MSK cluster across three Availability Zones, each node has a different broker.rack setting. When you deploy a six-node MSK cluster across three Availability Zones, you have a total of three unique broker.rack values.
- By default, Kafka consumers retrieve data from the leader of a partition, which could be in a different rack, or Availability Zone. Using Amazon MSK 2.4.1.1 or above, you can modify both broker and consumer's configuration to allow consumers to fetch data from the closest replica, using client.rack parameter on the consumers and replica.selector.class on the brokers, to avoid cross-AZ traffic costs.

### Note's:
**1. You have been running a workload with EMR and want to reduce the cost. You are considering using a commitment discount but do not want to pay upfront for it. What is your best option for this?**
- Saving Plans

**2. Which statement about MSK Data Transfer pricing is true?**
- You are not charged for data transfer between brokers

**3. A customer requires an auto-scaling data warehouse for variable workloads. What is the most cost-effective service for this?**
- Amazon Redshift Serverless




