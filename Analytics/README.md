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
