# aws_banhammer_soc
An event-driven automated security orchestration tool that detects unauthorized AWS API activity and blocks source IPs at the VPC Network ACL level.
PREREQUSITES: An AWS account, AWS CloudTrail enabled, a VPC with a public subnet

ARCHITECTURE -------------------------------------

Logging: AWS CloudTrail
Monitoring: AWS CloudTrail Log Groups + Subscription Filters
Compute: AWS Lambda - Python 3.14
Remediation: VPC Network ACLs 

FEATURES -------------------------------------

Point-of-Impact Blocking: Uses stateless NACL rules for immediate traffic dropping
Safety Switch: Integrated logic to prevent blocking of administrative IPs
IPv4 & IPv6 support

INSTALLATION -------------------------------------

Deploying the software -----------------
By default, CloudTrail only logs to S3 buckets. We need CloudTrail to stream to CloudWatch for real-time responses.

 Navigate to the CloudTrail Console > Trails.

 Select your trail and go to the CloudWatch Logs section.

 Click Edit > Enabled.

 Create a new Log Group as well as a new IAM Role for the trail to use.

 Save changes.

 Then, Lambda function is deployed under the new IAM Role. Paste the code from this repo into the lambda code editor and update the variables for your NACL ID and administrative IP address. Click deploy. 

 Grant IAM permissions to Lambda -----------------
 Lambda needs authority to modify netwokk settings, we grant that in this step. 

 In the Lambda console, click Configuration > Permissions > Role Name (you created this in a previous step) 

 In the IAM console, click Add permissions > Create an Inline Policy

 Select JSON and paste the code from the Lambda permissions document in this repo. 

 
 
