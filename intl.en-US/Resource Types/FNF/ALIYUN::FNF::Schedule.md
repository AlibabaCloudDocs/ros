# ALIYUN::FNF::Schedule

ALIYUN::FNF::Schedule is used to create a time-based schedule.

## Syntax

```
{
  "Type": "ALIYUN::FNF::Schedule",
  "Properties": {
    "Description": String,
    "FlowName": String,
    "Enable": Boolean,
    "Payload": String,
    "CronExpression": String,
    "ScheduleName": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Description|String|No|Yes|The description of the time-based schedule.|None|
|FlowName|String|Yes|No|The name of the flow that is bound to the time-based schedule.|None|
|Enable|Boolean|No|Yes|Specifies whether to enable the time-based schedule.|Valid values: -   true
-   false |
|Payload|String|No|Yes|The trigger message of the time-based schedule.|The value of this parameter must be in the JSON format. Example: `"{\"key\": \"value\"}"`.|
|CronExpression|String|Yes|Yes|The cron expression of the time-based schedule.|None|
|ScheduleName|String|Yes|No|The name of the time-based schedule.|None|

## Response parameters

Fn::GetAtt

-   FlowName: the name of the flow that is bound to the time-based schedule.
-   ScheduleId: the ID of the time-based schedule.
-   ScheduleName: the name of the time-based schedule.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Description": {
      "Type": "String",
      "Description": "Description of the schedule."
    },
    "FlowName": {
      "Type": "String",
      "Description": "Flow name."
    },
    "Enable": {
      "Type": "Boolean",
      "Description": "Whether enable schedule.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "Payload": {
      "Type": "String",
      "Description": "Payload."
    },
    "CronExpression": {
      "Type": "String",
      "Description": "Cron expression."
    },
    "ScheduleName": {
      "Type": "String",
      "Description": "Schedule name."
    }
  },
  "Resources": {
    "Schedule": {
      "Type": "ALIYUN::FNF::Schedule",
      "Properties": {
        "Description": {
          "Ref": "Description"
        },
        "FlowName": {
          "Ref": "FlowName"
        },
        "Enable": {
          "Ref": "Enable"
        },
        "Payload": {
          "Ref": "Payload"
        },
        "CronExpression": {
          "Ref": "CronExpression"
        },
        "ScheduleName": {
          "Ref": "ScheduleName"
        }
      }
    }
  },
  "Outputs": {
    "FlowName": {
      "Description": "Flow name.",
      "Value": {
        "Fn::GetAtt": [
          "Schedule",
          "FlowName"
        ]
      }
    },
    "ScheduleId": {
      "Description": "Schedule Id",
      "Value": {
        "Fn::GetAtt": [
          "Schedule",
          "ScheduleId"
        ]
      }
    },
    "ScheduleName": {
      "Description": "Schedule name.",
      "Value": {
        "Fn::GetAtt": [
          "Schedule",
          "ScheduleName"
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
  Description:
    Type: String
    Description: Description of the schedule.
  FlowName:
    Type: String
    Description: Flow name.
  Enable:
    Type: Boolean
    Description: Whether enable schedule.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
  Payload:
    Type: String
    Description: Payload.
  CronExpression:
    Type: String
    Description: Cron expression.
  ScheduleName:
    Type: String
    Description: Schedule name.
Resources:
  Schedule:
    Type: 'ALIYUN::FNF::Schedule'
    Properties:
      Description:
        Ref: Description
      FlowName:
        Ref: FlowName
      Enable:
        Ref: Enable
      Payload:
        Ref: Payload
      CronExpression:
        Ref: CronExpression
      ScheduleName:
        Ref: ScheduleName
Outputs:
  FlowName:
    Description: Flow name.
    Value:
      'Fn::GetAtt':
        - Schedule
        - FlowName
  ScheduleId:
    Description: Schedule Id
    Value:
      'Fn::GetAtt':
        - Schedule
        - ScheduleId
  ScheduleName:
    Description: Schedule name.
    Value:
      'Fn::GetAtt':
        - Schedule
        - ScheduleName
```

