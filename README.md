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

 Review the code and save as a relevant name you will remember. 


 Attach the CloudWatch trigger -----------------
 

 Go to CloudWatch > Log Groups

 Select the aws-cloudtrail-logs group.

 Click Actions > Subscription filters > Create Lambda subscription filter.

 Select the Lambda function that you created in a previous step. 

 For the log format, select JSON, and use this subscription filter pattern: { $.errorCode = "AccessDenied" }

 Name the filter something relevant and click start streaming. 


 TESTING AND ADVISORIES -------------------------------------


 To test, log onto AWS from a different network (one you don't mind being banned on such as a mobile hotspot) and attempt a forbidden action for your user, such as creating an S3 bucket. 
 Access should be denied, and if you check your NACL, you should see a ban rule for the IP address you used. 

 CAUTION: This tool is designed to be highly aggressive, so please ensure you have your correct IP address in the safety switch section of the banhammer code.
 


 
 
