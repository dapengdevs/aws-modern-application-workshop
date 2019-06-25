# Storage

## EBS
* Cold HDD, application with few data access, max IOPS 250
* Throughput HDD, data warehousing, log processing, max IOPS 500
* General Purpose SSD, OS boot volume, database, max IOPS 10000
* Provisioned IOPS SSD, large database, NoSQL, max IOPS 20000

## S3
* object storage
* conssits of meta data and data
* Size: 0 - 5 TB
* S3 objects are replciated across multiple devices within a region
* To avoid accidental deletion, enable versioning and MFA
* Bucket name between 3 and 63 chars, can contain numbers, letters, hypen and period
* Conssitency
  * Read after write consistency for PUTs to new object
  * Eventual consistency for PUT/DELETE of existing object
* S3 storage classes
  * Standard: 99.99% availabiltiy, >=3 AZs
  * Intelligent tiering: 99.9% availability, storage duration is unknown. AI monitors the usage and moves to different class upon usage, >=3 AZs
  * Standard-IA: 99.9% availability, less frequnetly accessed data, min charge size: 128KB, >=3 AZs
  * One Zone IA: 99.5% availability, less frequnetly accessed data that requires sudden access, min charge size: 128KB, =1 AZ
  * Glacier: 99.9% availability, long-term archiving, no-upfront cost, cost based on GB, min charge size: 40KB, >=3 AZs.
    * 3 access methods
    * Expedited: retrieve data within 1 - 5 mins
    * Standard: retrieve data within 3 - 5 hours
    * Bulk: retrieve data within 5 - 12 hours
  * GlacierDeep Archive: 99.9% availability, min charge size: 40KB, >=3 AZs. Retrieval in 12 hours
* Typical worklaod: 100 requests per second
* Introduce randomness into key naming to avoid partition congestion, so that obejcts are targetd at different partitions (parallel accesses)
* For PUT, use multipart upload to improve performance
* For GET, use range HTTP header to retrieve objects in multiple parts
* It is hard to sort or manipulate contents of LIST. Build and maintain a secondary index outside of S3 (DynamoDB or RDS) to store, index and query objects metadata rather than performing operations on S3

    

