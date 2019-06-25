## ELB
* Internet facing: has a public IP
* Internal LB: routes traffice within a VPC
* Application LB
  * operates at layer 7
  * has access to URI (location based routing)
  * Supprots WebSockets, SNI & IPV6
* Network LB
  * operates at layer 4
  * Preserve source IP
  * Reduced latency, handles mio requests per second  
* Network LB
  * operates at layer 4
  * Cross zone load balancing
* Idle connection timeout: inactivity between EC2 and client, in which LB terminates the conenction, default 60S
* Enable cross zone LB
* Connection draining: stops the LB to send traffic to faulty instances
* Proxy protocol: receive client IP and user agent (only on network and classic LB)

## VPC
* VPC is in one region only
* VPC and subnet IP range can't be altered after creation
* A new VPC has following resources:
  * subnets
  * Route tables
  * DHCP
  * Security Group
  * Network ACL
* Subnet can have 16(728 netmask) - 65536(/16 netmask) IPs
* 5 IPs are reserved by AWS
* 3 types of subnets: public, private and VPC only
* Public subnet needs a IGW
* VPC peering: not possible to create cross-region peering
