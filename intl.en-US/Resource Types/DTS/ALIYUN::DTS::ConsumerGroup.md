# ALIYUN::DTS::ConsumerGroup

ALIYUN::DTS::ConsumerGroup is used to create a consumer group for a change tracking instance.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ConsumerGroupPassword|String|Yes|Yes|The password that corresponds to the username of the consumer group.|The password must be 8 to 32 characters in length. It must contain at least two of the following character types: letters, digits, and special characters.|
|ConsumerGroupUserName|String|Yes|No|The username of the consumer group.|The username can be up to 16 characters in length. It can contain letters, digits, and underscores \(\_\).|
|ConsumerGroupName|String|Yes|No|The name of the consumer group.|The name can be up to 128 characters in length. We recommend that you use a descriptive name for easy identification. |
|SubscriptionInstanceId|String|Yes|No|The ID of the change tracking instance.|None|

## Response parameters

Fn::GetAtt

-   ConsumerGroupID: the ID of the consumer group.
-   ConsumerGroupName: the name of the consumer group.
-   SubscriptionInstanceId: the ID of the change tracking instance.

## Examples

`JSON` format

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

`YAML` format

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

