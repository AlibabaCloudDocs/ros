# ALIYUN::CMS::DynamicTagGroup

ALIYUN::CMS::DynamicTagGroup类型用于云产品自动创建应用分组。

**说明：** 目前只支持云服务器ECS（Elastic Compute Service）、阿里云关系型数据库RDS（Relational Database Service）、负载均衡SLB（Server Load Balancer）。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ContactGroupList|List|是|否|报警联系人。|无|
|MatchExpressFilterRelation|String|否|否|条件表达式之间的关系。|取值：-   and：与的关系。
-   or：或的关系。 |
|EnableSubscribeEvent|Boolean|否|否|是否启用事件订阅。|取值：-   true：启用。
-   false：不启用。 |
|TemplateIdList|List|否|否|报警模板ID。|无|
|TagKey|String|是|否|标签键。|无|
|EnableInstallAgent|Boolean|否|否|是否启用初始化安装监控插件。|取值：-   true：启用。

**说明：** 如果生成应用分组的ECS实例没有安装监控插件则会尝试自动安装。

-   false（默认值）：不启用。 |
|MatchExpress|List|否|否|条件表达式。|只允许设置一个条件表达式。详情请参见[MatchExpress属性](#section_klz_dlm_73a)。 |

## MatchExpress语法

```
"MatchExpress": [
  {
    "TagValue": String,
    "TagValueMatchFunction": String
  }
]
```

## MatchExpress属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|TagValue|String|是|否|标签值。|无|
|TagValueMatchFunction|String|是|否|标签值的匹配方法。|取值：-   contains：包含。
-   startWith：前缀。
-   endWith：后缀。
-   notContains：不包含。
-   equals：等于。
-   all：全部。 |

## 返回值

Fn::GetAtt

-   DynamicTagRuleId：智能标签规则ID。
-   TagKey：标签键。

## 示例

`JSON`格式

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

`YAML`格式

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

