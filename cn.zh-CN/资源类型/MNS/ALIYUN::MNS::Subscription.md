# ALIYUN::MNS::Subscription

ALIYUN::MNS::Subscription类型用于描述一个订阅关系，包括被订阅的主题和接收消息的终端地址（Endpoint）。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|TopicName|String|是|否|主题名称。|同一账号同一地域下，主题名称不能重复。

长度不超过256个字符。必须以英文字母开头，可包含英文字母、数字和短划线（-）。 |
|SubscriptionName|String|是|否|订阅名称。|长度不超过256个字符。必须以英文字母开头，可包含英文字母、数字和短划线（-）。|
|Endpoint|String|是|否|此次订阅中接收消息的终端地址。|取值： -   HttpEndpoint：必须以`http://`作为前缀。
-   QueueEndpoint：格式为`acs:mns:{REGION}:{AccountID}:queues/{QueueName}`。
-   MailEndpoint：格式为`mail:directmail:{MailAddress}`。
-   SmsEndpoint：格式为`sms:directsms:anonymous`或`sms:directsms:{Phone}`。 |
|FilterTag|String|否|否|此次订阅中消息过滤的标签。|不超过16个字符，默认不进行消息过滤。 **说明：** 标签一致的消息才会被推送。 |
|NotifyStrategy|String|否|是|向Endpoint推送消息出现错误时的重试策略。|取值： -   BACKOFF\_RETRY（默认值）
-   EXPONENTIAL\_DECAY\_RETRY

重试策略详情，请参见[NotifyStrategy](https://help.aliyun.com/document_detail/27481.html)。|
|NotifyContentFormat|String|否|否|向Endpoint推送的消息格式。|取值： -   XML（默认值）
-   JSON
-   SIMPLIFIED

消息格式详情，请参见[NotifyContentFormat](https://help.aliyun.com/document_detail/27482.html)。 |

## 返回值

Fn::GetAtt

-   SubscriptionUrl：创建的订阅URL。
-   SubscriptionName：订阅名称。
-   TopicName：主题名称。

## 示例

`JSON`格式

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

`YAML`格式

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

更多示例，请参见创建主题、创建消息队列和描述订阅关系的组合示例：[JSON示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/MNS/JSON/Subscription.json)和[YAML示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/MNS/YAML/Subscription.yml)。

