# ALIYUN::ECS::Invocation

ALIYUN::ECS::Invocation类型用于为一台或多台ECS实例触发一条云助手命令。

## 语法

```
{
  "Type": "ALIYUN::ECS::Invocation",
  "Properties": {
    "Timed": Boolean,
    "Frequency": String,
    "CommandId": String,
    "Parameters": Map,
    "InstanceIds": List
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Timed|Boolean|否|否|命令是否为周期执行。|取值： -   true
-   false（默认值） |
|Frequency|String|否|否|周期任务的执行周期。该参数值结构以[Cron 表达式](https://www.alibabacloud.com/help/faq-detail/64769.htm)为准。|两次周期任务的时间间隔不能低于10秒。当Timed的值为true时，Frequency必填。|
|CommandId|String|是|否|命令ID。|无|
|InstanceIds|List|是|否|执行命令的实例列表。|最多能指定50台实例ID。|
|Parameters|Map|否|否|启用自定义参数功能时，执行命令时传入的自定义参数的键值对。示例值：`{"name": "Jack", "accessKey": "LTAIdyv******aRY"}`。|自定义参数的取值范围：0~10。 Map的键不允许为空字符串，最多支持64个字符。Map的值允许为空字符串。

自定义参数与原始命令内容在Base64编码后，综合长度不能超过16KB。

设置的自定义参数名集合必须为创建命令时定义的参数集的子集。对于未传入的参数，您可以使用空字符串代替。 |

## 返回值

Fn::GetAtt

InvokeId：命令进程执行ID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Parameters": {
      "Type": "Json",
      "Description": "The key-value pairs of custom parameters passed in when the script contains custom parameters.\nNumber of custom parameters: 0 to 10.\nThe key cannot be an empty string. It can be up to 64 characters in length.\nThe value can be an empty string.\nAfter the custom parameters and the original script content are Base64 encoded, the total size cannot exceed 16 KB.\nThe set of custom parameter names must be a subset of the parameter set that is defined when you created the script. You can use an empty string to represent the parameters that are not passed in.\nDefault value: null, indicating that this parameter is canceled and customer parameters are disabled.",
      "MaxLength": 10
    },
    "Timed": {
      "Type": "Boolean",
      "Description": "Whether it is timed execution. Default is False.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "Frequency": {
      "Type": "String",
      "Description": "The frequency of timing execution (the shortest frequency is performed every 1 minute). It iss mandatory when Timing is True.The value rule follows the rules of the cron expression. "
    },
    "CommandId": {
      "Type": "String",
      "Description": "The id of command."
    },
    "InstanceIds": {
      "Type": "CommaDelimitedList",
      "Description": "The instance id list. Select up to 20 instances at a time.Instances status must be running."
    }
  },
  "Resources": {
    "Invocation": {
      "Type": "ALIYUN::ECS::Invocation",
      "Properties": {
        "Parameters": {
          "Ref": "Parameters"
        },
        "Timed": {
          "Ref": "Timed"
        },
        "Frequency": {
          "Ref": "Frequency"
        },
        "CommandId": {
          "Ref": "CommandId"
        },
        "InstanceIds": {
          "Ref": "InstanceIds"
        }
      }
    }
  },
  "Outputs": {
    "InvokeId": {
      "Description": "The id of command execution.",
      "Value": {
        "Fn::GetAtt": [
          "Invocation",
          "InvokeId"
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
  Parameters:
    Type: Json
    Description: >-
      The key-value pairs of custom parameters passed in when the script
      contains custom parameters.
      Number of custom parameters: 0 to 10.
      The key cannot be an empty string. It can be up to 64 characters in
      length.
      The value can be an empty string.
      After the custom parameters and the original script content are Base64
      encoded, the total size cannot exceed 16 KB.
      The set of custom parameter names must be a subset of the parameter set
      that is defined when you created the script. You can use an empty string
      to represent the parameters that are not passed in.
      Default value: null, indicating that this parameter is canceled and
      customer parameters are disabled.
    MaxLength: 10
  Timed:
    Type: Boolean
    Description: Whether it is timed execution. Default is False.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
  Frequency:
    Type: String
    Description: >-
      The frequency of timing execution (the shortest frequency is performed
      every 1 minute). It iss mandatory when Timing is True.The value rule
      follows the rules of the cron expression.
  CommandId:
    Type: String
    Description: The id of command.
  InstanceIds:
    Type: CommaDelimitedList
    Description: >-
      The instance id list. Select up to 20 instances at a time.Instances status
      must be running.
Resources:
  Invocation:
    Type: 'ALIYUN::ECS::Invocation'
    Properties:
      Parameters:
        Ref: Parameters
      Timed:
        Ref: Timed
      Frequency:
        Ref: Frequency
      CommandId:
        Ref: CommandId
      InstanceIds:
        Ref: InstanceIds
Outputs:
  InvokeId:
    Description: The id of command execution.
    Value:
      'Fn::GetAtt':
        - Invocation
        - InvokeId
```

