# E-Commerce Data Analysis with Hadoop, MySQL, and Hive

This README provides step-by-step instructions for setting up a Hadoop cluster, MySQL, and Hive, loading E-Commerce data into Hadoop Distributed File System (HDFS), and running basic analysis before and after optimization. The provided data source is from Kaggle's E-Commerce Behavior Data from a Multi-Category Store.

## Table of Contents
- [Prerequisites](#prerequisites)
- [Setting Up Hadoop](#setting-up-hadoop)
- [Setting Up MySQL](#setting-up-mysql)
- [Setting Up Hive](#setting-up-hive)
- [Data Preparation and Loading](#data-preparation-and-loading)
- [Basic Analysis](#basic-analysis)
- [Optimization with Bucketed Partitioning](#optimization-with-bucketed-partitioning)
- [Final Analysis](#final-analysis)
- [Results](#results)

## Prerequisites

Before starting, make sure you have the following installed:
- Hadoop
- MySQL
- Hive
- Java

## Setting Up Hadoop

1. Install Hadoop following the official installation guide for your platform.

2. Configure your Hadoop cluster by editing `core-site.xml`, `hdfs-site.xml`, and `yarn-site.xml`. Set up NameNode, DataNode, ResourceManager, and NodeManager as needed.

3. Start the Hadoop cluster and verify that it's running.

## Setting Up MySQL

1. Install MySQL following the official installation guide for your platform.

2. Create a MySQL database for storing metadata or any additional data as needed for your analysis.

## Setting Up Hive

1. Install Hive following the official installation guide for your platform.

2. Configure Hive by editing `hive-site.xml`.

3. Create Hive tables corresponding to your dataset, specifying the appropriate column names and data types.

## Data Preparation and Loading

1. Download the E-Commerce dataset from [Kaggle](https://www.kaggle.com/datasets/mkechinov/ecommerce-behavior-data-from-multi-category-store/?select=2019-Oct.csv).

2. Load the data into HDFS using the `hadoop fs` command.

3. Create an external table in Hive that references the data in HDFS.

## Basic Analysis

```sql
 select month(event_time) as pur_month,
sum(price) as pur_total_price
from ecommerce_stats
where year(event_time) = 2019
and event_type = 'purchase'
group by month(event_time);
```
```
select distinct category_id as product_category
from ecommerce_stats;
```
## Time Taken:

Time taken 1st: 213.554 seconds, Fetched: 1 row(s)
Time taken 2nd: 104.22 seconds, Fetched: 625 row(s)


##Optimization with Bucketed Partitioning
Implement bucketed partitioning in Hive by creating a table with buckets based on year and month.

Load the data into the new partitioned table.


## Time Taken After optimization:
Time taken 1st: 194.112 seconds previously(213.554), Fetched: 1 row(s)
Time taken 2nd: 89.407 seconds previously(104.22), Fetched: 625 row(s)

Average percentage Reduction in time : 11.63 %.
