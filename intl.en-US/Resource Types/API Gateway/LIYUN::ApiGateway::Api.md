# LIYUN::ApiGateway::Api {#concept_61459_zh .concept}

The ALIYUN::ApiGateway::Api can be used to create an API.

## Syntax {#section_bnr_dxz_lfb .section}

```language-json
{
    "Type" : "ALIYUN::ApiGateway::Api",
    "Properties" : {
         "ErrorCodeSamples" : List,
         "Description" : String,
         "ServiceConfig" : Map,
         "SystemParameters" : List,
         "ServiceParameters" : List,
         "OpenIdConnectConfig" : Map,
         "RequestConfig" : Map,
         "AuthType" : String,
         "Visibility" : String,
         "ResultSample" : String,
         "ResultType" : String,
         "ServiceParametersMap" : List,
         "FailResultSample" : String,
         "ApiName" : String,
         "GroupId" : String,
         "RequestParameters" : List,
         "ConstParameters" : List
    }
}

```

## Properties { .section}

|Name|Type|Required|Update allowed|Description|
|ServiceConfig|map|Yes|Yes|Configuration items of the API request sent by the gateway to the backend service|
|RequestConfig|map|Yes|Yes|Configuration items of the API request sent by the consumer to the gateway|
|Visibility|string|Yes|Yes| Whether the API is public. The optional values are as follows:

 -   PUBLIC: The API is public. If this attribute is set to PUBLIC, the definition of this API’s online environment will be visible on the “Discover APIs” page on the console to all users
-   PRIVATE: The API is not public. If the attribute is set to PRIVATE, APIs of the private type are unavailable when the API group is available on the cloud marketplace

 |
|ResultSample|string|Yes|Yes|Sample of the reply returned by the backend service|
|ResultType|string|Yes|Yes|Format of the reply returned by the backend service. Currently, allowed formats are JSON, TEXT, BINARY, XML, HTML, and PASSTHROUGH. The default value is JSON|
|ApiName|string|Yes|Yes|API name. The name must be unique in the group. It must be a string of 4 to 50 characters, which can contain Chinese characters, English letters, digits, and underscores \(\_\), but starts only with an English letter or a Chinese character|
|GroupId|string|Yes|No|ID of the specified group|
|ErrorCodeSamples|list|No|Yes|Sample of the error code returned by the backend service|
|Description|string|No|Yes|API description, up to 180 characters|
|SystemParameters|list|No|Yes|System parameters of the API|
|ServiceParameters|list|No|Yes|Description on parameters of the API request sent by the gateway to a backend service|
|OpenIdConnectConfig|map|No|Yes|Configuration items of the third-party authenticated OpenID Connect|
|AuthType|string|No|Yes| API security authorization type. The optional values are as follows:

 -   APP: Only authorized APPs can call the API
-   ANONYMOUS: The API can be called anonymously. In such mode, you must note the following:

Anyone who can obtain this API service information can call this API. The gateway does not authenticate the identity of callers and cannot set traffic limits for individual users. If you activate this API, set API-based throttling. We recommend that anonymous APIs not to be made available on the cloud marketplace. The gateway can neither gets the callers traffic separately nor does it control the number of calls. If the group including this API is to be added to the Cloud Marketplace, we recommend that you move this API to another group, set its type to PRIVATE, or select the APP certification method

-   APPOPENID: Supports third-party authenticated OpenID Connect. Only authorized APPs can call the API. If the attribute is set to APPOPENID, the OpenIdConnectConfig parameter is required

 |
|ServiceParametersMap|list|No|Yes|Mappings between parameters of a request sent by a consumer to the gateway and parameters of a request sent by the gateway to a backend service|
|FailResultSample|string|No|Yes|Sample of the reply failure returned by the backend service|
|RequestParameters|list|No|Yes|Parameter description of the API request sent by the consumer to the gateway|
|ConstParameters|list|No|Yes|Constant parameter of the specified API|

## ErrorCodeSample syntax { .section}

```language-json
"ErrorCodeSample" : {
    "Message" : String,
    "Code" : String,
    "Description" : String
}

```

## ErrorCodeSample properties { .section}

|Name|Type|Required|Update allowed|Description|
|Message|string|Yes|Yes|Error message|
|Code|string|Yes|Yes|Error code|
|Description|string|No|Yes|Error description|

## ServiceConfig syntax { .section}

```language-json
"ServiceConfig" : {
    "ServiceTimeOut" : Integer,
    "VpcConfig" : Map，
    "MockResult" : String,
    "ServicePath" : String,
    "ServiceProtocol" : String,
    "ServiceVpcEnable" : String,
    "ServiceAddress" : String,
    "ContentTypeValue" : String,
    "ServiceHttpMethod" : String,
    "ContentTypeCatagory" : String,
    "AoneAppName" : String,
    "Mock" : String
}

```

## ServiceConfig properties { .section}

|Name|Type|Required|Update allowed|Description|
|ServiceTimeOut|integer|Yes|Yes|Backend service timeout time, in milliseconds|
|ServiceAddress|string|Yes|Yes|Backend service call address. If the complete backend service address is http://api.a.com:8080/object/add?key1=value1&key2=value2, ServiceAddress is http://api.a.com:8080|
|ServicePath|string|Yes|Yes|Backend service call path. If the complete backend service address is http://api.a.com:8080/object/add?key1=value1&key2=value2, ServicePath is /object/add|
|ServiceProtocol|string|Yes|Yes|Backend service protocol type, which must be HTTP currently. The default value is HTTP|
|ServiceHttpMethod|string|Yes|Yes|Backend service HTTP call method. The optional values are GET, POST, DELETE, PUT, HEADER, TRACE, PATCH, CONNECT, and OPTIONS. The default value is GET|
|ContentTypeCatagory|string|Yes|Yes| Strategy of obtaining the value of the ContentType header when you call the HTTP service of the backend service. The optional values are as follows:

 -   DEFAULT: Use the default value of the API gateway
-   CUSTOM: Use the custom value
-   CLIENT: Use the header of ContentType of the client’s upstream

 The default value is CLIENT

 |
|ContentTypeValue|string|No|Yes|Value of the ContentType header when you call the HTTP service of the backend service and ContentTypeCatagory is set to DEFAULT or CUSTOM|
|Mock|string|Yes|Yes|Whether the Mock mode is used. Optional values: TRUE and FALSE. The default value is FALSE|
|MockResult|string|No|Yes|Results returned when the Mock mode is enabled|
|ServiceVpcEnable|string|Yes|Yes|Whether the VPC channel is enabled. The optional values are TRUE and FALSE. The VPC channel can be enabled only after VPC authorization is successfully added. The default value is FALSE|
|VpcConfig|map|No|Yes|Configuration items of the VPC channel if the VPC channel is enabled|

## VpcConfi syntax {#section_j34_bzz_lfb .section}

```language-json
"VpcConfig" : {
	"InstanceId" : String,
	"VpcId" : String,
	"Port" : Integer,
}

```

## VpcConfig properties { .section}

|Name|Type|Required|Update allowed|Description|
|InstanceId|string|Yes|Yes|ID of the instance \(ECS/Server Load Balancer\) in VPC|
|VpcId|string|Yes|Yes|VPC ID|
|Port|integer|Yes|Yes|Number of the port corresponding to the instance|

## SystemParameters syntax { .section}

```language-json
"SystemParameter" : {
    "Location" : String,
    "ParameterName" : String,
    "Description" : String,
    "DemoValue" : String,
    "ServiceParameterName" : String
}

```

## SystemParameter properties { .section}

|Name|Type|Required|Update allowed|Description|
|Location|string|Yes|Yes|Parameter location. The optional values are BODY and HEAD. The default value is HEAD|
|ParameterName|string|Yses|Yes|System parameter name. The optional values are as follows: CaClientIp, CaDomain, CaRequestHandleTime, CaAppId, CaRequestId, CaHttpSchema, and CaProxy|
|ServiceParameterName|string|Yes|Yes|Corresponding backend parameter name|
|Description|string|No|Yes|Parameter description|
|DemoValue|string|No|Yes|Example|

## ServiceParameter syntax { .section}

```language-json
"ServiceParameter" : {
    "ParameterType" : String,
    "Location" : String,
    "ServiceParameterName" : String,
}

```

## ServiceParameter properties { .section}

|Name|Type|Required|Update allowed|Description|
|ParameterType|string|Yes|Yes|Backend parameter type. The optional values are STRING \(character type\), NUMBER \(numeric type\), and BOOLEAN \(Boolean type\)|
|Location|string|Yes|Yes|Parameter location. The optional values are BODY, HEAD, QUERY, and PATH|
|ServiceParameterName|string|Yes|Yes|Backend parameter name|

## OpenIdConnectConfig syntax { .section}

```language-json
"OpenIdConnectConfig" : {
    "OpenIdApiType" : String,
    "PublicKey" : String,
    "PublicKeyId" : String,
    "IdTokenParamName" : String,
}

```

## OpenIdConnectConfig properties { .section}

|Name|Type|Required|Update allowed|Description|
|OpenIdApiType|string|Yes|Yes| OpenID Connect mode. The optional values are as follows:

 -   IDTOKEN: Indicates the authorization API, which is used to issue a Token. If the attribute is set to IDTOKEN, the PublicKeyId and PublicKey parameters are required.
-   BUSINESS: Indicates the service API, which is used to verify a Token. If this attribute is set to BUSINESS, the IdTokenParamName parameter is required

 |
|PublicKey|string|No|Yes|Public key|
|PublicKeyId|string|No|Yes|KeyID of a public key|
|IdTokenParamName|string|No|Yes|Name of the parameter corresponding to a Token|

## RequestConfig syntax { .section}

```language-json
"RequestConfig" : {
    "RequestMode" : String,
    "RequestPath" : String,
    "PostBodyDescription" : String,
    "RequestProtocol" : String,
    "RequestHttpMethod" : String,
    "BodyFormat" : String
}

```

## RequestConfig properties { .section}

|Name|Type|Required|Update allowed|Description|
|RequestMode|string|Yes|Yes|Request mode. The optional values are MAPPING \(input mapping\) and PASSTHROUGH \(input passthrough\). The default value is MAPPING|
|RequestPath|string|Yes|Yes|API path. If the complete API address is http://api.a.com：8080/object/add?key1=value1&key2=value2, the path is /object/add|
|RequestProtocol|string|Yes|Yes|API-supported protocol type. If multiple values are entered, they must be separated by commas\(,\). For example, HTTP,HTTPS. The optional values are HTTP and HTTPS|
|RequestHttpMethod|string|Yes|Yes|HTTP method. The optional values are GET, POST, DELETE, PUT, HEADER, TRACE, PATCH, CONNECT, and OPTIONS. The default value is GET|
|PostBodyDescription|string|No|Yes|Body description|
|BodyFormat|string|No|Yes|Method of transmitting data to the server when a POST, PUT or PATCH request is sent. The optional values are FORM \(data is transmitted as forms, which is applicable to key-value pairs\) and STREAM \(data is transmitted as byte streams\). This parameter is valid when RequestMode is set to MAPPING|

## ServiceParametersMap syntax { .section}

```language-json
"ServiceParametersMap" : [
    "RequestParameterName" : String,
    "ServiceParameterName" : String
]

```

## ServiceParametersMap properties { .section}

|Namde|Type|Required|Update allowed|Description|
|RequestParameterName|string|Yes|Yes|Corresponding frontend input parameter name, which must be included in RequestParameter and matches RequestParameter.ApiParameterName|
|ServiceParameterName|string|Yes|Yes|Backend parameter name|

## RequestParameter syntax { .section}

```language-json
"RequestParameters" : {
    "ParameterType" : String,
    "RegularExpression" : String,
    "Description" : String,
    "MinLength" : Integer,
    "DefaultValue" : String,
    "Required" : String,
    "MaxValue" : Integer,
    "MinValue" : Integer,
    "JsonScheme" : String,
    "DocOrder" : Integer,
    "ApiParameterName" : String,
    "Location" : String,
    "DocShow" : String,
    "MaxLength" : Integer,
    "EnumValue" : String,
    "DemoValue" : String
}

```

## RequestParameter properties { .section}

|Name|Type|Required|Update allowed|Description|
|ParameterType|string|Yes|No|Parameter type. The optional values are as follows: String \(character type\), Int \(integer type\), Long \(long integer type\), Float \(single-precision floating-point type\), Double \(double-precision floating-point type\), and Boolean \(Boolean type\)|
|Required|string|Yes|Yes|Required or not. The optional values are REQUIRED \(required\) and OPTIONAL \(optional\)|
|ApiParameterName|string|Yes|Yes|Parameter name|
|Location|string|Yes|Yes|Parameter location. The optional values are BODY, HEAD, QUERY, and PATH|
|RegularExpression|string|No|Yes|Parameter validation \(regular expression\) when ParameterType is set to String|
|Description|string|No|Yes|Parameter description|
|DefaultValue|string|No|Yes|Default value|
|MaxLength|integer|No|Yes|Maximum parameter length when ParameterType is set to String|
|MinLength|integer|No|Yes|Minimum parameter length when ParameterType is set to String|
|MaxValue|integer|No|Yes|Maximum parameter value when ParameterType is set to Int, Long, Float, or Double|
|MinValue|integer|No|Yes|Minimum parameter value when ParameterType is set to Int, Long, Float, or Double|
|EnumValue|string|No|Yes|ParameterType is set to Int, Long, Float, Double, or String. Different values must be separated by commas\(,\). For example, 1,2,3,4,9 or A,B,C,E,F|
|JsonScheme|string|No|Yes|JSON validation \(JSON Schema\) when ParameterType is set to String|
|DocOrder|integer|No|Yes|Sequence in the document|
|DocShow|string|No|Yes|Document visibility, which can be set to PUBLIC or PRIVATE|
|DemoValue|string|No|Yes|Example|

## ConstParameter syntax { .section}

```language-json
"ConstParameter" : {
    "Location" : String,
    "ConstValue" : String,
    "Description" : String,
    "ServiceParameterName" : String
}

```

## ConstParameter properties { .section}

|Namde|Type|Required|Update allowed|Description|
|Location|string|Yes|Yes|Parameter location, which can be set to BODY or HEAD. The default value is HEAD|
|ConstValue|string|Yes|Yes|Parameter value|
|ServiceParameterName|string|Yes|Yes|Backend parameter name|
|Description|string|No|Yes|Parameter description|

## Response value { .section}

**Fn::GetAtt**

ApiId None The id of the API.

## Example {#section_zhq_syz_lfb .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "GroupId": {
      "Type": "String",
      "Default": "xxxxec10b1b4dc7a2e6ba8ca3xxxx",
      "Description": "Operated group"
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
          "Servicepath": "/Data ",
          "ServiceHttpMethod": "GET",
          "ContentTypeCatagory": "DEFAULT",
          "ServiceVpcEnable": "FALSE",
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

