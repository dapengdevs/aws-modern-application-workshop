# Lambda

## General

* Specify the amount of required memory
* AWS Lambda allocates CPU proportional to memory
* Lambda can access AWS and Non-AWS services (on EC2)
* Memory 128MB - 3008 MB with 64M increment
* Max execution timeout: 15 minutes, default 3 seonds
* Components
  * code and dependencies
  * event source
  * downstream resources such as S3 or DynamoDB
  * log streams
* Lambda stores code in S3 (encrypted)
* Lambda scales out(not up)
* To enable VPC support, specify one or more subnets in a VPC and SG as part of the configuration
* Lambda provides access only to one VPC
* Lambda doesn't have access to Internet by default. NAT must be configured

## Lambda@Edge
* Run code across AWS locations globally
* Upload Node.js code to Lambda and configure the trigger in response to a CloudFront request

## Limits
* temp disk space 512MB
* concurrency 1000

## Charges
* number of requests, first 1 mio free
* duration * memory
