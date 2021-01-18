# ALIYUN::CMS::DynamicTagGroup

ALIYUN::CMS::DynamicTagGroup is used to create a tag rule based on which cloud resources can be automatically added to an application group.

**Note:** This resource type is supported only for Elastic Compute Service \(ECS\), ApsaraDB RDS, and Server Load Balancer \(SLB\) instances.

## Syntax

```
{
  "Type": "ALIYUN::CMS::DynamicTagGroup",
  "Properties": {
    "ContactGroupList": List,
    "MatchExpressFilterRelation": String,
    "EnableSubscribeEvent": Boolean,
    "TemplateIdList": List,
    "TagKey": String,
    "EnableInstallAgent": Boolean,
    "MatchExpress": List
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ContactGroupList|List|Yes|No|The list of one or more alert contacts to receive alert notifications.|None|
|MatchExpressFilterRelation|String|No|No|The logical operator used between conditional expressions that are used to match instances.|Valid values:-   and
-   or |
|EnableSubscribeEvent|Boolean|No|No|Specifies whether to enable event subscription.|Valid values:-   true: Event subscription is enabled.
-   false: Event subscription is disabled. |
|TemplateIdList|List|No|No|The list of one or more IDs of the alert templates.|None|
|TagKey|String|Yes|No|The tag key.|None|
|EnableInstallAgent|Boolean|No|No|Specifies whether to install the Cloud Monitor agent on ECS instances that are automatically added to the application group.|Default value: false. Valid values:-   true: The Cloud Monitor agent is installed.
-   false: The Cloud Monitor agent is not installed.

**Note:** If the Cloud Monitor agent is not installed on an ECS instance that is added to the application group, the system installs the Cloud Monitor agent on the ECS instance. |
|MatchExpress|List|No|No|The conditional expression that is used to match instances.|Only one conditional expression can be set.For more information, see [MatchExpress properties](#section_klz_dlm_73a). |

## MatchExpress syntax

```
"MatchExpress": [
  {
    "TagValue": String,
    "TagValueMatchFunction": String
  }
]
```

## MatchExpress properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|TagValue|String|Yes|No|The tag value.|None|
|TagValueMatchFunction|String|Yes|No|The method used to match the value of the tag.|Valid values:-   contains
-   startWith
-   endWith
-   notContains
-   equals
-   all |

## Response parameters

Fn::GetAtt

-   DynamicTagRuleId: the ID of the tag rule.
-   TagKey: the tag key.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "ContactGroupList": {
      "Type": "Json",
      "Description": "Alarm contacts."
    },
    "MatchExpressFilterRelation": {
      "Type": "String",
      "Description": "The relationship between the conditional expressions. Values are:\nand: the relationship between\nor: the relationship or the\nDescription currently supports only one combination of conditions, the follow-up Ali cloud will support a variety of combinations of conditions.",
      "AllowedValues": [
        "and",
        "or"
      ]
    },
    "EnableSubscribeEvent": {
      "Type": "Boolean",
      "Description": "Whether the event subscription is enabled. Values are\n:true: enable event subscription\nfalse: disable event subscription",
      "AllowedValues": [
        "true",
        "false"
      ]
    },
    "TemplateIdList": {
      "Type": "Json",
      "Description": "Alarm template ID list.\nWhen the automatically generated application group synchronizes tags, it will generate alarm rules according to the specified alarm template.",
      "MaxLength": 5
    },
    "TagKey": {
      "Type": "String",
      "Description": "Tag key."
    },
    "EnableInstallAgent": {
      "Type": "Boolean",
      "Description": "Whether to enable initial installation monitoring plug, not installed by default. Values are:\ntrue: enable installation\nNote If ECS generated instances group does not monitor plug-in installed will attempt to automatically install.\nfalse: disable installation",
      "AllowedValues": [
        "true",
        "false"
      ]
    },
    "MatchExpress": {
      "Type": "Json",
      "Description": "Matching list. Only supports one currently.",
      "MaxLength": 1
    }
  },
  "Resources": {
    "DynamicTagGroup": {
      "Type": "ALIYUN::CMS::DynamicTagGroup",
      "Properties": {
        "ContactGroupList": {
          "Ref": "ContactGroupList"
        },
        "MatchExpressFilterRelation": {
          "Ref": "MatchExpressFilterRelation"
        },
        "EnableSubscribeEvent": {
          "Ref": "EnableSubscribeEvent"
        },
        "TemplateIdList": {
          "Ref": "TemplateIdList"
        },
        "TagKey": {
          "Ref": "TagKey"
        },
        "EnableInstallAgent": {
          "Ref": "EnableInstallAgent"
        },
        "MatchExpress": {
          "Ref": "MatchExpress"
        }
      }
    }
  },
  "Outputs": {
    "DynamicTagRuleId": {
      "Description": "Dynamic tag rule ID.",
      "Value": {
        "Fn::GetAtt": [
          "DynamicTagGroup",
          "DynamicTagRuleId"
        ]
      }
    },
    "TagKey": {
      "Description": "Tag key.",
      "Value": {
        "Fn::GetAtt": [
          "DynamicTagGroup",
          "TagKey"
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
  ContactGroupList:
    Type: Json
    Description: Alarm contacts.
  MatchExpressFilterRelation:
    Type: String
    Description: >-
      The relationship between the conditional expressions. Values are:

      and: the relationship between

      or: the relationship or the

      Description currently supports only one combination of conditions, the
      follow-up Ali cloud will support a variety of combinations of conditions.
    AllowedValues:
      - and
      - or
  EnableSubscribeEvent:
    Type: Boolean
    Description: |-
      Whether the event subscription is enabled. Values are
      :true: enable event subscription
      false: disable event subscription
    AllowedValues:
      - 'true'
      - 'false'
  TemplateIdList:
    Type: Json
    Description: >-
      Alarm template ID list.

      When the automatically generated application group synchronizes tags, it
      will generate alarm rules according to the specified alarm template.
    MaxLength: 5
  TagKey:
    Type: String
    Description: Tag key.
  EnableInstallAgent:
    Type: Boolean
    Description: >-
      Whether to enable initial installation monitoring plug, not installed by
      default. Values are:

      true: enable installation

      Note If ECS generated instances group does not monitor plug-in installed
      will attempt to automatically install.

      false: disable installation
    AllowedValues:
      - 'true'
      - 'false'
  MatchExpress:
    Type: Json
    Description: Matching list. Only supports one currently.
    MaxLength: 1
Resources:
  DynamicTagGroup:
    Type: 'ALIYUN::CMS::DynamicTagGroup'
    Properties:
      ContactGroupList:
        Ref: ContactGroupList
      MatchExpressFilterRelation:
        Ref: MatchExpressFilterRelation
      EnableSubscribeEvent:
        Ref: EnableSubscribeEvent
      TemplateIdList:
        Ref: TemplateIdList
      TagKey:
        Ref: TagKey
      EnableInstallAgent:
        Ref: EnableInstallAgent
      MatchExpress:
        Ref: MatchExpress
Outputs:
  DynamicTagRuleId:
    Description: Dynamic tag rule ID.
    Value:
      'Fn::GetAtt':
        - DynamicTagGroup
        - DynamicTagRuleId
  TagKey:
    Description: Tag key.
    Value:
      'Fn::GetAtt':
        - DynamicTagGroup
        - TagKey
```

