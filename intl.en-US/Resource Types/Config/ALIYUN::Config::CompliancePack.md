# ALIYUN::Config::CompliancePack

ALIYUN::Config::CompliancePack is used to create a compliance package.

## Syntax

```
{
  "Type": "ALIYUN::Config::CompliancePack",
  "Properties": {
    "CompliancePackName": String,
    "Description": String,
    "ConfigRules": List,
    "CompliancePackTemplateId": String,
    "RiskLevel": Integer
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|CompliancePackName|String|Yes|No|The name of the compliance package.|None|
|Description|String|Yes|Yes|The description of the compliance package.|None|
|ConfigRules|List|No|Yes|The configuration rules.|For more information, see [ConfigRules properties](#section_res_mla_m9a).|
|CompliancePackTemplateId|String|No|No|The ID of the compliance package template.|None|
|RiskLevel|Integer|Yes|Yes|The risk level.|Valid values:-   1: high risk
-   2: medium risk
-   3: low risk |

## ConfigRules syntax

```
"ConfigRules": [
  {
    "ConfigRuleId": String,
    "ConfigRuleName": String,
    "ManagedRuleIdentifier": String,
    "ConfigRuleParameters": List
  }
]
```

## ConfigRules properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ConfigRuleId|String|No|No|The ID of the configuration rule.|None|
|ConfigRuleName|String|No|No|The name of the configuration rule.|None|
|ManagedRuleIdentifier|String|No|No|The identifier of the configuration rule.|None|
|ConfigRuleParameters|List|No|No|The parameters of the configuration rule.|For more information, see [ConfigRuleParameters properties](#section_uu3_jza_rva).|

## ConfigRuleParameters syntax

```
"ConfigRuleParameters": [
  {
    "ParameterValue": String,
    "Required": Boolean,
    "ParameterName": String
  }
]
```

## ConfigRuleParameters properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ParameterValue|String|No|No|The value of the parameter.|None|
|Required|Boolean|No|No|Specifies whether the parameter is required.|Valid values:-   true
-   false |
|ParameterName|String|No|No|The name of the parameter.|None|

## Response parameters

Fn::GetAtt

-   CompliancePackId: the ID of the compliance package.
-   Description: the description of the compliance package.
-   CompliancePackName: the name of the compliance package.
-   AccountId: the ID of the Alibaba Cloud account.
-   CompliancePackTemplateId: the ID of the compliance package template.
-   RiskLevel: the risk level.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Description": {
      "Type": "String",
      "Description": "Description"
    },
    "CompliancePackName": {
      "Type": "String",
      "Description": "Compliance Package Name"
    },
    "ConfigRules": {
      "Type": "Json",
      "Description": "Config Rule List"
    },
    "CompliancePackTemplateId": {
      "Type": "String",
      "Description": "Compliance Package Template Id"
    },
    "RiskLevel": {
      "Type": "Number",
      "Description": "Ris Level"
    }
  },
  "Resources": {
    "ConfigCompliancePack": {
      "Type": "ALIYUN::Config::CompliancePack",
      "Properties": {
        "Description": {
          "Ref": "Description"
        },
        "CompliancePackName": {
          "Ref": "CompliancePackName"
        },
        "ConfigRules": {
          "Ref": "ConfigRules"
        },
        "CompliancePackTemplateId": {
          "Ref": "CompliancePackTemplateId"
        },
        "RiskLevel": {
          "Ref": "RiskLevel"
        }
      }
    }
  },
  "Outputs": {
    "CompliancePackId": {
      "Description": "Compliance Package ID",
      "Value": {
        "Fn::GetAtt": [
          "ConfigCompliancePack",
          "CompliancePackId"
        ]
      }
    },
    "Description": {
      "Description": "Description",
      "Value": {
        "Fn::GetAtt": [
          "ConfigCompliancePack",
          "Description"
        ]
      }
    },
    "CompliancePackName": {
      "Description": "Compliance Package Name",
      "Value": {
        "Fn::GetAtt": [
          "ConfigCompliancePack",
          "CompliancePackName"
        ]
      }
    },
    "AccountId": {
      "Description": "Aliyun User Id",
      "Value": {
        "Fn::GetAtt": [
          "ConfigCompliancePack",
          "AccountId"
        ]
      }
    },
    "CompliancePackTemplateId": {
      "Description": "Compliance Package Template Id",
      "Value": {
        "Fn::GetAtt": [
          "ConfigCompliancePack",
          "CompliancePackTemplateId"
        ]
      }
    },
    "RiskLevel": {
      "Description": "Ris Level",
      "Value": {
        "Fn::GetAtt": [
          "ConfigCompliancePack",
          "RiskLevel"
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
  CompliancePackName:
    Description: Compliance Package Name
    Type: String
  CompliancePackTemplateId:
    Description: Compliance Package Template Id
    Type: String
  ConfigRules:
    Description: Config Rule List
    Type: Json
  Description:
    Description: Description
    Type: String
  RiskLevel:
    Description: Ris Level
    Type: Number
Resources:
  ConfigCompliancePack:
    Properties:
      CompliancePackName:
        Ref: CompliancePackName
      CompliancePackTemplateId:
        Ref: CompliancePackTemplateId
      ConfigRules:
        Ref: ConfigRules
      Description:
        Ref: Description
      RiskLevel:
        Ref: RiskLevel
    Type: ALIYUN::Config::CompliancePack
Outputs:
  AccountId:
    Description: Aliyun User Id
    Value:
      Fn::GetAtt:
      - ConfigCompliancePack
      - AccountId
  CompliancePackId:
    Description: Compliance Package ID
    Value:
      Fn::GetAtt:
      - ConfigCompliancePack
      - CompliancePackId
  CompliancePackName:
    Description: Compliance Package Name
    Value:
      Fn::GetAtt:
      - ConfigCompliancePack
      - CompliancePackName
  CompliancePackTemplateId:
    Description: Compliance Package Template Id
    Value:
      Fn::GetAtt:
      - ConfigCompliancePack
      - CompliancePackTemplateId
  Description:
    Description: Description
    Value:
      Fn::GetAtt:
      - ConfigCompliancePack
      - Description
  RiskLevel:
    Description: Ris Level
    Value:
      Fn::GetAtt:
      - ConfigCompliancePack
      - RiskLevel
```

