# ALIYUN::Config::Rule

ALIYUN::Config::Rule类型用于新建或修改规则。

## 语法

```
{
  "Type": "ALIYUN::Config::Rule",
  "Properties": {
    "TagKeyScope": String,
    "TagValueScope": String,
    "Description": String,
    "ExcludeResourceIdsScope": String,
    "SourceOwner": String,
    "SourceIdentifier": String,
    "MaximumExecutionFrequency": String,
    "RegionIdsScope": String,
    "ConfigRuleTriggerTypes": String,
    "ResourceGroupIdsScope": String,
    "RiskLevel": Integer,
    "ResourceTypesScope": List,
    "RuleName": String,
    "InputParameters": Map
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|TagKeyScope|String|否|是|规则的标签键。|当SourceOwner取值为ALIYUN（托管规则）时该参数有效。|
|TagValueScope|String|否|是|规则的标签值。|当SourceOwner取值为ALIYUN（托管规则）时该参数有效。|
|Description|String|否|是|规则的描述信息。|无|
|ExcludeResourceIdsScope|String|否|是|规则排除的资源ID。|多个资源ID间以半角逗号（,）分隔。当SourceOwner取值为ALIYUN（托管规则）时该参数有效。 |
|SourceOwner|String|是|否|规则来源的归属。|取值：-   CUSTOM\_FC：用户自定义函数。
-   ALIYUN：托管规则。 |
|SourceIdentifier|String|是|否|规则标识或函数ARN。|当SourceOwner取值为ALIYUN（托管规则）时，该参数为规则标识。当SourceOwner取值为CUSTOM\_FC（用户自定义函数）时，该参数为函数ARN。 |
|MaximumExecutionFrequency|String|否|是|规则执行周期。|取值：-   One\_Hour：1小时。
-   Three\_Hours：3小时。
-   Six\_Hours：6小时。
-   Twelve\_Hours：12小时。
-   TwentyFour\_Hours：24小时。 |
|RegionIdsScope|String|否|是|规则的地域ID。|多个地域ID间以半角逗号（,）分隔。当SourceOwner取值为ALIYUN（托管规则）时该参数有效。 |
|ConfigRuleTriggerTypes|String|是|是|规则的触发器类型。|取值：-   ConfigurationItemChangeNotification：规则在配置更改时触发。
-   ScheduledNotification：规则按计划触发。 |
|ResourceGroupIdsScope|String|否|是|规则的资源组ID。|多个资源组ID间以半角逗号（,）分隔。当SourceOwner取值为ALIYUN（托管规则）时该参数有效。 |
|RiskLevel|Integer|是|是|风险等级。|取值：-   1：高风险。
-   2：中风险。
-   3：低风险。 |
|ResourceTypesScope|List|是|是|需要根据规则评估的资源类型。|无|
|RuleName|String|是|否|规则名称。|无|
|InputParameters|Map|否|是|规则入参。|取值示例：`{"cpuCount": "2"}`。|

## 返回值

Fn::GetAtt

-   TagKeyScope：规则的标签键。
-   TagValueScope：规则的标签值。
-   Description：规则的描述信息。
-   ExcludeResourceIdsScope：规则排除的资源ID。
-   SourceOwner：规则来源的归属。
-   SourceIdentifier：规则标识。
-   MaximumExecutionFrequency：规则执行周期。
-   CompliancePackId：规则所属的合规包ID。
-   ConfigRuleId：规则ID。
-   EventSource：事件来源。
-   RegionIdsScope：规则的地域ID。
-   ConfigRuleArn：规则ARN。
-   ConfigRuleTriggerTypes：规则的触发器类型。
-   ResourceGroupIdsScope：规则的资源组ID。
-   RiskLevel：规则的风险等级。
-   ResourceTypesScope：需要根据规则评估的资源类型。
-   RuleName：规则名称。
-   InputParameters：规则入参。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "TagKeyScope": {
      "Type": "String",
      "Description": "The rule monitors the tag key, only applies to rules created based on managed rules"
    },
    "TagValueScope": {
      "Type": "String",
      "Description": "The rule monitors the tag value, only applies to rules created based on managed rules"
    },
    "Description": {
      "Type": "String",
      "Description": "The description of the rule"
    },
    "ExcludeResourceIdsScope": {
      "Type": "String",
      "Description": "The rule monitors excluded resource IDs, multiple of which are separated by commas, only applies to rules created based on managed rules, , custom rule this field is empty"
    },
    "SourceOwner": {
      "Type": "String",
      "Description": "Specifies whether you or Alibaba Cloud owns and manages the rule. Valid values:  CUSTOM_FC: The rule is a custom rule and you own the rule. ALIYUN: The rule is a managed rule and Alibaba Cloud owns the rule"
    },
    "SourceIdentifier": {
      "Type": "String",
      "Description": "The identifier of the rule.  For a managed rule, the value is the name of the managed rule. For a custom rule, the value is the ARN of the custom rule"
    },
    "MaximumExecutionFrequency": {
      "Type": "String",
      "Description": "The frequency of the compliance evaluations. Valid values:  One_Hour Three_Hours Six_Hours Twelve_Hours TwentyFour_Hours"
    },
    "RegionIdsScope": {
      "Type": "String",
      "Description": "The rule monitors region IDs, separated by commas, only applies to rules created based on managed rules"
    },
    "ConfigRuleTriggerTypes": {
      "Type": "String",
      "Description": "The trigger type of the rule. Valid values:  ConfigurationItemChangeNotification: The rule is triggered upon configuration changes. ScheduledNotification: The rule is triggered as scheduled."
    },
    "ResourceGroupIdsScope": {
      "Type": "String",
      "Description": "The rule monitors resource group IDs, separated by commas, only applies to rules created based on managed rules"
    },
    "RiskLevel": {
      "Type": "Number",
      "Description": "The risk level of the resources that are not compliant with the rule. Valid values:  1: critical 2: warning 3: info"
    },
    "ResourceTypesScope": {
      "Type": "Json",
      "Description": "The types of the resources to be evaluated against the rule"
    },
    "RuleName": {
      "Type": "String",
      "Description": "The name of the rule."
    },
    "InputParameters": {
      "Type": "Json",
      "Description": "The settings of the input parameters for the rule"
    }
  },
  "Resources": {
    "ConfigRule": {
      "Type": "ALIYUN::Config::Rule",
      "Properties": {
        "TagKeyScope": {
          "Ref": "TagKeyScope"
        },
        "TagValueScope": {
          "Ref": "TagValueScope"
        },
        "Description": {
          "Ref": "Description"
        },
        "ExcludeResourceIdsScope": {
          "Ref": "ExcludeResourceIdsScope"
        },
        "SourceOwner": {
          "Ref": "SourceOwner"
        },
        "SourceIdentifier": {
          "Ref": "SourceIdentifier"
        },
        "MaximumExecutionFrequency": {
          "Ref": "MaximumExecutionFrequency"
        },
        "RegionIdsScope": {
          "Ref": "RegionIdsScope"
        },
        "ConfigRuleTriggerTypes": {
          "Ref": "ConfigRuleTriggerTypes"
        },
        "ResourceGroupIdsScope": {
          "Ref": "ResourceGroupIdsScope"
        },
        "RiskLevel": {
          "Ref": "RiskLevel"
        },
        "ResourceTypesScope": {
          "Ref": "ResourceTypesScope"
        },
        "RuleName": {
          "Ref": "RuleName"
        },
        "InputParameters": {
          "Ref": "InputParameters"
        }
      }
    }
  },
  "Outputs": {
    "TagKeyScope": {
      "Description": "The rule monitors the tag key, only applies to rules created based on managed rules",
      "Value": {
        "Fn::GetAtt": [
          "ConfigRule",
          "TagKeyScope"
        ]
      }
    },
    "TagValueScope": {
      "Description": "The rule monitors the tag value, only applies to rules created based on managed rules",
      "Value": {
        "Fn::GetAtt": [
          "ConfigRule",
          "TagValueScope"
        ]
      }
    },
    "Description": {
      "Description": "The description of the rule",
      "Value": {
        "Fn::GetAtt": [
          "ConfigRule",
          "Description"
        ]
      }
    },
    "ExcludeResourceIdsScope": {
      "Description": "The rule monitors excluded resource IDs, multiple of which are separated by commas, only applies to rules created based on managed rules, , custom rule this field is empty",
      "Value": {
        "Fn::GetAtt": [
          "ConfigRule",
          "ExcludeResourceIdsScope"
        ]
      }
    },
    "SourceOwner": {
      "Description": "Specifies whether you or Alibaba Cloud owns and manages the rule. Valid values:  CUSTOM_FC: The rule is a custom rule and you own the rule. ALIYUN: The rule is a managed rule and Alibaba Cloud owns the rule",
      "Value": {
        "Fn::GetAtt": [
          "ConfigRule",
          "SourceOwner"
        ]
      }
    },
    "SourceIdentifier": {
      "Description": "The identifier of the rule.  For a managed rule, the value is the name of the managed rule. For a custom rule, the value is the ARN of the custom rule",
      "Value": {
        "Fn::GetAtt": [
          "ConfigRule",
          "SourceIdentifier"
        ]
      }
    },
    "MaximumExecutionFrequency": {
      "Description": "The frequency of the compliance evaluations. Valid values:  One_Hour Three_Hours Six_Hours Twelve_Hours TwentyFour_Hours",
      "Value": {
        "Fn::GetAtt": [
          "ConfigRule",
          "MaximumExecutionFrequency"
        ]
      }
    },
    "CompliancePackId": {
      "Description": "Compliance Package ID",
      "Value": {
        "Fn::GetAtt": [
          "ConfigRule",
          "CompliancePackId"
        ]
      }
    },
    "ConfigRuleId": {
      "Description": "The ID of the rule",
      "Value": {
        "Fn::GetAtt": [
          "ConfigRule",
          "ConfigRuleId"
        ]
      }
    },
    "EventSource": {
      "Description": "The event source of the rule.",
      "Value": {
        "Fn::GetAtt": [
          "ConfigRule",
          "EventSource"
        ]
      }
    },
    "RegionIdsScope": {
      "Description": "The rule monitors region IDs, separated by commas, only applies to rules created based on managed rules",
      "Value": {
        "Fn::GetAtt": [
          "ConfigRule",
          "RegionIdsScope"
        ]
      }
    },
    "ConfigRuleArn": {
      "Description": "config rule arn",
      "Value": {
        "Fn::GetAtt": [
          "ConfigRule",
          "ConfigRuleArn"
        ]
      }
    },
    "ConfigRuleTriggerTypes": {
      "Description": "The trigger type of the rule. Valid values:  ConfigurationItemChangeNotification: The rule is triggered upon configuration changes. ScheduledNotification: The rule is triggered as scheduled.",
      "Value": {
        "Fn::GetAtt": [
          "ConfigRule",
          "ConfigRuleTriggerTypes"
        ]
      }
    },
    "ResourceGroupIdsScope": {
      "Description": "The rule monitors resource group IDs, separated by commas, only applies to rules created based on managed rules",
      "Value": {
        "Fn::GetAtt": [
          "ConfigRule",
          "ResourceGroupIdsScope"
        ]
      }
    },
    "RiskLevel": {
      "Description": "The risk level of the resources that are not compliant with the rule. Valid values:  1: critical 2: warning 3: info",
      "Value": {
        "Fn::GetAtt": [
          "ConfigRule",
          "RiskLevel"
        ]
      }
    },
    "ResourceTypesScope": {
      "Description": "The types of the resources to be evaluated against the rule",
      "Value": {
        "Fn::GetAtt": [
          "ConfigRule",
          "ResourceTypesScope"
        ]
      }
    },
    "RuleName": {
      "Description": "The name of the rule.",
      "Value": {
        "Fn::GetAtt": [
          "ConfigRule",
          "RuleName"
        ]
      }
    },
    "InputParameters": {
      "Description": "The settings of the input parameters for the rule",
      "Value": {
        "Fn::GetAtt": [
          "ConfigRule",
          "InputParameters"
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
  ConfigRuleTriggerTypes:
    Description: 'The trigger type of the rule. Valid values:  ConfigurationItemChangeNotification:
      The rule is triggered upon configuration changes. ScheduledNotification: The
      rule is triggered as scheduled.'
    Type: String
  Description:
    Description: The description of the rule
    Type: String
  ExcludeResourceIdsScope:
    Description: The rule monitors excluded resource IDs, multiple of which are separated
      by commas, only applies to rules created based on managed rules, , custom rule
      this field is empty
    Type: String
  InputParameters:
    Description: The settings of the input parameters for the rule
    Type: Json
  MaximumExecutionFrequency:
    Description: 'The frequency of the compliance evaluations. Valid values:  One_Hour
      Three_Hours Six_Hours Twelve_Hours TwentyFour_Hours'
    Type: String
  RegionIdsScope:
    Description: The rule monitors region IDs, separated by commas, only applies to
      rules created based on managed rules
    Type: String
  ResourceGroupIdsScope:
    Description: The rule monitors resource group IDs, separated by commas, only applies
      to rules created based on managed rules
    Type: String
  ResourceTypesScope:
    Description: The types of the resources to be evaluated against the rule
    Type: Json
  RiskLevel:
    Description: 'The risk level of the resources that are not compliant with the
      rule. Valid values:  1: critical 2: warning 3: info'
    Type: Number
  RuleName:
    Description: The name of the rule.
    Type: String
  SourceIdentifier:
    Description: The identifier of the rule.  For a managed rule, the value is the
      name of the managed rule. For a custom rule, the value is the ARN of the custom
      rule
    Type: String
  SourceOwner:
    Description: 'Specifies whether you or Alibaba Cloud owns and manages the rule.
      Valid values:  CUSTOM_FC: The rule is a custom rule and you own the rule. ALIYUN:
      The rule is a managed rule and Alibaba Cloud owns the rule'
    Type: String
  TagKeyScope:
    Description: The rule monitors the tag key, only applies to rules created based
      on managed rules
    Type: String
  TagValueScope:
    Description: The rule monitors the tag value, only applies to rules created based
      on managed rules
    Type: String
Resources:
  ConfigRule:
    Properties:
      ConfigRuleTriggerTypes:
        Ref: ConfigRuleTriggerTypes
      Description:
        Ref: Description
      ExcludeResourceIdsScope:
        Ref: ExcludeResourceIdsScope
      InputParameters:
        Ref: InputParameters
      MaximumExecutionFrequency:
        Ref: MaximumExecutionFrequency
      RegionIdsScope:
        Ref: RegionIdsScope
      ResourceGroupIdsScope:
        Ref: ResourceGroupIdsScope
      ResourceTypesScope:
        Ref: ResourceTypesScope
      RiskLevel:
        Ref: RiskLevel
      RuleName:
        Ref: RuleName
      SourceIdentifier:
        Ref: SourceIdentifier
      SourceOwner:
        Ref: SourceOwner
      TagKeyScope:
        Ref: TagKeyScope
      TagValueScope:
        Ref: TagValueScope
    Type: ALIYUN::Config::Rule
Outputs:
  CompliancePackId:
    Description: Compliance Package ID
    Value:
      Fn::GetAtt:
      - ConfigRule
      - CompliancePackId
  ConfigRuleArn:
    Description: config rule arn
    Value:
      Fn::GetAtt:
      - ConfigRule
      - ConfigRuleArn
  ConfigRuleId:
    Description: The ID of the rule
    Value:
      Fn::GetAtt:
      - ConfigRule
      - ConfigRuleId
  ConfigRuleTriggerTypes:
    Description: 'The trigger type of the rule. Valid values:  ConfigurationItemChangeNotification:
      The rule is triggered upon configuration changes. ScheduledNotification: The
      rule is triggered as scheduled.'
    Value:
      Fn::GetAtt:
      - ConfigRule
      - ConfigRuleTriggerTypes
  Description:
    Description: The description of the rule
    Value:
      Fn::GetAtt:
      - ConfigRule
      - Description
  EventSource:
    Description: The event source of the rule.
    Value:
      Fn::GetAtt:
      - ConfigRule
      - EventSource
  ExcludeResourceIdsScope:
    Description: The rule monitors excluded resource IDs, multiple of which are separated
      by commas, only applies to rules created based on managed rules, , custom rule
      this field is empty
    Value:
      Fn::GetAtt:
      - ConfigRule
      - ExcludeResourceIdsScope
  InputParameters:
    Description: The settings of the input parameters for the rule
    Value:
      Fn::GetAtt:
      - ConfigRule
      - InputParameters
  MaximumExecutionFrequency:
    Description: 'The frequency of the compliance evaluations. Valid values:  One_Hour
      Three_Hours Six_Hours Twelve_Hours TwentyFour_Hours'
    Value:
      Fn::GetAtt:
      - ConfigRule
      - MaximumExecutionFrequency
  RegionIdsScope:
    Description: The rule monitors region IDs, separated by commas, only applies to
      rules created based on managed rules
    Value:
      Fn::GetAtt:
      - ConfigRule
      - RegionIdsScope
  ResourceGroupIdsScope:
    Description: The rule monitors resource group IDs, separated by commas, only applies
      to rules created based on managed rules
    Value:
      Fn::GetAtt:
      - ConfigRule
      - ResourceGroupIdsScope
  ResourceTypesScope:
    Description: The types of the resources to be evaluated against the rule
    Value:
      Fn::GetAtt:
      - ConfigRule
      - ResourceTypesScope
  RiskLevel:
    Description: 'The risk level of the resources that are not compliant with the
      rule. Valid values:  1: critical 2: warning 3: info'
    Value:
      Fn::GetAtt:
      - ConfigRule
      - RiskLevel
  RuleName:
    Description: The name of the rule.
    Value:
      Fn::GetAtt:
      - ConfigRule
      - RuleName
  SourceIdentifier:
    Description: The identifier of the rule.  For a managed rule, the value is the
      name of the managed rule. For a custom rule, the value is the ARN of the custom
      rule
    Value:
      Fn::GetAtt:
      - ConfigRule
      - SourceIdentifier
  SourceOwner:
    Description: 'Specifies whether you or Alibaba Cloud owns and manages the rule.
      Valid values:  CUSTOM_FC: The rule is a custom rule and you own the rule. ALIYUN:
      The rule is a managed rule and Alibaba Cloud owns the rule'
    Value:
      Fn::GetAtt:
      - ConfigRule
      - SourceOwner
  TagKeyScope:
    Description: The rule monitors the tag key, only applies to rules created based
      on managed rules
    Value:
      Fn::GetAtt:
      - ConfigRule
      - TagKeyScope
  TagValueScope:
    Description: The rule monitors the tag value, only applies to rules created based
      on managed rules
    Value:
      Fn::GetAtt:
      - ConfigRule
      - TagValueScope
```

