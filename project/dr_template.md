# Infrastructure

## AWS Zones
Identify your zones here
us-east-2
us-west-1

## Servers and Clusters

###  Table 1.1 Summary
| Asset      | Purpose           | Size                                                                   | Qty                                                             | DR                                                                                                           |
|------------|-------------------|------------------------------------------------------------------------|-----------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EC2 instance | Running Flask App | t3.medium  |  instances | Identify if this asset is deployed to DR, replicated, created in multiple locations or just stored elsewhere |
|  Kubernetes cluster | For monitoring stack | NA | 2 nodes | Identify if this asset is deployed to DR, replicated, created in multiple locations or just stored elsewhere |
| Load balancer | Load balancer for the website | NA  | 1 | Identify if this asset is deployed to DR, replicated, created in multiple locations or just stored elsewhere |
| S3 buckets | S3 buckets storage | NA | 2 | Identify if this asset is deployed to DR, replicated, created in multiple locations or just stored elsewhere |
| S3 key pairs | SSH keys for administering the EC2 instances | NA | 2| Identify if this asset is deployed to DR, replicated, created in multiple locations or just stored elsewhere |
|  Monitoring platform | Monitoring platform for the web application | NA | 1 | Identify if this asset is deployed to DR, replicated, created in multiple locations or just stored elsewhere |
| GitHub repo | GitHub repo for storing the Terraform code | NA | 1 | Identify if this asset is deployed to DR, replicated, created in multiple locations or just stored elsewhere |
| RDS cluster | Backend database | db.t2.small | 2 | Identify if this asset is deployed to DR, replicated, created in multiple locations or just stored elsewhere |

### Descriptions
More detailed descriptions of each asset identified above.

The EC2 instances run the Flask App. 2 SSH key pairs to ssh in the EC2 servers. GitHub repo for storing the Terraform code.
2 nodes kubernetes cluster for monitoring stack, Monitoring platform (Grafana and Prometheus) are running. 1 Load balancer for the website. 1 node RDS cluster for backend db. DB  backups stored in S3 buckets.

## DR Plan
### Pre-Steps:
List steps you would perform to setup the infrastructure in the other region. It doesn't have to be super detailed, but high-level should suffice.
First I would perform steps to make the application HA:
- Change from 2 db node to 3 nodes.
- Change from 2 K8s nodes cluster to 3 K8s nodes cluster.
Then make sure to run application in multiple regions, for this we use IAC in terraform
Use DNS for DB name
For DB's try to use automatic failover to avoid any downtime. 
Make sure entire infrastructure is set up in both regions. 

## Steps:
You won't actually perform these steps, but write out what you would do to "fail-over" your application and database cluster to the other region. Think about all the pieces that were setup and how you would use those in the other region
Create a cloud load balancer and point DNS to the load balancer. During a failover scenario, we will fail at the DNS entry and point to the DR site
Failover the database to the secondary region - us-west-1 (Either manual or automatic)