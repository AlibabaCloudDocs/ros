# ALIYUN::ApiGateway::Api {#concept_61459_zh .concept}

ALIYUN::ApiGateway::Api is used to create an API.

## Syntax {#section_bnr_dxz_lfb .section}

```language-json
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
    "ServiceParametersMap": List,
    "FailResultSample": String,
    "ApiName": String,
    "GroupId": String,
    "RequestParameters": List,
    "ConstParameters": List
  }
}
```

## Properties { .section}

|Name|Type|Required|Editable|Description|
|----|----|--------|--------|-----------|
|ServiceConfig|Map|Yes|Yes|The configuration items of an API request sent by API Gateway to a back-end service.|
|RequestConfig|Map|Yes|Yes|The configuration items of an API request sent by a consumer to API Gateway.|
|Visibility|String|Yes|Yes| Indicates whether the API is public. Valid values:

 -   PUBLIC: The API is public. If you set this parameter to PUBLIC, the publishing stage of this API will be shown on the Discover APIs console page for all users.
-   PRIVATE: The API is not public. When the API group becomes available in the Alibaba Cloud Marketplace, private APIs are not shown.

 |
|ResultSample|String|Yes|Yes|The sample response from the back-end service.|
|ResultType|String|Yes|Yes|The format of the response from the back-end service. Valid values: JSON, TEXT, BINARY, XML, HTML, and PASSTHROUGH. Default value: JSON.|
|ApiName|String|Yes|Yes|The name of the API. The name must be unique in the group. It must be 4 to 50 characters in length and can contain letters, digits, and underscores \(\_\). It must start with a letter.|
|GroupId|String|Yes|No|The ID of the specified group.|
|ErrorCodeSamples|List|No|Yes|The samples of error codes returned by the back-end service.|
|Description|String|No|Yes|The description of the API. The description must be 1 to 180 characters in length.|
|SystemParameters|List|No|Yes|The system parameters of the API.|
|ServiceParameters|List|No|Yes|The parameters of the API request sent by API Gateway to the back-end service.|
|OpenIdConnectConfig|Map|No|Yes|The configuration items of the third-party authenticated OpenID Connect.|
|AuthType|String|No|Yes| The API security authorization method. Valid values:

 -   APP: Only authorized applications can call the API.
-   ANONYMOUS: The API can be called anonymously. In such a mode, you must pay attention to the following rules:

Anyone who can obtain the API service information will have the permissions to call this API. API Gateway does not authenticate callers and cannot set user-specific throttling policies. If you make this API public, set API-based throttling policies. We do not recommend making APIs with anonymous authentication available in the Alibaba Cloud Marketplace. API Gateway cannot bill callers separately or control the number of calls. Before you add a group containing such APIs to the Marketplace, we recommend that you move them to another group, set their Visibility to PRIVATE, or set their AuthType to APP.

-   APPOPENID: The OpenID Connect authentication method is used, allowing only authorized applications to call the API. If this method is selected, the OpenIdConnectConfig parameter is required.

 |
|ServiceParametersMap|List|No|Yes|The mappings between parameters of a request sent by a consumer to API Gateway and parameters of a request sent by API Gateway to a back-end service.|
|FailResultSample|String|No|Yes|The sample error response from the back-end service.|
|RequestParameters|List|No|Yes|The parameters of an API request sent by a consumer to API Gateway.|
|ConstParameters|List|No|Yes|The constant parameters of the specified API.|

## ErrorCodeSample syntax { .section}

```language-json
"ErrorCodeSample": {
  "Message": String,
  "Code": String,
  "Description": String
}
```

## ErrorCodeSample properties { .section}

|Name|Type|Required|Editable|Description|
|----|----|--------|--------|-----------|
|Message|String|Yes|Yes|The error message.|
|Code|String|Yes|Yes|The error code.|
|Description|String|No|Yes|The error description.|

## ServiceConfig syntax { .section}

```language-json
"ServiceConfig": {
  "ServiceTimeOut": Integer,
  "VpcConfig": Map,
  "MockResult": String,
  "ServicePath": String,
  "ServiceProtocol": String,
  "ServiceVpcEnable": String,
  "ServiceAddress": String,
  "ContentTypeValue": String,
  "ServiceHttpMethod": String,
  "ContentTypeCatagory": String,
  "AoneAppName": String,
  "Mock": String
}
```

## ServiceConfig properties { .section}

|Name|Type|Required|Editable|Description|
|----|----|--------|--------|-----------|
|ServiceTimeOut|Integer|Yes|Yes|The timeout period of a back-end service. Unit: millisecond.|
|ServiceAddress|String|Yes|Yes|The URL used to call the back-end service. If the complete back-end service URL is `http://api.a.com:8080/object/add?key1=value1&key2=value2`, ServiceAddress is `http://api.a.com:8080`.|
|ServicePath|String|Yes|Yes|The path used to call the back-end service. If the complete back-end service path is `http://api.a.com:8080/object/add?key1=value1&key2=value2`, ServicePath is `/object/add`.|
|ServiceProtocol|String|Yes|Yes|The protocol type of the back-end service. Valid value: HTTP. Default value: HTTP.|
|ServiceHttpMethod|String|Yes|Yes|The HTTP method used to call the back-end service. Valid values: GET, POST, DELETE, PUT, HEADER, TRACE, PATCH, CONNECT, and OPTIONS. Default value: GET.

 |
|ContentTypeCatagory|String|Yes|Yes| The ContentType header type used when you call the HTTP service of the back-end service. Valid values:

 -   DEFAULT: the default type in API Gateway.
-   CUSTOM: the custom type.
-   CLIENT: the ContentType header type on the client.

 Default value: CLIENT.

 |
|ContentTypeValue|String|No|Yes|The ContentType header value used when you call the HTTP service of the back-end service. This parameter is applicable only when the ContentTypeCatagory parameter is set to DEFAULT or CUSTOM.|
|Mock|String|Yes|Yes|Indicates whether Mock is enabled. Valid values: TRUE and FALSE. Default value: FALSE.|
|MockResult|String|No|Yes|The result returned when Mock is enabled.|
|ServiceVpcEnable|String|Yes|Yes|Indicates whether a VPC channel is enabled. Valid values: TRUE and FALSE. A VPC channel can be enabled only after a VPC authorization is added. Default value: FALSE.

 |
|VpcConfig|Map|No|Yes|The configuration items of a VPC channel if it is enabled.|

## VpcConfig syntax {#section_j34_bzz_lfb .section}

```language-json
"VpcConfig": {
  "InstanceId": String,
  "VpcId": String,
  "Port": Integer,
}
```

## VpcConfig properties { .section}

|Name|Type|Required|Editable|Description|
|----|----|--------|--------|-----------|
|InstanceId|String|Yes|Yes|The ID of an ECS or SLB instance in a VPC.|
|VpcId|String|Yes|Yes|The ID of the VPC.|
|Port|Integer|Yes|Yes|The port number corresponding to the instance.|

## SystemParameter syntax { .section}

```language-json
"SystemParameter": {
  "Location": String,
  "ParameterName": String,
  "Description": String,
  "DemoValue": String,
  "ServiceParameterName": String
}
```

## SystemParameter properties { .section}

|Name|Type|Required|Editable|Description|
|----|----|--------|--------|-----------|
|Location|String|Yes|Yes|The parameter location. Valid values: BODY and HEAD. Default value: HEAD.|
|ParameterName|String|Yes|Yes|The name of the system parameter. Valid values: CaClientIp, CaDomain, CaRequestHandleTime, CaAppId, CaRequestId, CaHttpSchema, and CaProxy.|
|ServiceParameterName|String|Yes|Yes|The name of the corresponding back-end service parameter.|
|Description|String|No|Yes|The parameter description.|
|DemoValue|String|No|Yes|The sample value.|

## ServiceParameter syntax { .section}

```language-json
"ServiceParameter": {
  "ParameterType": String,
  "Location": String,
  "ServiceParameterName": String,
}
```

## ServiceParameter properties { .section}

|Name|Type|Required|Editable|Description|
|----|----|--------|--------|-----------|
|ParameterType|String|Yes|Yes|The type of a back-end service parameter. Valid values: STRING, NUMBER, and BOOLEAN.|
|Location|String|Yes|Yes|The parameter location. Valid values: BODY, HEAD, QUERY, and PATH.|
|ServiceParameterName|String|Yes|Yes|The name of the back-end service parameter.|

## OpenIdConnectConfig syntax { .section}

```language-json
"OpenIdConnectConfig": {
  "OpenIdApiType": String,
  "PublicKey": String,
  "PublicKeyId": String,
  "IdTokenParamName": String,
}
```

## OpenIdConnectConfig properties { .section}

|Name|Type|Required|Editable|Description|
|----|----|--------|--------|-----------|
|OpenIdApiType|String|Yes|Yes| The type of an OpenID Connect API. Valid values:

 -   IDTOKEN: indicates an authorization API, which is used to issue a token. If you set this parameter to IDTOKEN, the PublicKeyId and PublicKey parameters are required.
-   BUSINESS: indicates a business API, which is used to verify a token. If you set this parameter to BUSINESS, the IdTokenParamName parameter is required.

 |
|PublicKey|String|No|Yes|The public key used for token verification.|
|PublicKeyId|String|No|Yes|The ID of a public key.|
|IdTokenParamName|String|No|Yes|The name of the parameter corresponding to a token.|

## RequestConfig syntax { .section}

```language-json
"RequestConfig": {
  "RequestMode": String,
  "RequestPath": String,
  "PostBodyDescription": String,
  "RequestProtocol": String,
  "RequestHttpMethod": String,
  "BodyFormat": String
}
```

## RequestConfig properties { .section}

|Name|Type|Required|Editable|Description|
|----|----|--------|--------|-----------|
|RequestMode|String|Yes|Yes|The request mode. Valid values: MAPPING and PASSTHROUGH. Default value: MAPPING.|
|RequestPath|String|Yes|Yes|The API request path. If the complete API URL is `http://api.a.com:8080/object/add?key1=value1&key2=value2`, the API request path is `/object/add`.|
|RequestProtocol|String|Yes|Yes|The API-supported protocol type. Multiple values must be separated by commas\(,\). For example, HTTP, HTTPS. Valid values: HTTP and HTTPS.|
|RequestHttpMethod|String|Yes|Yes|The HTTP method used to make the request. Valid values: GET, POST, DELETE, PUT, HEADER, TRACE, PATCH, CONNECT, and OPTIONS. Default value: GET.

 |
|PostBodyDescription|String|No|Yes|The body description.|
|BodyFormat|String|No|Yes|The method used to transmit data to the server when a POST, PUT, or PATCH request is sent. Valid values: FORM and STREAM. FORM indicates that data in key-value pairs is transmitted as forms. STREAM indicates that data is transmitted as byte streams. This parameter is applicable only when the RequestMode parameter is set to MAPPING.|

## ServiceParametersMap syntax { .section}

```language-json
"ServiceParametersMap": [
  "RequestParameterName": String,
  "ServiceParameterName": String
]
```

## ServiceParametersMap properties { .section}

|Name|Type|Required|Editable|Description|
|----|----|--------|--------|-----------|
|RequestParameterName|String|Yes|Yes|The name of a front-end request parameter. It must be included in RequestParameter and matches ApiParameterName in RequestParameter data.|
|ServiceParameterName|String|Yes|Yes|The name of a back-end service parameter.|

## RequestParameter syntax { .section}

```language-json
"RequestParameters": {
  "ParameterType": String,
  "RegularExpression": String,
  "Description": String,
  "MinLength": Integer,
  "DefaultValue": String,
  "Required": String,
  "MaxValue": Integer,
  "MinValue": Integer,
  "JsonScheme": String,
  "DocOrder": Integer,
  "ApiParameterName": String,
  "Location": String,
  "DocShow": String,
  "MaxLength": Integer,
  "EnumValue": String,
  "DemoValue": String
}
```

## RequestParameter properties { .section}

|Name|Type|Required|Editable|Description|
|----|----|--------|--------|-----------|
|ParameterType|String|Yes|No|The type of a request parameter. Valid values: String, Int, Long, Float, Double, and Boolean.|
|Required|String|Yes|Yes|Indicates whether the parameter is required. Valid values: REQUIRED and OPTIONAL.|
|ApiParameterName|String|Yes|Yes|The parameter name.|
|Location|String|Yes|Yes|The parameter location. Valid values: BODY, HEAD, QUERY, and PATH.|
|RegularExpression|String|No|Yes|The regular parameter validation expression. This parameter is applicable when the ParameterType parameter is set to String.|
|Description|String|No|Yes|The parameter description.|
|DefaultValue|String|No|Yes|The default value of the parameter.|
|MaxLength|Integer|No|Yes|The maximum parameter length. This parameter is applicable when the ParameterType parameter is set to String.|
|MinLength|Integer|No|Yes|The minimum parameter length. This parameter is applicable when the ParameterType parameter is set to String.|
|MaxValue|Integer|No|Yes|The maximum parameter value. This parameter is applicable when the ParameterType parameter is set to Int, Long, Float, or Double.|
|MinValue|Integer|No|Yes|The minimum parameter value. This parameter is applicable when the ParameterType parameter is set to Int, Long, Float, or Double.|
|EnumValue|String|No|Yes|The hash values that can be entered when the ParameterType parameter is set to Int, Long, Float, Double, or String. Different values must be separated by commas \(,\), such as 1,2,3,4,9 and A,B,C,E,F.|
|JsonScheme|String|No|Yes|The JSON schema used for JSON validation. This parameter is applicable when the ParameterType parameter is set to String.|
|DocOrder|Integer|No|Yes|The sequence in the document.|
|DocShow|String|No|Yes|Indicates whether the document is public. Valid values: PUBLIC and PRIVATE.|
|DemoValue|String|No|Yes|The sample value.|

## ConstParameter syntax { .section}

```language-json
"ConstParameter": {
  "Location": String,
  "ConstValue": String,
  "Description": String,
  "ServiceParameterName": String
}
```

## ConstParameter properties { .section}

|Name|Type|Required|Editable|Description|
|----|----|--------|--------|-----------|
|Location|String|Yes|Yes|The parameter location. Valid values: BODY and HEAD. Default value: HEAD|
|ConstValue|String|Yes|Yes|The parameter value.|
|ServiceParameterName|String|Yes|Yes|The name of a back-end service parameter.|
|Description|String|No|Yes|The parameter description.|

## Response parameters { .section}

**Fn::GetAtt**

APIId: the ID of the specified API.

## Examples {#section_zhq_syz_lfb .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "GroupId": {
      "Type": "String",
      "Default": "xxxxec10b1b4dc7a2e6ba8ca3xxxx",
      "Description": "The API group ID"
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
        "FailResultSample": "demo failed sample result",
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
            "DemoValue": "192.168.1.1",
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

