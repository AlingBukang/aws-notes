You can integrate an API method in your API Gateway with a custom HTTP endpoint of your application in two ways:

 – HTTP proxy integration

 – HTTP custom integration

In your API Gateway console, you can define the type of HTTP integration of your resource by checking, or not checking, the “Configure as proxy resource” checkbox. 


With proxy integration, the setup is simple. You only need to set the HTTP method and the HTTP endpoint URI, according to the backend requirements, if you are not concerned with content encoding or caching.

With custom integration, setup is more involved. In addition to the proxy integration setup steps, you need to specify how the incoming request data is mapped to the integration request and how the resulting integration response data is mapped to the method response. API Gateway supports the following endpoint ports: 80, 443 and 1024-65535.

Programmatically, you choose an integration type by setting the type property on the Integration resource. For the Lambda proxy integration, the value is AWS_PROXY. For the Lambda custom integration and all other AWS integrations, it is AWS. For the HTTP proxy integration and HTTP integration, the value is HTTP_PROXY and HTTP, respectively. For the mock integration, the type value is MOCK.


-------

All of the APIs created with Amazon API Gateway expose HTTPS endpoints only. Amazon API Gateway does not support unencrypted (HTTP) endpoints. By default, Amazon API Gateway assigns an internal domain to the API that automatically uses the Amazon API Gateway certificate. When configuring your APIs to run under a custom domain name, you can provide your own certificate for the domain.



# Controlling access to APIs
- `Lambda authorizer`
    - a Lambda function that you provide to control access to your API. When your API is called, this Lambda function is invoked with a request context or an authorization token that are provided by the client application. The Lambda function returns a policy document that specifies the operations that the caller is authorized to perform.
    - used for authorizing non-AWS users that uses 3rd-party auth like SAML, OAuth.

    Two types of Lambda authorizers:
    - `Token based` type receives the caller’s identity in a bearer token, such as a JSON Web Token (JWT) or an OAuth token.
    - `Request parameter based` type receives the caller’s identity in a combination of headers, query string parameters, stageVariables, and $context variables.

- `Amazon Cognito user pool` 
    - user directories in Amazon Cognito. A client of your API must first sign a user in to the user pool and obtain an identity or access token for the user. Then your API is called with one of the returned tokens. The API call succeeds only if the required token is valid.
    - used for authorizing users with IAM account.
