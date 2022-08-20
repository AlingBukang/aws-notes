# Elastic Beanstalk
https://docs.aws.amazon.com/whitepapers/latest/introduction-devops-aws/aeb-deployment-strategies.html

- uses CloudFormation
- stores artefacts in S3
- can be used with Docker
- can't modify load balancer type once deployed
- an EB application can have several environments

# Environment Tiers
`Web Server` - ELB, SG, SG
- used for standard applications that listen for and then process HTTP requests

`Use Case:`
- run a website, web application, or web API that serves HTTP requests

`Worker Environment` - SQS, SG, ASG, No ELB; uses SQS #ofMessages to scale
- used for specialised applications that have a background processing task that listens for messages on an SQS queue and post those messages to the web application via HTTP

`Use Case:`
- run a worker application that processes long-running workloads on demand or performs tasks on a schedule

# Deployment Modes
- Single Instance - great for dev
- High availability with load balancer - great for prod

# Deployment Strategies
- All at once - deploy all in one go; fast but with downtime; no additional cost
- Rolling - update a few instances at a time(batch); one batch at a time; no additional cost but long deployment
- Rolling with additional batches - like rolling but spins up new instances to move the batch - the old app is still available; small additional cost and longer deployment; good for prod
- Immutable - spins new full instances on temporary ASG; zero downtime; high cost and double capacity; longest deployment; quick rollback in case of failures
- Blue/Green - not a direct feature of EB
	- create a new "stage" environment and deploy V2 there
	- swap CNAMEs of the two environments to redirect traffic to the new version

## Example scenario: Requires 4 running instances
- All at once - deploy 4 new instances and the existing 4 instances will be terminated; no running instance while new deployment is running
- Rolling - deploy 2 new instances while the other 2 instances are running then 2 again once the first deployment is successful; 2 running instances while new deployment in running
- Rolling with batches - deploy 2 additional instances while the other 4 instances are running then remove 2 once deploy successful; then repeat; 4 running instances while deployment is running; at a point, there will be 6 running instances while old instances are terminating
- Immutable - deploy 4 new instances and terminate old instances once deployment is successful; 4 running instances while deployment is running; at a point, there will be 8 running instances until the old instances are terminated


# EB Traffic Splitting:
- used for canary testing
- new application version is deployed to a temporary ASG with the same capacity
- deployment health is monitored
- no app downtime
- in case of deployment failure, it triggers and automated rollback
- new instances are migrated from the temporary to the original ASG; old app version is then terminated
- better that 'blue/green' deployment version


# Deployment process:
1. Describe dependencies - requirements.txt for Python; package.json for Node.js
2. Package app code as zip
3. Upload zip file
4. Deploy

# Lifecycle Policy:
- EB can store up to 1000 app versions
- Use a `lifecycle policy` to delete old app versions
	- based on time/age or storage space
- Versions that are currently running won't be deleted
- There's an option not to delete the source bundle in S3

# EB extensions
- used to customise app's config settings
- Requirements:
	- in the `.ebextensions/` directory in the root of source code
	- yaml or json format
	- can modify some default settings using: `option_settings`
	- ability to add resources such as RDS, Elasticache, DynamoDB, etc.
- Resources managed by `.ebextensions` are always deleted when the environment is deleted

# Migration steps:
- recreate environment, create snapshot of RDS, if any, then use swap Url or Route 53 to redirect traffic

# EB with Docker
- Dockerrun.aws.json - config file that contains ECS task definitions


# Secure EB
- Provision SSL certificate using ACM(certificate manager) or CLI
- Configure a security group rule to allow incoming port 443(https) requests
- Load SSL certificate on the load balancer
	- using Console in load balancer configuration, or
	- using code with .ebextensions/securelistener-alb.config
