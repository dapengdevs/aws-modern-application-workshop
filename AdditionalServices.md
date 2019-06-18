# Desktop

## Workspaces
* managed desktop sercvice
* Supports Windows, Max, Chromebooks, iPad, Fire tablets, Android tablets, Chrome and Firefox
* You will be given local admin access
* Workspaces are persistent
* You don't need an AWS account to login into workspaces

# Compute

## Batch
* Specify executions parameters and job dependendies
* Facilitates itnegration with a lot of batch computing workflow engines and languages (Peagasus, WMS, Luigi, AWS Steps)
* Dynamiccally provisons and scales EC2 and Spot instances

## Beanstalk
* Upload application code and sBeanstalk automatically handles all the details such as resource provisioning, load balancing, auto-scaling and monitoring
* Ideal for PHP, Java, Pythoon, Ruby, Node.JS, .Net, Go or Docker web applications
* Beanstalk uses EC2, ECS, Auto-Scaling, ELB

# Migration

## Migration Hub
* AWS Migration Hub provides a single location to track the progress of application migrations across multiple AWS and partner solutions
* Using Migration Hub allows you to choose the AWS and partner migration tools that best fit your needs, while providing visibility into the status of migrations across your portfolio of applications
* For example, you might use AWS Database Migration Service, AWS Server Migration Service, and partner migration tools such as ATADATA ATAmotion, CloudEndure Live Migration, or RiverMeadow Server Migration SaaS to migrate an application comprised of a database, virtualized web servers, and a bare metal server
* Using Migration Hub, you can view the migration progress of all the resources in the application

## Database Migration Service
* AWS Database Migration Service helps you migrate databases to AWS quickly and securely
* The source database remains fully operational during the migration, minimizing downtime to applications that rely on the database
* The AWS Database Migration Service can migrate your data to and from most widely used commercial and open-source databases
* AWS Database Migration Service supports homogenous migrations such as Oracle to Oracle, as well as heterogeneous migrations between different database platforms, such as Oracle or Microsoft SQL Server to Amazon Aurora
* With AWS Database Migration Service, you can continuously replicate your data with high availability and consolidate databases into a petabyte-scale data warehouse by streaming data to Amazon Redshift and Amazon S3

## Server Migration Service
* AWS Server Migration Service (SMS) is an agentless service which makes it easier and faster for you to migrate thousands of on-premises workloads to AWS
* AWS SMS allows you to automate, schedule, and track incremental replications of live server volumes, making it easier for you to coordinate large-scale server migrations

# Developer Tools

## CodeStar
* AWS CodeStar enables you to quickly develop, build, and deploy applications on AWS. AWS CodeStar provides a unified user interface, enabling you to easily manage your software development activities in one place
* With AWS CodeStar, you can set up your entire continuous delivery toolchain in minutes, allowing you to start releasing code faster. * AWS CodeStar makes it easy for your whole team to work together securely, allowing you to easily manage access and add owners, contributors, and viewers to your projects
* With AWS CodeStar, you can use a variety of project templates to start developing applications on Amazon EC2, AWS Lambda, and AWS Elastic Beanstalk
* AWS CodeStar projects support many popular programming languages including Java, JavaScript, PHP, Ruby, and Python

## CodeCommit
* Source-control service (Git Repos)

## CodeBuild
* CI

## CodeDeploy
* CD for EC2, Lambda and on-prem server

## CodePipeline
* CI/CD service

## X-Ray
* Analyze and debug applications
* X-Ray provides an end-to-end view of requests as they travel through your application, and shows a map of your application’s underlying components
* You can use X-Ray to analyze both applications in development and in production, from simple three-tier applications to complex microservices applications consisting of thousands of service

# Application Integration

## Step Functions
* Coordinate multiple AWS services into serverless workflows
* Design and run workflows that stitch together services such as lambda and ECS
* Workflows made up of steps, with output of one step as input into the next step

## MQ
* Managed Active MQ

# Management Tools

## Config
* AWS Config is a service that enables you to assess, audit, and evaluate the configurations of your AWS resources
* Config continuously monitors and records your AWS resource configurations and allows you to automate the evaluation of recorded configurations against desired configurations
* With Config, you can review changes in configurations and relationships between AWS resources, dive into detailed resource configuration histories, and determine your overall compliance against the configurations specified in your internal guidelines

## OpsWorks
* AWS OpsWorks is a configuration management service that provides managed instances of Chef and Puppet
* OpsWorks has three offerings, AWS Opsworks for Chef Automate, AWS OpsWorks for Puppet Enterprise, and AWS OpsWorks Stacks

## Systems Manager
* AWS Systems Manager gives you visibility and control of your infrastructure on AWS
* Systems Manager provides a unified user interface so you can view operational data from multiple AWS services and allows you to automate operational tasks across your AWS resources
* With Systems Manager, you can group resources, like Amazon EC2 instances, Amazon S3 buckets, or Amazon RDS instances, by application, view operational data for monitoring and troubleshooting, and take action on your groups of resources
* Systems Manager simplifies resource and application management, shortens the time to detect and resolve operational problems, and makes it easy to operate and manage your infrastructure securely at scale

# Analytics

## Athena
* Amazon Athena is an interactive query service that makes it easy to analyze data in Amazon S3 using standard SQL
* Athena is serverless, so there is no infrastructure to manage, and you pay only for the queries that you run
* With a few clicks in the AWS Management Console, customers can point Athena at their data stored in S3 and begin using standard SQL to run ad-hoc queries and get results in seconds
* You can use Athena to process logs, perform ad-hoc analysis, and run interactive queries
* Athena scales automatically – executing queries in parallel – so results are fast, even with large datasets and complex queries

## EMR
* Amazon Elastic Map Reduce (EMR) provides a managed Hadoop framework that makes it easy, fast, and cost-effective to process vast amounts of data across dynamically scalable Amazon EC2 instances
* You can also run other popular distributed frameworks such as Apache Spark, HBase, Presto, and Flink in Amazon EMR, and interact with data in other AWS data stores such as Amazon S3 and Amazon DynamoDB
* Amazon EMR securely and reliably handles a broad set of big data use cases, including log analysis, web indexing, data transformations (ETL), machine learning, financial analysis, scientific simulation, and bioinformatic

## CloudSearch
* Amazon CloudSearch is a managed service in the AWS Cloud that makes it simple and cost-effective to set up, manage, and scale a search solution for your website or application.
* Amazon CloudSearch supports 34 languages and popular search features such as highlighting, autocomplete, and geospatial search

## Kinesis
* Amazon Kinesis makes it easy to collect, process, and analyze real-time, streaming data so you can get timely insights and react quickly to new information
* There are four types of Kinesis service:
  * Kinesis Video Streams makes it easy to securely stream video from connected devices to AWS for analytics, machine learning (ML), and other processing
  * Kinesis Data Streams enables you to build custom applications that process or analyze streaming data for specialized needs
  * Kinesis Data Firehose is the easiest way to load streaming data into data stores and analytics tools
  * Amazon Kinesis Data Analytics is the easiest way to process and analyze real-time, streaming data

## Data Pipeline
* AWS Data Pipeline is a web service that helps you reliably process and move data between different AWS compute and storage services, as well as on-premises data sources, at specified intervals
* With AWS Data Pipeline, you can regularly access your data where it’s stored, transform and process it at scale, and efficiently transfer the results to AWS services such as Amazon S3, Amazon RDS, Amazon DynamoDB, and Amazon EMR
* AWS Data Pipeline helps you easily create complex data processing workloads that are fault tolerant, repeatable, and highly available

## Glue
* AWS Glue is a fully managed extract, transform, and load (ETL) service that makes it easy for customers to prepare and load their data for analytics
* You can create and run an ETL job with a few clicks in the AWS Management Console
* You simply point AWS Glue to your data stored on AWS, and AWS Glue discovers your data and stores the associated metadata (e.g. table definition and schema) in the AWS Glue Data Catalog
* Once cataloged, your data is immediately searchable, queryable, and available for ETL
* AWS Glue generates the code to execute your data transformations and data loading processes
