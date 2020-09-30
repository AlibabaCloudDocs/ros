# ALIYUN::FC::FunctionInvoker

ALIYUN::FC::FunctionInvoker类型用于主动执行函数。

## 语法

```
{
  "Type": "ALIYUN::FC::FunctionInvoker",
  "Properties": {
    "Qualifier": String,
    "ServiceName": String,
    "ExecuteVersion": Integer,
    "Async": Boolean,
    "Event": String,
    "FunctionName": String,
    "CheckError": Boolean,
    "ServiceRegionId": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ServiceName|String|是|是|服务名称。|长度为1~128个字符。|
|FunctionName|String|是|是|函数名称。|无|
|Async|Boolean|否|是|是否异步调用。|取值：-   true
-   false（默认值） |
|Event|String|否|是|用户自定义的函数入参。|该参数在函数执行时会被编码为UTF-8字符串传递给函数。如果需要传递二进制或其他编码的字符串，可以先使用Base64进行编码，再传递给该参数。|
|Qualifier|String|否|是|服务版本。|取值： -   versionId：版本号。
-   aliasName：别名。 |
|ExecuteVersion|Integer|否|是|创建该资源时，如果不指定该参数，则不会触发函数调用，否则触发函数调用。

更新该资源时，如果该参数发生了变化，且变化后的值为整数，则触发函数调用，否则不触发函数调用。

|无|
|CheckError|Boolean|否|否|是否检查调用结果。|取值： -   true

**说明：** 如果取值为true且函数调用结果为失败，则认为资源创建失败。

-   false（默认值） |
|ServiceRegionId|String|否|否|函数服务所属地域。|无|

## 返回值

Fn::GetAtt

-   ResultType：
    -   Async为true且ResultType为NoResult时，表示没有调用结果。
    -   Async为false且ResultType为Success时，表示执行成功。
    -   Async为false且ResultType为Failure时，表示执行失败。
-   Result：
    -   ResultType为NoResult时Result为空值。
    -   ResultType为Success时Result为invoke function返回的结果（字符串），具体内容由用户解释。要求返回的结果必须是UTF-8编码的字符串，否则ROS会认为函数执行失败。如果要返回二进制或其他编码的字符串，可以在返回前使用Base64进行编码。
    -   ResultType为Failure时Result为报错信息。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "FunctionName": {
      "Type": "String",
      "Description": "Function name"
    },
    "ExecuteVersion": {
      "Type": "Number",
      "Description": "If the property is not specified for creation and update, the function will not be invoked. The change of the property leads to the invoke of the function."
    },
    "ServiceRegionId": {
      "Type": "String",
      "Description": "Which region service belongs to."
    },
    "ServiceName": {
      "Type": "String",
      "Description": "Service name",
      "MinLength": 1,
      "MaxLength": 128
    },
    "Async": {
      "Type": "Boolean",
      "Description": "Invocation type, Sync or Async. Defaults to Sync.",
      "AllowedValues": [
        true,
        false
      ],
      "Default": false
    },
    "Event": {
      "Type": "String",
      "Description": "This value is passed to function as utf-8 encoded string.It’s function’s responsibility to interpret the value.\nIf the value needs to be binary, encode it via base64 before passing to this property."
    },
    "Qualifier": {
      "Type": "String",
      "Description": "service version, can be versionId or aliasName"
    },
    "CheckError": {
      "Type": "Boolean",
      "Description": "Whether check error for function invocation result.\nIf set true and function invocation result has error, the resource creation will be regard as failed.\nDefault is false",
      "AllowedValues": [
        true,
        false
      ]
    }
  },
  "Resources": {
    "FunctionInvoker": {
      "Type": "ALIYUN::FC::FunctionInvoker",
      "Properties": {
        "FunctionName": {
          "Ref": "FunctionName"
        },
        "ExecuteVersion": {
          "Ref": "ExecuteVersion"
        },
        "ServiceRegionId": {
          "Ref": "ServiceRegionId"
        },
        "ServiceName": {
          "Ref": "ServiceName"
        },
        "Async": {
          "Ref": "Async"
        },
        "Event": {
          "Ref": "Event"
        },
        "Qualifier": {
          "Ref": "Qualifier"
        },
        "CheckError": {
          "Ref": "CheckError"
        }
      }
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
      "Description": "Depends on result type:\nNoResult: Async invoke has no result.\nSuccess: The response of the function. The response should be utf-8 encoded string, otherwise ROS will report an error. If the response is binary, encode it via base64 before it is returned.\nFailure: Error Message.",
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

`YAML`格式

```
ROSTemplateFormatVersion: '2015-09-01'
Parameters:
  FunctionName:
    Type: String
    Description: Function name
  ExecuteVersion:
    Type: Number
    Description: >-
      If the property is not specified for creation and update, the function
      will not be invoked. The change of the property leads to the invoke of the
      function.
  ServiceRegionId:
    Type: String
    Description: Which region service belongs to.
  ServiceName:
    Type: String
    Description: Service name
    MinLength: 1
    MaxLength: 128
  Async:
    Type: Boolean
    Description: 'Invocation type, Sync or Async. Defaults to Sync.'
    AllowedValues:
      - true
      - false
    Default: false
  Event:
    Type: String
    Description: >-
      This value is passed to function as utf-8 encoded string.It’s function’s
      responsibility to interpret the value.

      If the value needs to be binary, encode it via base64 before passing to
      this property.
  Qualifier:
    Type: String
    Description: 'service version, can be versionId or aliasName'
  CheckError:
    Type: Boolean
    Description: >-
      Whether check error for function invocation result.

      If set true and function invocation result has error, the resource
      creation will be regard as failed.

      Default is false
    AllowedValues:
      - true
      - false
Resources:
  FunctionInvoker:
    Type: 'ALIYUN::FC::FunctionInvoker'
    Properties:
      FunctionName:
        Ref: FunctionName
      ExecuteVersion:
        Ref: ExecuteVersion
      ServiceRegionId:
        Ref: ServiceRegionId
      ServiceName:
        Ref: ServiceName
      Async:
        Ref: Async
      Event:
        Ref: Event
      Qualifier:
        Ref: Qualifier
      CheckError:
        Ref: CheckError
Outputs:
  ResultType:
    Description: |-
      Result type:
      NoResult: Async invoke has no result.
      Success: Sync invoke succeeds.
      Failure: Sync invoke fails.
    Value:
      'Fn::GetAtt':
        - FunctionInvoker
        - ResultType
  Result:
    Description: >-
      Depends on result type:

      NoResult: Async invoke has no result.

      Success: The response of the function. The response should be utf-8
      encoded string, otherwise ROS will report an error. If the response is
      binary, encode it via base64 before it is returned.

      Failure: Error Message.
    Value:
      'Fn::GetAtt':
        - FunctionInvoker
        - Result
```

