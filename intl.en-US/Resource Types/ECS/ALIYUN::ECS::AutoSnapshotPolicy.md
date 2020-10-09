# ALIYUN::ECS::AutoSnapshotPolicy

ALIYUN::ECS::AutoSnapshotPolicy is used to create an automatic snapshot policy.

## Syntax

```
{
  "Type" : "ALIYUN::ECS::AutoSnapshotPolicy",
  "Properties" : {
    "TimePoints" : String,
    "RepeatWeekdays" : String,
    "RetentionDays" : Integer,
    "DiskIds" : List,
    "AutoSnapshotPolicyName" : String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|TimePoints|List|Yes|Yes|The points in time at which to create automatic snapshots.|Valid values: 0 to 23. The values correspond to the hours of a day from 00:00 to 23:00. For example, 1 indicates 01:00.Unit: hours.

To schedule multiple automatic snapshots to be created in a day, you can specify multiple hours.

-   You can specify up to 24 hours in a day.
-   You must specify the parameter as a list. Example: \[0, 1, ... 23\]. Separate multiple hours with commas \(,\). |
|RepeatWeekdays|List|Yes|Yes|The days of a week on which to create automatic snapshots.|Valid values: 1 to 7, which correspond to Monday to Sunday. 1 indicates Monday.Unit: days.

Cycle: week.

To schedule multiple automatic snapshots to be created in a week, you can specify multiple days.

-   You can specify up to seven days over a one-week period.
-   You must specify the parameter as a list. Example: \[1, 2, ... 7\]. Separate multiple days with commas \(,\). |
|RetentionDays|Integer|Yes|Yes|The number of days for which you want to retain automatic snapshots.|Default value: -1. Valid values:

-   -1: Automatic snapshots are permanently retained.
-   1 to 65535: Automatic snapshots are retained for a specified number of days.

Unit: days. |
|DiskIds|List|No|Yes|The IDs of disks to which you want to apply the automatic snapshot policy.

|To apply the automatic snapshot policy to multiple disks, set this parameter to a list in the \["d-xxxxxxxxx", "d-yyyyyyyyy", ... "d-zzzzzzzzz"\] format. Separate multiple IDs with commas \(,\).|
|AutoSnapshotPolicyName|String|No|Yes|The name of the automatic snapshot policy.|The name must be 2 to 128 characters in length and can contain letters, digits, periods \(.\), underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with `http://` or `https://`. This parameter is empty by default. |

## Response parameters

Fn::GetAtt

AutoSnapshotPolicyId: the ID of the automatic snapshot policy.

## Examples

`JSON` format

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

`YAML` format

```
ROSTemplateFormatVersion: '2015-09-01'
Parameters:
  TimePoints:
    Type: CommaDelimitedList
    Description: >-
      The automatic snapshot creation schedule, and the unit of measurement is
      hour. Value range: [0, 23], which represents from 00:00 to 24:00, for
      example 1 indicates 01:00. When you want to schedule multiple automatic
      snapshot tasks for a disk in a day, you can set the TimePoints to an
      array.

      A maximum of 24 time points can be selected.

      The format is a list of [0, 1, ..., 23] and the time points are separated
      by commas (,).
  DiskIds:
    Type: Json
    Description: >-
      The disk ID. When you want to apply the automatic snapshot policy to
      multiple disks, you can set the DiskIds to an array. The format is list of
      ["d-xxxxxxxxx", "d-yyyyyyyyy", ..., "d-zzzzzzzzz"] and the IDs are
      separated by commas (,).
  RetentionDays:
    Type: Number
    Description: >-
      The snapshot retention time, and the unit of measurement is day. Optional
      values:

      -1: The automatic snapshots are retained permanently.

      [1, 65536]: The number of days retained.

      Default value: -1.
    MinValue: -1
    MaxValue: 65536
  RepeatWeekdays:
    Type: Json
    Description: >-
      The automatic snapshot repetition dates. The unit of measurement is day
      and the repeating cycle is a week. Value range: [1, 7], which represents
      days starting from Monday to Sunday, for example 1 indicates Monday. When
      you want to schedule multiple automatic snapshot tasks for a disk in a
      week, you can set the RepeatWeekdays to an array.

      A maximum of seven time points can be selected.

      The format is a list of [1, 2, ..., 7] and the time points are separated
      by commas (,).
  AutoSnapshotPolicyName:
    Type: String
    Description: >-
      The name of the automatic snapshot policy.

      It can consist of [2, 128] English or Chinese characters.

      Must begin with an uppercase or lowercase letter or a Chinese character.
      Can contain numbers, periods (.), colons (:), underscores (_), and hyphens
      (-).

      Cannot start with http:// or https://.

      Default value: null.
Resources:
  AutoSnapshotPolicy:
    Type: 'ALIYUN::ECS::AutoSnapshotPolicy'
    Properties:
      TimePoints:
        Ref: TimePoints
      DiskIds:
        Ref: DiskIds
      RetentionDays:
        Ref: RetentionDays
      RepeatWeekdays:
        Ref: RepeatWeekdays
      AutoSnapshotPolicyName:
        Ref: AutoSnapshotPolicyName
Outputs:
  AutoSnapshotPolicyId:
    Description: The automatic snapshot policy ID.
    Value:
      'Fn::GetAtt':
        - AutoSnapshotPolicy
        - AutoSnapshotPolicyId
```

