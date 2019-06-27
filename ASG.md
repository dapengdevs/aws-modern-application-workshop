# Auto Scaling Group

## General
* ASG = colelction of ECs instances
* Triggered by a scaling action (either launch or terminate)
* Region-specifc service
* Can span multiple AZs within the same region
* No additional cost for auto scaling
* Launch configuration can't bed edited after creation
* ASG can be edited after creation
* Can attach one or more ELB to an ASG
* ELB must be in the same region
* Scaling options:
  * Maintain: keep a specific or min number of instances
  * Manual: manually changed the capacity (change is rare)
  * Scheduled: in- or decrease based on schedule
  * Dynamic: scale based on real-time metrics
* Scaling pilicies:
  * Target track policy: add/remove instance to keep emtric close to target value, e.g. avg. CPU at 70%
  * Simple: Wait until health check and cool down eperiod expirs before reevaluating
  * Step: add/remove instance based on scaling adjustments(step adjustments)
* AS can perform rebalancing across AZs
* Health check
  * By default uses EC2 status check
  * Can also use ELB or custom health check
  * Activate ELB health check in addition to EC2 health check
  * Health check grace period = warmup period
* An isntance can be attached to one ASG only
* Instances will be determinated when ASG is deleted
* Can't mix spot and on-deamnd isntacnes
* Use SNS to send ASG actions (launch, termination)
* Cooldown period default 300s
* Monitoring: CloudWatch metrics every 5 mins
