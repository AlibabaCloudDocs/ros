# ALIYUN::ApiGateway::Api {#concept_61459_zh .concept}

ALIYUN::ApiGateway::Api is used to create an API.

## Syntax {#section_bnr_dxz_lfb .section}

``` {#codeblock_7ry_xww_fld .language-json}
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

## Properties {#section_0zo_jzv_h28 .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|ServiceConfig|Map|Yes|Yes|The configuration items of API requests sent by API Gateway to the back-end service.|None|
|RequestConfig|Map|Yes|Yes|The configuration items of API requests sent by the consumer to API Gateway.|None|
|Visibility|String|Yes|Yes| Specifies whether the API is public. Valid values:

 -   PUBLIC: The API is public. If you set this parameter to PUBLIC, this API will be displayed on the API List page for all users when the API is published to the production environment.
-   PRIVATE: The API is not public. Private APIs are not displayed in the Alibaba Cloud Marketplace when the API group to which they belong is made available.

 |None|
|ResultSample|String|Yes|Yes|The sample response from the back-end service.|None|
|ResultType|String|Yes|Yes|The format of the response from the back-end service. Valid values: JSON, TEXT, BINARY, XML, HTML, and PASSTHROUGH. Default value: JSON.|None|
|ApiName|String|Yes|Yes|The name of the API. The name must be unique within the API group. It must be 4 to 50 characters in length and can contain letters, digits, and underscores \(\_\). It must start with a letter.|None|
|GroupId|String|Yes|No|The ID of the API group to which the API belongs.|None|
|ErrorCodeSamples|List|No|Yes|The sample error codes returned by the back-end service.|None|
|Description|String|No|Yes|The description of the API. The description can be up to 180 characters in length.|None|
|SystemParameters|List|No|Yes|The system parameters of the API.|None|
|ServiceParameters|List|No|Yes|The parameters of API requests sent by API Gateway to the back-end service.|None|
|OpenIdConnectConfig|Map|No|Yes|The configuration items of the third-party OpenID Connect authentication method.|None|
|AuthType|String|No|Yes| The API security authentication method. Valid values:

 -   APP: Only authorized applications can call the API.
-   ANONYMOUS: The API can be called anonymously. In this mode, you must take note of the following points:

Anyone who can obtain the API service information is permitted to call this API. API Gateway does not authenticate callers and cannot set user-specific throttling policies. If you make an API that has anonymous authentication enabled public, set API-based throttling policies. We do not recommend making APIs with anonymous authentication available in the Alibaba Cloud Marketplace. API Gateway cannot bill callers separately or control the number of calls. Before you add a group containing such APIs to the Marketplace, we recommend that you move them to another group, set their Visibility to PRIVATE, or set their AuthType to APP.

-   APPOPENID: The OpenID Connect authentication method is used. Only applications authorized by OpenID Connect can call the API. If this method is selected, the OpenIdConnectConfig parameter is required.

 |Valid values: APP, ANONYMOUS, and APPOPENID.|
|ServiceParametersMap|List|No|Yes|The mappings between parameters of requests sent by the consumer to API Gateway and parameters of requests sent by API Gateway to the back-end service.|None|
|FailResultSample|String|No|Yes|The sample error response from the back-end service.|None|
|RequestParameters|List|No|Yes|The parameters of API requests sent by the consumer to API Gateway.|None|
|ConstParameters|List|No|Yes|The constant parameters of the specified API.|None|

## ErrorCodeSamples syntax {#section_wn8_jbq_6ky .section}

``` {#codeblock_oi5_bdm_lwa .language-json}
"ErrorCodeSamples": [
  {
    "Message": String,
    "Code": String,
    "Description": String
  }
]
```

## ErrorCodeSamples properties {#section_htb_g01_ctj .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Message|String|Yes|Yes|The error message.|None|
|Code|String|Yes|Yes|The error code.|None|
|Description|String|No|Yes|The error description.|None|

## ServiceConfig syntax {#section_rdq_ro8_66l .section}

``` {#codeblock_uhr_wsx_hzh .language-json}
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

## ServiceConfig properties {#section_0la_mr3_swj .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|FunctionComputeConfig|Map|No|Yes| The configuration items of Function Compute as the back-end service.

 |None|
|MockStatusCode|Integer|No|Yes|The status code returned in an HTTP/1.1 compatible format.|None|
|MockHeaders|List|No|Yes| The mock response headers defined when mock mode is enabled.

 |None|
|ServiceTimeOut|Integer|Yes|Yes|The timeout period of the back-end service. Unit: milliseconds.|None|
|ServiceAddress|String|Yes|Yes|The URL used to call the back-end service. If the complete back-end service URL is `http://api.a.com:8080/object/add?key1=value1&key2=value2`, the value of ServiceAddress is `http://api.a.com:8080`.|None|
|ServicePath|String|Yes|Yes|The path used to call the back-end service. If the complete back-end service path is `http://api.a.com:8080/object/add?key1=value1&key2=value2`, the value of ServicePath is `/object/add`.|None|
|ServiceProtocol|String|Yes|Yes|The protocol of the back-end service. Set the value to HTTP. Default value: HTTP.|None|
|ServiceHttpMethod|String|Yes|Yes|The HTTP method used to call the back-end service. Default value: GET.

 |Valid values: GET, POST, DELETE, PUT, HEADER, TRACE, PATCH, CONNECT, and OPTIONS.|
|ContentTypeCatagory|String|Yes|Yes| The ContentType header type used when you call the back-end service over HTTP. Valid values:

 -   DEFAULT: the default header type in API Gateway.
-   CUSTOM: a custom header type.
-   CLIENT: the ContentType header type of the client.

 Default value: CLIENT.

 |Valid values: DEFAULT, CUSTOM, and CLIENT.|
|ContentTypeValue|String|No|Yes|The ContentType header value used when you call the back-end service over HTTP. This parameter is only valid when the ContentTypeCatagory parameter is set to DEFAULT or CUSTOM.|None|
|Mock|String|Yes|Yes|Specifies whether to use mock mode. Default value: FALSE.|Valid values: TRUE and FALSE.|
|MockResult|String|No|Yes|The result returned when mock mode is enabled.|None|
|ServiceVpcEnable|String|Yes|Yes|Specifies whether to enable a VPC. A VPC can be enabled only after the VPC is authorized. Default value: FALSE.

 |Valid values: TRUE and FALSE.|
|VpcConfig|Map|No|Yes|The configuration items of a VPC.|None|

## VpcConfig syntax {#section_j34_bzz_lfb .section}

``` {#codeblock_z3a_srj_hnm .language-json}
"VpcConfig": {
  "InstanceId": String,
  "VpcId": String,
  "Port": Integer
}
```

## VpcConfig properties {#section_2jq_h8s_euq .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|InstanceId|String|Yes|Yes|The ID of an ECS or SLB instance in the VPC.|None|
|VpcId|String|Yes|Yes|The ID of the VPC to which the specified instance belongs.|None|
|Port|Integer|Yes|Yes|The port number corresponding to the instance.|None|

## SystemParameters syntax {#section_eor_kp1_216 .section}

``` {#codeblock_icc_erz_kze .language-json}
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

## SystemParameters properties {#section_jx9_98n_szh .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Location|String|Yes|Yes|The location of the system parameter. Default value: HEAD.|Valid values: BODY and HEAD.|
|ParameterName|String|Yes|Yes|The name of the system parameter.|Valid values: CaClientIp, CaDomain, CaRequestHandleTime, CaAppId, CaRequestId, CaHttpSchema, and CaProxy.|
|ServiceParameterName|String|Yes|Yes|The name of the corresponding back-end service parameter.|None|
|Description|String|No|Yes|The description of the system parameter.|None|
|DemoValue|String|No|Yes|The sample value of the system parameter.|None|

## ServiceParameters syntax {#section_mop_no7_osa .section}

``` {#codeblock_h0z_acf_vep .language-json}
"ServiceParameters": [
  {
    "ParameterType": String,
    "Location": String,
    "ServiceParameterName": String
  }
]
```

## ServiceParameters properties {#section_5ox_ipa_s7s .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|ParameterType|String|Yes|Yes|The data type of the back-end service parameter.|Valid values: STRING, NUMBER, and BOOLEAN.|
|Location|String|Yes|Yes|The location of the back-end service parameter.|Valid values: BODY, HEAD, QUERY, and PATH.|
|ServiceParameterName|String|Yes|Yes|The name of the back-end service parameter.|None|

## OpenIdConnectConfig syntax {#section_ffj_1ez_mu6 .section}

``` {#codeblock_hx9_f6n_z0w .language-json}
"OpenIdConnectConfig": {
  "OpenIdApiType": String,
  "PublicKey": String,
  "PublicKeyId": String,
  "IdTokenParamName": String
}
```

## OpenIdConnectConfig properties {#section_6qc_wi9_wp2 .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|OpenIdApiType|String|Yes|Yes| The authorization type of an OpenID Connect API. Valid values:

 -   IDTOKEN: specifies an authorization API, which is used to issue a token. If you set this parameter to IDTOKEN, the PublicKeyId and PublicKey parameters are required.
-   BUSINESS: specifies a business API, which is used to verify a token. If you set this parameter to BUSINESS, the IdTokenParamName parameter is required.

 |Valid values: IDTOKEN and BUSINESS.|
|PublicKey|String|No|Yes|The public key used for token verification.|None|
|PublicKeyId|String|No|Yes|The ID of the public key.|None|
|IdTokenParamName|String|No|Yes|The name of the authentication token.|None|

## RequestConfig syntax {#section_hdw_hil_bzc .section}

``` {#codeblock_187_k9v_5wu .language-json}
"RequestConfig": {
  "RequestMode": String,
  "RequestPath": String,
  "PostBodyDescription": String,
  "RequestProtocol": String,
  "RequestHttpMethod": String,
  "BodyFormat": String
}
```

## RequestConfig properties {#section_tws_ib2_ui4 .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|RequestMode|String|Yes|Yes|The request mode. Default value: MAPPING.|Valid values: MAPPING and PASSTHROUGH.|
|RequestPath|String|Yes|Yes|The API request path. If the complete API URL is `http://api.a.com:8080/object/add?key1=value1&key2=value2`, the API request path is `/object/add`.|None|
|RequestProtocol|String|Yes|Yes|The API-supported protocol type. Use commas \(,\) to separate multiple values. Example: HTTP,HTTPS|Valid values: HTTP and HTTPS.|
|RequestHttpMethod|String|Yes|Yes|The HTTP method used to make the request. Default value: GET.

 |Valid values: GET, POST, DELETE, PUT, HEADER, TRACE, PATCH, CONNECT, and OPTIONS.|
|PostBodyDescription|String|No|Yes|The description of the request body.|None|
|BodyFormat|String|No|Yes|The method used to transmit data to the server when a POST, PUT, or PATCH request is sent. A value of FORM indicates that data in key-value pairs is transmitted as forms. A value of STREAM indicates that data is transmitted as byte streams. This parameter is only valid when the RequestMode parameter is set to MAPPING.|Valid values: FORM and STREAM.|

## ServiceParametersMap syntax {#section_6kt_qtd_4x4 .section}

``` {#codeblock_t9n_2ss_hkz .language-json}
"ServiceParametersMap": [
  {
    "RequestParameterName": String,
    "ServiceParameterName": String
  }
]
```

## ServiceParametersMap properties {#section_hf2_f94_yxq .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|RequestParameterName|String|Yes|Yes|The name of the front-end request parameter.|It must be included in RequestParameter and matches ApiParameterName in RequestParameter data.|
|ServiceParameterName|String|Yes|Yes|The name of the corresponding back-end service parameter.|None|

## RequestParameters syntax {#section_q3w_71y_pbc .section}

``` {#codeblock_554_y1z_9yb .language-json}
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

## RequestParameters properties {#section_f24_n0m_w1o .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|ParameterType|String|Yes|No|The type of the request parameter.|Valid values: String, Int, Long, Float, Double, and Boolean.|
|Required|String|Yes|Yes|Specifies whether the parameter is required.|Valid values: REQUIRED and OPTIONAL.|
|ApiParameterName|String|Yes|Yes|The name of the parameter.|None|
|Location|String|Yes|Yes|The location of the parameter.|Valid values: BODY, HEAD, QUERY, and PATH.|
|RegularExpression|String|No|Yes|The regular parameter validation expression. This parameter is only valid when the ParameterType parameter is set to String.|None|
|Description|String|No|Yes|The description of the parameter.|None|
|DefaultValue|String|No|Yes|The default value of the parameter.|None|
|MaxLength|Integer|No|Yes|The maximum length of the parameter. This parameter is only valid when the ParameterType parameter is set to String.|None|
|MinLength|Integer|No|Yes|The minimum length of the parameter. This parameter is only valid when the ParameterType parameter is set to String.|None|
|MaxValue|Integer|No|Yes|The maximum value of the parameter. This parameter is only valid when the ParameterType parameter is set to Int, Long, Float, or Double.|None|
|MinValue|Integer|No|Yes|The minimum value of the parameter. This parameter is only valid when the ParameterType parameter is set to Int, Long, Float, or Double.|None|
|EnumValue|String|No|Yes|The hash values that can be entered when the ParameterType parameter is set to Int, Long, Float, Double, or String. Different values must be separated by commas \(,\), such as in 1,2,3,4,9 and A,B,C,E,F.|None|
|JsonScheme|String|No|Yes|The JSON schema used for JSON validation. This parameter is only valid when the ParameterType parameter is set to String.|None|
|DocOrder|Integer|No|Yes|The sequence of the parameter in the document.|None|
|DocShow|String|No|Yes|Specifies whether the parameter is public in the document.|Valid values: PUBLIC and PRIVATE.|
|DemoValue|String|No|Yes|The sample value of the parameter.|None|

## ConstParameters syntax {#section_i7a_nn7_jr4 .section}

``` {#codeblock_nk5_wxu_vu1 .language-json}
"ConstParameters": [
  {
    "ConstValue": String,
    "ServiceParameterName": String,
    "Description": String,
    "Location": String
  }
]
```

## ConstParameters properties {#section_m5p_znp_n4c .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Location|String|Yes|Yes|The location of the constant parameter. Default value: HEAD.|Valid values: BODY and HEAD.|
|ConstValue|String|Yes|Yes|The value of the parameter.|None|
|ServiceParameterName|String|Yes|Yes|The name of the back-end service parameter.|None|
|Description|String|No|Yes|The description of the parameter.|None|

## FunctionComputeConfig syntax {#section_i7a_nn7_jr4 .section}

``` {#codeblock_nk5_wxu_vu1 .language-json}
"FunctionComputeConfig": {
  "fcRegionId": String,
  "roleArn": String,
  "serviceName": String,
  "functionName": String
}
```

## FunctionComputeConfig properties {#section_dap_hno_5q9 .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|fcRegionId|String|Yes|Yes|The region where Function Compute is located.|None|
|roleArn|String|Yes|Yes|The Alibaba Cloud Resource Name \(ARN\) of the RAM role to be assumed by API Gateway to access Function Compute.|None|
|serviceName|String|Yes|Yes|The service name defined in Function Compute.|None|
|functionName|String|Yes|Yes|The function name defined in Function Compute.|None|

## Response parameters {#section_whc_v01_txt .section}

**Fn::GetAtt**

ApiId: the ID of the specified API.

## Examples {#section_zhq_syz_lfb .section}

``` {#codeblock_59u_4qw_2z2 .language-json}
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

