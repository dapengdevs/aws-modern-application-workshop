# Storage

## EBS

### General
* EBS volumes are network attached storage that can be attached to EC2 instances
* EBS volume data persists independently of the life of the instance
* EBS volumes do not need to be attached to an instance
* You can attach multiple EBS volumes to an instance
* You cannot attach an EBS volume to multiple instances (use Elastic File Store instead)
* EBS volume data is replicated across multiple servers in an AZ
* EBS volumes must be in the same AZ as the instances they are attached to
* EBS is designed for an annual failure rate of 0.1%-0.2% & an SLA of 99.95%
* Root EBS volumes are deleted on termination by default
* Extra non-boot volumes are not deleted on termination by default
* You can now create AMIs with encrypted root/boot volumes as well as data volumes
* Volume sizes and types can be upgraded without downtime (except for magnetic standard)
* Elastic Volumes allow you to increase volume size, adjust performance, or change the volume type while the volume is in use
* To migrate volumes between AZ’s create a snapshot then create a volume in another AZ from the snapshot (possible to change size and type)
* The root device is created under /dev/sda1 or /dev/xvda
* Throughput optimized EBS volumes cannot be a boot volume
* You can use block device mapping to specify additional EBS volumes or instance store volumes to attach to an instance when it’s launched
* You can also attach additional EBS volumes to a running instance
* You cannot decrease an EBS volume size
* When changing volumes the new volume must be at least the size of the current volume’s snapshot
* Images can be made public but not if they’re encrypted
* AMIs can be shared with other accounts
* You can have up to 5,000 EBS volumes by default
* You can have up to 10,000 snapshots by default

### Volume Types
* Cold HDD (sc1), application with few data access, max IOPS 250
* Throughput HDD (st1), data warehousing, log processing, max IOPS 500
* General Purpose SSD (gp2), OS boot volume, database, max IOPS 10000 -- 16000 
* Provisioned IOPS SSD (io1), large database, NoSQL, max IOPS 20000 -- 64000
* HDD Magnetic: Stnadard & Cheap, lowest cost storage that can be a root volume
* EBS optimized instances, avail for selected instance types, additional fee

### Snapshots
* Snapshots capture a point-in-time state of an instance
* Can be used to migrate a system to a new AZ or region
* Can convert an unencrypted volume to an encrypted volume
* Snapshots are stored on S3
* If you make periodic snapshots of a volume, the snapshots are incremental, which means that only the blocks on the device that have changed after your last snapshot are saved in the new snapshot
* Even though snapshots are saved incrementally, the snapshot deletion process is designed so that you need to retain only the most recent snapshot in order to restore the volume
* Snapshots can only be accessed through the EC2 APIs
* EBS volumes are AZ specific but snapshots are region specific
* Volumes can be created from EBS snapshots that are the same size or larger
* Snapshots can be taken of non-root EBS volumes while running
* To take a consistent snapshots writes must be stopped (paused) until the snapshot is complete – if not possible the volume needs to be detached, or if it’s an EBS root volume the instance must be stopped
* Deleting a snapshot removes only the data not needed by any other snapshot
* Snapshots can be copied between regions (and be encrypted). Images are then created from the snapshot in the other region which creates an AMI that can be used to boot an instance
* You can create volumes from snapshots and choose the availability zone within the region

### Encryption
* Snapshots of encrypted volumes are encrypted automatically
* EBS volumes restored from encrypted snapshots are encrypted automatically
* EBS volumes created from encrypted snapshots are also encrypted
* You can share snapshots, but if they’re encrypted it must be with a custom CMK key
* There is no direct way to change the encryption state of a volume
* Either create an encrypted volume and copy data to it or take a snapshot, encrypt it, and create a new encrypted volume from the snapshot
* To encrypt a volume or snapshot you need an encryption key, these are customer managed keys (CMK) and they are managed by the AWS Key Management Service (KMS)
* A default CMK key is generated for the first encrypted volumes
* The CMK used to encrypt a volume is used by any snapshots and volumes created from snapshots
* You cannot change the CMK key that is used to encrypt a volume
* By default only the account owner can create volumes from snapshots
* You can share unencrypted snapshots with the AWS community by making them public
* You can also share unencrypted snapshots with other AWS accounts by making them private and selecting the accounts to share them with
* You cannot make encrypted snapshots public
* Copying snapshots may be required for:
  * Creating services in other regions
  * DR – the ability to restore from snapshot in another region
  * Migration to another region
  * Applying encryption
  * Data retention
* To take application-consistent snapshots of RAID arrays:
  * Stop the application from writing to disk
  * Flush all caches to the disk
  * Freeze the filesystem
  * Unmount the RAID array
  * Shut down the associated EC2 instance

### RAID
* RAID can be used to increase IOPS
* RAID 0 = 0 striping – data is written across multiple disks and increases performance but no redundancy
* RAID 1 = 1 mirroring – creates 2 copies of the data but does not increase performance, only redundancy
* RAID 10 = 10 combination of RAID 1 and 2 resulting in increase performance and redundancy (at the cost of additional disks)
* You can configure multiple striped gp2 or standard volumes (typically RAID 0)
* You can configure multiple striped PIOPS volumes (typically RAID 0)
* EBS optimized EC2 instances are another way of increasing performance
* Ensure the EC2 instance can handle the bandwidth required for the increased performance
* Not recommended to use RAID for root/boot volumes

### AMIs
* An Amazon Machine Image (AMI) is a special type of virtual appliance that is used to create a virtual machine within EC2
  * A template for the root volume for the instance (for example, an operating system, an application server, and applications)
  * Launch permissions that control which AWS accounts can use the AMI to launch instances
  * A block device mapping that specifies the volumes to attach to the instance when it’s launched
* Instance store-backed:
  * Launch an EC2 instance from an AWS instance store-backed AMI
  * Update the root volume as required
  * Create the AMI which will upload to a user-specified S3 bucket (user bucket)
  * Register the AMI with EC2 (creates another EC2 controlled S3 image)
  * Instance store-backed volumes can only be created at launch time
* EBS-backed:
  * Must stop the instance to create a consistent image and then create the AMI
  * AWS registers the AMIs manually
  * During creation AWS creates snapshots of all attached volumes 
  * You cannot delete the snapshot of the root volume as long as the AMI is registered (deregister and delete)
* Copying AMIs:
  * You can copy an Amazon Machine Image (AMI) within or across an AWS region using the AWS Management Console, the AWS AWS Command Line Interface or SDKs, or the Amazon EC2 API, all of which support theCopyImage action
  * You can copy both Amazon EBS-backed AMIs and instance store-backed AMIs
  * You can copy encrypted AMIs and AMIs with encrypted snapshots

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

### Access Control
* When you create a file system, you create endpoints in your VPC called “mount targets”
* When mounting from an EC2 instance, your file system’s DNS name, which you provide in your mount command, resolves to a mount target’s IP address
* You can control who can administer your file system using IAM
* You can control access to files and directories with POSIX-compliant user and group-level permissions
* EFS Security Groups act as a firewall, and the rules you add define the traffic flow

###  Encryption
* EFS offers the ability to encrypt data at rest and in transit
* Encryption keys are managed by the AWS Key Management Service (KMS)
* Data encryption in transit uses industry standard Transport Layer Security (TLS) 1.2
* Enable encryption at rest in the EFS console or by using the AWS CLI or SDKs

### EFS Data Sync
* EFS File Sync provides a fast and simple way to securely sync existing file systems into Amazon EFS/S3
* EFS File Sync copies files and directories into Amazon EFS at speeds up to 5x faster than standard Linux copy tools, with simple setup and management in the AWS Console
* EFS File Sync securely and efficiently copies files over the internet or an AWS Direct Connect connection
* Copies file data and file system metadata such as ownership, timestamps, and access permissions 
* Run AWS DataSync Agent on on-prem system

### Pricing and Billing
* You pay only for the amount of file system storage you use per month
* When using the Provisioned Throughput mode you pay for the throughput you provision per month
* There is no minimum fee and there are no set-up charges

## Storage Gateway
* Enables hybrid storage between on-prem and on-cloud
* Implemented usnig a VM running on-prem
* Provides local storage backed by S3 and Glacier
* Supports 3 storage interfaces: file, volume and tape
* File gateway: EC2 or on-prem to store objects in S3
* Volume Gateway Stored Mode/Gateway Stored Volumes: async. replication of on-prem data to S3
* Volume Gateway Cached Mode/Gateway Cached Volumes: sync. storage in S3 with frequnetly accessed data cached locally on-prem
* Tape Gateway/Gateway-Virtual tape Library
* Data transfer between Gateway and S3 is server-side encrypted with SSE-S3
* File gateway supprots SSE-KMS
* File Gateway supprot S3 Standard, S3 IA and S3 One Zone IA
* Volume 

