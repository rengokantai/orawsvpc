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
######NACL
It will examine across different subnets.(2b and 2c)  
web layer: inbound: http https ssh(from bastion) outbound:8080
app layer: inbound: 8080 SSH(from bastion) outboundL to RDS 3306
RDS: inbound:3306

