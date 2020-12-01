# Aliyun::Serverless::MNSTopic

Aliyun::Serverless::MNSTopic is used to create a Message Service \(MNS\) topic.

## Syntax

```
{
  "Type": "Aliyun::Serverless::MNSTopic",
  "Properties": {
    "LoggingEnabled": Boolean,
    "MaximumMessageSize": Integer
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|MaximumMessageSize|Integer|No|Yes|The maximum size of a message that is to be sent to the topic.|Valid values: 1024 \(1 KB\) to 65536 \(64 KB\).

Unit: bytes.

Default value: 65536 \(64 KB\). |
|LoggingEnabled|Boolean|No|Yes|Specifies whether to enable the log management feature.|Default value: false. Valid values: -   true: enables the log management feature.
-   false: disables the log management feature. |

## Response parameters

Fn::GetAtt

-   TopicUrl: the URL of the topic.
-   TopicName: the name of the topic.
-   ARN.WithSlash: the Alibaba Cloud Resource Name \(ARN\) of the topic.

## Examples

`JSON` format

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Transform": "Aliyun::Serverless-2018-04-03",
  "Resources": {
    "MnsTopic": {
      "Type": "Aliyun::Serverless::MNSTopic",
      "Properties": {
        "MaximumMessageSize": 2048,
        "LoggingEnabled": false
      }
    }
  },
  "Outputs": {
    "TopicUrl": {
      "Value": {
        "Fn::GetAtt": [
          "MnsTopic",
          "TopicUrl"
        ]
      }
    },
    "TopicName": {
      "Value": {
        "Fn::GetAtt": [
          "MnsTopic",
          "TopicName"
        ]
      }
    },
    "ARN.WithSlash": {
      "Value": {
        "Fn::GetAtt": [
          "MnsTopic",
          "ARN.WithSlash"
        ]
      }
    }
  }
}
```

`YAML` format

```
ROSTemplateFormatVersion: '2015-09-01'
Transform: 'Aliyun::Serverless-2018-04-03'
Resources:
  MnsTopic:
    Type: 'Aliyun::Serverless::MNSTopic'
    Properties:
      MaximumMessageSize: 2048
      LoggingEnabled: false
Outputs:
  TopicUrl:
    Value:
      'Fn::GetAtt':
        - MnsTopic
        - TopicUrl
  TopicName:
    Value:
      'Fn::GetAtt':
        - MnsTopic
        - TopicName
  ARN.WithSlash:
    Value:
      'Fn::GetAtt':
        - MnsTopic
        - ARN.WithSlash
```

