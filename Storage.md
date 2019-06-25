# Storage

## EBS
* Cold HDD, application with few data access, max IOPS 250
* Throughput HDD, data warehousing, log processing, max IOPS 500
* General Purpose SSD, OS boot volume, database, max IOPS 10000
* Provisioned IOPS SSD, large database, NoSQL, max IOPS 20000

## EFS
* Pay for what you use (in contrast to EBS, pay for what you privison)
* Multi-AZ metadata and storage
* Can configure mount-points in one, or many, AZs
* Can be mounted from on-premises systems ONLY if using Direct Connect or a VPN connection
* Good for big data and analytics, media processing workflows, content management, web serving, home directories etc.
* Can scale up to petabytes
* EFS is elastic and grows and shrinks as you add and remove data
* Can concurrently connect 1 to 1000s of EC2 instances, from multiple AZs
* By default you can create up to 10 file systems per account
* Can choose General Purpose or Max I/O (both SSD)
* The VPC of the connecting instance must have DNS hostnames enabled
* Data is stored across multiple AZ’s within a region
* Read after write consistency
* Need to create mount targets and choose AZ’s to include (recommended to include all AZ’s)
* Limited region support currently
* Using the EFS-to-EFS Backup solution, you can schedule automatic incremental backups of your Amazon EFS file system
* A file system can be accessed concurrently from all AZs in the region where it is located

## Access Control
* When you create a file system, you create endpoints in your VPC called “mount targets”
* When mounting from an EC2 instance, your file system’s DNS name, which you provide in your mount command, resolves to a mount target’s IP address
* You can control who can administer your file system using IAM
* You can control access to files and directories with POSIX-compliant user and group-level permissions
* EFS Security Groups act as a firewall, and the rules you add define the traffic flow

##  Encryption
* EFS offers the ability to encrypt data at rest and in transit
* Encryption keys are managed by the AWS Key Management Service (KMS)
* Data encryption in transit uses industry standard Transport Layer Security (TLS) 1.2
* Enable encryption at rest in the EFS console or by using the AWS CLI or SDKs

## EFS File Sync
* EFS File Sync provides a fast and simple way to securely sync existing file systems into Amazon EFS
* EFS File Sync copies files and directories into Amazon EFS at speeds up to 5x faster than standard Linux copy tools, with simple setup and management in the AWS Console
* EFS File Sync securely and efficiently copies files over the internet or an AWS Direct Connect connection
* Copies file data and file system metadata such as ownership, timestamps, and access permissions 

## Pricing and Billing
* You pay only for the amount of file system storage you use per month
* When using the Provisioned Throughput mode you pay for the throughput you provision per month
* There is no minimum fee and there are no set-up charges
