# ALIYUN::ECS::Disk {#concept_51201_zh .concept}

ALIYUN::ECS::Disk 用于创建 ECS 磁盘。

## 语法 {#section_d3k_mwd_lfb .section}

``` {#codeblock_ffo_t4a_64k .language-json}
{
  "Type": "ALIYUN::ECS::Disk",
  "Properties": {
    "DiskName": String,
    "Description": String,
    "Tags": List,
    "DiskCategory": String,
    "ResourceGroupId": String,
    "SnapshotId": String,
    "ZoneId": String,
    "Size": Integer
  }
}
```

## 属性 {#section_y14_4wd_lfb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ResourceGroupId|String|否|否|实例所在的资源组ID。|无。|
|ZoneId|String|是|否|可用区 ID。|无。|
|DiskName|String|否|否|磁盘名称。| -   不填则默认值为空。
-   字符长度为\[2, 128\]。
-   必须以大小字母或中文开头，可包含字母、汉字、数字，点（.）、下划线 （\_）、连字符 （-）。
-   不能以 http:// 或 https:// 开头。
-   磁盘名称会在控制台显示。

 |
|Description|String|否|否|磁盘描述。| -   不填则默认值为空。
-   字符长度为\[2, 256\]。
-   不能以 http:// 或 https:// 开头。
-   磁盘描述会在控制台显示。

 |
|Tags|List|否|否|用户自定义标签。|最多支持 4 个标签，格式: \[\{“Key”:”tagKey”,”Value”:”tagValue”\},\{“Key”:”tagKey2”,”Value”:”tagValue2”\}\]。|
|DiskCategory|String|否|否|数据盘的磁盘种类。| 可选值：cloud、cloud\_efficiency、cloud\_ssd、cloud\_essd、san\_ssd、san\_efficiency。

 默认值：cloud。

 |
|SnapshotId|String|否|否|创建数据盘使用的快照。| -   同时指定该参数和 \`Size\`时，以该参数值为准。
-   实际创建的磁盘大小为指定快照的大小。
-   2013 年 7 月 15 日（含）前创建的快照不能用来创建磁盘。

 |
|Size|Integer|否|否|磁盘容量大小，以 GB 为单位。| -   \`cloud\`磁盘取值范围为\[5, 2000\]。
-   \`cloud\_efficiency\`磁盘取值范围为\[20 , 2048\]。
-   \`cloud\_ssd\`磁盘取值范围为\[20, 1024\]。
-   \`Size\`取值必须大于等于\`SnapshotId\` 的值。

 |

## Tags 语法 {#section_48n_ko3_jep .section}

``` {#codeblock_xim_uay_hy8 .language-json}
"Tags" : [
  {
    "Value" : String,
    "Key" : String
  }
]
```

## Tags 属性 {#section_inj_lxd_lfb .section}

|属性名称|类型|必须|允许更新|
|----|--|--|----|
|Key|String|是|否|
|Value|String|否|否|

## 返回值 {#section_avf_hxd_lfb .section}

**Fn::GetAtt**

-   DiskId：新建磁盘的 ID。
-   Status：新建磁盘的状态。

## 示例 {#section_knj_lxd_lfb .section}

``` {#codeblock_tfi_64b_v90 .language-json}
{
  "ROSTemplateFormatVersion" : "2015-09-01",
  "Resources" : {
    "DataDisk": {
      "Type": "ALIYUN::ECS::Disk",
      "Properties": {
        "Size": 10,
        "ZoneId": "cn-beijing-a",
        "DiskName": "\u4e2d\u6587",
        "Description": "中文"
      }
    }
  },
  "Outputs": {
    "DiskId": {
         "Value" : {"Fn::GetAtt": ["DataDisk","DiskId"]}
    },
    "Status": {
         "Value" : {"Fn::GetAtt": ["DataDisk","Status"]}
    }
  }
}
```

