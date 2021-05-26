# ALIYUN::MNS::Subscription

ALIYUN::MNS::Subscription is used to subscribe an endpoint to an Alibaba Cloud Message Service \(MNS\) topic. For a subscription to be created, the owner of the endpoint must confirm the subscription.

## Syntax

```
{
  "Type": "ALIYUN::MNS::Subscription",
  "Properties": {
    "Endpoint": String,
    "NotifyStrategy": String,
    "FilterTag": String,
    "NotifyContentFormat": String,
    "SubscriptionName": String,
    "TopicName": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|TopicName|String|Yes|No|The name of the topic.|The topic name must be unique within an Alibaba Cloud account in a region.

The name can be up to 256 characters in length and can contain letters, digits, and hyphens \(-\). It must start with a letter. |
|SubscriptionName|String|Yes|No|The name of the subscription.|The name can be up to 256 characters in length and can contain letters, digits, and hyphens \(-\). It must start with a letter.|
|Endpoint|String|Yes|No|The endpoint that the subscriber uses to receive messages.|Valid values: -   HttpEndpoint: This type of endpoints must be prefixed with `http://`.
-   QueueEndpoint: This type of endpoints must be in the `acs:mns:{REGION}:{AccountID}:queues/{QueueName}` format.
-   MailEndpoint: This type of endpoints must be in the `mail:directmail:{MailAddress}` format.
-   SmsEndpoint: This type of endpoints must be in the `sms:directsms:anonymous` or `sms:directsms:{Phone}` format. |
|FilterTag|String|No|No|The message filtering tag in the subscription.|The parameter value can be up to 16 characters in length. By default, no messages are filtered. **Note:** Only messages that have consistent tags are pushed. |
|NotifyStrategy|String|No|Yes|The retry policy that is applied when an error occurs when message is delivered to the endpoint.|Default value: BACKOFF\_RETRY. Valid values: -   BACKOFF\_RETRY
-   EXPONENTIAL\_DECAY\_RETRY |
|NotifyContentFormat|String|No|No|The format of the message content pushed to the endpoint.|Default value: XML. Valid values: -   XML
-   JSON
-   SIMPLIFIED |

## Response parameters

Fn::GetAtt

-   SubscriptionUrl: the URL of the created subscription.
-   SubscriptionName: the name of the subscription.
-   TopicName: the name of the topic.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Endpoint": {
      "Type": "String",
      "Description": "Terminal address of the message recipient for the created subscription.\nCurrently, four types of endpoints are supported: \n1. HttpEndpoint, which must be prefixed with \"http://\"; \n2. QueueEndpoint, in the format of acs:mns:{REGION}:{AccountID}:queues/{QueueName}; \n3. MailEndpoint, in the format of mail:directmail:{MailAddress}; \n4. SmsEndpoint, in the format of sms:directsms:anonymous or sms:directsms:{Phone}."
    },
    "NotifyStrategy": {
      "Type": "String",
      "Description": "Retry policy that will be applied when an error occurs during message push to the endpoint.\nBACKOFF_RETRY or EXPONENTIAL_DECAY_RETRY; default value: BACKOFF_RETRY. For details about retry policies, refer to Basic Concepts/NotifyStrategy.",
      "AllowedValues": [
        "BACKOFF_RETRY",
        "EXPONENTIAL_DECAY_RETRY"
      ],
      "Default": "BACKOFF_RETRY"
    },
    "NotifyContentFormat": {
      "Type": "String",
      "Description": "Format of the message content pushed to the endpoint.\nXML, JSON, or SIMPLIFIED; default value: XML. For details about message formats, refer to Basic Concepts/NotifyContentFormat.",
      "AllowedValues": [
        "XML",
        "JSON",
        "SIMPLIFIED"
      ],
      "Default": "XML"
    },
    "FilterTag": {
      "Type": "String",
      "Description": "Message filter tag in the created subscription (Only messages with consistent tags are pushed.)\nThe value is a string of no more than 16 characters. The default value is no message filter.",
      "MaxLength": 16
    },
    "SubscriptionName": {
      "Type": "String",
      "Description": "Subscription name",
      "MinLength": 1,
      "MaxLength": 256
    },
    "TopicName": {
      "Type": "String",
      "Description": "Topic name",
      "MinLength": 1,
      "MaxLength": 256
    }
  },
  "Resources": {
    "Subscription": {
      "Type": "ALIYUN::MNS::Subscription",
      "Properties": {
        "Endpoint": {
          "Ref": "Endpoint"
        },
        "NotifyStrategy": {
          "Ref": "NotifyStrategy"
        },
        "NotifyContentFormat": {
          "Ref": "NotifyContentFormat"
        },
        "FilterTag": {
          "Ref": "FilterTag"
        },
        "SubscriptionName": {
          "Ref": "SubscriptionName"
        },
        "TopicName": {
          "Ref": "TopicName"
        }
      }
    }
  },
  "Outputs": {
    "SubscriptionUrl": {
      "Description": "URL of created subscription",
      "Value": {
        "Fn::GetAtt": [
          "Subscription",
          "SubscriptionUrl"
        ]
      }
    },
    "SubscriptionName": {
      "Description": "Subscription name",
      "Value": {
        "Fn::GetAtt": [
          "Subscription",
          "SubscriptionName"
        ]
      }
    },
    "TopicName": {
      "Description": "Topic name",
      "Value": {
        "Fn::GetAtt": [
          "Subscription",
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
  Endpoint:
    Description: "Terminal address of the message recipient for the created subscription.\n\
      Currently, four types of endpoints are supported: \n1. HttpEndpoint, which must\
      \ be prefixed with \"http://\"; \n2. QueueEndpoint, in the format of acs:mns:{REGION}:{AccountID}:queues/{QueueName};\
      \ \n3. MailEndpoint, in the format of mail:directmail:{MailAddress}; \n4. SmsEndpoint,\
      \ in the format of sms:directsms:anonymous or sms:directsms:{Phone}."
    Type: String
  FilterTag:
    Description: 'Message filter tag in the created subscription (Only messages with
      consistent tags are pushed.)

      The value is a string of no more than 16 characters. The default value is no
      message filter.'
    MaxLength: 16
    Type: String
  NotifyContentFormat:
    AllowedValues:
    - XML
    - JSON
    - SIMPLIFIED
    Default: XML
    Description: 'Format of the message content pushed to the endpoint.

      XML, JSON, or SIMPLIFIED; default value: XML. For details about message formats,
      refer to Basic Concepts/NotifyContentFormat.'
    Type: String
  NotifyStrategy:
    AllowedValues:
    - BACKOFF_RETRY
    - EXPONENTIAL_DECAY_RETRY
    Default: BACKOFF_RETRY
    Description: 'Retry policy that will be applied when an error occurs during message
      push to the endpoint.

      BACKOFF_RETRY or EXPONENTIAL_DECAY_RETRY; default value: BACKOFF_RETRY. For
      details about retry policies, refer to Basic Concepts/NotifyStrategy.'
    Type: String
  SubscriptionName:
    Description: Subscription name
    MaxLength: 256
    MinLength: 1
    Type: String
  TopicName:
    Description: Topic name
    MaxLength: 256
    MinLength: 1
    Type: String
Resources:
  Subscription:
    Properties:
      Endpoint:
        Ref: Endpoint
      FilterTag:
        Ref: FilterTag
      NotifyContentFormat:
        Ref: NotifyContentFormat
      NotifyStrategy:
        Ref: NotifyStrategy
      SubscriptionName:
        Ref: SubscriptionName
      TopicName:
        Ref: TopicName
    Type: ALIYUN::MNS::Subscription
Outputs:
  SubscriptionName:
    Description: Subscription name
    Value:
      Fn::GetAtt:
      - Subscription
      - SubscriptionName
  SubscriptionUrl:
    Description: URL of created subscription
    Value:
      Fn::GetAtt:
      - Subscription
      - SubscriptionUrl
  TopicName:
    Description: Topic name
    Value:
      Fn::GetAtt:
      - Subscription
      - TopicName
```

For more examples, visit [Subscription.json](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/MNS/JSON/Subscription.json) and [Subscription.yml](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/MNS/YAML/Subscription.yml). In the examples, the ALIYUN::MNS::Topic, ALIYUN::MNS::Queue, and ALIYUN::MNS::Subscription resource types are involved.

