# ALIYUN::ECS::Snapshot {#concept_55972_zh .concept}

ALIYUN::ECS::Snapshot 类型用于创建磁盘快照。

## 语法 {#section_w3h_5bf_lfb .section}

``` {#codeblock_efu_1eq_p6u .language-json}
{
  "Type": "ALIYUN::ECS::Snapshot",
  "Properties": {
    "SnapshotName": String,
    "Timeout": Integer,
    "Description": String,
    "DiskId": String
  }
}
```

## 属性 {#section_hq0_vlr_3e4 .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|DiskId|String|是|否|将要创建磁盘快照的磁盘 ID。|无|
|SnapshotName|String|否|否|快照的显示名称。|长度为\[2, 128\] 字符。必须以大小字母或中文开头，可包含字母、汉字、数字、下划线（\_）和连字符（-），且不能以 auto 开头（auto 开头的快照名是预留给自动快照的）。不能以 http:// 和 https:// 开头。|
|Timeout|Integer|否|否|创建快照的超时时间。|设置此时间会延长创建资源栈的超时时间。如果快照在指定的时间内没有创建完成，则整个资源栈将创建失败。请根据磁盘的大小，数据的多少，设置合理的超时时间。取值范围：\[200, 1440\]，单位：分钟。默认为 200 分钟。|
|Description|String|否|否|快照的描述。|长度范围 \[2, 256\] 个字符。不填则为空，默认为空。不能以 http:// 和 https:// 开头。|

## 返回值 {#section_xvw_ocs_58y .section}

**Fn::GetAtt**

SnapshotId：快照 ID。

## 示例 {#section_ddi_67v_2p8 .section}

``` {#codeblock_efu_1eq_p6u .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "Snapshot": {
      "Type": "ALIYUN::ECS::Snapshot",
      "Properties": {
        "DiskId": "d-2zedgvuvu8cylvrd****"
      }
    }
  },
  "Outputs": {
    "SnapshotId": {
      "Value": {
        "Fn::GetAtt": [
          "Snapshot",
          "SnapshotId"
        ]
      }
    }
  }
}
```

