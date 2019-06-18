
# SQS

## General
* Reliable, highly-scalbale, hosted queue
* Can be used with Redshift, DynamoDB, EC2, ECS, RDS, S3 and Lambda
* Pull based (polling), not push based
* Message size = 256KB
* Retention period: 1 min to 14 days, default 4 days
* Visibility timeout = amount of time a message is invisible in the queue after being picked up by a reader
* Max visibility timeout = 12 hours
* Message can contain up to 10 metadata attributes
* In-flight messages: messaages that have been picked upm but not deleted
* 120000 in-flight messages per standard queue
* 20000 in-flight messages per FIFO queue
* Queue name up to 80 chars
* You can have multiple queues with different prios
* Scaling is performed by creating more queues
* SQS stores all message queues and messages within a single, highly-available AWS region with multiple redundant AZs

## Polling
* Short Polling
  * Doesn't wait
  * Queries only a subset of servers
  * Default mode
  * ReceiveMessageWaitTime = 0
  * Higher cost, since requests can fetch no messages
* Long Polling
  * Uses fewer requests and reduces cost
  * Eliminates empty responses by querying all servers
  * SQS waits until a msg is available before sending resposne
  * ReceiveMessageWaitTime > 0 (up to 20 seconds)
  * Same charge as short polling

## Queues
* Names must be unique within a region
* Standard
  * massivly scalble
  * No exact order
  * At least once delivery
* FIFO
  * Exact order
  * Exactly once processing
  * Available in limited regions (15 regions in 2019)
  * High throughput: up to 300 msgs per second, with batch of 10, --> 3000 msgs
 
## Security
* Use IAM policies to control read/write
* SQS supports HTTPS and TLS1.0-TLS1.2
* SSE lets you transmit data in encrypted queues

## Monitoring
* CloudWatch metrics every 5 mintues
* CloudWatch considers a queue to be active for up to 6 hours if it contains any messages or if any API action accesses it
* CloudTrail captures APIs calls from SQS and logs to a S3 bucket

## Charges
* cost is calculated per request, plus data transfer charges for data transferred out of SQS

