# ALIYUN::ApiGateway::Api

ALIYUN::ApiGateway::Api is used to create an API.

## Syntax

```
{
  "Type": "ALIYUN::ApiGateway::Api",
  "Properties": {
    "ErrorCodeSamples": List,
    "Description": String,
    "ServiceConfig": Map,
    "SystemParameters": List,
    "ServiceParameters": List,
    "OpenIdConnectConfig": Map,
    "RequestConfig": Map,
    "AuthType": String,
    "Visibility": String,
    "ResultSample": String,
    "ResultType": String,
    "ApiName": String,
    "FailResultSample": String,
    "ConstParameters": List,
    "GroupId": String,
    "ServiceParametersMap": List,
    "RequestParameters": List,
    "AppCodeAuthType": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ServiceConfig|Map|Yes|Yes|The configuration items of API requests sent by API Gateway to the backend service.|None.|
|RequestConfig|Map|Yes|Yes|The configuration items of API requests sent by the consumer to API Gateway.|None.|
|Visibility|String|Yes|Yes|Specifies whether the API is public.

|Valid values: -   PUBLIC: The API is public.
-   PRIVATE: The API is not public. |
|ResultSample|String|Yes|Yes|The sample response from the backend service.|None.|
|ResultType|String|Yes|Yes|The format of the response from the backend service.|Default value: JSON. Valid values: -   JSON.
-   TEXT
-   BINARY
-   XML
-   PASSTHROUGH |
|ApiName|String|Yes|Yes|The name of the API.|-   The name must be 4 to 50 characters in length.
-   The name must start with a letter.
-   The name can contain letters, digits, and underscores \(\_\).

**Note:** The names must be unique within an API group. |
|GroupId|String|Yes|No|The ID of the API group.|None.|
|ErrorCodeSamples|List|No|Yes|The sample error codes returned by the backend service.|None.|
|Description|String|No|Yes|The description of the API.|The description can be up to 180 characters in length.|
|SystemParameters|List|No|Yes|The system parameters of the API.|None.|
|ServiceParameters|List|No|Yes|The parameters of API requests sent by API Gateway to the backend service.|None.|
|OpenIdConnectConfig|Map|No|Yes|The configuration items of the third-party OpenID Connect authentication method.|None.|
|AuthType|String|No|Yes|The security authentication method of the API.

|Valid values: -   APP: Only authorized applications can call the API operation.
-   ANONYMOUS: The API operation can be called anonymously. API Gateway does not authenticate callers and cannot set user-specific throttling policies. Before you add an API group that contains such APIs to Alibaba Cloud Marketplace, we recommend that you move the APIs to another API group, set their Visibility to PRIVATE, or set their AuthType to APP.
-   APPOPENID: The OpenID Connect authentication method is used. Only applications authorized by OpenID Connect can call the API operation. If this method is specified, the OpenIdConnectConfig parameter is required. |
|ServiceParametersMap|List|No|Yes|The mappings between parameters of requests sent by the consumer to API Gateway and parameters of requests sent by API Gateway to the backend service.|None.|
|FailResultSample|String|No|Yes|The sample error response from the backend service.|None.|
|RequestParameters|List|No|Yes|The parameters of API requests sent by the consumer to API Gateway.|None.|
|ConstParameters|List|No|Yes|The constant parameters of the specified API.|None.|
|AppCodeAuthType|String|No|Yes|The AppCode authentication method.|This parameter takes effect only when the AuthType parameter is set to APP. Default value: DEFAULT. Valid values: -   DEFAULT: AppCode authentication is configured along with the API group.
-   DISABLE: AppCode authentication is disabled.
-   HEADER: AppCode can be placed in the Header parameter for authentication.
-   HEADER\_QUERY: AppCode can be placed in the Header or Query parameter for authentication. |

## ErrorCodeSamples syntax

```
"ErrorCodeSamples": [
  {
    "Message": String,
    "Code": String,
    "Description": String
  }
]
```

## ErrorCodeSamples properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Message|String|Yes|Yes|The error message.|None.|
|Code|String|Yes|Yes|The error code.|None.|
|Description|String|No|Yes|The error description.|None.|

## ServiceConfig syntax

```
"ServiceConfig": {
  "ServiceTimeOut": Integer,
  "FunctionComputeConfig": Map,
  "VpcConfig": Map,
  "MockResult": String,
  "MockStatusCode": Integer,
  "ServiceHttpMethod": String,
  "ServiceProtocol": String,
  "ServiceVpcEnable": String,
  "ServiceAddress": String,
  "ContentTypeValue": String,
  "MockHeaders": List,
  "ContentTypeCatagory": String,
  "ServicePath": String,
  "Mock": String
}
```

## ServiceConfig properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|FunctionComputeConfig|Map|No|Yes|The configuration items of Function Compute as the backend service.

|None.|
|MockStatusCode|Integer|No|Yes|The status code.|The status code returned in an HTTP/1.1 compatible format.|
|MockHeaders|List|No|Yes|The mock response headers defined when the mock mode is enabled.

|None.|
|ServiceTimeOut|Integer|No|Yes|The timeout period of the backend service.|Unit: milliseconds.|
|ServiceAddress|String|No|Yes|The URL used to call the backend service.|If the complete backend service URL is `http://api.a.com:8080/object/add?key1=value1&key2=value2`, the value of ServiceAddress is `http://api.a.com:8080`.|
|ServicePath|String|No|Yes|The path used to call the backend service.|If the complete backend service URL is `http://api.a.com:8080/object/add?key1=value1&key2=value2`, the value of ServicePath is `/object/add`.|
|ServiceProtocol|String|No|Yes|The protocol of the backend service.|Valid values: -   HTTP
-   HTTPS
-   FunctionCompute |
|ServiceVpcEnable|String|No|Yes|Specifies whether to enable a VPC.|Default value: FALSE. Valid values: -   TRUE
-   FALSE |
|ServiceHttpMethod|String|No|Yes|The HTTP method used to call the backend service.|Default value: GET. Valid values: -   GET
-   POST
-   DELETE
-   PUT
-   HEAD
-   TRACE
-   PATCH
-   CONNECT
-   OPTIONS
-   ANY |
|ContentTypeCatagory|String|No|Yes|The ContentType header type used when you call the backend service over HTTP.

|Default value: CLIENT. Valid values: -   DEFAULT: the default header type in API Gateway.
-   CUSTOM: a custom header type.
-   CLIENT: the ContentType header type of the client. |
|ContentTypeValue|String|No|Yes|This parameter takes effect only when the ContentTypeCatagory parameter is set to DEFAULT or CUSTOM.|None.|
|Mock|String|No|Yes|Specifies whether to use the mock mode.|Default value: FALSE. Valid values: -   TRUE
-   FALSE |
|MockResult|String|No|Yes|The result returned when the mock mode is enabled.|None.|
|VpcConfig|Map|No|Yes|The VPC configurations.|None.|

## VpcConfig syntax

```
"VpcConfig": {
  "InstanceId": String,
  "VpcId": String,
  "Port": Integer
}
```

## VpcConfig properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|InstanceId|String|Yes|Yes|The ID of the instance in the VPC.|Only ECS or SLB instances are supported.|
|VpcId|String|Yes|Yes|The ID of the VPC.|None.|
|Port|Integer|Yes|Yes|The port number that corresponds to the instance.|None.|

## SystemParameters syntax

```
"SystemParameters": [
  {
    "DemoValue": String,
    "ParameterName": String,
    "ServiceParameterName": String,
    "Location": String,
    "Description": String
  }
]
```

## SystemParameters properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Location|String|Yes|Yes|The location of the system parameter.|None.|
|ParameterName|String|Yes|Yes|The name of the system parameter.|Valid values: -   CaClientIp
-   CaDomain
-   CaRequestHandleTime
-   CaAppId
-   CaRequestId
-   CaHttpSchema
-   CaProxy |
|ServiceParameterName|String|Yes|Yes|The name of the backend service parameter.|None.|
|Description|String|No|Yes|The description of the system parameter.|None.|
|DemoValue|String|No|Yes|Examples|None.|

## ServiceParameters syntax

```
"ServiceParameters": [
  {
    "ParameterType": String,
    "Location": String,
    "ServiceParameterName": String
  }
]
```

## ServiceParameters properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ParameterType|String|Yes|Yes|The data type of the backend service parameter.|Valid values: -   STRING
-   NUMBER
-   BOOLEAN |
|Location|String|Yes|Yes|The location of the backend service parameter.|Valid values: -   BODY
-   HEAD
-   QUERY
-   PATH |
|ServiceParameterName|String|Yes|Yes|The name of the backend service parameter.|None.|

## OpenIdConnectConfig syntax

```
"OpenIdConnectConfig": {
  "OpenIdApiType": String,
  "PublicKey": String,
  "PublicKeyId": String,
  "IdTokenParamName": String
}
```

## OpenIdConnectConfig properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|OpenIdApiType|String|Yes|Yes|The authorization type of an OpenID Connect API.

|Valid values: -   IDTOKEN: specifies an authorization API, which is used to issue a token. If you set this parameter to IDTOKEN, the PublicKeyId and PublicKey parameters are required.
-   BUSINESS: specifies a business API, which is used to verify a token. If you set this parameter to BUSINESS, the IdTokenParamName parameter is required. |
|PublicKey|String|No|Yes|The public key used for token verification.|None.|
|PublicKeyId|String|No|Yes|The ID of the public key.|None.|
|IdTokenParamName|String|No|Yes|The name of the parameter that corresponds to the token.|None.|

## RequestConfig syntax

```
"RequestConfig": {
  "RequestMode": String,
  "RequestPath": String,
  "PostBodyDescription": String,
  "RequestProtocol": String,
  "RequestHttpMethod": String,
  "BodyFormat": String
}
```

## RequestConfig properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|RequestMode|String|Yes|Yes|The request mode.|Default value: MAPPING. Valid values: -   MAPPING: request parameter mapping
-   PASSTHROUGH: request parameter passthrough |
|RequestPath|String|Yes|Yes|The API request path.|If the complete API URL is `http://api.a.com:8080/object/add?key1=value1&key2=value2`, the API request path is `/object/add`.|
|RequestProtocol|String|Yes|Yes|The API-supported protocol type.|Valid values: -   HTTP
-   HTTPS

Separate multiple protocol types with commas \(,\). Example: `HTTP,HTTPS`.|
|RequestHttpMethod|String|Yes|Yes|The HTTP method used to make the request.|Default value: GET. Valid values: -   GET
-   POST
-   DELETE
-   PUT
-   HEADER
-   TRACE
-   PATCH
-   OPTIONS |
|PostBodyDescription|String|No|Yes|The description of the request body.|None.|
|BodyFormat|String|No|Yes|The method used to transmit data to the server when a POST, PUT, or PATCH request is sent.|Valid values: -   FORM
-   STREAM

This parameter takes effect only when the RequestMode parameter is set to MAPPING.|

## ServiceParametersMap syntax

```
"ServiceParametersMap": [
  {
    "RequestParameterName": String,
    "ServiceParameterName": String
  }
]
```

## ServiceParametersMap properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|RequestParameterName|String|Yes|Yes|The name of the frontend request parameter.|It must be included in RequestParameters and must match ApiParameterName in RequestParameter data.|
|ServiceParameterName|String|Yes|Yes|The name of the backend service parameter.|None.|

## RequestParameters syntax

```
"RequestParameters": [
  {
    "ParameterType": String,
    "Required": String,
    "Description": String,
    "DemoValue": String,
    "MinLength": Integer,
    "DefaultValue": String,
    "RegularExpression": String,
    "MaxValue": Integer,
    "MinValue": Integer,
    "JsonScheme": String,
    "ApiParameterName": String,
    "Location": String,
    "DocShow": String,
    "MaxLength": Integer,
    "EnumValue": String,
    "DocOrder": Integer
  }
]
```

## RequestParameters properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ParameterType|String|Yes|No|The type of the request parameter.|Valid values: -   String
-   Int
-   Long
-   Float
-   Double
-   Boolean |
|Required|String|Yes|Yes|Required|Valid values: -   REQUIRED
-   OPTIONAL |
|ApiParameterName|String|Yes|Yes|Parameter|None.|
|Location|String|Yes|Yes|The location of the request parameter.|Valid values: -   BODY
-   HEAD
-   QUERY
-   PATH |
|RegularExpression|String|No|Yes|The regular expression for parameter validation. This parameter takes effect only when the ParameterType parameter is set to String.|None.|
|Description|String|No|Yes|The description of the request parameter.|None.|
|DefaultValue|String|No|Yes|The default value of the parameter.|None.|
|MaxLength|Integer|No|Yes|The maximum length of the parameter. This parameter takes effect only when the ParameterType parameter is set to String.|None.|
|MinLength|Integer|No|Yes|The minimum length of the parameter. This parameter takes effect only when the ParameterType parameter is set to String.|None.|
|MaxValue|Integer|No|Yes|The maximum value of the parameter. This parameter takes effect only when the ParameterType parameter is set to Int, Long, Float, or Double.|None.|
|MinValue|Integer|No|Yes|The minimum value of the parameter. This parameter takes effect only when the ParameterType parameter is set to Int, Long, Float, or Double.|None.|
|EnumValue|String|No|Yes|The hash values that can be entered when the ParameterType parameter is set to Int, Long, Float, Double, or String.|Separate multiple values with commas \(,\), such as 1,2,3,4,9 and A,B,C,E,F.|
|JsonScheme|String|No|Yes|The JSON schema used for JSON validation. This parameter takes effect only when the ParameterType parameter is set to String.|None.|
|DocOrder|Integer|No|Yes|The sequence of the parameter in the document.|None.|
|DocShow|String|No|Yes|Specifies whether the parameter is public in the SDK or document generated by API Gateway.|Valid values: -   PUBLIC
-   PRIVATE |
|DemoValue|String|No|Yes|Examples|None.|

## ConstParameters syntax

```
"ConstParameters": [
  {
    "ConstValue": String,
    "ServiceParameterName": String,
    "Description": String,
    "Location": String
  }
]
```

## ConstParameters properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Location|String|Yes|Yes|The location of the constant parameter.|Default value: HEAD. Valid values: -   BODY
-   HEAD |
|ConstValue|String|Yes|Yes|The value of the constant parameter.|None.|
|ServiceParameterName|String|Yes|Yes|The name of the backend service parameter.|None.|
|Description|String|No|Yes|The description of the constant parameter.|None.|

## FunctionComputeConfig syntax

```
"FunctionComputeConfig": {
  "fcRegionId": String,
  "roleArn": String,
  "serviceName": String,
  "functionName": String
  "qualifier": String
}
```

## FunctionComputeConfig properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|fcRegionId|String|Yes|Yes|The region where Function Compute is deployed.|None.|
|roleArn|String|Yes|Yes|The Alibaba Cloud Resource Name \(ARN\) of the RAM role to be assumed by API Gateway to access Function Compute.|None.|
|serviceName|String|Yes|Yes|The service name defined in Function Compute.|None.|
|functionName|String|Yes|Yes|The function name defined in Function Compute.|None.|
|qualifier|String|No|Yes|The alias of Function Compute.|None.|

## MockHeaders syntax

```
"MockHeaders": [
  {
    "HeaderValue": String,
    "HeaderName": String
  }
]    
```

## MockHeaders properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|HeaderName|String|Yes|Yes|The name of the response header.|None.|
|HeaderValue|String|Yes|Yes|The value of the response header.|None.|

## Response parameters

Fn::GetAtt

ApiId: the ID of the specified API.

## Examples

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "GroupId": {
      "Type": "String",
      "Default": "xxxxec10b1b4dc7a2e6ba8ca3xxxx",
      "Description": "API group ID"
    }
  },
  "Resources": {
    "API": {
      "Type": "ALIYUN::ApiGateway::Api",
      "Properties": {
        "GroupId": {
          "Ref": "GroupId"
        },
        "ApiName": "API_test",
        "Visibility": "PRIVATE",
        "Description": "keep for test",
        "AuthType": "APP",
        "RequestConfig": {
          "RequestHttpMethod": "GET",
          "RequestProtocol": "HTTP",
          "BodyFormat": "FORM",
          "PostBodyDescription": "k:v",
          "RequestPath": "/demo_test_345"
        },
        "ServiceConfig": {
          "ServiceProtocol": "HTTP",
          "ContentTypeValue": "application/x-www-form-urlencoded; charset=UTF-8",
          "Mock": "FALSE",
          "MockResult": "Nothing",
          "ServiceTimeOut": 20000,
          "ServiceAddress": "https://mytest.cn",
          "ServicePath": "/data",
          "ServiceHttpMethod": "GET",
          "ContentTypeCatagory": "DEFAULT",
          "ServiceVpcEnable": "FALSE"
        },
        "RequestParameters": [
          {
            "Required": "OPTION",
            "ParameterType": "String",
            "ApiParameterName": "x-demo",
            "DocShow": "PUBLIC",
            "DefaultValue": "x-demo-val",
            "Location": "HEAD",
            "DocOrder": 0
          },
          {
            "Required": "OPTION",
            "ParameterType": "String",
            "ApiParameterName": "y-demo",
            "DocShow": "PUBLIC",
            "DefaultValue": "y-demo-val",
            "Location": "QUERY",
            "DocOrder": 1
          }
        ],
        "ServiceParameters": [
          {
            "ServiceParameterName": "x-demo-ser",
            "ParameterType": "STRING",
            "Location": "HEAD"
          },
          {
            "ServiceParameterName": "y-demo-ser",
            "ParameterType": "STRING",
            "Location": "QUERY"
          }
        ],
        "ServiceParametersMap": [
          {
            "ServiceParameterName": "x-demo-ser",
            "RequestParameterName": "x-demo"
          },
          {
            "ServiceParameterName": "y-demo-ser",
            "RequestParameterName": "y-demo"
          }
        ],
        "ResultType": "JSON",
        "ResultSample": "demo sample result",
        "FailResultSample": "demo faile sample result",
        "ErrorCodeSamples": [
          {
            "Description": "??",
            "Message": "Missing",
            "Code": "400"
          },
          {
            "Description": "???",
            "Message": "Missing",
            "Code": "401"
          }
        ],
        "SystemParameters": [
          {
            "Description": "ClientIP",
            "ServiceParameterName": "demo-sys-ser",
            "DemoValue": "192.168.XX.XX",
            "Location": "HEAD",
            "ParameterName": "CaClientIp"
          }
        ],
        "ConstParameters": [
          {
            "Description": "demo_const",
            "ServiceParameterName": "demo-const-ser",
            "Location": "HEAD",
            "ConstValue": "demo_const_val"
          }
        ]
      }
    }
  }
}
```

