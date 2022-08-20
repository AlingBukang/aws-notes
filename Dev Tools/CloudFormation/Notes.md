# Physical & Logical Resources


# UserData - Bootstrap via metadata
Bootstrapping - procedural; passes script; run only once


# Pseudo Parameters


# Intrinsic Functions
`Fn::Ref` or `!Ref` - function that can be leveraged to reference
    - Parameters - returns the value of the parameter
    - Resources - returns the physical ID of the underlying resource, e.g. EC2 ID

`Fn::GetAtt` - to get an attribute of a resource

`Fn::FindMap` - to access mapping values

`Fn::ImportValue` - to access 

`Fn::Join` - to join values with a delimeter

`Fn::Sub` or `!Sub` - to substitute values from a text

### Condition Functions

`Fn::And` 
`Fn::Equals`
`Fn::If`
`Fn::Not`
`Fn::Or`


# Mappings
- hardcoded values within the template


# Outputs
- output values that can be referenced by other stacks/cfn templates
- stack that generated the output cannot be delete if output being referenced by other stacks

# Stack Roles
- Allows an IAM role to be passed to the stack via PassRole
- A stack uses this role, rather than the identity interacting with the stack to create, update and delete AWS resources
- It allows role separation and is a powerful security feature

`Use Case:`
When a user needs access to create, update or delete CFN Stacks but should not have permissions to manipulate AWS resources. The user can pass in the role that has permissions to manipulate AWS resources but cannot assume it.


# Nested Stacks
- stacks that are part of other stacks
- to reuse components within a template
- nested stack is only hared to the higher level stack


# Cross-stack
- helpful when stacks have different lifecycles
- use Output Export and `Fn::ImportValue`
- use when you nedd to pass export values to other stacks


# Stack Sets
- use to create, update, or delete stacks across multiple accounts and regions with a single operation
- when stack set is updated, all associated stack instances are updated throughout all accounts and regions.


# Deletion Policy



# Conditions

## DependsOn

## Wait Conditions

## cfn-signal

## CloudFormationInit and cfn-init
`CloudFormationInit` - defines a desired state of an EC2 instance; idempotent

- Simple config management system using the UserData feature of EC2
- Configuration directives stored in template
- Part of the EC2 logical structure
- Run only once when instance in deployed; isn't rerun when updated

`cfn-init` - the helper script that will use the resource metadata specified in the `AWS::CloudFormation::Init` metadata key

## cfn-hup
- A helper tool that detects changes in resource metadata and subsequently runs user-specified actions
- This allows configuration updates on running EC2 instances via UpdateStack API
- Run in conjunction with CloudFormationInit to implement resource metadata updates via running the `cfn-init` script when update is detected

`Use Case:`
- There's a need to modify the UserData of an existing CFN stack


# ChangeSets
- Used to preview how proposed stack changes might affect running resources
- This is valuable when planning to modify an existing CFN stack as some changes might generate some interruptions and replacement of resources when modified
- Can have multiple versions of change sets
- It won't say if the update will be successful


# Custom Resources
- Enables writing custom provisioning logic in templates that CFN runs when creating, updating or deleting stacks

`Use Cases:`
- Populate S3 bucket with default files
- Empty S3 bucket before deletion
- Request custom resources from other AWS resources or 3rd-party services

# Rollbacks
- Stack creation fails:
    - Default: everything gets deleted(roll back)
    - Option: disable rollback and troubleshoot yourself

- Stack update fails:
    - stack rolls back to previous known working state