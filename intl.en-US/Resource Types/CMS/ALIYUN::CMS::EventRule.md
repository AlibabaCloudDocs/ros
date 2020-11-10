# ALIYUN::CMS::EventRule

ALIYUN::CMS::EventRule is used to create or modify an event-triggered alert rule. If the specified rule name does not exist, an event-triggered alert rule is created. If the specified rule name exists, the specified event-triggered alert rule is modified.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Description|String|No|Yes|The description of the alert rule.|None|
|EventType|String|No|Yes|The type of the event.|Valid values:-   SYSTEM
-   CUSTOM |
|EventPattern|List|Yes|Yes|The list of event pattern parameters.|The list can contain a maximum of 50 event pattern parameters.For more information, see [EventPattern properties](#section_zls_ezy_5fg). |
|State|String|No|Yes|The status of the alert rule.|Valid values:-   ENABLED
-   DISABLED |
|RuleName|String|Yes|No|The name of the alert rule.|None|
|GroupId|String|No|Yes|The ID of the application group.|None|

## EventPattern syntax

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

## EventPattern properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|StatusList|List|No|Yes|The list of one or more event statuses.|None|
|NameList|List|No|Yes|The list of one or more event names.|None|
|Product|String|No|Yes|The type of the cloud service.|None|
|EventTypeList|List|No|Yes|The list of one or more event types.|An asterisk \(\*\) indicates all types.|
|LevelList|List|No|Yes|The list of event alert levels.|Valid values:-   CRITICAL
-   WARN
-   INFO

An asterisk \(\*\) indicates all levels.|

## Response parameters

Fn::GetAtt

Data: the number of rows that are affected by the event-triggered alert rule.

## Examples

`JSON` format

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

`YAML` format

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

