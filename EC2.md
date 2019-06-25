# Amazon Ec2

## General
* Limit: 20 On-Demand, 20 Reserved Instance
* EC2 Compute Unit = ECU, relative measure of integer processing power of EC2 instance
* For windows, private key file is required to obtain the password

## Metadata and user data
* User data. data supplied by user at launch time
* User data, limited to 16KB

## Billing
* On-demand
  * pay for hours, no upfront cost
  * Ideal for auto-scaling groups and unrpredicatable workloads
  * dev/test
* Spot
  * Grid computing and HPC
  * Charged by hours unless AWS terminates, the hour is free
  * Sopt requests can be "fill or kill", "maintain" or "duration based"
  * One time request, data is ephemeral
  * Request and maintain, instance can terminate, stop, hibernate until price is met again
  * Can't use encrypted volumes
  * EC2 isntance will receive notification on termination, termination in 2 minutes
* Reserved
  * Provides a capacity reservation when used in a specific AZ
  * AWS Billing automatically applies discounted rates when you launch an instance that matches your purchased RI
  * Capacity reserved for 1 or 3 years
  * 3 RI types
    * Standard: 1 or 3 years, charged whether on or off
    * Convertible: can change instance family OS, payment options, benefit from price reducation. less discount.
    * Scheduled: reserved for specifc periods, accured charges hourly
  * Predictable workloads
  * Upfront payments
  * Can switch AZ within the same region
  * Can change size within the same instance type (not for Windows)
  * Instance type modification only for Linux
  * Can sell reservation on market place
  * Can be used in ASG, PG
  * Can be shared across accounts in consolidated Billing
  * RI attribtues:
    * Instance type
    * Platform/OS
    * Tenancy (default/shared or dedicated)
    * AZ (optional)
* Dedicated hosts
  * physical servers dedicated just for you
  * Available as on-demand or with decdicated host reservation
  * Server-bound license
  * Can run only one instance size and type
  * Complete isolation
  * Expensive, billing per host
* Dedicated instances
  * Virtualized instances on hardware just for you
  * Use physically dedicated servers
  * Billing per instance
  * May share hardware with other non-dedicated instances
  * Available as On-demand, RI and spot instances
  * Additional cost
* Instances are billed when they are in running state (stop or terminate to avoid payment)
* Billed by hour or second(Linux only)
* Data transfer btetween instances in different regions is charged (in and out)

## Instance Types
* D   Data      File servers, data warehouse
* R   RAM       Memory optimized
* M   MAIN      General purpose -- App server
* C   COMPUTE   compute optimized
* G   GRAPHISC  Grpahics intersive workloads
* I   IOPS      IO optimized (NoSQL, DW)
* F   FAST      FPGA hardware acceleration
* T   CHEAP     Low cost
* P   GPU       GPC requirements
* X   EXTREME RAM heavy memory (SAP HAAN, Apache Spark)

## Creating Instances
* T2 unlimited allows application to burst past CPU baselines
* can run script on startup (user data)
* AMI includes
  * A template for root volume (OS, application servers etc.)
  * Launch permissions
  * Block device mapping
* AMIs are regional. You can copy AMI to other regions.

## AMIs
* 4 types
 * published by AWS
 * AWS Marketplace
 * Existing instances's AMI
 * Uplaoded AMIs (imported/exported via AWS Import/Export) 

## Networking
* 5 elastic IPs per region
* Elastic IP will be charged if they are not used
* Elastic IP is bound to region
* Public IP assgined to instances in public subnets
* DNS record for elastic IP can be configured by filling out a form
* You can assign or remove IP addresses from EC2 instances while they are running or stopped
* You can attach a network interface to an instance in a different subnet as long as it is wihtin the same AZ
* Eth0 is the primary network interface and can't be moved to detached. Only ENI created by default.
* You can add one extra ENU when launching but more can be attached later
* ENI can be hot-attached to running instacnes, or warm-attched to stopped instances, cold-attached when launching
* If you add a second interface AWS will not assign a public IP address to eth0 (you would need to add an Elastic IP)
* Default interfaces are terminated with instance termination, Manually added interfaces are not terminated by default. You can change the termination behaviour
* ENI can have
  * One primary IPv4 address
  * One or more secondary IPv4 addresses
  * One Elastic IP address corresponding to each IPv4 address (via NAT)
  * One public IPv4 address
  * One or more IPv6 addresses
  * Up to 5 security groups

## Enhanced Networking
* If your packets-per-second rate appears to have reached its ceiling, you should consider moving to enhanced networking because you have likely reached the upper thresholds of the VIF driver
* AWS currently supports enhanced networking capabilities using SR-IOV
* SR-IOV provides direct access to network adapters, provides higher performance (packets-per-second) and lower latency
* Must launch an HVM AMI with the appropriate drivers
* Only available for certain instance types
* Only supported in VPC

## Networking Limits (per region)
* Elastic IP: 5
* VPC: 5
* Subents per VPC: 200
* SG per VPC: 500
* Rules per SG: 50
* Network Interfaces: 350
* ACL per VPC: 200
* Route tables per VPC: 200
* Entries per Route table: 50
* Active VPC Peering: 50

## Placement Groups

* Cluster: low-latency group in a single AZ
  *  application with low-latency, high network throughput
* Spread: spreads instances across underlying ahrdware (can span AZ)
  * each instance placed on distinct hardware for HA
* There is a maximum of 7 running instances per spread placement group within an AZ
* Spread placement groups are not supported for Dedicated Instances or Dedicated Hosts
* Recommended to keep instance types homogenous within a placement group
* Cannot merge placement groups
* Cannot move existing instances into a PG
* For existing instances, create an AMI then launch from the AMI into the placement group
* Can use reserved instances at an instance level but cannot reserve capacity for the placement group

## IAM Roles
* You can attach an IAM role to an instance at launch time or at any time after by using the AWS CLI, SDK, or the EC2 console
* IAM roles can be attached, modified, or replaced at any time
* Only one IAM role can be attached to an EC2 instance at a time

## EC2 Migration
* VM Import/Export is a tool for migrating VMware, Microsoft, XEN VMs to the Cloud
* Can also be used to convert EC2 instances to VMware, Microsoft or XEN VMs
* Supported for:
  * Windows and Linux
  * VMware ESX VMDKs and (OVA images for export only)
  * Citrix XEN VHD
  * Microsoft Hyper-V VHD
* Can only be used via the API or CLI (not the console)
* Stop the VM before generating VMDK or VHD images
* AWS Server Migration Service (SMS) is an agent-less service which makes it easier and faster for you to migrate thousands of on-premises workloads to AWS
* AWS SMS allows you to automate, schedule, and track incremental replications of live server volumes, making it easier for you to coordinate large-scale server migrations
* Automates migration of on-premises VMware vSphere or Microsoft Hyper-V/SCVMM virtual machines to AWS
* Replicates VMs to AWS, syncing volumes and creating periodic AMIs
* Supports Windows and Linux VMs only (just like AWS)
* The Server Migration Connector is downloaded as a virtual appliance into your on-premises vSphere or Hyper-V environments

## Monitoring
* EC2 status check performed every minute
* If all checks pass, status __OK__. If one fails, status __impaired__
* System status check detect problems that AWS needs to fix
* Instance status check detect problems you need to fix
* Status check cannot be disabled
* CloudWatch aliams taht monitor EC2 isntances and automatically perform an action if status check fails
  * Recover instance
  * Stop instance
  * Terminate instance
  * Reboot instance (best practice)
