`CodeDeploy` is a deployment service that automates application deployments to `EC2 instances, on-premises instances, Lambda, and ECS services`.

Supports sourcecode bundle stored in S3, GitHub, and Bitbucket. It can also deploy a Lambda function.

Installation of `CodeDeploy agent` is required for EC2/on-premise platform but not for ECS and Lambda. It communicates outbound using HTTPS over port 443.


# Primary Components

## Application
- identifies the application version to deploy
- must have a unique name


## Application Specification
appspec.yml - deployment config file
- files - list of files to copy from source(S3/Github, etc) to destination(AWS filesystem)
	- source
	- destination
- hooks - set of instructions to follow for deployment; it can have timeouts
	Instructions in order:
	- ApplicationStop
	- DownloadBundle
	- BeforeInstall
	- Install
	- AfterInstall
	- ApplicationStart
	- ValidateService -> very important!


## Deployment Configuration
- set of conditions and deployment rules that applied during deployment
- deployment configurations vary on compute type being used

- `EC2/on-premise Configurations:`
	- `One at a time` - one ec2 at a time; if one instance fails then deployment stops
	- `Half at a time` - 50%
	- `All at once` - quick but no healthy host; downtime; great for dev

- `Lambda/ECS Configurations:`
    - `All at once` - quick but with downtime; great for dev
    - `Linear` - traffic is shifted in equal increments with equal time in between increments
    - `Canary` - traffic is shifted in two increments with set interval


- Handling Failures:
	- Failed EC2 instances will stay in 'failed' state
	- New deployments will first be deployed to failed instances
	- To rollback, redeploy old deployment or enable automated rollback for failures


## Deployment Group
- set of instances or Lambda functions to deploy the code version to
- can create multiple deployment groups within an application

- `Strategies:`
	- use tagged EC3 instances
	- use ASG
	- customise in script using `deploymeny_group_name` env variable


### Deployment Types
- `In-place`
	- stops, updates then restarts existing EC2 instances
    - can use ELB
	- new EC2 instances created by ASG will be deployed automatically
    - for EC2/On-Premises compute platform only
- `Blue/Green` - deployment behaviour depends on compute platform type
	- a new ASG will be created; settings are copied from old instances
	- define how long to keep the old EC2 instances (old ASG)
	- must use ELB
    - for EC2, Lambda, and ECS compute platform only; Not for on-premise servers

    - Blue/green on EC2: The instances in a deployment group (the original environment) are replaced by a different set of instances (the replacement environment).

    - Blue/green on Lambda: Traffic is shifted from current serverless environment to new environment with updated Lambda function versions. Lambda deployments are always blue/green so there's need to specify a deployment type.

    - Blue/green on ECS: Traffic is shifted from the existing task set to a replacement task set in the same service. The protocol and port of a specified load balancer listener are used to reroute production traffic. A test listener can be used to serve traffic to the replacement task set while validation tests are run.
