# aws_banhammer_soc
An event-driven automated security orchestration tool that detects unauthorized AWS API activity and blocks source IPs at the VPC Network ACL level.
PREREQUSITES: An AWS account, AWS CloudTrail enabled, a VPC with a public subnet

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

By default, CloudTrail only logs to S3 buckets. We need CloudTrail to stream to CloudWatch for real-time responses.

 Navigate to the CloudTrail Console > Trails.

 Select your trail and go to the CloudWatch Logs section.

 Click Edit > Enabled.

 Create a new Log Group as well as a new IAM Role for the trail to use.

 Save changes.

 From here, the lambda function is deployed under the new IAM Role. 
