# ALIYUN::FC::FunctionInvoker {#concept_186391 .concept}

ALIYUN::FC::FunctionInvoker 类型用于主动执行函数。

## 语法 {#section_kob_3dx_ii2 .section}

``` {#codeblock_qvl_ezc_106 .language-json}
{
  "Type": "ALIYUN::FC::FunctionInvoker",
  "Properties": {
    "Qualifier": String,
    "ServiceName": String,
    "ExecuteVersion": Integer,
    "Async": Boolean,
    "Event": String,
    "FunctionName": String
  }
}
```

## 属性 {#section_hzr_gxr_88m .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ServiceName|String|是|是|service名称。|长度为1-128字符。|
|FunctionName|String|是|是|function名称。|无|
|Async|Boolean|否|是|是否异步调用，默认False。|无|
|Event|String|否|是|该属性在函数执行时会被编码为utf-8字符串传递给函数。如果需要传递二进制或其他编码的字符串，可以先使用base64进行编码，再传递给该属性。|无|
|Qualifier|String|否|是|service版本, 可以是versionId或者aliasName。|无|
|ExecuteVersion|Integer|否|是| 创建该资源时，如果不指定该属性，则不会触发函数调用，否则触发函数调用。

 更新该资源时，如果该属性发生了变化，且变化后的值为整数，则触发函数调用，否则不触发函数调用。

 |无|

## 返回值 {#section_118_83r_kqk .section}

**Fn::GetAtt**

-   ResultType：取值如下：

    NoResult：Async为true时，没有调用结果。

    Success：Async为false时，且执行成功。

    Failure：Async为false时，且执行失败。

-   Result：依赖于ResultType：

    NoResult：空值。

    Success：invoke function返回的结果，字符串，具体内容由用户解释。要求返回的结果必须是utf-8编码的字符串，否则ROS会认为函数执行失败。如果要返回二进制或其他编码的字符串，可以在返回前使用base64进行编码。

    Failure：报错信息。


## 示例 {#section_d5t_sdt_xy2 .section}

``` {#codeblock_liy_4w5_fc1 .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "FunctionInvoker": {
      "Type": "ALIYUN::FC::FunctionInvoker",
      "Properties": {
        "FunctionName": {
          "Ref": "FunctionName"
        },
        "ServiceName": {
          "Ref": "ServiceName"
        },
        "ExecuteVersion": {
          "Ref": "ExecuteVersion"
        },
        "Async": {
          "Ref": "Async"
        },
        "Event": {
          "Ref": "Event"
        },
        "Qualifier": {
          "Ref": "Qualifier"
        }
      }
    }
  },
  "Parameters": {
    "FunctionName": {
      "Type": "String",
      "Description": "Function name"
    },
    "ServiceName": {
      "MinLength": 1,
      "Type": "String",
      "Description": "Service name",
      "MaxLength": 128
    },
    "ExecuteVersion": {
      "Type": "Number",
      "Description": "If the property is not specified for creation and update, the function will not be invoked. The change of the property leads to the invoke of the function."
    },
    "Async": {
      "Default": false,
      "Type": "Boolean",
      "Description": "Invocation type, Sync or Async. Defaults to Sync.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "Event": {
      "Type": "String",
      "Description": "Event, binary type. This value is passed to function without any transformation. It\u2019s function\u2019s responsibility to interpret the value.\nUse Fn::Base64Decode to pass value if needed."
    },
    "Qualifier": {
      "Type": "String",
      "Description": "service version, can be versionId or aliasName"
    }
  },
  "Outputs": {
    "ResultType": {
      "Description": "Result type:\nNoResult: Async invoke has no result.\nSuccess: Sync invoke succeeds.\nFailure: Sync invoke fails.",
      "Value": {
        "Fn::GetAtt": [
          "FunctionInvoker",
          "ResultType"
        ]
      }
    },
    "Result": {
      "Description": "Depends on result type:\nNoResult: Async invoke has no result.\nSuccess: The response of run function. It\u2019s in binary format. Users can interpret the data according to their function implementation.\nFailure: Error Message.",
      "Value": {
        "Fn::GetAtt": [
          "FunctionInvoker",
          "Result"
        ]
      }
    }
  }
}
```

