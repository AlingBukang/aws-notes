

# Key Concepts:
- Segments
- Subsegments
- Trace - segments collected together to form an end-to-end trace
- Sampling - reduce the amount of requests sent to X-Ray; reduce cost
- Annotations - key-value pairs used to index traces and use with filters
- Metadata - key-value pairs; not indexed; can't be used for searching
- X-Ray daemon/agent - to send traces cros-account
    - Ensure proper IAM permissions set - agent will assume the role
    - Allows to have cental account for all your application tracing

# X-Ray Sampling Rules
- Can set custom sampling rules
- By default, X-Ray SDK records the first request each second, and 5% on subsequent requests
- One request per second is the reservoir - to ensure at least one trace is recorded each second the service is serving requests.
- 5% is the rate

# Explainer
A segment provides the name of the compute resources running your application logic, details about the request sent by your application, and details about the work done.

A segment can break down the data about the work done into subsegments. Subsegments provide more granular timing information and details about downstream calls that your application made to fulfill the original request. A subsegment can contain additional details about a call to an AWS service, an external HTTP API, or an SQL database. You can even define arbitrary subsegments to instrument specific functions or lines of code in your application.

For services that don’t send their own segments like Amazon DynamoDB, X-Ray uses subsegments to generate inferred segments and downstream nodes on the service map. This lets you see all of your downstream dependencies, even if they don’t support tracing, or are external.

Subsegments represent your application’s view of a downstream call as a client. If the downstream service is also instrumented, the segment that it sends replaces the inferred segment generated from the upstream client’s subsegment. The node on the service graph always uses information from the service’s segment, if it’s available, while the edge between the two nodes uses the upstream service’s subsegment.


Annotations are simple key-value pairs that are indexed for use with filter expressions. Use annotations to record data that you want to use to group traces in the console, or when calling the GetTraceSummaries API. X-Ray indexes up to 50 annotations per trace.

Metadata are key-value pairs with values of any type, including objects and lists, but that are not indexed. Use metadata to record data you want to store in the trace but don’t need to use for searching traces. You can view annotations and metadata in the segment or subsegment details in the X-Ray console.

A trace segment is a JSON representation of a request that your application serves. A trace segment records information about the original request, information about the work that your application does locally, and subsegments with information about downstream calls that your application makes to AWS resources, HTTP APIs, and SQL databases.


