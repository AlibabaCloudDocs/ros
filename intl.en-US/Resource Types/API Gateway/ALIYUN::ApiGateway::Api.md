# ALIYUN::ApiGateway::Api

ALIYUN::ApiGateway::Api is used to create an API operation.

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
    "Tags": List,
    "ResultSample": String,
    "ResultType": String,
    "ApiName": String,
    "FailResultSample": String,
    "DisableInternet": Boolean,
    "ForceNonceCheck": Boolean,
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
|ServiceConfig|Map|Yes|Yes|The configuration items of API requests sent by API Gateway to the backend service.|For more information, see the [ServiceConfig properties](#section_0la_mr3_swj) section in this topic.|
|RequestConfig|Map|Yes|Yes|The configuration items of API requests sent by the consumer to API Gateway.|For more information, see the [RequestConfig properties](#section_tws_ib2_ui4) section in this topic.|
|Visibility|String|Yes|Yes|Specifies whether the API operation is public.

|Valid values: -   PUBLIC: The API operation is public.
-   PRIVATE: The API operation is not public. |
|ResultSample|String|Yes|Yes|The sample response from the backend service.|None|
|ResultType|String|Yes|Yes|The format of the response from the backend service.|Default value: JSON. Valid values: -   JSON
-   TEXT
-   BINARY
-   XML
-   PASSTHROUGH |
|ApiName|String|Yes|Yes|The name of the API operation.|The name must be 4 to 50 characters in length. The name must start with a letter and can contain letters, digits, and underscores \(\_\). **Note:** The name must be unique within an API group. |
|GroupId|String|Yes|No|The ID of the API group.|None|
|ErrorCodeSamples|List|No|Yes|The sample error codes returned by the backend service.|For more information, see the [ErrorCodeSamples properties](#section_htb_g01_ctj) section in this topic.|
|Description|String|No|Yes|The description of the API operation.|The description can be up to 180 characters in length.|
|DisableInternet|Boolean|No|Yes|Specifies whether to disable calls to the API operation over the Internet.|Valid values:-   true
-   false |
|ForceNonceCheck|Boolean|No|Yes|Specifies whether to forcibly check X-Ca-Nonce when the request is sent.|Valid values:-   true
-   false |
|Tags|List|No|Yes|The tags of the API operation.|A maximum of 20 tags can be specified. For more information, see the [Tags properties](#section_yf3_rbl_k6g) section in this topic. |
|SystemParameters|List|No|Yes|The system parameters of the API operation.|For more information, see the [SystemParameters properties](#section_jx9_98n_szh) section in this topic.|
|ServiceParameters|List|No|Yes|The parameters of API requests sent by API Gateway to the backend service.|For more information, see the [ServiceParameters properties](#section_5ox_ipa_s7s) section in this topic.|
|OpenIdConnectConfig|Map|No|Yes|The configuration items of the third-party OpenID Connect authentication method.|For more information, see the [OpenIdConnectConfig properties](#section_6qc_wi9_wp2) section in this topic.|
|AuthType|String|No|Yes|The security authentication method of the API operation.

|Valid values: -   APP: Only authorized applications can call the API operation.
-   ANONYMOUS: The API operation can be called anonymously. API Gateway does not authenticate callers and cannot set user-specific throttling policies. Before you add an API group that contains such API operations to Alibaba Cloud Marketplace, we recommend that you move the API operations to another API group, set their Visibility to PRIVATE, or set their AuthType to APP.
-   APPOPENID: The OpenID Connect authentication method is used. Only applications authorized by OpenID Connect can call the API operation. If this method is specified, the OpenIdConnectConfig parameter is required. |
|ServiceParametersMap|List|No|Yes|The mappings between parameters of requests sent by the consumer to API Gateway and parameters of requests sent by API Gateway to the backend service.|For more information, see the [ServiceParametersMap properties](#section_hf2_f94_yxq) section in this topic.|
|FailResultSample|String|No|Yes|The sample error response from the backend service.|None|
|RequestParameters|List|No|Yes|The parameters of API requests sent by the consumer to API Gateway.|For more information, see the [RequestParameters properties](#section_f24_n0m_w1o) section in this topic.|
|ConstParameters|List|No|Yes|The constant parameters of the specified API operation.|For more information, see the [ConstParameters properties](#section_m5p_znp_n4c) section in this topic.|
|AppCodeAuthType|String|No|Yes|The AppCode authentication method.|This parameter takes effect only when the AuthType parameter is set to APP. Default value: DEFAULT. Valid values: -   DEFAULT: AppCode authentication is configured along with the API group.
-   DISABLE: AppCode authentication is disabled.
-   HEADER: AppCode can be placed in the Header parameter for authentication.
-   HEADER\_QUERY: AppCode can be placed in the Header or Query parameter for authentication. |

## Tags syntax

```
"Tags": [
  {
    "Key": String,
    "Value": String
  }
]  
```

## Tags properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Key|String|Yes|No|The key of the tag.|The tag key must be 1 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|
|Value|String|No|No|The value of the tag.|The tag value must be 0 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|

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
|Message|String|Yes|Yes|The error message.|None|
|Code|String|Yes|Yes|The error code.|None|
|Description|String|No|Yes|The error description.|None|

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
|FunctionComputeConfig|Map|No|Yes|The configuration of Function Compute as the backend service.|None

For more information, see the [FunctionComputeConfig properties](#section_dap_hno_5q9) section in this topic.|
|MockStatusCode|Integer|No|Yes|The status code.|The status code returned in an HTTP/1.1 compatible format.|
|MockHeaders|List|No|Yes|The mock response headers defined when the mock mode is enabled.|None

For more information, see the [MockHeaders properties](#section_6hy_tfc_d55) section in this topic.|
|ServiceTimeOut|Integer|No|Yes|The timeout period of the backend service.|Unit: milliseconds.|
|ServiceAddress|String|No|Yes|The endpoint of the backend service.|If the complete backend service endpoint is `http://api.a.com:8080/object/add?key1=value1&key2=value2`, the value of ServiceAddress is `http://api.a.com:8080`.|
|ServicePath|String|No|Yes|The path of the backend service.|If the complete backend service endpoint is `http://api.a.com:8080/object/add?key1=value1&key2=value2`, the value of ServicePath is `/object/add`.|
|ServiceProtocol|String|No|Yes|The protocol of the backend service.|Valid values: -   HTTP
-   HTTPS
-   FunctionCompute |
|ServiceVpcEnable|String|No|Yes|Specifies whether to enable the VPC service.|Default: FALSE. Valid values: -   TRUE
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
|ContentTypeValue|String|No|Yes|The value of the ContentType header when the ServiceProtocol parameter is set to HTTP and the ContentTypeCatagory parameter is set to DEFAULT or CUSTOM.|None|
|Mock|String|No|Yes|Specifies whether to use the mock mode.|Default value: FALSE. Valid values: -   TRUE
-   FALSE |
|MockResult|String|No|Yes|The result returned when the mock mode is enabled.|None|
|VpcConfig|Map|No|Yes|The VPC configurations.|For more information, see the [VpcConfig properties](#section_2jq_h8s_euq) section in this topic.|

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
|InstanceId|String|Yes|Yes|The ID of the instance in the VPC.|Only ECS instances and SLB instances are supported.|
|VpcId|String|Yes|Yes|The ID of the VPC.|None|
|Port|Integer|Yes|Yes|The port number corresponding to the instance.|None|

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
|Location|String|Yes|Yes|The location of the parameter.|None|
|ParameterName|String|Yes|Yes|The name of the system parameter.|Valid values: -   CaClientIp
-   CaDomain
-   CaRequestHandleTime
-   CaAppId
-   CaRequestId
-   CaHttpSchema
-   CaProxy |
|ServiceParameterName|String|Yes|Yes|The name of the backend service parameter.|None|
|Description|String|No|Yes|The description of the parameter.|None|
|DemoValue|String|No|Yes|The sample value of the system parameter.|None|

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
|Location|String|Yes|Yes|The location of the parameter.|Valid values: -   BODY
-   HEAD
-   QUERY
-   PATH |
|ServiceParameterName|String|Yes|Yes|The name of the backend service parameter.|None|

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
|OpenIdApiType|String|Yes|Yes|The authorization type of an OpenID Connect API.|Valid values: -   IDTOKEN: specifies an authorization API, which is used to issue a token. If you set this parameter to IDTOKEN, the PublicKeyId and PublicKey parameters are required.
-   BUSINESS: specifies a business API, which is used to verify a token. If you set this parameter to BUSINESS, the IdTokenParamName parameter is required. |
|PublicKey|String|No|Yes|The public key used for token verification.|None|
|PublicKeyId|String|No|Yes|The ID of the public key.|None|
|IdTokenParamName|String|No|Yes|The name of the parameter that corresponds to the token.|None|

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
|RequestPath|String|Yes|Yes|The API request path.|If the complete API endpoint is `http://api.a.com:8080/object/add?key1=value1&key2=value2`, the API request path is `/object/add`.|
|RequestProtocol|String|Yes|Yes|The protocol type supported by the API operation.|Valid values: -   HTTP
-   HTTPS

Separate multiple protocol types with commas \(,\). Example: `HTTP,HTTPS`.|
|RequestHttpMethod|String|Yes|Yes|The API request method.|Default value: GET. Valid values: -   GET
-   POST
-   DELETE
-   PUT
-   HEADER
-   TRACE
-   PATCH
-   OPTIONS |
|PostBodyDescription|String|No|Yes|The description of the request body.|None|
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
|RequestParameterName|String|Yes|Yes|The name of the frontend request parameter.|It must be included in RequestParameters and must match ApiParameterName in RequestParameters data.|
|ServiceParameterName|String|Yes|Yes|The name of the backend service parameter.|None|

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
|Required|String|Yes|Yes|Specifies whether the request parameter is required.|Valid values: -   REQUIRED
-   OPTIONAL |
|ApiParameterName|String|Yes|Yes|The name of the request parameter.|None|
|Location|String|Yes|Yes|The location of the parameter.|Valid values: -   BODY
-   HEAD
-   QUERY
-   PATH |
|RegularExpression|String|No|Yes|The regular expression for parameter validation. This parameter takes effect only when the ParameterType parameter is set to String.|None|
|Description|String|No|Yes|The description of the parameter.|None|
|DefaultValue|String|No|Yes|The default value of the parameter.|None|
|MaxLength|Integer|No|Yes|The maximum length of the parameter. This parameter takes effect only when the ParameterType parameter is set to String.|None|
|MinLength|Integer|No|Yes|The minimum length of the parameter. This parameter takes effect only when the ParameterType parameter is set to String.|None|
|MaxValue|Integer|No|Yes|The maximum value of the parameter. This parameter takes effect only when the ParameterType parameter is set to Int, Long, Float, or Double.|None|
|MinValue|Integer|No|Yes|The minimum value of the parameter. This parameter takes effect only when the ParameterType parameter is set to Int, Long, Float, or Double.|None|
|EnumValue|String|No|Yes|The hash values that can be entered when the ParameterType parameter is set to Int, Long, Float, Double, or String.|Separate multiple values with commas \(,\), such as `1,2,3,4,9` and `A,B,C,E,F`.|
|JsonScheme|String|No|Yes|The JSON schema used for JSON validation. This parameter takes effect only when the ParameterType parameter is set to String.|None|
|DocOrder|Integer|No|Yes|The sequence of the parameter in the document.|None|
|DocShow|String|No|Yes|Specifies whether the parameter is public in the SDK or document generated by API Gateway.|Valid values: -   PUBLIC
-   PRIVATE |
|DemoValue|String|No|Yes|An example value of the parameter.|None|

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
|Location|String|Yes|Yes|The location of the parameter.|Default value: HEAD. Valid values: -   BODY
-   HEAD |
|ConstValue|String|Yes|Yes|The value of the parameter.|None|
|ServiceParameterName|String|Yes|Yes|The name of the backend service parameter.|None|
|Description|String|No|Yes|The description of the parameter.|None|

## FunctionComputeConfig syntax

```
"FunctionComputeConfig": {
  "FcRegionId": String,
  "RoleArn": String,
  "ServiceName": String,
  "FunctionName": String,
  "Qualifier": String,
  "ContentTypeValue": String,
  "ContentTypeCatagory": String,
  "FcBaseUrl": String,
  "FcType": String,
  "Method": String,
  "OnlyBusinessPath": Boolean,
  "Path": String
}
```

## FunctionComputeConfig properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|FcRegionId|String|No|Yes|The ID of the region where Function Compute is provided.|None|
|RoleArn|String|No|Yes|The Alibaba Cloud Resource Name \(ARN\) of the RAM role to be assumed by API Gateway to access Function Compute.|None|
|ServiceName|String|No|Yes|The service name defined in Function Compute.|None|
|FunctionName|String|No|Yes|The function name defined in Function Compute.|None|
|Qualifier|String|No|Yes|The alias of Function Compute.|None|
|ContentTypeCatagory|String|No|Yes|The ContentType header type used when you call the backend service over HTTP.|Default value: CLIENT. Valid values:-   DEFAULT: the default header type in API Gateway.
-   CUSTOM: a custom header type.
-   CLIENT: the ContentType header type of the client. |
|ContentTypeValue|String|No|Yes|The value of the ContentType header when the ServiceProtocol parameter is set to HTTP and the ContentTypeCatagory parameter is set to DEFAULT or CUSTOM.|None|
|FcBaseUrl|String|No|Yes|The URL of the trigger.|The URL starts with `http://` or `https://`.|
|FcType|String|No|Yes|The type of the function.|Default value: FCEvent. Valid values:-   FCEvent
-   HttpTrigger |
|Method|String|No|Yes|The request method.|Default value: GET. Valid values: -   GET
-   POST
-   DELETE
-   PUT
-   HEAD
-   PATCH
-   OPTIONS
-   ANY |
|OnlyBusinessPath|Boolean|No|Yes|Specifies whether to pass only the custom backend request path to the backend.|Valid values:-   true
-   false |
|Path|String|No|Yes|The backend request path.|Parameters must be enclosed in square brackets. Example:`/ getUserInfo / [userId]`.|

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
|HeaderName|String|Yes|Yes|The name of the response header.|None|
|HeaderValue|String|Yes|Yes|The value of the response header.|None|

## Response parameters

Fn::GetAtt

ApiId: The ID of the API operation.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "RequestConfig": {
      "Type": "Json",
      "Description": "The configuration of the request"
    },
    "Description": {
      "Type": "String",
      "Description": "Description of the API, less than 180 characters."
    },
    "ResultSample": {
      "Type": "String",
      "Description": "The sample of the result."
    },
    "DisableInternet": {
      "Type": "Boolean",
      "Description": "Set DisableInternet to true, only support intranet to call API. \nSet DisableInternet to false, then the call is not restricted. \n",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "ApiName": {
      "Type": "String",
      "Description": "The name of the API.Need [4, 50] Chinese\\English\\Number characters or \"_\",and should start with Chinese/English character."
    },
    "ForceNonceCheck": {
      "Type": "Boolean",
      "Description": "Set ForceNonceCheck to true, compulsorily check X-Ca-Nonce when requesting, \nthis is the unique identifier of the request, generally using UUID to identify. \nThe API gateway will verify the validity of this parameter after receiving this parameter. \nThe same value can only be used once within 15 minutes. It can effectively prevent API replay attacks.\nSet ForceNonceCheck to false, then no check. ",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "ResultType": {
      "Type": "String",
      "Description": "The format of service's response, \"JSON\", \"TEXT\", \"BINARY\", \"XML\", \"HTML\" or \"PASSTHROUGH\". Default is \"JSON\".",
      "AllowedValues": [
        "JSON",
        "TEXT",
        "BINARY",
        "XML",
        "HTML",
        "PASSTHROUGH"
      ],
      "Default": "JSON"
    },
    "FailResultSample": {
      "Type": "String",
      "Description": "The sample of the fail result."
    },
    "ErrorCodeSamples": {
      "Type": "Json",
      "Description": "The Error Code samples."
    },
    "GroupId": {
      "Type": "String",
      "Description": "The id of the Group."
    },
    "ServiceParametersMap": {
      "Type": "Json",
      "Description": "The mapping relation between (request parameters\\const parameters\\system parameters) and service parameters."
    },
    "RequestParameters": {
      "Type": "Json",
      "Description": "The request parameters.",
      "Default": []
    },
    "AppCodeAuthType": {
      "Type": "String",
      "Description": "When AuthType is APP authentication, the optional values are as follows: If not passed, the default value is DEFAULT:\nDEFAULT: Default (set by group).\nDISABLE: Not allowed\nHEADER: Allow AppCode header authentication\nHEADER_QUERY: Allow AppCode header and query authentication",
      "AllowedValues": [
        "DEFAULT",
        "DISABLE",
        "HEADER",
        "HEADER_QUERY"
      ]
    },
    "ServiceConfig": {
      "Type": "Json",
      "Description": "The configuration of the service."
    },
    "ConstParameters": {
      "Type": "Json",
      "Description": "The const parameters."
    },
    "SystemParameters": {
      "Type": "Json",
      "Description": "The system parameters."
    },
    "OpenIdConnectConfig": {
      "Type": "Json",
      "Description": "The configuration of the open id."
    },
    "Visibility": {
      "Type": "String",
      "Description": "Whether to make the API public. \"PUBLIC\" or \"PRIVATE\".",
      "AllowedValues": [
        "PUBLIC",
        "PRIVATE"
      ]
    },
    "ServiceParameters": {
      "Type": "Json",
      "Description": "The service parameters."
    },
    "AuthType": {
      "Type": "String",
      "Description": "Type of authorization of the API . \"APP\",\"ANONYMOUS\", or \"APPOPENID\"",
      "AllowedValues": [
        "APP",
        "ANONYMOUS",
        "APPOPENID"
      ]
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to instance. Max support 20 tags to add during create instance. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
    }
  },
  "Resources": {
    "API": {
      "Type": "ALIYUN::ApiGateway::Api",
      "Properties": {
        "RequestConfig": {
          "Ref": "RequestConfig"
        },
        "Description": {
          "Ref": "Description"
        },
        "ResultSample": {
          "Ref": "ResultSample"
        },
        "DisableInternet": {
          "Ref": "DisableInternet"
        },
        "ApiName": {
          "Ref": "ApiName"
        },
        "ForceNonceCheck": {
          "Ref": "ForceNonceCheck"
        },
        "ResultType": {
          "Ref": "ResultType"
        },
        "FailResultSample": {
          "Ref": "FailResultSample"
        },
        "ErrorCodeSamples": {
          "Ref": "ErrorCodeSamples"
        },
        "GroupId": {
          "Ref": "GroupId"
        },
        "ServiceParametersMap": {
          "Ref": "ServiceParametersMap"
        },
        "RequestParameters": {
          "Ref": "RequestParameters"
        },
        "AppCodeAuthType": {
          "Ref": "AppCodeAuthType"
        },
        "ServiceConfig": {
          "Ref": "ServiceConfig"
        },
        "ConstParameters": {
          "Ref": "ConstParameters"
        },
        "SystemParameters": {
          "Ref": "SystemParameters"
        },
        "OpenIdConnectConfig": {
          "Ref": "OpenIdConnectConfig"
        },
        "Visibility": {
          "Ref": "Visibility"
        },
        "ServiceParameters": {
          "Ref": "ServiceParameters"
        },
        "AuthType": {
          "Ref": "AuthType"
        },
        "Tags": {
          "Ref": "Tags"
        }
      }
    }
  },
  "Outputs": {
    "ApiId": {
      "Description": "The id of the API.",
      "Value": {
        "Fn::GetAtt": [
          "API",
          "ApiId"
        ]
      }
    }
  }
}
            
```

`YAML` format

```
ROSTemplateFormatVersion: '2015-09-01'
Parameters:
  ApiName:
    Description: The name of the API.Need [4, 50] Chinese\English\Number characters
      or "_",and should start with Chinese/English character.
    Type: String
  AppCodeAuthType:
    AllowedValues:
    - DEFAULT
    - DISABLE
    - HEADER
    - HEADER_QUERY
    Description: 'When AuthType is APP authentication, the optional values are as
      follows: If not passed, the default value is DEFAULT:

      DEFAULT: Default (set by group).

      DISABLE: Not allowed

      HEADER: Allow AppCode header authentication

      HEADER_QUERY: Allow AppCode header and query authentication'
    Type: String
  AuthType:
    AllowedValues:
    - APP
    - ANONYMOUS
    - APPOPENID
    Description: Type of authorization of the API . "APP","ANONYMOUS", or "APPOPENID"
    Type: String
  ConstParameters:
    Description: The const parameters.
    Type: Json
  Description:
    Description: Description of the API, less than 180 characters.
    Type: String
  DisableInternet:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Description: "Set DisableInternet to true, only support intranet to call API.\
      \ \nSet DisableInternet to false, then the call is not restricted. \n"
    Type: Boolean
  ErrorCodeSamples:
    Description: The Error Code samples.
    Type: Json
  FailResultSample:
    Description: The sample of the fail result.
    Type: String
  ForceNonceCheck:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Description: "Set ForceNonceCheck to true, compulsorily check X-Ca-Nonce when\
      \ requesting, \nthis is the unique identifier of the request, generally using\
      \ UUID to identify. \nThe API gateway will verify the validity of this parameter\
      \ after receiving this parameter. \nThe same value can only be used once within\
      \ 15 minutes. It can effectively prevent API replay attacks.\nSet ForceNonceCheck\
      \ to false, then no check. "
    Type: Boolean
  GroupId:
    Description: The id of the Group.
    Type: String
  OpenIdConnectConfig:
    Description: The configuration of the open id.
    Type: Json
  RequestConfig:
    Description: The configuration of the request
    Type: Json
  RequestParameters:
    Default: []
    Description: The request parameters.
    Type: Json
  ResultSample:
    Description: The sample of the result.
    Type: String
  ResultType:
    AllowedValues:
    - JSON
    - TEXT
    - BINARY
    - XML
    - HTML
    - PASSTHROUGH
    Default: JSON
    Description: The format of service's response, "JSON", "TEXT", "BINARY", "XML",
      "HTML" or "PASSTHROUGH". Default is "JSON".
    Type: String
  ServiceConfig:
    Description: The configuration of the service.
    Type: Json
  ServiceParameters:
    Description: The service parameters.
    Type: Json
  ServiceParametersMap:
    Description: The mapping relation between (request parameters\const parameters\system
      parameters) and service parameters.
    Type: Json
  SystemParameters:
    Description: The system parameters.
    Type: Json
  Tags:
    Description: Tags to attach to instance. Max support 20 tags to add during create
      instance. Each tag with two properties Key and Value, and Key is required.
    MaxLength: 20
    Type: Json
  Visibility:
    AllowedValues:
    - PUBLIC
    - PRIVATE
    Description: Whether to make the API public. "PUBLIC" or "PRIVATE".
    Type: String
Resources:
  API:
    Properties:
      ApiName:
        Ref: ApiName
      AppCodeAuthType:
        Ref: AppCodeAuthType
      AuthType:
        Ref: AuthType
      ConstParameters:
        Ref: ConstParameters
      Description:
        Ref: Description
      DisableInternet:
        Ref: DisableInternet
      ErrorCodeSamples:
        Ref: ErrorCodeSamples
      FailResultSample:
        Ref: FailResultSample
      ForceNonceCheck:
        Ref: ForceNonceCheck
      GroupId:
        Ref: GroupId
      OpenIdConnectConfig:
        Ref: OpenIdConnectConfig
      RequestConfig:
        Ref: RequestConfig
      RequestParameters:
        Ref: RequestParameters
      ResultSample:
        Ref: ResultSample
      ResultType:
        Ref: ResultType
      ServiceConfig:
        Ref: ServiceConfig
      ServiceParameters:
        Ref: ServiceParameters
      ServiceParametersMap:
        Ref: ServiceParametersMap
      SystemParameters:
        Ref: SystemParameters
      Tags:
        Ref: Tags
      Visibility:
        Ref: Visibility
    Type: ALIYUN::ApiGateway::Api
Outputs:
  ApiId:
    Description: The id of the API.
    Value:
      Fn::GetAtt:
      - API
      - ApiId
```

For more examples, visit [Api.json](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ApiGateway/JSON/Api.json) and [Api.yml](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ApiGateway/YAML/Api.yml). In the examples, the ALIYUN::ApiGateway::Api, ALIYUN::ApiGateway::App, ALIYUN::ApiGateway::Authorization, ALIYUN::ApiGateway::Deployment, ALIYUN::ApiGateway::Signature, ALIYUN::ApiGateway::SignatureBinding, ALIYUN::ApiGateway::TrafficControl, and ALIYUN::ApiGateway::TrafficControlBinding resources are involved.

