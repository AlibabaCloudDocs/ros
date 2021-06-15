# ALIYUN::Config::DeliveryChannel

ALIYUN::Config::DeliveryChannel类型用于创建或更新投递渠道。

## 语法

```
{
  "Type": "ALIYUN::Config::DeliveryChannel",
  "Properties": {
    "Description": String,
    "DeliveryChannelName": String,
    "DeliveryChannelTargetArn": String,
    "DeliveryChannelAssumeRoleArn": String,
    "DeliveryChannelType": String,
    "DeliveryChannelCondition": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Description|String|否|是|投递渠道描述。|无|
|DeliveryChannelName|String|否|是|投递渠道名称。|无|
|DeliveryChannelTargetArn|String|是|是|投递渠道目标地址的ARN。|取值：-   当投递渠道为OSS时，格式为：`acs:oss:{RegionId}:{Aliuid}:{bucketName}`。
-   当投递渠道为MNS时，格式为：`acs:mns:{RegionId}:{Aliuid}:/topics/{topicName}`。
-   当投递渠道为SLS时，格式为：`acs:log:{RegionId}:{Aliuid}:project/{projectName}/logstore/{logstoreName}`。 |
|DeliveryChannelAssumeRoleArn|String|是|是|投递角色ARN。|如果您使用配置审计服务角色，则可按照示例值填写，将其中的账号ID替换为您的真实账号ID。|
|DeliveryChannelType|String|是|否|投递渠道类型。|取值：-   OSS：对象存储。
-   MNS：消息服务。
-   SLS：日志服务。 |
|DeliveryChannelCondition|String|否|是|投递渠道附加规则。|当前仅支持MNS类型的投递渠道。您可以指定MNS订阅事件的最低风险等级和资源类型，具体如下：

-   订阅事件的最低风险等级为：`{"filterType":"RuleRiskLevel","value":"1","multiple":false}`。value表示您需要过滤的风险等级，取值：
    -   1：高风险。
    -   2：中风险。
    -   3：低风险。
-   订阅事件的资源类型为：`{"filterType":"ResourceType","values":["ACS::ACK::Cluster","ACS::ActionTrail::Trail","ACS::CBWP::CommonBandwidthPackage"],"multiple":true}`。values表示您需要订阅事件的资源类型，是一个资源类型的JSON数组。例如：`[{"filterType":"ResourceType","values":["ACS::ActionTrail::Trail","ACS::CBWP::CommonBandwidthPackage","ACS::CDN::Domain","ACS::CEN::CenBandwidthPackage","ACS::CEN::CenInstance","ACS::CEN::Flowlog","ACS::DdosCoo::Instance"],"multiple":true}]`。 |

## 返回值

Fn::GetAtt

DeliveryChannelId：投递渠道ID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Description": {
      "Type": "String",
      "Description": "The description of the delivery method."
    },
    "DeliveryChannelName": {
      "Type": "String",
      "Description": "The name of the delivery method."
    },
    "DeliveryChannelTargetArn": {
      "Type": "String",
      "Description": "The ARN of the delivery destination. This parameter is required when you create a\ndelivery method. The value must be in one of the following formats:\nacs:oss:{RegionId}:{Aliuid}:{bucketName} if your delivery destination is an Object Storage Service (OSS) bucket.\nacs:mns:{RegionId}:{Aliuid}:/topics/{topicName} if your delivery destination is a Message Service (MNS) topic.\nacs:log:{RegionId}:{Aliuid}:project/{projectName}/logstore/{logstoreName} if your delivery destination is a Log Service Logstore."
    },
    "DeliveryChannelAssumeRoleArn": {
      "Type": "String",
      "Description": "The Alibaba Cloud Resource Name (ARN) of the role to be assumed by the delivery method.\nThis parameter is required when you create a delivery method.\nNote If the delivery method assumes the service linked role for Cloud Config, you can specify\nthe ARN in the format of the provided example and replace the account ID with the\nID of your Alibaba Cloud account."
    },
    "DeliveryChannelType": {
      "Type": "String",
      "Description": "The type of the delivery method. This parameter is required when you create a delivery\nmethod. Valid values:\nOSS\nMNS\nSLS",
      "AllowedValues": [
        "MNS",
        "OSS",
        "SLS"
      ]
    },
    "DeliveryChannelCondition": {
      "Type": "String",
      "Description": "The rule attached to the delivery method. This parameter is applicable only to delivery\nmethods of the MNS type.\nThis parameter allows you to specify the lowest risk level for the events to subscribe\nto and the resource types for which you want to subscribe to events.\nTo specify the lowest risk level for the events to subscribe to, use the following\nformat:{\"filterType\":\"RuleRiskLevel\",\"value\":\"1\",\"multiple\":false}.\nThe value field indicates the lowest risk level and can be set to 1, 2, or 3, which\nindicates the high risk level, the medium risk level, and the low risk level, respectively.\nTo specify the resource types for which you want to subscribe to events, use the following\nformat:{\"filterType\":\"ResourceType\",\"values\":[\"ACS::ACK::Cluster\",\"ACS::ActionTrail::Trail\",\"ACS::CBWP::CommonBandwidthPackage\"],\"multiple\":true}.\nThe values field indicates the resource types. Its value is a JSON array.\nExample: [{\"filterType\":\"ResourceType\",\"values\":[\"ACS::ActionTrail::Trail\",\"ACS::CBWP::CommonBandwidthPackage\",\"ACS::CDN::Domain\",\"ACS::CEN::CenBandwidthPackage\",\"ACS::CEN::CenInstance\",\"ACS::CEN::Flowlog\",\"ACS::DdosCoo::Instance\"],\"multiple\":true}]"
    }
  },
  "Resources": {
    "DeliveryChannel": {
      "Type": "ALIYUN::Config::DeliveryChannel",
      "Properties": {
        "Description": {
          "Ref": "Description"
        },
        "DeliveryChannelName": {
          "Ref": "DeliveryChannelName"
        },
        "DeliveryChannelTargetArn": {
          "Ref": "DeliveryChannelTargetArn"
        },
        "DeliveryChannelAssumeRoleArn": {
          "Ref": "DeliveryChannelAssumeRoleArn"
        },
        "DeliveryChannelType": {
          "Ref": "DeliveryChannelType"
        },
        "DeliveryChannelCondition": {
          "Ref": "DeliveryChannelCondition"
        }
      }
    }
  },
  "Outputs": {
    "DeliveryChannelId": {
      "Description": "The ID of the delivery method. ",
      "Value": {
        "Fn::GetAtt": [
          "DeliveryChannel",
          "DeliveryChannelId"
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
  DeliveryChannelAssumeRoleArn:
    Description: 'The Alibaba Cloud Resource Name (ARN) of the role to be assumed
      by the delivery method.

      This parameter is required when you create a delivery method.

      Note If the delivery method assumes the service linked role for Cloud Config,
      you can specify

      the ARN in the format of the provided example and replace the account ID with
      the

      ID of your Alibaba Cloud account.'
    Type: String
  DeliveryChannelCondition:
    Description: 'The rule attached to the delivery method. This parameter is applicable
      only to delivery

      methods of the MNS type.

      This parameter allows you to specify the lowest risk level for the events to
      subscribe

      to and the resource types for which you want to subscribe to events.

      To specify the lowest risk level for the events to subscribe to, use the following

      format:{"filterType":"RuleRiskLevel","value":"1","multiple":false}.

      The value field indicates the lowest risk level and can be set to 1, 2, or 3,
      which

      indicates the high risk level, the medium risk level, and the low risk level,
      respectively.

      To specify the resource types for which you want to subscribe to events, use
      the following

      format:{"filterType":"ResourceType","values":["ACS::ACK::Cluster","ACS::ActionTrail::Trail","ACS::CBWP::CommonBandwidthPackage"],"multiple":true}.

      The values field indicates the resource types. Its value is a JSON array.

      Example: [{"filterType":"ResourceType","values":["ACS::ActionTrail::Trail","ACS::CBWP::CommonBandwidthPackage","ACS::CDN::Domain","ACS::CEN::CenBandwidthPackage","ACS::CEN::CenInstance","ACS::CEN::Flowlog","ACS::DdosCoo::Instance"],"multiple":true}]'
    Type: String
  DeliveryChannelName:
    Description: The name of the delivery method.
    Type: String
  DeliveryChannelTargetArn:
    Description: 'The ARN of the delivery destination. This parameter is required
      when you create a

      delivery method. The value must be in one of the following formats:

      acs:oss:{RegionId}:{Aliuid}:{bucketName} if your delivery destination is an
      Object Storage Service (OSS) bucket.

      acs:mns:{RegionId}:{Aliuid}:/topics/{topicName} if your delivery destination
      is a Message Service (MNS) topic.

      acs:log:{RegionId}:{Aliuid}:project/{projectName}/logstore/{logstoreName} if
      your delivery destination is a Log Service Logstore.'
    Type: String
  DeliveryChannelType:
    AllowedValues:
    - MNS
    - OSS
    - SLS
    Description: 'The type of the delivery method. This parameter is required when
      you create a delivery

      method. Valid values:

      OSS

      MNS

      SLS'
    Type: String
  Description:
    Description: The description of the delivery method.
    Type: String
Resources:
  DeliveryChannel:
    Properties:
      DeliveryChannelAssumeRoleArn:
        Ref: DeliveryChannelAssumeRoleArn
      DeliveryChannelCondition:
        Ref: DeliveryChannelCondition
      DeliveryChannelName:
        Ref: DeliveryChannelName
      DeliveryChannelTargetArn:
        Ref: DeliveryChannelTargetArn
      DeliveryChannelType:
        Ref: DeliveryChannelType
      Description:
        Ref: Description
    Type: ALIYUN::Config::DeliveryChannel
Outputs:
  DeliveryChannelId:
    Description: 'The ID of the delivery method. '
    Value:
      Fn::GetAtt:
      - DeliveryChannel
      - DeliveryChannelId
```

