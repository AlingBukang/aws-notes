# AWS Serverless Application Model (SAM)

- It is an open-source framework for building serverless applications.
- It provides shorthand syntax to express functions, APIs, databases, and event source mappings.
- It uses YAML file format.
- SAM syntax transforms and expands into a compliant AWS CloudFormation template during deployment.

>Transform: AWS::Serverless-2016-10-31
Resources:
MyServerlessFunctionLogicalID:
Type: AWS::Serverless::Function
Properties:
Handler: index.handler
Runtime: nodejs8.10
CodeUri: 's3://testBucket/mySourceCode.zip'

AWS SAM uses AWS CloudFormation as the underlying deployment mechanism. You can deploy your application by using AWS SAM command line interface (CLI) commands. You can also use other AWS services that integrate with AWS SAM to automate your deployments.

After you develop and test your serverless application locally, you can deploy your application by using the sam package and sam deploy commands.

The sam package command zips your code artifacts, uploads them to Amazon S3, and produces a packaged AWS SAM template file that’s ready to be used. The sam deploy command uses this file to deploy your application.

To deploy an application that contains one or more nested applications, you must include the CAPABILITY_AUTO_EXPAND capability in the sam deploy command.

sam publish command publishes an AWS SAM application to the AWS Serverless Application Repository. It takes a packaged AWS SAM template and publishes the application to the specified region.


# Overview of Syntax

- `AWS::Serverless::Api`
    describes an API Gateway resource. It’s useful for advanced use cases where you want full control and flexibility when you configure your APIs.
- `AWS::Serverless::Application`
    embeds a serverless application from the AWS Serverless Application Repository or from an Amazon S3 bucket as a nested application. Nested applications are deployed as nested stacks, which can contain multiple other resources.
- `AWS::Serverless::Function`
    describes configuration information for creating a Lambda function. You can describe any event source that you want to attach to the Lambda function—such as Amazon S3, Amazon DynamoDB Streams, and Amazon Kinesis Data Streams.
- `AWS::Serverless::LayerVersion`
    creates a Lambda layer version that contains library or runtime code needed by a Lambda function. When a serverless layer version is transformed, AWS SAM also transforms the logical ID of the resource so that old layer versions are not automatically deleted by AWS CloudFormation when the resource is updated.
- `AWS::Serverless::SimpleTable`
    provides simple syntax for describing how to create DynamoDB tables.

# Commonly used SAM CLI commands

- `sam init` generates pre-configured AWS SAM templates.
- `sam local` supports local invocation and testing of your Lambda functions and SAM-based serverless applications by executing your function code locally in a Lambda-like execution environment.
- `sam package` and `sam deploy` bundle your application code and dependencies into a “deployment package” and then deploy to AWS Cloud.
- `sam logs` to fetch, tail, and filter logs for Lambda functions. 
- `sam publish` to publish deployed package.
- `sam validate` to validate SAM template.

GitHub repo:
https://github.com/aws/serverless-application-model

To install AWS Toolkit for Visual Studio Code:
https://docs.aws.amazon.com/toolkit-for-vscode/latest/userguide/connect.html
