# ALIYUN::MNS::Topic

ALIYUN::MNS::Topic类型用于创建主题。

## 语法

```
{
  "Type": "ALIYUN::MNS::Topic",
  "Properties": {
    "LoggingEnabled": Boolean,
    "TopicName": String,
    "MaximumMessageSize": Integer
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|TopicName|String|是|否|主题名称。|同一账号同一地域下，主题名称不能重复。 长度不超过256个字符。以英文字母开头，可包含英文字母、数字和短划线（-）。 |
|MaximumMessageSize|Integer|否|是|发送到该主题的消息体最大长度。|取值范围：1024（1KB）~65,536（64KB）。

单位：Byte。

默认值：65,536（64KB）。 |
|LoggingEnabled|Boolean|否|是|是否开启日志管理功能。|取值： -   true：启用。
-   false（默认值）：停用。 |

## 返回值

Fn::GetAtt

-   TopicUrl：所创建的主题的URL。
-   TopicName：主题名称。
-   ARN.WithSlash：主题的ARN。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "MaximumMessageSize": {
      "Type": "Number",
      "Description": "Maximum body length of a message sent to the topic, in the unit of bytes.\nAn integer in the range of 1,024 (1 KB) to 65, 536 (64 KB); default value: 65,536 (64 KB).",
      "MinValue": 1024,
      "MaxValue": 65536,
      "Default": 65536
    },
    "LoggingEnabled": {
      "Type": "Boolean",
      "Description": "Whether to enable log management. \"true\" indicates that log management is enabled, whereas \"false\" indicates that log management is disabled. \nThe default value is false",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ],
      "Default": false
    },
    "TopicName": {
      "Type": "String",
      "Description": "Topic name",
      "MinLength": 1,
      "MaxLength": 256
    }
  },
  "Resources": {
    "Topic": {
      "Type": "ALIYUN::MNS::Topic",
      "Properties": {
        "MaximumMessageSize": {
          "Ref": "MaximumMessageSize"
        },
        "LoggingEnabled": {
          "Ref": "LoggingEnabled"
        },
        "TopicName": {
          "Ref": "TopicName"
        }
      }
    }
  },
  "Outputs": {
    "TopicUrl": {
      "Description": "URL of created topic",
      "Value": {
        "Fn::GetAtt": [
          "Topic",
          "TopicUrl"
        ]
      }
    },
    "ARN": {
      "Description": "The ARN for ALIYUN::ROS::CustomResource",
      "Value": {
        "Fn::GetAtt": [
          "Topic",
          "ARN.WithSlash"
        ]
      }
    },
    "TopicName": {
      "Description": "Topic name",
      "Value": {
        "Fn::GetAtt": [
          "Topic",
          "TopicName"
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
  MaximumMessageSize:
    Type: Number
    Description: >-
      Maximum body length of a message sent to the topic, in the unit of bytes.

      An integer in the range of 1,024 (1 KB) to 65, 536 (64 KB); default value:
      65,536 (64 KB).
    MinValue: 1024
    MaxValue: 65536
    Default: 65536
  LoggingEnabled:
    Type: Boolean
    Description: >-
      Whether to enable log management. "true" indicates that log management is
      enabled, whereas "false" indicates that log management is disabled.

      The default value is false
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
    Default: false
  TopicName:
    Type: String
    Description: Topic name
    MinLength: 1
    MaxLength: 256
Resources:
  Topic:
    Type: 'ALIYUN::MNS::Topic'
    Properties:
      MaximumMessageSize:
        Ref: MaximumMessageSize
      LoggingEnabled:
        Ref: LoggingEnabled
      TopicName:
        Ref: TopicName
Outputs:
  TopicUrl:
    Description: URL of created topic
    Value:
      'Fn::GetAtt':
        - Topic
        - TopicUrl
  ARN:
    Description: 'The ARN for ALIYUN::ROS::CustomResource'
    Value:
      'Fn::GetAtt':
        - Topic
        - ARN.WithSlash
  TopicName:
    Description: Topic name
    Value:
      'Fn::GetAtt':
        - Topic
        - TopicName
```

