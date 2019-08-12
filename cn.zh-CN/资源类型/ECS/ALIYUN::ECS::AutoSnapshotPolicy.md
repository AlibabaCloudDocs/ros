# ALIYUN::ECS::AutoSnapshotPolicy {#concept_tjw_v2k_wgb .concept}

ALIYUN::ECS::AutoSnapshotPolicy用于自动快照策略。

## 语法 {#section_xyg_tn2_lfb .section}

``` {#codeblock_05s_gty_43g .language-json}
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

## 属性 {#section_cgd_53n_4fb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|TimePoints|List|是|是|自动快照的创建时间点，单位为小时。| 取值范围：\[0, 23\]，代表 00:00 至 23:00 共 24 个时间点，如 `1` 表示 01:00。当一天内需要创建多次自动快照时，可以传入多个时间点：

 -   最多传入 24 个时间点。
-   多个时间点用一个格式类似 \[0, 1, … 23\] 的 列表表示，时间点之间用半角逗号（,）隔开。

 |
|RepeatWeekdays|List|是|是|自动快照的重复日期，单位为天，周期为星期。| 取值范围：\[1, 7\]，如 `1` 表示周一。当一星期内需要创建多次自动快照时，可以传入多个时间点：

 -   最多传入 7 个时间点。
-   多个时间点用一个格式类似 \[1, 2, … 7\] 的 列表表示，时间点之间用半角逗号（,）隔开。

 |
|RetentionDays|Integer|是|是|自动快照的保留时间，单位为天。| 取值范围：

 -   -1：永久保存。
-   \[1, 65536\]：指定保存天数。

 默认值：-1

 |
|DiskIds|List|是|是| 目标磁盘 ID。

 当您需要将自动快照策略应用于多块磁盘时，多块磁盘 ID 用一个格式类似 \["d-xxxxxxxxx", "d-yyyyyyyyy", … "d-zzzzzzzzz"\] 的 列表表示，磁盘 ID 之间用半角逗号（,）隔开。

 |无|
|AutoSnapshotPolicyName|String|否|是|自动快照策略的名称。| -   长度为 \[2, 128\] 个英文或中文字符。
-   必须以大小字母或中文开头，可包含数字、半角冒号（:）、下划线（\_）或连字符（-）。
-   不能以 http:// 和 https:// 开头。

 默认值：空

 |

## 返回值 {#section_y5a_2if_n88 .section}

**Fn::GetAtt**

AutoSnapshotPolicyId： 自动快照策略 ID。

## 示例 {#section_klp_54n_4fb .section}

``` {#codeblock_7aw_yzc_7xv .language-json}
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

