# ALIYUN::CMS::EventRule

ALIYUN::CMS::EventRule类型用于创建或者修改事件的报警规则。如果报警规则名称不存在，则创建新的报警规则；如果报警规则存在，则修改已有的报警规则。

## 语法

```
{
  "Type": "ALIYUN::CMS::EventRule",
  "Properties": {
    "Description": String,
    "EventType": String,
    "EventPattern": List,
    "State": String,
    "RuleName": String,
    "GroupId": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Description|String|否|是|报警规则描述信息。|无|
|EventType|String|否|是|事件报警类型。|取值：-   SYSTEM：系统事件。
-   CUSTOM：自定义事件。 |
|EventPattern|List|是|是|事件模式相关参数。|列表最大长度为50。详情请参见[EventPattern属性](#section_zls_ezy_5fg)。 |
|State|String|否|是|报警规则状态。|取值：-   ENABLED：启用。
-   DISABLED：禁用。 |
|RuleName|String|是|否|报警规则名称。|无|
|GroupId|String|否|是|应用分组ID。|无|

## EventPattern语法

```
"EventPattern": [
  {
    "StatusList": List,
    "NameList": List,
    "Product": String,
    "EventTypeList": List,
    "LevelList": List
  }
]
```

## EventPattern属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|StatusList|List|否|是|事件状态。|无|
|NameList|List|否|是|事件名称。|无|
|Product|String|否|是|产品类型。|无|
|EventTypeList|List|否|是|事件类型。|星号（\*）表示不限制类型。|
|LevelList|List|否|是|事件报警等级。|取值：-   CRITICAL：严重。
-   WARN：警告。
-   INFO：信息。

星号（\*）表示所有等级。|

## 返回值

Fn::GetAtt

Data：报警规则变更行数。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "EventRule": {
      "Type": "ALIYUN::CMS::EventRule",
      "Properties": {
        "Description": {
          "Ref": "Description"
        },
        "EventType": {
          "Ref": "EventType"
        },
        "EventPattern": {
          "Ref": "EventPattern"
        },
        "State": {
          "Ref": "State"
        },
        "RuleName": {
          "Ref": "RuleName"
        },
        "GroupId": {
          "Ref": "GroupId"
        }
      }
    }
  },
  "Parameters": {
    "Description": {
      "Type": "String",
      "Description": "The description of the alert rule."
    },
    "EventType": {
      "Type": "String",
      "Description": "The type of the event alert. Valid values: SYSTEM or CUSTOM."
    },
    "EventPattern": {
      "Type": "Json"
    },
    "State": {
      "Type": "String",
      "Description": "The status of the alert rule. Valid values: ENABLED or DISABLED."
    },
    "RuleName": {
      "Type": "String",
      "Description": "The name of the alarm rule."
    },
    "GroupId": {
      "Type": "String",
      "Description": "The ID of the application group."
    }
  },
  "Outputs": {
    "Data": {
      "Description": "Number of rows affected.",
      "Value": {
        "Fn::GetAtt": [
          "EventRule",
          "Data"
        ]
      }
    }
  }
}
```

`YAML`格式

```
ROSTemplateFormatVersion: '2015-09-01'
Resources:
  EventRule:
    Type: ALIYUN::CMS::EventRule
    Properties:
      Description:
        Ref: Description
      EventType:
        Ref: EventType
      EventPattern:
        Ref: EventPattern
      State:
        Ref: State
      RuleName:
        Ref: RuleName
      GroupId:
        Ref: GroupId
Parameters:
  Description:
    Type: String
    Description: The description of the alert rule.
  EventType:
    Type: String
    Description: The type of the event alert. Valid values: SYSTEM or CUSTOM.
  EventPattern:
    Type: Json
  State:
    Type: String
    Description: The status of the alert rule. Valid values: ENABLED or DISABLED.
  RuleName:
    Type: String
    Description: The name of the alarm rule.
  GroupId:
    Type: String
    Description: The ID of the application group.
Outputs:
  Data:
    Description: Number of rows affected.
    Value:
      Fn::GetAtt:
      - EventRule
      - Data
```

