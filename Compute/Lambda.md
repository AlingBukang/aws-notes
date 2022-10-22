The unit of scale for AWS Lambda is a concurrent execution. However, scaling indefinitely is not desirable in all scenarios. For example, you may want to control your concurrency for cost reasons or to regulate how long it takes you to process a batch of events, or to simply match it with a downstream resource. To assist with this, Lambda provides a concurrent execution limit control at both the account level and the function level.

The concurrent executions refers to the number of executions of your function code that are happening at any given time. You can estimate the concurrent execution count, but the concurrent execution count will differ depending on whether or not your Lambda function is processing events from a poll-based event source.

By default, an AWS account’s concurrent execution limit is 1000 which will be shared by all Lambda functions. 

If you create a Lambda function to process events from event sources that aren’t poll-based (for example, Lambda can process every event from other sources, like Amazon S3 or API Gateway), each published event is a unit of work, in parallel, up to your account limits. Therefore, the number of invocations these event sources make influences the concurrency.

If you set the concurrent execution limit for a function, the value is deducted from the unreserved concurrency pool. For example, if your account’s concurrent execution limit is 1000 and you have 10 functions, you can specify a limit on one function at 200 and another function at 100. The remaining 700 will be shared among the other 8 functions.

AWS Lambda will keep the unreserved concurrency pool at a minimum of 100 concurrent executions, so that functions that do not have specific limits set can still process requests. So, in practice, if your total account limit is 1000, you are limited to allocating 900 to individual functions.



----
# Lambda Limits
- Execution
    - memory allocation: 128MB - 10GB (1MB increments)
    - max execution time: 900 seconds(15 minutes)
    - environment variables: 4KB
    - temporary disk capacity(/tmp dir): 512MB
    - concurrent executions: 1000 (can be increased with AWS request)
- Deployment
    - deployment size(.zip compressed): 50MB
    - uncompressed deployment(code and dependencies): 250MB
    - can use /tmp dir to load other files at startup
    - environment variables: 4KB
    

# Lambda Execution Context
- it is a temporary runtime environment that initialises any external dependencies needed by the Lambda code, e.g. DB connections, HTTP/SDK clients etc.
- it is retained for sometime after invocation so succeeding invocation can re-use the context to execution time and save time and improve performance of Lambda
 - store temporary files in /tmp directory
 - store non-temporary files in S3


# Concurrent executions
Concurrent executions refers to the number of executions of your function code that are happening at any given time. 

## Concurrent execution count
- will differ whether Lambda function is processing events from a poll-based event source
- for Lambda functions that process Kinesis or DynamoDB streams, the number of shards is the unit of concurrency. If the stream has 100 active shards, there will be at most 100 Lambda function invocations running concurrently. This is because Lambda processes each shard’s events in sequence.


# Synchronous Invocation
- 
- User Invoked
    - Elastic Load Balancer (ALB)
    - API Gateway
    - CloudFront (Lambda@Edge)
    - S3 Batch
- Service Invoked
    - Cognito
    - Step Functions
- Other Services
    - Lex
    - Kinesis Data Firehose


# Assynchronous Invocation
- Services: S3, SNS, CloudWatch Events/EventBridge, CodeCommit, CodePipeline, etc.
- events are placed in an Event Queue
- Lambda attempts retry on errors
    - 3 tries total
    - 1 minute wait after qst try then 2 minutes wait
- can define a DLQ    


# Event Source Mapping
- has 2 source types: Stream and Lambda
- Kinesis Data Streams
- SQS, SQS FIFO
- DynamoDB Streams
- records need to be polled from the source
- Lambda function is invoked synchronously


# Lambda Tracing with X-Ray
- enable in Lmbda configuration(Active tracing)
- runs X-Ray daemon
- ensure lambda Function has correct IAM execution role
    - AWSXRAYDaemonWriteAccess - managed policy name
- environment variables set with X-Ray
    - _X_AMZN_TRACE_ID - contains the tracing header
    - AWS_XRAY_CONTEXT_MISSING - by default, LOG_ERROR
    - AWS_XRAY_DAEMON_ADDRESS - the X-Ray daemon IP address and port


# Lambda in VPC
- by default, Lambda function is launched outside VPC therefore it can't access resources inside VPC and private subnet
- to deploy Lambda inside VPC:
    - define the VPC ID, subnets and security groups
    - Lambda creates an ENI(elastic network interface) in the subnets
    - creates AWSLambdaVPCAccessExecutionRole
- a Lambda function inside a VPC will not have internet access
- Lambda deployed in public subnet will not have internet access or a public IP
- to have Lambda access internet:
    - deploy Lambda function in a private subnet and assign a NAT Gateway/Instance deployed in a public subnet
    - use VPC endpoints for Lambda to access private AWS services as an alternative to NAT
