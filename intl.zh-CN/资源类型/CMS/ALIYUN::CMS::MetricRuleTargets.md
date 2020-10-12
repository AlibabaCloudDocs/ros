# ALIYUN::CMS::MetricRuleTargets

ALIYUN::CMS::MetricRuleTargets类型用于添加或修改报警规则的目标。

## 语法

```
{
  "Type": "ALIYUN::CMS::MetricRuleTargets",
  "Properties": {
    "RuleId": String,
    "Targets": List
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|RuleId|String|是|否|报警规则的ID。|无|
|Targets|List|是|否|报警规则的目标。|最多设置5个目标。详情请参见[Targets属性](#section_3g2_2as_gkt)。|

## Targets语法

```
"Targets": [
  {
    "Level": String,
    "Id": String,
    "Arn": String
  }
]
```

## Targets属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Level|String|否|否|报警级别。|取值：-   INFO：提示。
-   WARN：警告。
-   CRITICAL：紧急。 |
|Id|String|是|否|目标ID。|规则内唯一。|
|Arn|String|是|否|资源描述。|ARN规则为：`acs:{产品缩写}:{regionId}:{userId}:/{消息资源类型}/{资源名称}/message`。例如：`acs:mns:cn-hangzhou:111:/queues/test/message`。-   \{产品缩写\}：目前仅支持MNS，取值为mns。
-   \{regionId\}：消息队列或者主题所在的地域ID。
-   \{userId\}：用户账号ID。
-   \{消息资源类型\}：可选择为queues（队列）或者topics（主题）。
-   \{资源名称\}：队列或主题的名称。 |

## 返回值

Fn::GetAtt

-   Arns：目标的ARN。
-   Ids：目标ID。

## 示例

`JSON`格式

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

`YAML`格式

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

