# ALIYUN::MNS::Queue {#concept_188112 .concept}

ALIYUN::MNS::Queue is used to create a queue to contain messages. Queues can be classified into standard queues and delayed queues.

If the DelaySeconds parameter is not specified when messages are sent, messages sent to standard queues can be consumed immediately. However, messages sent to delayed queues can be consumed only after the preset delay time.

## Syntax {#section_lhz_ra1_s8p .section}

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

## Properties { .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|QueueName|String|Yes|No|The name of the queue.| The name must be unique to an Alibaba Cloud account in a region. The name can be up to 256 characters in length and can contain letters, digits, and hyphens \(-\). It must start with a letter or digit.

 |
|DelaySeconds|Integer|No|Yes|The delay time after which all messages sent to the queue can be consumed. Unit: second.|The parameter value must be an integer in the range of 0 to 604800 \(7 days\). Default value: 0.|
|MaximumMessageSize|Integer|No|Yes|The maximum body length of a message sent to the queue. Unit: byte.|The parameter value must be an integer in the range of 1024 \(1 KB\) to 65536 \(64 KB\). Default value: 65536 \(64 KB\).|
|MessageRetentionPeriod|Integer|No|No|The maximum lifetime of a message in the queue. After the time specified by this parameter expires, the message will be deleted, regardless of whether the message has been consumed. Unit: second.|The parameter value must be an integer in the range of 60 \(1 minute\) to 604800 \(7 days\). Default value: 345600 \(4 days\).|
|VisibilityTimeout|Integer|No|Yes|The duration in which a message stays in the Inactive state after it is consumed from the queue. Unit: second.|The parameter value must be an integer in the range of 1 to 43200 \(12 hours\). Default value: 30.|
|PollingWaitSeconds|Integer|No|Yes|The maximum time that a ReceiveMessage request can wait until a message is in the queue. Unit: second.| The parameter value must be an integer in the range of 0 to 30. Default value: 0.

 |
|LoggingEnabled|Boolean|No|Yes|Indicates whether to enable log management. Valid values: True and False.|Default value: False.|

## Response parameters {#section_7q9_79e_vi5 .section}

**Fn::GetAtt**

QueueUrl: The URL of the created queue.

## Examples { .section}

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
      "Description": "It is the maximum time that a ReceiveMessage request could be waiting for any incoming messages, while there is no message in the queue. Measured in seconds.\nAn integer between 0 and 30 seconds. The default value is 0 (seconds)",
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
      "Description": "Maximum lifetime of the message in the queue, measured in seconds. After the time specified by this parameter expires, the message will be deleted regardless of whether it has been consumed.\nAn integer between 60 (1 minute) and 1296000 (15 days). The default value is 345600 (4 days)",
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

