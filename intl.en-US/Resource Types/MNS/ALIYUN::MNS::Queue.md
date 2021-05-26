# ALIYUN::MNS::Queue

ALIYUN::MNS::Queue is used to create a queue to contain messages. Queues can be classified into standard and delayed queues.

If the DelaySeconds parameter is not specified when messages are sent, messages that are sent to standard queues can be immediately consumed. However, messages that are sent to delayed queues can be consumed only after the preset delay time.

## Syntax

```
{
  "Type": "ALIYUN::MNS::Queue",
  "Properties": {
    "PollingWaitSeconds": Integer,
    "LoggingEnabled": Boolean,
    "MessageRetentionPeriod": Integer,
    "MaximumMessageSize": Integer,
    "DelaySeconds": Integer,
    "VisibilityTimeout": Integer,
    "QueueName": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|QueueName|String|Yes|No|The name of the MNS queue.|The name must be unique to an Alibaba Cloud account in a region. The name can be up to 256 characters in length and can contain letters, digits, and hyphens \(-\). It must start with a letter or digit. |
|DelaySeconds|Integer|No|Yes|The delay time after which all messages that are sent to the queue can be consumed.|Valid values: 0 to 604800 \(7 days\). Unit: seconds.

Default value: 0. |
|MaximumMessageSize|Integer|No|Yes|The maximum size of a message that can be sent to the queue.|Valid values: 1024 \(1 KB\) to 65536 \(64 KB\). Unit: bytes.

Default value: 65536 \(64 KB\). |
|MessageRetentionPeriod|Integer|No|Yes|The maximum lifetime of a message in the queue. After the time that is specified by this parameter expires, the message is deleted, regardless of whether the message has been consumed.|Valid values: 60 \(1 minute\) to 604800 \(7 days\). Unit: seconds.

Default value: 345600 \(4 days\). |
|VisibilityTimeout|Integer|No|Yes|The duration for which a message stays in the Inactive state after it is consumed from the queue.|Valid values: 1 to 43200 \(12 hours\). Unit: seconds.

Default value: 30. |
|PollingWaitSeconds|Integer|No|Yes|The maximum time period that a ReceiveMessage request can wait till a message is in the queue.|Valid values: 0 to 10.

Unit: seconds.

Default value: 0. |
|LoggingEnabled|Boolean|No|Yes|Specifies whether to enable the log management feature.|Default value: false. Valid values: -   true: The log management feature is enabled.
-   false: The log management feature is disabled. |

## Response parameters

Fn::GetAtt

-   QueueUrl: the URL of the queue.
-   ARN.WithSlash: the ARN of the queue.
-   QueueName: the name of the queue.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "DelaySeconds": {
      "Type": "Number",
      "Description": "It is measured in seconds. All messages sent to the queue can be consumed until the DelaySeconds expires.\nAn integer between 0 and 604800 (7 days). The default value is 0",
      "MinValue": 0,
      "MaxValue": 604800,
      "Default": 0
    },
    "PollingWaitSeconds": {
      "Type": "Number",
      "Description": "It is the maximum time that a ReceiveMessage request could be waiting for any incoming messages, while there are no message in the queue. Measured in seconds.\nAn integer between 0 and 30 seconds. The default value is 0 (seconds)",
      "MinValue": 0,
      "MaxValue": 30,
      "Default": 0
    },
    "MessageRetentionPeriod": {
      "Type": "Number",
      "Description": "Maximum lifetime of the message in the queue, measured in seconds. After the time specified by this parameter expires, the message will be deleted no matter whether it has been consumed or not.\nAn integer between 60 (1 minute) and 1296000 (15 days). The default value is 345600 (4 days)",
      "MinValue": 60,
      "MaxValue": 604800,
      "Default": 345600
    },
    "MaximumMessageSize": {
      "Type": "Number",
      "Description": "Maximum body length of a message sent to the queue, measured in bytes.\nAn integer between 1024 (1K) and 65536 (64K). The default value is 65536 (64K).",
      "MinValue": 1024,
      "MaxValue": 65536,
      "Default": 65536
    },
    "VisibilityTimeout": {
      "Type": "Number",
      "Description": "Duration in which a message stays in Inactive status after it is consumed from the queue. Measured in seconds.\nAn integer between 1 and 43200 (12 hours). The default value is 30 (seconds)",
      "MinValue": 1,
      "MaxValue": 43200,
      "Default": 30
    },
    "QueueName": {
      "Type": "String",
      "Description": "Queue name",
      "MinLength": 1,
      "MaxLength": 256
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
    }
  },
  "Resources": {
    "Queue": {
      "Type": "ALIYUN::MNS::Queue",
      "Properties": {
        "DelaySeconds": {
          "Ref": "DelaySeconds"
        },
        "PollingWaitSeconds": {
          "Ref": "PollingWaitSeconds"
        },
        "MessageRetentionPeriod": {
          "Ref": "MessageRetentionPeriod"
        },
        "MaximumMessageSize": {
          "Ref": "MaximumMessageSize"
        },
        "VisibilityTimeout": {
          "Ref": "VisibilityTimeout"
        },
        "QueueName": {
          "Ref": "QueueName"
        },
        "LoggingEnabled": {
          "Ref": "LoggingEnabled"
        }
      }
    }
  },
  "Outputs": {
    "QueueName": {
      "Description": "Queue name",
      "Value": {
        "Fn::GetAtt": [
          "Queue",
          "QueueName"
        ]
      }
    },
    "ARN": {
      "Description": "The ARN for ALIYUN::ROS::CustomResource",
      "Value": {
        "Fn::GetAtt": [
          "Queue",
          "ARN"
        ]
      }
    },
    "ARN.WithSlash": {
      "Description": "The ARN: acs:mns:$region:$accountid:/queues/$queueName",
      "Value": {
        "Fn::GetAtt": [
          "Queue",
          "ARN.WithSlash"
        ]
      }
    },
    "QueueUrl": {
      "Description": "URL of created queue",
      "Value": {
        "Fn::GetAtt": [
          "Queue",
          "QueueUrl"
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
  DelaySeconds:
    Default: 0
    Description: 'It is measured in seconds. All messages sent to the queue can be
      consumed until the DelaySeconds expires.

      An integer between 0 and 604800 (7 days). The default value is 0'
    MaxValue: 604800
    MinValue: 0
    Type: Number
  LoggingEnabled:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Default: false
    Description: "Whether to enable log management. \"true\" indicates that log management\
      \ is enabled, whereas \"false\" indicates that log management is disabled. \n\
      The default value is false"
    Type: Boolean
  MaximumMessageSize:
    Default: 65536
    Description: 'Maximum body length of a message sent to the queue, measured in
      bytes.

      An integer between 1024 (1K) and 65536 (64K). The default value is 65536 (64K).'
    MaxValue: 65536
    MinValue: 1024
    Type: Number
  MessageRetentionPeriod:
    Default: 345600
    Description: 'Maximum lifetime of the message in the queue, measured in seconds.
      After the time specified by this parameter expires, the message will be deleted
      no matter whether it has been consumed or not.

      An integer between 60 (1 minute) and 1296000 (15 days). The default value is
      345600 (4 days)'
    MaxValue: 604800
    MinValue: 60
    Type: Number
  PollingWaitSeconds:
    Default: 0
    Description: 'It is the maximum time that a ReceiveMessage request could be waiting
      for any incoming messages, while there are no message in the queue. Measured
      in seconds.

      An integer between 0 and 30 seconds. The default value is 0 (seconds)'
    MaxValue: 30
    MinValue: 0
    Type: Number
  QueueName:
    Description: Queue name
    MaxLength: 256
    MinLength: 1
    Type: String
  VisibilityTimeout:
    Default: 30
    Description: 'Duration in which a message stays in Inactive status after it is
      consumed from the queue. Measured in seconds.

      An integer between 1 and 43200 (12 hours). The default value is 30 (seconds)'
    MaxValue: 43200
    MinValue: 1
    Type: Number
Resources:
  Queue:
    Properties:
      DelaySeconds:
        Ref: DelaySeconds
      LoggingEnabled:
        Ref: LoggingEnabled
      MaximumMessageSize:
        Ref: MaximumMessageSize
      MessageRetentionPeriod:
        Ref: MessageRetentionPeriod
      PollingWaitSeconds:
        Ref: PollingWaitSeconds
      QueueName:
        Ref: QueueName
      VisibilityTimeout:
        Ref: VisibilityTimeout
    Type: ALIYUN::MNS::Queue
Outputs:
  ARN:
    Description: The ARN for ALIYUN::ROS::CustomResource
    Value:
      Fn::GetAtt:
      - Queue
      - ARN
  ARN.WithSlash:
    Description: 'The ARN: acs:mns:$region:$accountid:/queues/$queueName'
    Value:
      Fn::GetAtt:
      - Queue
      - ARN.WithSlash
  QueueName:
    Description: Queue name
    Value:
      Fn::GetAtt:
      - Queue
      - QueueName
  QueueUrl:
    Description: URL of created queue
    Value:
      Fn::GetAtt:
      - Queue
      - QueueUrl
```

For more examples, visit [Subscription.json](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/MNS/JSON/Subscription.json) and [Subscription.yml](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/MNS/YAML/Subscription.yml). In the examples, the ALIYUN::MNS::Topic, ALIYUN::MNS::Queue, and ALIYUN::MNS::Subscription resource types are involved.

