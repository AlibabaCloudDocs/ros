# ALIYUN::MNS::Subscription {#concept_188157 .concept}

ALIYUN::MNS::Subscription类型用于描述一个订阅关系，包括被订阅的主题和接收消息的Endpoint。

## 语法 {#section_as0_t0t_6dd .section}

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

## 属性 { .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|TopicName|String|是|否|主题名称。| 同一账号同一Region下，主题名称不能重复，必须以英文字母开头，剩余名称可以是英文，数字，横划线，长度不超过256个字符。

 |
|SubscriptionName|String|是|否|订阅名称。|必须以英文字母开头，剩余名称可以是英文，数字，横划线，长度不超过256个字符。|
|Endpoint|String|是|否|描述此次订阅中接收消息的终端地址。|目前四种Endpoint： 1.  HttpEndpoint，必须以”http://"为前缀.
2.  QueueEndpoint, 格式为acs:mns:\{REGION\}:\{AccountID\}:queues/\{QueueName\}。
3.  MailEndpoint, 格式为mail:directmail:\{MailAddress\}。
4.  SmsEndpoint, 格式为sms:directsms:anonymous 或sms:directsms:\{Phone\}。

 |
|FilterTag|String|否|否|描述了该订阅中消息过滤的标签（标签一致的消息才会被推送）。|不超过16个字符的字符串，默认不进行消息过滤。|
|NotifyStrategy|String|否|是|描述了向 Endpoint 推送消息出现错误时的重试策略。|BACKOFF\_RETRY 或者 EXPONENTIAL\_DECAY\_RETRY，默认为BACKOFF\_RETRY，重试策略的具体描述请参考。|
|NotifyContentFormat|String|否|否|描述了向 Endpoint 推送的消息格式。| XML 、JSON 或者 SIMPLIFIED，默认为 XML，消息格式的具体描述请参考。

 |

## 返回值 {#section_496_hfg_5h1 .section}

**Fn::GetAtt**

SubscriptionUrl：所创建的订阅URL。

## 示例 { .section}

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

