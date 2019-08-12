# ALIYUN::ApiGateway::Api {#concept_61459_zh .concept}

ALIYUN::ApiGateway::Api 类型可用于创建 API。

## 语法 {#section_bnr_dxz_lfb .section}

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

## 属性 {#section_0zo_jzv_h28 .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ServiceConfig|Map|是|是|网关向后端服务发送 API 请求的相关配置项。|无。|
|RequestConfig|Map|是|是|Consumer 向网关发送 API 请求的相关配置项。|无。|
|Visibility|String|是|是| API 是否公开，可以取值：

 -   PUBLIC：公开。如选择此类型，该 API 的线上环境定义会在所有用户的控制台发现API页面可见。
-   PRIVATE：不公开。如选择此类型，当该组 API 在云市场上架时，私有类型的 API 不会上架。

 |无。|
|ResultSample|String|是|是|后端服务返回应答的示例。|无。|
|ResultType|String|是|是|后端服务返回应答的格式。目可以设置为：JSON、TEXT、BINARY、XML、HTML、PASSTHROUGH。默认值是 JSON。|无。|
|ApiName|String|是|是|设置 API 的名称。组内不允许重复。支持汉字、英文、数字、下划线，且只能以英文和汉字开头，长度为 4~50 个字符。|无。|
|GroupId|String|是|否|指定的分组编号。|无。|
|ErrorCodeSamples|List|否|是|后端服务返回的错误码示例。|无。|
|Description|String|否|是|API 描述信息，最多 180 个字符。|无。|
|SystemParameters|List|否|是|API 的系统参数。|无。|
|ServiceParameters|List|否|是|网关向后端服务发送 API 请求的参数描述。|无。|
|OpenIdConnectConfig|Map|否|是|第三方账号认证 OpenID Connect 相关配置项。|无。|
|AuthType|String|否|是| API 安全认证类型，目前可以取值：

 -   APP：只允许已授权的 APP 调用。
-   ANONYMOUS：允许匿名调用。设置为允许匿名调用需要注意：

任何能够获取该 API 服务信息的人，都将能够调用该 API。网关不会对调用者做身份认证，也无法设置根据用户的流量控制。若开放该 API，请设置 API 的流量控制。 ANONYMOUS API 不建议上架云市场。网关无法对调用者区分计量，也无法限制调用次数。若所在分组要上架云市场，建议将该 API 转移至其他分组，或将类型设置为 PRIVATE，或选择 APP 认证方式。

-   APPOPENID：支持第三方账号认证 OpenID Connect，而且只允许已授权的 APP 调用。当设置此项时，参数 OpenIdConnectConfig 为必传。

 |可用值：APP、ANONYMOUS、APPOPENID。|
|ServiceParametersMap|List|否|是|Consumer 向网关发送请求的参数和网关向后端服务发送请求的参数的映射关系。|无。|
|FailResultSample|String|否|是|后端服务失败返回应答的示例。|无。|
|RequestParameters|List|否|是|Consumer 向网关发送 API 请求的参数描述。|无。|
|ConstParameters|List|否|是|指定 API 的常量参数。|无。|

## ErrorCodeSamples 语法 {#section_wn8_jbq_6ky .section}

``` {#codeblock_oi5_bdm_lwa .language-json}
"ErrorCodeSamples": [
  {
    "Message": String,
    "Code": String,
    "Description": String
  }
]
```

## ErrorCodeSamples 属性 {#section_htb_g01_ctj .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Message|String|是|是|错误信息。|无。|
|Code|String|是|是|错误码。|无。|
|Description|String|否|是|错误描述。|无。|

## ServiceConfig 语法 {#section_rdq_ro8_66l .section}

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

## ServiceConfig 属性 {#section_0la_mr3_swj .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|FunctionComputeConfig|Map|否|是| 后端服务为函数计算，函数计算后端相关的配置项。

 |无。|
|MockStatusCode|Integer|否|是|状态码，以兼容HTTP 1.1 Response Status Code的格式返回及其状态。|无。|
|MockHeaders|List|否|是| 启用Mock时，自定义的Mock响应头相关信息。

 |无。|
|ServiceTimeOut|Integer|是|是|后端服务超时时间，单位：毫秒。|无。|
|ServiceAddress|String|是|是|调用后端服务地址，例如后端服务完全地址为： `http://api.a.com:8080/object/add?key1=value1&key2=value2`，ServiceAddress 是指 `http://api.a.com:8080`这部分。|无。|
|ServicePath|String|是|是|调用后端服务 path，例如后端服务完全地址为 `http://api.a.com:8080/object/add?key1=value1&key2=value2`， ServicePath 是指 `/object/add`这一部分。|无。|
|ServiceProtocol|String|是|是|后端服务协议类型，目前可选值： HTTP。默认值是 HTTP。|无。|
|ServiceHttpMethod|String|是|是|调用后端服务 HTTP 协议时的 Method， 默认值是 GET。

 |可用值：GET、POST、DELETE、PUT、HEADER、TRACE、PATCH、CONNECT、OPTIONS。|
|ContentTypeCatagory|String|是|是| 调用后端服务 HTTP 服务时，ContentType 头的取值策略：

 -   DEFAULT：使用 API 网关默认的值。
-   CUSTOM：自定义。
-   CLIENT：使用客户端上行的 ContentType 的头。

 默认值是 CLIENT。

 |可用值：DEFAULT、CUSTOM、CLIENT。|
|ContentTypeValue|String|否|是|调用后端服务 HTTP 服务，ContentTypeCatagory 的值为 DEFAULT 或者 CUSTOM 时，ContentType 头的取值。|无。|
|Mock|String|是|是|是否采取 Mock 模式，默认值是 FALSE。|目前可用值：TRUE、FALSE。|
|MockResult|String|否|是|如果启用 Mock 模式，返回的结果。|无。|
|ServiceVpcEnable|String|是|是|是否启用 VPC 通道。目前可以取值： TRUE， FALSE。必须先添加 VPC 授权成功后才能启用。 默认值是 FALSE。

 |目前可用值： TRUE、 FALSE。|
|VpcConfig|Map|否|是|如果启用 VPC 通道，VPC 通道相关配置项。|无。|

## VpcConfig 语法 {#section_j34_bzz_lfb .section}

``` {#codeblock_z3a_srj_hnm .language-json}
"VpcConfig": {
  "InstanceId": String,
  "VpcId": String,
  "Port": Integer
}
```

## VpcConfig 属性 {#section_2jq_h8s_euq .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|InstanceId|String|是|是|专用网络中的实例 ID（ECS/SLB）。|无。|
|VpcId|String|是|是|VPC ID。|无。|
|Port|Integer|是|是|实例对应的端口号。|无。|

## SystemParameters 语法 {#section_eor_kp1_216 .section}

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

## SystemParameters 属性 {#section_jx9_98n_szh .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Location|String|是|是|参数位置，默认值是 HEAD。|可用值：BODY、HEAD。|
|ParameterName|String|是|是|系统参数名。|可用值：CaClientIp、CaDomain、CaRequestHandleTime、CaAppId、CaRequestId、CaHttpSchema、CaProxy。|
|ServiceParameterName|String|是|是|对应后端参数名称。|无。|
|Description|String|否|是|参数描述。|无。|
|DemoValue|String|否|是|示例。|无。|

## ServiceParameters 语法 {#section_mop_no7_osa .section}

``` {#codeblock_h0z_acf_vep .language-json}
"ServiceParameters": [
  {
    "ParameterType": String,
    "Location": String,
    "ServiceParameterName": String
  }
]
```

## ServiceParameters 属性 {#section_5ox_ipa_s7s .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ParameterType|String|是|是|后端参数数据类型，取值为：STRING、NUMBER、BOOLEAN，分别表示字符、数值、布尔。|可用值：STRING、NUMBER、BOOLEAN。|
|Location|String|是|是|参数位置，取值为：BODY、HEAD、QUERY、PATH。|可用值：BODY、HEAD、QUERY、PATH。|
|ServiceParameterName|String|是|是|后端参数名称。|无。|

## OpenIdConnectConfig 语法 {#section_ffj_1ez_mu6 .section}

``` {#codeblock_hx9_f6n_z0w .language-json}
"OpenIdConnectConfig": {
  "OpenIdApiType": String,
  "PublicKey": String,
  "PublicKeyId": String,
  "IdTokenParamName": String
}
```

## OpenIdConnectConfig 属性 {#section_6qc_wi9_wp2 .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|OpenIdApiType|String|是|是| OpenID Connect 模式，目前可以取值：

 -   IDTOKEN：获取授权 API，颁发 Token。当设置此项时，参数 PublicKeyId 和 PublicKey 为必传。
-   BUSINESS：业务 API，Token 验证，当设置此项时，参数 IdTokenParamName 为必传。

 |目前可用值：IDTOKEN、BUSINESS。|
|PublicKey|String|否|是|公钥。|无。|
|PublicKeyId|String|否|是|公钥 KeyId。|无。|
|IdTokenParamName|String|否|是|Token 对应的参数名称。|无。|

## RequestConfig 语法 {#section_hdw_hil_bzc .section}

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

## RequestConfig 属性 {#section_tws_ib2_ui4 .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|RequestMode|String|是|是|请求的模式，MAPPING、PASSTHROUGH，分别表示入参映射、入参透传。默认值是 MAPPING。|可用值：MAPPING、PASSTHROUGH。|
|RequestPath|String|是|是|API path，例如 API 的完全地址为 `http://api.a.com：8080/object/add?key1=value1&key2=value2`，path 是指 `/object/add`这一部分。|无。|
|RequestProtocol|String|是|是|API 支持的协议类型。可以多选，多选情况下以英文逗号隔开，如：“HTTP，HTTPS”。|可用值：HTTP、HTTPS。|
|RequestHttpMethod|String|是|是|HTTP Method。 默认值是 GET。

 |可用值：GET、POST、DELETE、PUT、HEADER、TRACE、PATCH、CONNECT、OPTIONS。|
|PostBodyDescription|String|否|是|Body 的描述。|无。|
|BodyFormat|String|否|是|POST/PUT/PATCH 请求时，表示数据以何种方式传递给服务器，FORM、STREAM，分别表示表单形式（k-v 对应）、字节流形式。当 RequestMode 值为 MAPPING 时有效。|可用值：FORM、STREAM。|

## ServiceParametersMap 语法 {#section_6kt_qtd_4x4 .section}

``` {#codeblock_t9n_2ss_hkz .language-json}
"ServiceParametersMap": [
  {
    "RequestParameterName": String,
    "ServiceParameterName": String
  }
]
```

## ServiceParametersMap 属性 {#section_hf2_f94_yxq .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|RequestParameterName|String|是|是|对应前端入参名称。|值必须存在于 RequestParameters 中，即RequestParameters.ApiParameterName。|
|ServiceParameterName|String|是|是|后端参数名称。|无。|

## RequestParameters 语法 {#section_q3w_71y_pbc .section}

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

## RequestParameters 属性 {#section_f24_n0m_w1o .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ParameterType|String|是|否|参数类型，String、Int、Long、Float、Double、Boolean，分别表示字符、整型、长整型、单精度浮点型、双精度浮点型、布尔。|可用值：String、Int、Long、Float、Double、Boolean。|
|Required|String|是|是|是否必填，REQUIRED、OPTIONAL，分别表示必填、不必填。|可用值：REQUIRED、OPTIONAL。|
|ApiParameterName|String|是|是|参数名。|无。|
|Location|String|是|是|参数位置。|可用值：BODY、HEAD、QUERY、PATH。|
|RegularExpression|String|否|是|当 ParameterType 为 String 时，参数验证（正则表达式）。|无。|
|Description|String|否|是|参数描述。|无。|
|DefaultValue|String|否|是|默认值。|无。|
|MaxLength|Integer|否|是|当 ParameterType 为 String 时，参数的最大长度限定。|无。|
|MinLength|Integer|否|是|当 ParameterType 为 String 时，参数的最小长度限定。|无。|
|MaxValue|Integer|否|是|当 ParameterType 为 Int、Long、Float、Double 时，参数的最大值限定。|无。|
|MinValue|Integer|否|是|当 ParameterType 为 Int、Long、Float、Double 时，参数的最小值限定。|无。|
|EnumValue|String|否|是|当 ParameterType 为 Int、Long、Float、Double 或 String 时，允许输入的散列值，不同的值用英文的逗号分隔，形如：1,2,3,4,9 或 A,B,C,E,F。|无。|
|JsonScheme|String|否|是|当 ParameterType 为 String，JSON 验证（Json Scheme）。|无。|
|DocOrder|Integer|否|是|文档中的顺序。|无。|
|DocShow|String|否|是|文档可见。|可用值：PUBLIC、PRIVATE。|
|DemoValue|String|否|是|示例。|无。|

## ConstParameters 语法 {#section_i7a_nn7_jr4 .section}

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

## ConstParameters 属性 {#section_m5p_znp_n4c .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Location|String|是|是|参数位置，默认值是 HEAD。|可用值：BODY、HEAD。|
|ConstValue|String|是|是|参数值。|无。|
|ServiceParameterName|String|是|是|后端参数名称。|无。|
|Description|String|否|是|参数描述。|无。|

## FunctionComputeConfig 语法 {#section_i7a_nn7_jr4 .section}

``` {#codeblock_nk5_wxu_vu1 .language-json}
"FunctionComputeConfig": {
  "fcRegionId": String,
  "roleArn": String,
  "serviceName": String,
  "functionName": String
}
```

## FunctionComputeConfig 属性 {#section_dap_hno_5q9 .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|fcRegionId|String|是|是|函数计算所在 Region。|无。|
|roleArn|String|是|是|RAM 授权给 API 网关访问函数计算的 arn。|无。|
|serviceName|String|是|是|函数计算定义的 ServiceName。|无。|
|functionName|String|是|是|函数计算定义的 FunctionName。|无。|

## 返回值 {#section_whc_v01_txt .section}

**Fn::GetAtt**

ApiId：指定的API编号。

## 示例 {#section_zhq_syz_lfb .section}

``` {#codeblock_59u_4qw_2z2 .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "GroupId": {
      "Type": "String",
      "Default": "xxxxec10b1b4dc7a2e6ba8ca3xxxx",
      "Description": "操作的分组"
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

