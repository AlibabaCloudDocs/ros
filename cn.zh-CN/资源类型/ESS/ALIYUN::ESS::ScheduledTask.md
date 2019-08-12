# ALIYUN::ESS::ScheduledTask {#concept_rwn_fy1_rgb .concept}

ALIYUN::ESS::ScheduledTask类型用于根据传入参数创建定时任务。

## 语法 {#section_xxx_ff1_mfb .section}

```language-json
{
  "Type": "ALIYUN::ESS::ScheduledTask",
  "Properties": {
    "TaskEnabled": Boolean,
    "Description": String,
    "ScheduledTaskName": String,
    "LaunchExpirationTime": Integer,
    "LaunchTime": String,
    "RecurrenceEndTime": String,
    "RecurrenceType": String,
    "RecurrenceValue": String,
    "ScheduledAction": String
  }
}
```

## 属性 {#section_gmr_gf1_mfb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|TaskEnabled|Boolean|否|是| 是否启动定时任务。

 -   true：启动任务；
-   false：停止任务。

 默认为true。

 |无|
|Description|String|否|是|定时任务的描述信息。|2-200 个英文或中文字符。|
|ScheduledTaskName|String|否|是|定时任务的显示名称。| 2-40 个英文或中文字符，以数字、大小字母或中文开头，可包含数字，"\_"、"-"或”.”。

 同一用户账号同一地域内唯一。

 如果没有指定该参数，默认值为ScheduledScalingTaskId。

 |
|LaunchExpirationTime|Integer|否|是| 定时任务触发操作失败后，在此时间内重试。

 默认600秒。

 |取值范围：\[0, 21600\]|
|LaunchTime|String|是|是| 定时任务触发的时间点。

 按照ISO8601标准表示，并需要使用UTC时间。

 如果指定了RecurrenceType，则此属性指定的时间点，默认为循环执行的时间点。

 如果未指定RecurrenceType，则按指定的日期和时间执行一次。

 不能填写自创建或修改当天起90日后的时间。

 |格式为：YYYY-MM-DDThh:mmZ。|
|RecurrenceEndTime|String|否|是| 重复执行定时任务的结束时间。

 按照ISO8601标准表示，并需要使用UTC时间。

 不能填写自创建或修改当天起90日后的时间。

 RecurrenceType、RecurrenceValue和RecurrenceEndTime需要同时指定。

 |格式为：YYYY-MM-DDThh:mmZ。|
|RecurrenceType|String|否|是|重复执行定时任务的类型。|可选值： -   Daily：每多少天重复执行一次定时任务。
-   Weekly：每周指定几天重复执行一次定时任务。
-   Monthly：每月内指定几天重复执行一次定时任务。
-   Cron：按照指定的Cron表达式执行定时任务。

 RecurrenceType、RecurrenceValue和RecurrenceEndTime需要同时指定。

 |
|RecurrenceValue|String|否|是|重复执行定时任务的数值。| -   Daily：只能填一个值，取值范围：\[1,31\]。
-   Weekly：可以填入多值。周日、周一……周六的值依次为：0, 1,2,…, 6，多天使用英文逗号（,）分隔。
-   Monthly：格式为A-B。A、B的取值范围为\[1,31\]，并且B必须大于等于A。
-   Cron：表示UTC时间，支持分、时、日、月、星期的5域表达式，支持通配符英文逗号（,）、英文问号（?）、连词符（-）、星号（\*）、井号（\#）、斜线（/）、L 和 W。

 RecurrenceType、RecurrenceValue和RecurrenceEndTime需要同时指定。

 |
|ScheduledAction|String|是|是| 定时任务触发时需要执行的操作。

 此处填写伸缩规则的唯一标识符。

 |字符最大长度200。|

## 返回值 {#section_x4l_kf1_mfb .section}

**Fn::GetAtt**

ScheduledTaskId： 定时任务的ID，由系统生成，全局唯一。

## 示例 {#section_mmh_mf1_mfb .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "ScheduledTask": {
      "Type": "ALIYUN::ESS::ScheduledTask",
      "Properties": {
        "TaskEnabled": "true",
        "Description": "scheduledtask",
        "ScheduledTaskName": "task1",
        "LaunchTime": "2014-08-17T16:52Z",
        "RecurrenceEndTime": "2014-08-17T16:55Z",
        "RecurrenceType": "Daily",
        "RecurrenceValue": "1",
        "ScheduledAction": "ari:acs:ess:cn-qingdao:1344371:scalingRule/cCBpdYdQuBe2cUxOdu6piOk"
      }
    }
  },
  "Outputs": {
    "ScheduledTaskId": {
      "Value": {
        "FN::GetAtt": [
          "ScheduledTask",
          "ScheduledTaskId"
        ]
      }
    }
  }
}
```

