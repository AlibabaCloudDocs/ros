# ALIYUN::FNF::Schedule

ALIYUN::FNF::Schedule类型用于创建一个定时调度。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Description|String|否|是|定时调度描述。|无|
|FlowName|String|是|否|定时调度绑定的工作流名称。|无|
|Enable|Boolean|否|是|定时调度是否启用。|取值： -   true
-   false |
|Payload|String|否|是|定时调度触发消息。|必须为JSON格式，示例值：`"{\"key\": \"value\"}"`。|
|CronExpression|String|是|是|cron表达式。|无|
|ScheduleName|String|是|否|定时调度名称。|无|

## 返回值

Fn::GetAtt

-   FlowName：定时调度绑定的工作流名称。
-   ScheduleId：定时调度ID。
-   ScheduleName：定时调度名称。

## 示例

`JSON`格式

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

`YAML`格式

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

