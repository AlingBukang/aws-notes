The unit of scale for AWS Lambda is a concurrent execution. However, scaling indefinitely is not desirable in all scenarios. For example, you may want to control your concurrency for cost reasons or to regulate how long it takes you to process a batch of events, or to simply match it with a downstream resource. To assist with this, Lambda provides a concurrent execution limit control at both the account level and the function level.

The concurrent executions refers to the number of executions of your function code that are happening at any given time. You can estimate the concurrent execution count, but the concurrent execution count will differ depending on whether or not your Lambda function is processing events from a poll-based event source.

By default, an AWS account’s concurrent execution limit is 1000 which will be shared by all Lambda functions. 

If you create a Lambda function to process events from event sources that aren’t poll-based (for example, Lambda can process every event from other sources, like Amazon S3 or API Gateway), each published event is a unit of work, in parallel, up to your account limits. Therefore, the number of invocations these event sources make influences the concurrency.

If you set the concurrent execution limit for a function, the value is deducted from the unreserved concurrency pool. For example, if your account’s concurrent execution limit is 1000 and you have 10 functions, you can specify a limit on one function at 200 and another function at 100. The remaining 700 will be shared among the other 8 functions.

AWS Lambda will keep the unreserved concurrency pool at a minimum of 100 concurrent executions, so that functions that do not have specific limits set can still process requests. So, in practice, if your total account limit is 1000, you are limited to allocating 900 to individual functions.



----

Concurrent executions refers to the number of executions of your function code that are happening at any given time. You can estimate the concurrent execution count, but the it will differ depending on whether or not your Lambda function is processing events from a poll-based event source.

For Lambda functions that process Kinesis or DynamoDB streams, the number of shards is the unit of concurrency. If your stream has 100 active shards, there will be at most 100 Lambda function invocations running concurrently. This is because Lambda processes each shard’s events in sequence.


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