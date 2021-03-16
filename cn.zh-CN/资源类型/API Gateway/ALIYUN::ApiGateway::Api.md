# ALIYUN::ApiGateway::Api

ALIYUN::ApiGateway::Api类型用于创建API。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ServiceConfig|Map|是|是|网关向后端服务发送API请求的相关配置项。|更多信息，请参见[ServiceConfig属性](#section_0la_mr3_swj)。|
|RequestConfig|Map|是|是|Consumer向网关发送API请求的相关配置项 。|更多信息，请参见[RequestConfig属性](#section_tws_ib2_ui4)。|
|Visibility|String|是|是|API是否公开。

|取值： -   PUBLIC：公开。
-   PRIVATE：不公开。 |
|ResultSample|String|是|是|后端服务返回应答的示例。|无|
|ResultType|String|是|是|后端服务返回应答的格式。|取值： -   JSON（默认值）
-   TEXT
-   BINARY
-   XML
-   PASSTHROUGH |
|ApiName|String|是|是|API名称。|长度为4~50个字符。必须以英文字母或汉字开头。可包含英文字母、汉字、数字和下划线（\_）。**说明：** API分组内的API名称不允许重复。 |
|GroupId|String|是|否|API分组编号。|无|
|ErrorCodeSamples|List|否|是|后端服务返回的错误码示例。|更多信息，请参见[ErrorCodeSamples属性](#section_htb_g01_ctj)。|
|Description|String|否|是|API描述信息。|最多支持180个字符。|
|DisableInternet|Boolean|否|是|是否禁止公网调用API。|取值：-   true
-   false |
|ForceNonceCheck|Boolean|否|是|请求时是否强制检查X-Ca-Nonce。|取值：-   true
-   false |
|Tags|List|否|是|标签。|最多支持添加20个标签。更多信息，请参见[Tags属性](#section_yf3_rbl_k6g)。 |
|SystemParameters|List|否|是|API的系统参数。|更多信息，请参见[SystemParameters属性](#section_jx9_98n_szh)。|
|ServiceParameters|List|否|是|网关向后端服务发送API请求的参数描述。|更多信息，请参见[ServiceParameters属性](#section_5ox_ipa_s7s)。|
|OpenIdConnectConfig|Map|否|是|第三方账号认证OpenID Connect相关配置项。|更多信息，请参见[OpenIdConnectConfig属性](#section_6qc_wi9_wp2)。|
|AuthType|String|否|是|API安全认证类型。

|取值： -   APP：只允许已授权的App调用。
-   ANONYMOUS：允许匿名调用，网关不会对调用者做身份认证，也无法根据用户需求设置流量控制。若所在分组要上架云市场，建议将该API转移至其他分组，或将类型设置为私有，或选择阿里云App认证方式。
-   APPOPENID：支持第三方账号认证OpenID Connect，而且只允许已授权的App调用。当设置此项时，参数OpenIdConnectConfig必须指定。 |
|ServiceParametersMap|List|否|是|Consumer向网关发送请求的参数和网关向后端服务发送请求的参数的映射关系。|更多信息，请参见[ServiceParametersMap属性](#section_hf2_f94_yxq)。|
|FailResultSample|String|否|是|后端服务失败返回应答的示例。|无|
|RequestParameters|List|否|是|Consumer向网关发送API请求的参数描述。|更多信息，请参见[RequestParameters属性](#section_f24_n0m_w1o)。|
|ConstParameters|List|否|是|指定API的常量参数。|更多信息，请参见[ConstParameters属性](#section_m5p_znp_n4c)。|
|AppCodeAuthType|String|否|是|AppCode认证方式。|AuthType取值为APP时该参数生效，取值： -   DEFAULT（默认值）：随分组设置。
-   DISABLE：不允许。
-   HEADER：允许AppCode的Header认证。
-   HEADER\_QUERY：允许AppCode的Header及Query认证。 |

## Tags语法

```
"Tags": [
  {
    "Key": String,
    "Value": String
  }
]  
```

## Tags属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Key|String|是|否|标签键。|长度为1~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或者`https://` 。|
|Value|String|否|否|标签值。|长度为0~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或者`https://` 。|

## ErrorCodeSamples语法

```
"ErrorCodeSamples": [
  {
    "Message": String,
    "Code": String,
    "Description": String
  }
]
```

## ErrorCodeSamples属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Message|String|是|是|错误信息。|无|
|Code|String|是|是|错误码。|无|
|Description|String|否|是|错误描述。|无|

## ServiceConfig语法

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

## ServiceConfig属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|FunctionComputeConfig|Map|否|是|后端服务为函数计算。|函数计算后端相关的配置项，请参见[FunctionComputeConfig](https://help.aliyun.com/document_detail/109314.html)。

无

更多信息，请参见[FunctionComputeConfig属性](#section_dap_hno_5q9)。|
|MockStatusCode|Integer|否|是|状态码。|以兼容HTTP 1.1 Response Status Code的格式返回。|
|MockHeaders|List|否|是|启用Mock时，自定义的Mock响应头相关信息。|更多信息，请参见[MockHeader](https://help.aliyun.com/document_detail/92157.html)。

无

更多信息，请参见[MockHeaders属性](#section_6hy_tfc_d55)。|
|ServiceTimeOut|Integer|否|是|后端服务超时时间。|单位：毫秒。|
|ServiceAddress|String|否|是|后端服务地址。|例如：后端服务完整地址为`http://api.a.com:8080/object/add?key1=value1&key2=value2`，后端服务地址指`http://api.a.com:8080`。|
|ServicePath|String|否|是|后端服务路径。|例如：后端服务完全地址为 `http://api.a.com:8080/object/add?key1=value1&key2=value2`， 后端服务路径指`/object/add`。|
|ServiceProtocol|String|否|是|后端服务协议类型。|取值： -   HTTP
-   HTTPS
-   FunctionCompute |
|ServiceVpcEnable|String|否|是|是否使用专有网络。|取值： -   TRUE
-   FALSE（默认值） |
|ServiceHttpMethod|String|否|是|调用后端服务HTTP协议时的方法。|取值： -   GET（默认值）
-   POST
-   DELETE
-   PUT
-   HEAD
-   TRACE
-   PATCH
-   CONNECT
-   OPTIONS
-   ANY |
|ContentTypeCatagory|String|否|是|调用后端HTTP服务时，ContentType头的取值策略。

|取值： -   DEFAULT：使用API网关默认值。
-   CUSTOM：自定义。
-   CLIENT（默认值）：使用客户端上行的ContentType头。 |
|ContentTypeValue|String|否|是|当后端服务是HTTP，ContentTypeCatagory取值为DEFAULT或CUSTOM时，ContentType头的取值。|无|
|Mock|String|否|是|是否采取Mock模式。|取值： -   TRUE
-   FALSE（默认值） |
|MockResult|String|否|是|启用Mock模式时返回的结果。|无|
|VpcConfig|Map|否|是|启用VPC通道时的相关配置项。|更多信息，请参见[VpcConfig属性](#section_2jq_h8s_euq)。|

## VpcConfig语法

```
"VpcConfig": {
  "InstanceId": String,
  "VpcId": String,
  "Port": Integer
}
```

## VpcConfig属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|InstanceId|String|是|是|专用网络中的实例ID。|目前只支持ECS实例和SLB实例。|
|VpcId|String|是|是|专有网络ID。|无|
|Port|Integer|是|是|实例对应的端口号。|无|

## SystemParameters语法

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

## SystemParameters属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Location|String|是|是|参数位置。|无|
|ParameterName|String|是|是|系统参数名称。|取值： -   CaClientIp
-   CaDomain
-   CaRequestHandleTime
-   CaAppId
-   CaRequestId
-   CaHttpSchema
-   CaProxy |
|ServiceParameterName|String|是|是|后端参数名称。|无|
|Description|String|否|是|参数描述。|无|
|DemoValue|String|否|是|示例。|无|

## ServiceParameters语法

```
"ServiceParameters": [
  {
    "ParameterType": String,
    "Location": String,
    "ServiceParameterName": String
  }
]
```

## ServiceParameters属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ParameterType|String|是|是|后端参数数据类型。|取值： -   STRING：字符。
-   NUMBER：数值。
-   BOOLEAN：布尔。 |
|Location|String|是|是|参数位置。|取值： -   BODY
-   HEAD
-   QUERY
-   PATH |
|ServiceParameterName|String|是|是|后端参数名称。|无|

## OpenIdConnectConfig语法

```
"OpenIdConnectConfig": {
  "OpenIdApiType": String,
  "PublicKey": String,
  "PublicKeyId": String,
  "IdTokenParamName": String
}
```

## OpenIdConnectConfig属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|OpenIdApiType|String|是|是|OpenID Connect模式。|取值： -   IDTOKEN：先获取授权API，再颁发Token。当设置此项时，参数PublicKeyId和PublicKey必须指定。
-   BUSINESS：先获取业务API，再进行Token验证。当设置此项时，参数IdTokenParamName必须指定。 |
|PublicKey|String|否|是|公钥。|无|
|PublicKeyId|String|否|是|公钥ID。|无|
|IdTokenParamName|String|否|是|Token对应的参数名称。|无|

## RequestConfig语法

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

## RequestConfig属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|RequestMode|String|是|是|请求模式。|取值： -   MAPPING（默认值）：入参映射。
-   PASSTHROUGH：入参透传。 |
|RequestPath|String|是|是|请求地址。|例如：API的完全地址为`http://api.a.com：8080/object/add?key1=value1&key2=value2`，请求地址指`/object/add`。|
|RequestProtocol|String|是|是|API支持的协议类型。|取值： -   HTTP
-   HTTPS

多个协议类型以半角逗号（,）隔开，例如：`HTTP,HTTPS`。|
|RequestHttpMethod|String|是|是|请求方式。|取值： -   GET（默认值）
-   POST
-   DELETE
-   PUT
-   HEADER
-   TRACE
-   PATCH
-   OPTIONS |
|PostBodyDescription|String|否|是|请求体的描述。|无|
|BodyFormat|String|否|是|POST、PUT或PATCH请求时，表示数据以何种方式传递给服务器。|取值： -   FORM：表单形式。
-   STREAM：字节流形式。

当RequestMode值为MAPPING时，该参数有效。|

## ServiceParametersMap语法

```
"ServiceParametersMap": [
  {
    "RequestParameterName": String,
    "ServiceParameterName": String
  }
]
```

## ServiceParametersMap属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|RequestParameterName|String|是|是|前端参数名称。|该参数取值必须存在于RequestParameters中，即RequestParameters.ApiParameterName。|
|ServiceParameterName|String|是|是|后端参数名称。|无|

## RequestParameters语法

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

## RequestParameters属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ParameterType|String|是|否|参数类型。|取值： -   String：字符。
-   Int：整型。
-   Long：长整型。
-   Float：单精度浮点型。
-   Double：双精度浮点型。
-   Boolean：布尔。 |
|Required|String|是|是|是否必填。|取值： -   REQUIRED：必填。
-   OPTIONAL：选填。 |
|ApiParameterName|String|是|是|参数名称。|无|
|Location|String|是|是|参数位置。|取值： -   BODY
-   HEAD
-   QUERY
-   PATH |
|RegularExpression|String|否|是|当ParameterType为String时，该参数通过正则表达式进行验证。|无|
|Description|String|否|是|参数描述。|无|
|DefaultValue|String|否|是|默认值。|无|
|MaxLength|Integer|否|是|当ParameterType为 String时，参数的最大长度限定。|无|
|MinLength|Integer|否|是|当ParameterType为String时，参数的最小长度限定。|无|
|MaxValue|Integer|否|是|当ParameterType为Int、Long、Float、Double 时，参数的最大值限定。|无|
|MinValue|Integer|否|是|当ParameterType为 Int、Long、Float、Double 时，参数的最小值限定。|无|
|EnumValue|String|否|是|当ParameterType为Int、Long、Float、Double或String时，允许输入的散列值。|不同的值用半角逗号（,）分隔，例如：`1,2,3,4,9`或`A,B,C,E,F`。|
|JsonScheme|String|否|是|当ParameterType为String时，该参数进行JSON验证。|无|
|DocOrder|Integer|否|是|文档中的顺序。|无|
|DocShow|String|否|是|API网关生成的SDK或文档是否可见。|取值： -   PUBLIC
-   PRIVATE |
|DemoValue|String|否|是|示例值。|无|

## ConstParameters语法

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

## ConstParameters属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Location|String|是|是|参数位置。|取值： -   BODY
-   HEAD（默认值） |
|ConstValue|String|是|是|参数值。|无|
|ServiceParameterName|String|是|是|后端参数名称。|无|
|Description|String|否|是|参数描述。|无|

## FunctionComputeConfig语法

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

## FunctionComputeConfig属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|FcRegionId|String|否|是|函数计算所在地域ID。|无|
|RoleArn|String|否|是|RAM授权给API网关访问函数计算的ARN。|无|
|ServiceName|String|否|是|函数计算定义的ServiceName。|无|
|FunctionName|String|否|是|函数计算定义的FunctionName。|无|
|Qualifier|String|否|是|函数计算的别名。|无|
|ContentTypeCatagory|String|否|是|调用后端服务HTTP服务时，ContentType头的取值策略。|取值：-   DEFAULT：使用API网关默认的值。
-   CUSTOM：自定义。
-   CLIENT（默认值）：使用客户端上行的ContentType的头。 |
|ContentTypeValue|String|否|是|调用后端HTTP服务，ContentTypeCatagory的值为DEFAULT或者CUSTOM时，ContentType头的取值。|无|
|FcBaseUrl|String|否|是|触发器地址。|以`http://`或`https://`开头。|
|FcType|String|否|是|函数类型。|取值：-   FCEvent（默认值）。
-   HttpTrigger。 |
|Method|String|否|是|HTTP请求方式。|取值： -   GET（默认值）
-   POST
-   DELETE
-   PUT
-   HEAD
-   PATCH
-   OPTIONS
-   ANY |
|OnlyBusinessPath|Boolean|否|是|是否只传递自定义的后端请求路径给后端。|取值：-   true
-   false |
|Path|String|否|是|后端请求路径。|参数必须放在方括号中，例如：`/ getUserInfo / [userId]`。|

## MockHeaders语法

```
"MockHeaders": [
  {
    "HeaderValue": String,
    "HeaderName": String
  }
]    
```

## MockHeaders属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|HeaderName|String|是|是|响应头名称。|无|
|HeaderValue|String|是|是|响应头值。|无|

## 返回值

Fn::GetAtt

ApiId：API ID。

## 示例

`JSON`格式

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

`YAML`格式

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

更多示例，请参见创建API、创建应用、为API授权应用的访问权限、发布API或快速切换API版本、创建后端签名密钥、绑定API与后端签名密钥、创建用户自定义的流控策略和为API绑定用户自定义流控的组合示例：[JSON示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ApiGateway/JSON/Api.json)和[YAML示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ApiGateway/YAML/Api.yml)。

