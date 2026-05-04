# aws_banhammer_soc
An event-driven automated security orchestration tool that detects unauthorized AWS API activity and blocks source IPs at the VPC Network ACL level.


Architecture -------------------------------------

Logging: AWS CloudTrail
Monitoring: AWS CloudTrail Log Groups + Subscription Filters
Compute: AWS Lambda - Python 3.14
Remediation: VPC Network ACLs 

Features -------------------------------------

Point-of-Impact Blocking: Uses stateless NACL rules for immediate traffic dropping
Safety Switch: Integrated logic to prevent blocking of administrative IPs
IPv4 & IPv6 support

Installation -------------------------------------

WIP
