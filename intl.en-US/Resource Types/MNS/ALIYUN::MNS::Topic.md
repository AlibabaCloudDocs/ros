# ALIYUN::MNS::Topic

ALIYUN::MNS::Topic is used to create a topic.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|TopicName|String|Yes|No|The name of the topic.|The name must be unique to an Alibaba Cloud account in a region. The name can be up to 256 characters in length and can contain letters, digits, and hyphens \(-\). It must start with a letter. |
|MaximumMessageSize|Integer|No|Yes|The maximum size of a message that can be sent to the topic.|Valid values: 1024 \(1 KB\) to 65536 \(64 KB\).

Unit: bytes.

Default value: 65536 \(64 KB\). |
|LoggingEnabled|Boolean|No|Yes|Specifies whether to enable the log management feature.|Default value: false. Valid values: -   true: enables the log management feature.
-   false: disables the log management feature. |

## Response parameters

Fn::GetAtt

-   TopicUrl: the URL of the created topic.
-   TopicName: the name of the created topic.
-   ARN.WithSlash: The ARN of the created topic.

## Examples

`JSON` format

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

`YAML` format

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

