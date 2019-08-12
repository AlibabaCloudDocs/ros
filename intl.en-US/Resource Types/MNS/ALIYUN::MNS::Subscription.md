# ALIYUN::MNS::Subscription {#concept_188157 .concept}

ALIYUN::MNS::Subscription is used to subscribe an endpoint to an Alibaba Cloud Message Service \(MNS\) topic. For a subscription to be created, the owner of the endpoint must confirm the subscription.

## Syntax {#section_as0_t0t_6dd .section}

```language-json
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

## Properties { .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|TopicName|String|Yes|No|The name of the topic.| The name must be unique to an Alibaba Cloud account in a region. The name can be up to 256 characters in length and can contain letters, digits, and hyphens \(-\). It must start with a letter.

 |
|SubscriptionName|String|Yes|No|The name of the subscription.|The name can be up to 256 characters in length and can contain letters, digits, and hyphens \(-\). It must start with a letter.|
|Endpoint|String|Yes|No|The endpoint that the subscriber uses to receive messages.|The following endpoint types can be specified: 1.  HttpEndpoint. This type of endpoints must be prefixed with http://.
2.  QueueEndpoint. This type of endpoints must be in the acs: mns: \{REGION \}:\{ AccountID\}: queues/\{QueueName \} format.
3.  MailEndpoint. This type of endpoints must be in the mail:directmail:\{MailAddress\} format.
4.  SmsEndpoint. This type of endpoints must be in the sms:directsms:anonymous or sms:directsms:\{Phone\} format.

 |
|FilterTag|String|No|No|The message filtering tag in the created subscription. Only messages with consistent tags are pushed.|The parameter value can be up to 16 characters in length. By default, no messages are filtered.|
|NotifyStrategy|String|No|Yes|The retry policy that is applied when an error occurs during message delivery to the endpoint.|Valid values: BACKOFF\_RETRY and EXPONENTIAL\_DECAY\_RETRY. Default value: BACKOFF\_RETRY. For more information about retry policies, see .|
|NotifyContentFormat|String|No|No|The format of the message content pushed to the endpoint.| Valid values: XML, JSON, and SIMPLIFIED. Default value: XML. For more information about message formats, see .

 |

## Response parameters {#section_496_hfg_5h1 .section}

 **Fn::GetAtt** 

SubscriptionUrl: the URL of the created subscription.

## Examples { .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "Topic": {
      "Type": "ALIYUN::MNS::Topic",
      "Properties": {
        "TopicName": "test"
      }
    },
    "Subscription": {
      "Type": "ALIYUN::MNS::Subscription",
      "Properties": {
        "TopicName": "test",
        "SubscriptionName": "test",
        "Endpoint": "http://your-endpoint.com",
        "FilterTag": "AFilterTag",
        "NotifyStrategy": "BACKOFF_RETRY",
        "NotifyContentFormat": "XML"
      }
    },
    "Outputs": {
      "SubscriptionUrl": {
        "Value": { "Fn::GetAtt": ["Subscription", "SubscriptionUrl"] }
      }
    }
  }
}
```

