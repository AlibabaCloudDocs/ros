# ALIYUN::MNS::Queue {#concept_188112 .concept}

ALIYUN::MNS::Queue类型是消息存储的目的地，队列可以分成普通队列和延时队列两类。

如果发送消息时不指定消息延时参数，被发送到普通队列的消息立刻可以被消费，而发送到延时队列需要经过设定的延时时间后才能被消费。

## 语法 {#section_lhz_ra1_s8p .section}

```language-json
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

## 属性 { .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|QueueName|String|是|否|队列名称。| 同一账号同一Region下， 队列名称不能重名;必须以英文字母或者数字开头，剩余名称可以是英文，数字，横划线，长度不超过256个字符。

 |
|DelaySeconds|Integer|否|是|发送到该 Queue 的所有消息默认将以DelaySeconds参数指定的秒数延后可被消费，单位为秒。|0-604800秒（7天）范围内某个整数值，默认值为0。|
|MaximumMessageSize|Integer|否|是|发送到该Queue的消息体的最大长度，单位为byte。|1024\(1KB\)-65536（64KB）范围内的某个整数值，默认值为65536（64KB）。|
|MessageRetentionPeriod|Integer|否|否|消息在该 Queue 中最长的存活时间，从发送到该队列开始经过此参数指定的时间后，不论消息是否被取出过都将被删除，单位为秒。|60 \(1分钟\)-604800 \(7 天\)范围内某个整数值，默认值345600 \(4 天\)。|
|VisibilityTimeout|Integer|否|是|消息从该 Queue 中取出后从Active状态变成Inactive状态后的持续时间，单位为秒。|1-43200\(12小时\)范围内的某个值整数值，默认为30（秒）。|
|PollingWaitSeconds|Integer|否|是|当 Queue 中没有消息时，针对该 Queue 的 ReceiveMessage 请求最长的等待时间，单位为秒。| 0-30秒范围内的某个整数值，默认为0（秒）。

 |
|LoggingEnabled|Boolean|否|是|是否开启日志管理功能，True表示启用，False表示停用。|可选值：True/False，默认为False。|

## 返回值 {#section_7q9_79e_vi5 .section}

**Fn::GetAtt**

QueueUrl：所创建的队列URL。

## 示例 { .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "Queue": {
      "Type": "ALIYUN::MNS::Queue",
      "Properties": {
        "PollingWaitSeconds": {
          "Ref": "PollingWaitSeconds"
        },
        "LoggingEnabled": {
          "Ref": "LoggingEnabled"
        },
        "MessageRetentionPeriod": {
          "Ref": "MessageRetentionPeriod"
        },
        "MaximumMessageSize": {
          "Ref": "MaximumMessageSize"
        },
        "DelaySeconds": {
          "Ref": "DelaySeconds"
        },
        "VisibilityTimeout": {
          "Ref": "VisibilityTimeout"
        },
        "QueueName": {
          "Ref": "QueueName"
        }
      }
    }
  },
  "Parameters": {
    "PollingWaitSeconds": {
      "Default": 0,
      "Type": "Number",
      "Description": "It is the maximum time that a ReceiveMessage request could be waiting for any incoming messages, while there are no message in the queue. Measured in seconds.\nAn integer between 0 and 30 seconds. The default value is 0 (seconds)",
      "MaxValue": 30,
      "MinValue": 0
    },
    "LoggingEnabled": {
      "Default": false,
      "Type": "Boolean",
      "Description": "Whether to enable log management. \"true\" indicates that log management is enabled, whereas \"false\" indicates that log management is disabled. \nThe default value is false",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "MessageRetentionPeriod": {
      "Default": 345600,
      "Type": "Number",
      "Description": "Maximum lifetime of the message in the queue, measured in seconds. After the time specified by this parameter expires, the message will be deleted no matter whether it has been consumed or not.\nAn integer between 60 (1 minute) and 1296000 (15 days). The default value is 345600 (4 days)",
      "MaxValue": 604800,
      "MinValue": 60
    },
    "MaximumMessageSize": {
      "Default": 65536,
      "Type": "Number",
      "Description": "Maximum body length of a message sent to the queue, measured in bytes.\nAn integer between 1024 (1K) and 65536 (64K). The default value is 65536 (64K).",
      "MaxValue": 65536,
      "MinValue": 1024
    },
    "DelaySeconds": {
      "Default": 0,
      "Type": "Number",
      "Description": "It is measured in seconds. All messages sent to the queue can be consumed until the DelaySeconds expires.\nAn integer between 0 and 604800 (7 days). The default value is 0",
      "MaxValue": 604800,
      "MinValue": 0
    },
    "VisibilityTimeout": {
      "Default": 30,
      "Type": "Number",
      "Description": "Duration in which a message stays in Inactive status after it is consumed from the queue. Measured in seconds.\nAn integer between 1 and 43200 (12 hours). The default value is 30 (seconds)",
      "MaxValue": 43200,
      "MinValue": 1
    },
    "QueueName": {
      "MinLength": 1,
      "Type": "String",
      "Description": "Queue name",
      "MaxLength": 256
    }
  },
  "Outputs": {
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

