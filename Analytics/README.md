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



