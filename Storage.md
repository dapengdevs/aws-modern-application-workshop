# Storage

## EBS
* Cold HDD, application with few data access, max IOPS 250
* Throughput HDD, data warehousing, log processing, max IOPS 500
* General Purpose SSD, OS boot volume, database, max IOPS 10000
* Provisioned IOPS SSD, large database, NoSQL, max IOPS 20000

## S3
* object storage
* conssits of key, value, version ID, meta data and ACL
* Size: 0 - 5 TB
* S3 objects are replciated across multiple devices within a region
* To avoid accidental deletion, enable versioning and MFA
* Bucket name between 3 and 63 chars, can contain numbers, letters, hypen and period
* Bucket name must start and end with lower case ltter or a number 3 and 63 chars, can contain numbers, letters, hypen and period
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
* S3 event notifications
 * SNS topic
 * SQS queue
 * Lambda
* Can provide time-limited access
* Additional features
 * transfer acceleration: speed up upload using cloud front in reverse
 * requester pays, not owner
 * static web hosting
 
## Bucket
* flat container for objects
* Doesn't provide hierarchy
* 100 buckets per account
* No nested buckets
* Bucket name can't be changed
* URL: https://s3-eu-west-1.amazonaws.com/bucketname
* Can backup a bucket to another bucket in another account
* Objects in a bucket never leave the region unless you move them or enable cross-region replication
* sub resources
 * Lifecycle
 * Website
 * Versioning
 * ACL
 * Bucket policies
 * CORS
 * Logging
* Access to S3
 * IAM policies
 * Bucket policies
 * ACL
 * Query string authentication (URL to S3 with a limited validity)
* By default, all objects(and sub resources) are private. Only resource owner can access objects
* ARN for S3: arn:aws:s3:region:namespace:bucket_name/key_name
* A bucket owner can grant cross-account permissions to another AWS account to upload objects
 * Other AWS account that uploads the objects owns them
 * Bucket owner has no permissions on these objects
  * He pays the cost
  * Can deny access to any objects
  * Can archive objects
* ACL
 * can be assigned to owner, public access, a dedicated account(identified by email or canonical ID), log delivery group (for storing server logs)
 * Only recommended use case is to grant write access to S3 log delivery group
 * Limitations
  * Can't grant access to individual users
  * Can't grant conditional access
  * Can't explicitly deny access
* Bucket policy
 * Grant users permissions to a bucket
 * Managing object permissions
 * Granting object permissions to users within the account
* For an IAM user to access resources in another account the following must be provided:
 * Permission from the parent account through a user policy
 * Permission from the resource owner to the IAM user through a bucket policy, or the parent account through a bucket policy, bucket ACL or object ACL
 
## Costs
* No charge for data transfer between EC2 and S3 in the same region
* Data transfer into S3 is free
* Data transfer to other regions is charged
* Data retrieval from IA is charged
* Charge
 * per GB/month
 * Out of S3
 * Upload requests(PUT/GET)
 * Retrieval (IA & Glacier)

## Transfer acceleration
* leverages ClouFront's global edge locations
* as secure as direct upload
* must be enabled  on S3 bucket
* Can't be disabled, only suspended
* URL: bucketname.s3-accelerate.amazonaws.com

## Static websites
* Can use custom domain name using Route 53 alias record
* URL: bucketname.s3-website.amazonws.com
* Doesn't support HTTPS
* Only GET and HEAD requests

## Pre-signed URL

 
 
