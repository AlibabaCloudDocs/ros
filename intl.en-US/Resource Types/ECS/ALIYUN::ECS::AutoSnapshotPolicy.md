# ALIYUN::ECS::AutoSnapshotPolicy {#concept_tjw_v2k_wgb .concept}

Configures the policy for automatically creating snapshots.

## Syntax {#section_xyg_tn2_lfb .section}

```language-json
{
  "Type" : "ALIYUN::ECS::AutoSnapshotPolicy",
  "Properties" : {
    "TimePoints" : String,
    "RepeatWeekdays" : String,
    "RetentionDays" : Integer,
    "DiskIds" : String,
    "AutoSnapshotPolicyName" : String
  }
}
```

## Properties {#section_cgd_53n_4fb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|TimePoints|List|Yes|Yes|The time for automatically creating snapshots, measured in hours.| The value ranges from 0 to 23, indicating 24 hours. For example, `1` indicates 01:00. Set the TimePoints parameter to an array if you want to schedule multiple automatic snapshot tasks for a day.

 -   A maximum of 24 points in time can be specified at a time.
-   List the points in time in the format of \[0, 1, ... 23\] and use half-width commas \(,\) to separate each value.

 |
|RepeatWeekdays|List|Yes|Yes|The points in time for the recurring task of automatically creating snapshots. Unit: day. Recurring cycle: week.| The value ranges from 1 to 7, indicating the seven days of a week. For example, `1` indicates Monday. Set the RepeatWeekdays parameter to an array if you want to schedule multiple points in time for the recurring task of automatically creating snapshots within a week.

 -   A maximum of seven days can be specified at a time.
-   List the days in the format of \[1, 2, ... 7\] and use half-width commas \(,\) to separate the days.

 |
|RetentionDays|Integer|Yes|Yes|The duration during which a snapshot can be retained. Unit: day.| Valid values:

 -   -1: indicates that the snapshots are permanently retained.
-   \[1, 65536\]: indicates the number of days during which the snapshots are retained.

 Default value: -1.

 |
|DiskIds|List|Yes|Yes| The destination disk ID.

 To apply an automatic snapshot policy to more than one disk, list the disk IDs in the form of \[\["d-xxxxxxxxx", "d-yyyyyyyyy", … "d-zzzzzzzzz"\], and use half-width commas \(,\) to separate disk IDs.

 |N/A|
|AutoSnapshotPolicyName|String|No|Yes|The name of the automatic snapshot policy.| -   The name must be 2 to 128 characters in length
-   and can contain digits, colons\(:\), underscores \(\_\), and hyphens \(-\).
-   It must start with an uppercase letter, lowercase letter, or a Chinese character and must not start with http:// or https://.

 Default value: empty.

 |

## Response elements {#section_fsg_t4n_4fb .section}

**FN::GetAtt**

-   AutoSnapshotPolicyId: indicates the ID of the automatic snapshot policy.

## Example {#section_klp_54n_4fb .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "AutoSnapshotPolicy": {
      "Type": "ALIYUN::ECS::AutoSnapshotPolicy",
      "Properties": {
        "TimePoints": ["0"],
        "RepeatWeekdays": ["1"],
        "RetentionDays": 10,
        "DiskIds": ["<DiskId>"],
        "AutoSnapshotPolicyName": "MyAutoSnapshotPolicy"
      }
    }
  }
}
```

