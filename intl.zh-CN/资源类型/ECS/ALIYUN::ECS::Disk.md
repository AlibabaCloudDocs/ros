# ALIYUN::ECS::Disk

ALIYUN::ECS::Disk类型用于创建ECS磁盘。

## 语法

```
{
  "Type": "ALIYUN::ECS::Disk",
  "Properties": {
    "StorageSetId": String,
    "Description": String,
    "Tags": List,
    "AutoSnapshotPolicyId": String,
    "Encrypted": Boolean,
    "DiskName": String,
    "DiskCategory": String,
    "ResourceGroupId": String,
    "KMSKeyId": String,
    "DeleteAutoSnapshot": Boolean,
    "SnapshotId": String,
    "StorageSetPartitionNumber": Integer,
    "PerformanceLevel": String,
    "ZoneId": String,
    "Size": Integer
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ResourceGroupId|String|否|否|实例所在的资源组ID。|无。|
|ZoneId|String|是|否|可用区ID。|无。|
|DiskName|String|否|否|磁盘名称。|-   长度为2~128个字符。
-   必须以大小字母或中文开头，可包含字母、汉字、数字，点、下划线 、连字符 。
-   不能以 http:// 或 https:// 开头。
-   磁盘名称会在控制台显示。 |
|Description|String|否|否|磁盘描述。|-   长度为2~256个字符。
-   不能以 `http://`或`https://`开头。
-   磁盘描述会在控制台显示。 |
|Tags|List|否|否|用户自定义标签。|最多支持4个标签，示例值：`[{"Key": "tagKey", "Value": "tagValue"},{"Key": "tagKey2", "Value": "tagValue2"}]`。|
|DiskCategory|String|否|否|数据盘的磁盘种类。|取值范围 -   cloud：普通云盘。
-   cloud\_efficiency：高效云盘。
-   cloud\_ssd：SSD云盘。
-   cloud\_essd：ESSD云盘。

 默认值：cloud。 |
|SnapshotId|String|否|否|创建数据盘使用的快照。|-   同时指定该参数和 \`Size\`时，以该参数值为准。
-   实际创建的磁盘大小为指定快照的大小。
-   2013年7月15日（含）前创建的快照不能用来创建磁盘。 |
|PerformanceLevel|String|否|否|创建一块ESSD云盘时，设置云盘的性能等级。|取值范围： -   PL1：单盘最高随机读写IOPS 5万。
-   PL2：单盘最高随机读写IOPS 10万。
-   PL3：单盘最高随机读写IOPS 10万。

 有关如何选择ESSD性能等级，请参见[ESSD云盘](/intl.zh-CN/块存储/块存储介绍/ESSD云盘.md)。|
|Size|Integer|否|否|容量大小，以GiB为单位。指定该参数后，其取值必须大于或等于指定快照ID的容量大小。|取值范围： -   cloud：5~2000
-   cloud\_efficiency：20~32768
-   cloud\_ssd：20~32768
-   cloud\_essd：20~32768 |
|AutoSnapshotPolicyId|String|否|否|自动快照策略ID。|无。|
|Encrypted|Boolean|否|否|是否加密云盘。|取值范围： -   true
-   false

 默认值：false。|
|DeleteAutoSnapshot|Boolean|否|否|删除云盘时是否删除自动快照。|取值范围： -   true
-   false

 默认值：true。|
|StorageSetId|String|否|否|存储集ID。|无。|
|KMSKeyId|String|否|否|云盘使用的KMS密钥ID。|无。|
|StorageSetPartitionNumber|Integer|否|否|存储集分区数。|无。|

## Tags语法

```
"Tags" : [
  {
    "Value" : String,
    "Key" : String
  }
]
```

## Tags属性

|属性名称|类型|必须|允许更新|
|----|--|--|----|
|Key|String|是|否|
|Value|String|否|否|

## 返回值

Fn::GetAtt

-   DiskId：新建磁盘的ID。
-   Status：新建磁盘的状态。

## 示例

```
{
  "ROSTemplateFormatVersion" : "2015-09-01",
  "Resources" : {
    "DataDisk": {
      "Type": "ALIYUN::ECS::Disk",
      "Properties": {
        "Size": 10,
        "ZoneId": "cn-beijing-a",
        "DiskName": "DataDisk",
        "Description": "ECSDataDisk"
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

