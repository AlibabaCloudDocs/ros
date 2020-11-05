# ALIYUN::SLS::Alert

ALIYUN::SLS::Alert类型用于创建告警。

## 语法

```
{
  "Type": "ALIYUN::SLS::Alert",
  "Properties": {
    "Project": String,
    "Detail": Map
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Project|String|是|否|日志项目名称。|无|
|Detail|Map|是|是|告警详情。|无|

## Detail语法

```
"Detail": {
  "Type": String,
  "Description": String,
  "Configuration": Map,
  "State": String,
  "Schedule": Map,
  "DisplayName": String,
  "Name": String
}
```

## Detail属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Type|String|否|否|告警类型。|无|
|Description|String|否|是|告警描述信息。|无|
|Configuration|Map|是|是|告警配置。|更多信息，请参见[Configuration属性](#section_nql_9cc_y8a)。|
|State|String|否|否|是否启用告警。|取值：-   Enable：启用。
-   Disabled：不启用。 |
|Schedule|Map|是|是|日志服务评估警报规则的时间间隔。|在警报规则评估期间，如果查询返回的日志条目超过100个，则只检查前100个日志条目。更多信息，请参见[Schedule属性](#section_ovp_1vg_fhp)。 |
|DisplayName|String|是|是|告警显示的名称。|长度为1~64个文字符。|
|Name|String|是|否|告警名称。|无|

## Configuration语法

```
"Configuration": {
  "Throttling": String,
  "Condition": String,
  "NotificationList": List,
  "NotifyThreshold": Integer,
  "Dashboard": String,
  "QueryList": List
}
```

## Configuration属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Throttling|String|是|是|通知间隔。|无|
|Condition|String|是|是|触发条件。|支持加（+）、减（-）、乘（\*）、除（/）、取模（%）5种基础运算符和大于（\>）、大于等于（\>=）、小于（<）、小于等于（<=）、等于（==）、不等于（!=）、正则匹配 （=~）、 正则不匹配（!~）8种比较运算符。更多信息，请参见[告警条件表达式语法](/cn.zh-CN/可视化与告警/告警/参考信息/告警条件表达式语法.md)。 |
|NotificationList|List|否|是|通知列表。|更多信息，请参见[NotificationList属性](#section_9gb_q4h_hsj)。|
|NotifyThreshold|Integer|否|是|触发通知阈值。|无|
|Dashboard|String|是|是|所属仪表盘。|无|
|QueryList|List|是|是|查询列表。|更多信息，请参见[QueryList属性](#section_vjj_ndk_7n6)。|

## NotificationList语法

```
"NotificationList": [
  {
    "Type": String,
    "MobileList": List,
    "ServiceUri": String,
    "Content": String,
    "EmailList": List
  }
]
```

## NotificationList属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Type|String|是|否|通知类型。|取值：-   SMS：短信。
-   Voice：语音。
-   Email：电子邮件。
-   MessageCenter：通知中心。
-   DingTalk：WebHook-钉钉机器人。
-   Webhook：WebHook-自定义。 |
|Content|String|否|否|通知内容。|支持使用模版变量：`${Project}, ${Condition}, ${AlertName}, ${AlertID}, ${Dashboard}, ${FireTime}, ${Results}`。更多信息，请参见[通知方式](/cn.zh-CN/可视化与告警/告警/通知方式.md)。 |
|MobileList|List|否|否|手机号码。|通知类型为短信、语音时该参数必填。

同一手机号码每天接收的通知不超过50条。 |
|ServiceUri|String|否|否|请求地址。|通知类型为WebHook-自定义或WebHook-钉钉机器人时该参数必填。|
|EmailList|List|否|否|收件人。|通知类型为电子邮件时该参数必填。同一邮箱每天接收的邮件不超过100条。 |

## QueryList语法

```
"QueryList": [
  {
    "Query": String,
    "LogStore": String,
    "Start": String,
    "TimeSpanType": String,
    "End": String,
    "ChartTitle": String
  }
]
```

## QueryList属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Query|String|是|否|查询语句。|无|
|LogStore|String|是|否|日志库。|无|
|Start|String|是|否|查询开始时间。|无|
|TimeSpanType|String|是|否|查询区间。|无|
|End|String|是|否|查询结束时间。|无|
|ChartTitle|String|是|否|图表标题。|无|

## Schedule语法

```
"Schedule": {
  "Type": String,
  "Interval": String
}
```

## Schedule属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Type|String|是|是|类型。|取值：-   Hourly：每小时。
-   Daily：每天。
-   Weekly：每周。
-   FixedRate：固定间隔。
-   Cron：Cron表达式。 |
|Interval|String|是|是|间隔。|无|

## 返回值

Fn::GetAtt

Name：告警名称。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Project": {
      "Type": "String",
      "Description": "Project name:\n1. Only supports lowercase letters, numbers, hyphens (-) and underscores (_).\n2. Must start and end with lowercase letters and numbers.\n3. The name length is 3-63 characters.",
      "AllowedPattern": "^[a-zA-Z0-9_-]+$",
      "MinLength": 3,
      "MaxLength": 63
    },
    "Detail": {
      "Type": "Json",
      "Description": ""
    }
  },
  "Resources": {
    "Alert": {
      "Type": "ALIYUN::SLS::Alert",
      "Properties": {
        "Project": {
          "Ref": "Project"
        },
        "Detail": {
          "Ref": "Detail"
        }
      }
    }
  },
  "Outputs": {
    "Name": {
      "Description": "Alert name.",
      "Value": {
        "Fn::GetAtt": [
          "Alert",
          "Name"
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
  Project:
    Type: String
    Description: >-
      Project name:

      1. Only supports lowercase letters, numbers, hyphens (-) and underscores
      (_).

      2. Must start and end with lowercase letters and numbers.

      3. The name length is 3-63 characters.
    AllowedPattern: '^[a-zA-Z0-9_-]+$'
    MinLength: 3
    MaxLength: 63
  Detail:
    Type: Json
    Description: ''
Resources:
  Alert:
    Type: 'ALIYUN::SLS::Alert'
    Properties:
      Project:
        Ref: Project
      Detail:
        Ref: Detail
Outputs:
  Name:
    Description: Alert name.
    Value:
      'Fn::GetAtt':
        - Alert
        - Name
```

