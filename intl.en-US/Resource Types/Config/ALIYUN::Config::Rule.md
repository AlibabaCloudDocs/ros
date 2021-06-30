# ALIYUN::Config::Rule

ALIYUN::Config::Rule is used to create or modify a rule.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|TagKeyScope|String|No|Yes|The tag key of the rule.|This parameter takes effect when the SourceOwner parameter is set to ALIYUN. A value of ALIYUN indicates that the rule is a managed rule of Alibaba Cloud.|
|TagValueScope|String|No|Yes|The tag value of the rule.|This parameter takes effect when the SourceOwner parameter is set to ALIYUN.|
|Description|String|No|Yes|The description of the rule.|None|
|ExcludeResourceIdsScope|String|No|Yes|The IDs of the resources excluded by the rule.|Separate multiple resource IDs with commas \(,\). This parameter takes effect when the SourceOwner parameter is set to ALIYUN. |
|SourceOwner|String|Yes|No|Specifies whether you or Alibaba Cloud owns and manages the rule.|Valid values:-   CUSTOM\_FC: The rule is a custom rule that you own.
-   ALIYUN: The rule is a managed rule of Alibaba Cloud. |
|SourceIdentifier|String|Yes|No|The identifier of the rule or the Alibaba Cloud Resource Name \(ARN\) of the function.|This parameter specifies the identifier of the rule when the SourceOwner parameter is set to ALIYUN. A value of ALIYUN indicates that the rule is a managed rule of Alibaba Cloud. This parameter specifies the function ARN when the SourceOwner parameter is set to CUSTOM\_FC. A value of CUSTOM\_FC indicates that the rule is a custom rule that you own. |
|MaximumExecutionFrequency|String|No|Yes|The frequency at which the rule is executed.|Valid values:-   One\_Hour
-   Three\_Hours
-   Six\_Hours
-   Twelve\_Hours
-   TwentyFour\_Hours |
|RegionIdsScope|String|No|Yes|The region IDs of the rule.|Separate multiple region IDs with commas \(,\). This parameter takes effect when the SourceOwner parameter is set to ALIYUN. |
|ConfigRuleTriggerTypes|String|Yes|Yes|The trigger type of the rule.|Valid values:-   ConfigurationItemChangeNotification: The rule is triggered by configuration changes.
-   ScheduledNotification: The rule is triggered as scheduled. |
|ResourceGroupIdsScope|String|No|Yes|The resource group IDs of the rule.|Separate multiple resource group IDs with commas \(,\). This parameter takes effect when the SourceOwner parameter is set to ALIYUN. |
|RiskLevel|Integer|Yes|Yes|The risk level of the rule.|Valid values:-   1: high risk
-   2: medium risk
-   3: low risk |
|ResourceTypesScope|List|Yes|Yes|The types of the resources to be evaluated based on the rule.|None|
|RuleName|String|Yes|No|The name of the rule.|None|
|InputParameters|Map|No|Yes|The settings of the input parameters for the rule.|Sample value: `{"cpuCount": "2"}`.|

## Response parameters

Fn::GetAtt

-   TagKeyScope: the tag key of the rule.
-   TagValueScope: the tag value of the rule.
-   Description: the description of the rule.
-   ExcludeResourceIdsScope: the IDs of the resources excluded by the rule.
-   SourceOwner: indicates whether you or Alibaba Cloud owns and manages the rule.
-   SourceIdentifier: the identifier of the rule.
-   MaximumExecutionFrequency: the frequency at which the rule is executed.
-   CompliancePackId: the ID of the compliance package to which the rule belongs.
-   ConfigRuleId: the ID of the rule.
-   EventSource: the source of the event.
-   RegionIdsScope: the region IDs of the rule.
-   ConfigRuleArn: the ARN of the rule.
-   ConfigRuleTriggerTypes: the trigger type of the rule.
-   ResourceGroupIdsScope: the resource group IDs of the rule.
-   RiskLevel: the risk level of the rule.
-   ResourceTypesScope: the types of the resources that are evaluated based on the rule.
-   RuleName: the name of the rule.
-   InputParameters: the settings of the input parameters for the rule.

## Examples

`JSON` format

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

`YAML` format

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

