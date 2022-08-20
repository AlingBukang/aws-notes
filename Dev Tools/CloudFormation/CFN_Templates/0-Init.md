Pre-req:
Verify that ImageID exists in the specific region you are deploying this to
Create key pair in EC2 -> Network & Scurity
Check for the instance type that you like to use

For env vars:
This involves manually creating environment variables for KeyName and ImageID via AWS Console/CLI     

For dynamic:
No need for key-pair, connect to EC2 instance via EC2 Instance Connect or SSM(session manager)
Remove AMIID parameter and reference an AWS SSM parameter which always references the latest Amazon Linux 2 AMI in a region.