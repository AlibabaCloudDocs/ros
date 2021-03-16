# ALIYUN::DTS::ConsumerGroup

ALIYUN::DTS::ConsumerGroup类型用于为数据订阅实例创建消费组。

## 语法

```
{
  "Type": "ALIYUN::DTS::ConsumerGroup",
  "Properties": {
    "ConsumerGroupPassword": String,
    "ConsumerGroupUserName": String,
    "ConsumerGroupName": String,
    "SubscriptionInstanceId": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ConsumerGroupPassword|String|是|是|消费组账号的密码。|长度为8~32个字符。至少包含英文字母、数字和特殊字符中的两种。|
|ConsumerGroupUserName|String|是|否|消费组账号。|最长16个字符。可包含英文字母、数字和下划线（\_）。|
|ConsumerGroupName|String|是|否|消费组名称。|最长128个字符。建议配置具有业务意义的名称，便于后续识别。 |
|SubscriptionInstanceId|String|是|否|数据订阅实例ID。|无|

## 返回值

Fn::GetAtt

-   ConsumerGroupID：消费组ID。
-   ConsumerGroupName：消费组名称。
-   SubscriptionInstanceId：数据订阅实例ID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "ConsumerGroupPassword": {
      "Type": "String",
      "Description": "Password of consumer group."
    },
    "ConsumerGroupUserName": {
      "Type": "String",
      "Description": "User name of consumer group."
    },
    "ConsumerGroupName": {
      "Type": "String",
      "Description": "Consumer group name."
    },
    "SubscriptionInstanceId": {
      "Type": "String",
      "Description": "Subscription instance ID."
    }
  },
  "Resources": {
    "ConsumerGroup": {
      "Type": "ALIYUN::DTS::ConsumerGroup",
      "Properties": {
        "ConsumerGroupPassword": {
          "Ref": "ConsumerGroupPassword"
        },
        "ConsumerGroupUserName": {
          "Ref": "ConsumerGroupUserName"
        },
        "ConsumerGroupName": {
          "Ref": "ConsumerGroupName"
        },
        "SubscriptionInstanceId": {
          "Ref": "SubscriptionInstanceId"
        }
      }
    }
  },
  "Outputs": {
    "ConsumerGroupID": {
      "Description": "Consumer group ID",
      "Value": {
        "Fn::GetAtt": [
          "ConsumerGroup",
          "ConsumerGroupID"
        ]
      }
    },
    "ConsumerGroupName": {
      "Description": "Consumer group name",
      "Value": {
        "Fn::GetAtt": [
          "ConsumerGroup",
          "ConsumerGroupName"
        ]
      }
    },
    "SubscriptionInstanceId": {
      "Description": "Subscription instance ID",
      "Value": {
        "Fn::GetAtt": [
          "ConsumerGroup",
          "SubscriptionInstanceId"
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
  ConsumerGroupName:
    Description: Consumer group name.
    Type: String
  ConsumerGroupPassword:
    Description: Password of consumer group.
    Type: String
  ConsumerGroupUserName:
    Description: User name of consumer group.
    Type: String
  SubscriptionInstanceId:
    Description: Subscription instance ID.
    Type: String
Resources:
  ConsumerGroup:
    Properties:
      ConsumerGroupName:
        Ref: ConsumerGroupName
      ConsumerGroupPassword:
        Ref: ConsumerGroupPassword
      ConsumerGroupUserName:
        Ref: ConsumerGroupUserName
      SubscriptionInstanceId:
        Ref: SubscriptionInstanceId
    Type: ALIYUN::DTS::ConsumerGroup
Outputs:
  ConsumerGroupID:
    Description: Consumer group ID
    Value:
      Fn::GetAtt:
      - ConsumerGroup
      - ConsumerGroupID
  ConsumerGroupName:
    Description: Consumer group name
    Value:
      Fn::GetAtt:
      - ConsumerGroup
      - ConsumerGroupName
  SubscriptionInstanceId:
    Description: Subscription instance ID
    Value:
      Fn::GetAtt:
      - ConsumerGroup
      - SubscriptionInstanceId
```

