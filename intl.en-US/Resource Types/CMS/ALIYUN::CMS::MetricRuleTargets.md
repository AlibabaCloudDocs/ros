# ALIYUN::CMS::MetricRuleTargets

ALIYUN::CMS::EventRuleTargets is used to add or modify the target of an alert rule.

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
|Targets|List|Yes|No|The targets of the alert rule.|A maximum of five targets can be set. For more information, see [Targets properties](#section_3g2_2as_gkt).|

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
|Level|String|No|No|The level of the alert.|Valid values for array elements:-   INFO
-   WARN
-   CRITICAL |
|Id|String|Yes|No|The ID of the target.|The ID must be unique in the alert rule.|
|Arn|String|Yes|No|The description of the resource.|The description is in the format of `acs:{Service name abbreviation}:{regionId}:{userId}:/{Message resource type}/{Resource name}/message`. For example, you can set the parameter to `acs:mns:cn-hangzhou:111:/queues/test/message`.-   \{Service name abbreviation\}: the abbreviation of the service name. Set the value to mns. This resource type only supports Message Notification Service \(MNS\).
-   \{regionId\}: the region ID of the message queue or topic.
-   \{userId\}: the account ID of the user.
-   \{Message resource type\}: the type of the message resource. Valid values: queues or topics.
-   \{Resource name\}: the name of the resource. |

## Response parameters

Fn::GetAtt

-   Arns: the ARN of the target.
-   Ids: the ID of the target.

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

