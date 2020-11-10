# ALIYUN::CMS::MetricRuleTargets

ALIYUN::CMS::MetricRuleTargets is used to add or modify one or more message resources of an alert rule.

## Syntax

```
{
  "Type": "ALIYUN::CMS::MetricRuleTargets",
  "Properties": {
    "RuleId": String,
    "Targets": List
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|RuleId|String|Yes|No|The ID of the alert rule.|None|
|Targets|List|Yes|No|The message resources of the alert rule.|A maximum of five message resources can be set. For more information, see [Targets properties](#section_3g2_2as_gkt).|

## Targets syntax

```
"Targets": [
  {
    "Level": String,
    "Id": String,
    "Arn": String
  }
]
```

## Targets properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Level|String|No|No|The level of the alert.|Valid values:-   INFO
-   WARN
-   CRITICAL |
|Id|String|Yes|No|The ID of the message resource.|The ID must be unique in the alert rule.|
|Arn|String|Yes|No|The Alibaba Cloud Resource Name \(ARN\) of the message resource.|The ARN must be in the format of `acs:{Service name abbreviation}:{regionId}:{userId}:/{Message resource type}/{Resource name}/message`. Example: `acs:mns:cn-hangzhou:111:/queues/test/message`-   \{Service name abbreviation\}: the abbreviation of the service name. Set the value to mns. This resource type only supports Message Notification Service \(MNS\) as the message service.
-   \{regionId\}: the region ID of the message queue or topic.
-   \{userId\}: the account ID of the user.
-   \{Message resource type\}: the type of the message resource. Valid values: queues and topics.
-   \{Resource name\}: the name of the resource. |

## Response parameters

Fn::GetAtt

-   Arns: the ARNs of the message resources.
-   Ids: the IDs of the message resources.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "RuleId": {
      "Type": "String",
      "Description": "The ID of the alert rule."
    },
    "Targets": {
      "Type": "Json",
      "MinLength": 1,
      "MaxLength": 5
    }
  },
  "Resources": {
    "MetricRuleTargets": {
      "Type": "ALIYUN::CMS::MetricRuleTargets",
      "Properties": {
        "RuleId": {
          "Ref": "RuleId"
        },
        "Targets": {
          "Ref": "Targets"
        }
      }
    }
  },
  "Outputs": {
    "Arns": {
      "Description": "The ARN list of targets",
      "Value": {
        "Fn::GetAtt": [
          "MetricRuleTargets",
          "Arns"
        ]
      }
    },
    "Ids": {
      "Description": "The ID list of targets",
      "Value": {
        "Fn::GetAtt": [
          "MetricRuleTargets",
          "Ids"
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
  RuleId:
    Type: String
    Description: The ID of the alert rule.
  Targets:
    Type: Json
    MinLength: 1
    MaxLength: 5
Resources:
  MetricRuleTargets:
    Type: 'ALIYUN::CMS::MetricRuleTargets'
    Properties:
      RuleId:
        Ref: RuleId
      Targets:
        Ref: Targets
Outputs:
  Arns:
    Description: The ARN list of targets
    Value:
      'Fn::GetAtt':
        - MetricRuleTargets
        - Arns
  Ids:
    Description: The ID list of targets
    Value:
      'Fn::GetAtt':
        - MetricRuleTargets
        - Ids
```

