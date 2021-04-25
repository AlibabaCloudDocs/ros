# ALIYUN::MNS::Queue

ALIYUN::MNS::Queue类型是消息存储的目的地，队列可以分成普通队列和延时队列两类。

如果发送消息时不指定消息延时参数，被发送到普通队列的消息可以立刻被消费，而发送到延时队列的消息需要经过设定的延时时间后才能被消费。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|QueueName|String|是|否|队列名称。|同一账号同一地域， 队列名称不能重复。 长度不超过256个字符，必须以英文字母或数字开头，可包含英文字母、数字和短划线（-）。 |
|DelaySeconds|Integer|否|是|发送到该队列的所有消息默认以DelaySeconds参数指定的秒数延后。|取值范围：0~604,800（7天）。 单位：秒。

默认值：0。 |
|MaximumMessageSize|Integer|否|是|发送到该队列消息体的最大长度。|取值范围：1024（1KB）~65,536（64KB）。 单位：byte。

默认值：65,536（64KB）。 |
|MessageRetentionPeriod|Integer|否|是|消息在该队列中最长的存活时间，从发送到该队列开始经过此参数指定的时间后，不论消息是否被取出过都将被删除。|取值范围：60（1分钟）~604,800（7 天） 。 单位：秒。

默认值：345,600（4 天）。 |
|VisibilityTimeout|Integer|否|是|消息从该队列中取出后从Active状态变成Inactive状态后的持续时间。|取值范围：1-43,200（12小时） 。 单位：秒。

默认值：30。 |
|PollingWaitSeconds|Integer|否|是|当队列中没有消息时，针对该队列的ReceiveMessage请求最长的等待时间。|取值范围：0~30。

单位：秒。

默认值：0。 |
|LoggingEnabled|Boolean|否|是|是否启用日志管理功能。|取值： -   true：启用。
-   false（默认值）：禁用。 |

## 返回值

Fn::GetAtt

-   QueueUrl：队列的URL。
-   ARN.WithSlash：队列的ARN。
-   QueueName：队列名称。

## 示例

`JSON`格式

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

`YAML`格式

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

更多示例，请参见创建主题、创建消息队列和描述订阅关系的组合示例：[JSON示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/MNS/JSON/Subscription.json)和[YAML示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/MNS/YAML/Subscription.yml)。

