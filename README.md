#### orawsvpc
#####2 The Basics Of VPC
######5 vpc,easyway2

cloudformation ->launch cloudformer
#####3 Going Deeper In The VPC - The Components Of A VPC
######4 vpc endpoint
choose privatereotetable.  
deny anyone without ssl.
principal:* aws service:amazons3 arn:* condition:Bool Key: asw:SecureTransport value:false  
Generate policy,copy,overrite original policy.

#####4 Security In The VPC
######1 security groups

from outer to inner:
vpc gateways,routes and subnets, networks access control, security group

######2 ddep dive
```
netstat -nt
```
######3 NACL
It will examine across different subnets.(2b and 2c)  
web layer: inbound: http https ssh(from bastion) outbound:8080  
app layer: inbound: 8080 SSH(from bastion) outboundL to RDS 3306  
RDS: inbound:3306  
######5
VPC->create flow log,filter->all(flow log role)
######6
cloudwatch->log->define metric filter
[version, accountid, interfaceid, srcaddr,dstaddr,srcport, dstport=22, protocol=6, packets,bytes,start,end,action=REJECT, logstatus]
#####5 Running Your EC2 Instances In The VPC
######1 Configuring Your EC2 Instance To Run In A VPC
PRIMARY elastic network interface (ENI)
- inherits the IP address of subnet
- Gets public IP addr at instance start, auto-assigned by subnet, or manually assigned  
- Can get elastic ip
- own mac address
- up to 5 sg
- multiple ip
- deleted by default on instance termination
- You can attach secondary ENI to instance, but second ENI must in diff 
subnet and same availability zone.(not deleted when attached to ec2 was deleted


secondary ENI use cases:  
- high avail NAT  
- secure subnet access  
- network security applicance  

hands on:  
create a eni, choose a bastion subnet, (private subnet, then attach bastion instance.


#####6 VPC Connectivity
######Creating Fault-Tolerant VPN Connections
server:VGW  ->VPN<- customer gateway  
In vpc->VPN connections->Virtual private gateways->create virtual private gateway->attach to vpc  
In vpc->VPN connections->Customer gateways->create customer gateway
######Connecting To Other VPCs Using VPC Peering
VPC peering:  
- Dont overlap IP Address ranges  
- Limit access viaroute tables in subnets
- Not transitive  

In VPC->Peering connection conection a to b  
in vpc b's route table, add a route from vpc a(10.1.0.0/16), target=pcx-xxxxxx,save.  
public route table, add same.
######Using Direct Connect
use case:
- High speed low latency requirements(Ad insertion, Realtime)
- High data volumes
- increased data security

#####7 Troubleshooting
######1 AWS services
no route found: check route table  
permission denied: check IAM role user group  
no message: check security group, check NACL
######2
Dedugging connection EC2 process:  
internet gateway->security allow access?->NACL allow access?->Is there a deny rule in the security group or NACL?  
Routing:Dynamic IP:? BGP ASN:62332  
VPN Connections-> connect   
Note:$0.05 per hour  
Download configuraion->Vendor:Generic,platform: G


