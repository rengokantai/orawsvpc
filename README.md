#### orawsvpc
#####2
######5 vpc,easyway2

cloudformation ->launch cloudformer
#####3
######4 vpc endpoint
choose privatereotetable.  
deny anyone without ssl.
principal:* aws service:amazons3 arn:* condition:Bool Key: asw:SecureTransport value:false  
Generate policy,copy,overrite original policy.

#####4
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
#####5 running EC2 in VPC
####1
secondary ENI use cases:  
high avail NAT  
secure subnet access  
network security applicance  

hands on:  
create a eni, choose a bastion subnet, (private subnet, then attach bastion instance.

#####6 troubleshooting
######1 AWS services
no route found: check route table  
permission denied: check IAM role user group  
no message: check security group, check NACL
######2
Dedugging connection EC2 process:  
internet gateway->security allow access?->NACL allow access?->Is there a deny rule in the security group or NACL?  



