# ALIYUN::ECS::AutoSnapshotPolicy

ALIYUN::ECS::AutoSnapshotPolicy用于创建自动快照策略。

## 语法

```
{
  "Type" : "ALIYUN::ECS::AutoSnapshotPolicy",
  "Properties" : {
    "TimePoints" : String,
    "RepeatWeekdays" : String,
    "RetentionDays" : Integer,
    "DiskIds" : List,
    "Tags": List,
    "AutoSnapshotPolicyName" : String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|TimePoints|List|是|是|自动快照的创建时间点。|取值范围：0~23。表示00:00至23:00共24个时间点，例如：1表示01:00。单位：小时。

当一天内需要创建多次自动快照时，可以传入多个时间点：

-   最多传入24个时间点。
-   多个时间点用格式为\[0, 1, … 23\]的列表表示，时间点之间用半角逗号（,）隔开。 |
|RepeatWeekdays|List|是|是|自动快照的重复日期。|取值：1~7，依次表示周一至周日。周期：星期。

如果一星期内需要创建多次自动快照时，可设置多个时间点，多个时间点用\[1, 2, … 7\]的列表表示，多个时间点之间用半角逗号（,）隔开。最多设置7个时间点。 |
|RetentionDays|Integer|是|是|自动快照的保留时间。|取值范围：

-   -1（默认值）：永久保存。
-   1~65,535：指定保存天数。

单位：天。 |
|DiskIds|List|否|是|目标磁盘ID。

|当您需要将自动快照策略应用于多块磁盘时，多块磁盘ID用\["d-xxxxxxxxx", "d-yyyyyyyyy", … "d-zzzzzzzzz"\]的列表表示，磁盘ID之间用半角逗号（,）隔开。|
|Tags|List|否|是|标签。|最多支持添加20个标签。更多信息，请参见[Tags属性](#section_vuj_is5_fgo)。 |
|AutoSnapshotPolicyName|String|否|是|自动快照策略的名称。|长度为2~128个字符。必须以英文字母或汉字开头，不能以`http://`和`https://`开头。可包含英文字母、汉字、数字、半角冒号（:）、下划线（\_）或短划线（-）。默认值：空。 |

## Tags语法

```
"Tags": [
  {
    "Key": String,
    "Value": String
  }
]  
```

## Tags属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Key|String|是|否|标签键。|长度为1~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或者`https://` 。|
|Value|String|否|否|标签值。|长度为0~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或者`https://` 。|

## 返回值

Fn::GetAtt

AutoSnapshotPolicyId：自动快照策略ID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "TimePoints": {
      "Type": "CommaDelimitedList",
      "Description": "The automatic snapshot creation schedule, and the unit of measurement is hour. Value range: [0, 23], which represents from 00:00 to 24:00, for example 1 indicates 01:00. When you want to schedule multiple automatic snapshot tasks for a disk in a day, you can set the TimePoints to an array.\nA maximum of 24 time points can be selected.\nThe format is a list of [0, 1, ..., 23] and the time points are separated by commas (,)."
    },
    "DiskIds": {
      "Type": "Json",
      "Description": "The disk ID. When you want to apply the automatic snapshot policy to multiple disks, you can set the DiskIds to an array. The format is list of [\"d-xxxxxxxxx\", \"d-yyyyyyyyy\", ..., \"d-zzzzzzzzz\"] and the IDs are separated by commas (,)."
    },
    "RetentionDays": {
      "Type": "Number",
      "Description": "The snapshot retention time, and the unit of measurement is day. Optional values:\n-1: The automatic snapshots are retained permanently.\n[1, 65536]: The number of days retained.\nDefault value: -1.",
      "MinValue": -1,
      "MaxValue": 65536
    },
    "RepeatWeekdays": {
      "Type": "Json",
      "Description": "The automatic snapshot repetition dates. The unit of measurement is day and the repeating cycle is a week. Value range: [1, 7], which represents days starting from Monday to Sunday, for example 1 indicates Monday. When you want to schedule multiple automatic snapshot tasks for a disk in a week, you can set the RepeatWeekdays to an array.\nA maximum of seven time points can be selected.\nThe format is a list of [1, 2, ..., 7] and the time points are separated by commas (,)."
    },
    "AutoSnapshotPolicyName": {
      "Type": "String",
      "Description": "The name of the automatic snapshot policy.\nIt can consist of [2, 128] English or Chinese characters.\nMust begin with an uppercase or lowercase letter or a Chinese character. Can contain numbers, periods (.), colons (:), underscores (_), and hyphens (-).\nCannot start with http:// or https://.\nDefault value: null."
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to instance. Max support 20 tags to add during create instance. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
    }
  },
  "Resources": {
    "AutoSnapshotPolicy": {
      "Type": "ALIYUN::ECS::AutoSnapshotPolicy",
      "Properties": {
        "TimePoints": {
          "Ref": "TimePoints"
        },
        "DiskIds": {
          "Ref": "DiskIds"
        },
        "RetentionDays": {
          "Ref": "RetentionDays"
        },
        "RepeatWeekdays": {
          "Ref": "RepeatWeekdays"
        },
        "AutoSnapshotPolicyName": {
          "Ref": "AutoSnapshotPolicyName"
        },
        "Tags": {
          "Ref": "Tags"
        }
      }
    }
  },
  "Outputs": {
    "AutoSnapshotPolicyId": {
      "Description": "The automatic snapshot policy ID.",
      "Value": {
        "Fn::GetAtt": [
          "AutoSnapshotPolicy",
          "AutoSnapshotPolicyId"
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
  AutoSnapshotPolicyName:
    Description: 'The name of the automatic snapshot policy.

      It can consist of [2, 128] English or Chinese characters.

      Must begin with an uppercase or lowercase letter or a Chinese character. Can
      contain numbers, periods (.), colons (:), underscores (_), and hyphens (-).

      Cannot start with http:// or https://.

      Default value: null.'
    Type: String
  DiskIds:
    Description: The disk ID. When you want to apply the automatic snapshot policy
      to multiple disks, you can set the DiskIds to an array. The format is list of
      ["d-xxxxxxxxx", "d-yyyyyyyyy", ..., "d-zzzzzzzzz"] and the IDs are separated
      by commas (,).
    Type: Json
  RepeatWeekdays:
    Description: 'The automatic snapshot repetition dates. The unit of measurement
      is day and the repeating cycle is a week. Value range: [1, 7], which represents
      days starting from Monday to Sunday, for example 1 indicates Monday. When you
      want to schedule multiple automatic snapshot tasks for a disk in a week, you
      can set the RepeatWeekdays to an array.

      A maximum of seven time points can be selected.

      The format is a list of [1, 2, ..., 7] and the time points are separated by
      commas (,).'
    Type: Json
  RetentionDays:
    Description: 'The snapshot retention time, and the unit of measurement is day.
      Optional values:

      -1: The automatic snapshots are retained permanently.

      [1, 65536]: The number of days retained.

      Default value: -1.'
    MaxValue: 65536
    MinValue: -1
    Type: Number
  Tags:
    Description: Tags to attach to instance. Max support 20 tags to add during create
      instance. Each tag with two properties Key and Value, and Key is required.
    MaxLength: 20
    Type: Json
  TimePoints:
    Description: 'The automatic snapshot creation schedule, and the unit of measurement
      is hour. Value range: [0, 23], which represents from 00:00 to 24:00, for example
      1 indicates 01:00. When you want to schedule multiple automatic snapshot tasks
      for a disk in a day, you can set the TimePoints to an array.

      A maximum of 24 time points can be selected.

      The format is a list of [0, 1, ..., 23] and the time points are separated by
      commas (,).'
    Type: CommaDelimitedList
Resources:
  AutoSnapshotPolicy:
    Properties:
      AutoSnapshotPolicyName:
        Ref: AutoSnapshotPolicyName
      DiskIds:
        Ref: DiskIds
      RepeatWeekdays:
        Ref: RepeatWeekdays
      RetentionDays:
        Ref: RetentionDays
      Tags:
        Ref: Tags
      TimePoints:
        Ref: TimePoints
    Type: ALIYUN::ECS::AutoSnapshotPolicy
Outputs:
  AutoSnapshotPolicyId:
    Description: The automatic snapshot policy ID.
    Value:
      Fn::GetAtt:
      - AutoSnapshotPolicy
      - AutoSnapshotPolicyId
```

更多示例，请参见：[JSON示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ECS/JSON/AutoSnapshotPolicy.json)和[YAML示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ECS/YAML/AutoSnapshotPolicy.yml)。

