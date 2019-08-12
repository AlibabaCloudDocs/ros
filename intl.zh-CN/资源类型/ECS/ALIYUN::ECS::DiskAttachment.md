# ALIYUN::ECS::DiskAttachment {#concept_51188_zh .concept}

挂载 ECS 磁盘。

## 语法 {#section_n3l_xxd_lfb .section}

```language-json
{
   "Type" : "ALIYUN::ECS::DiskAttachment",
   "Properties" : {
      "DiskId" : String,
      "InstanceId" : String,
      "Device" : String,
      "DeleteWithInstance" : String
   }
}

```

## 属性 {#section_mqw_zxd_lfb .section}

|名称|类型|是否必需|允许更新|描述|约束|
|--|--|----|----|--|--|
|InstanceId|String|是|否|需挂载磁盘的实例 ID。|无。|
|DiskId|String|是|否|磁盘 ID。|磁盘和 ECS 实例必须在同一个可用区。|
|Device|String|否|否|磁盘设备名。|如不指定，则默认由系统按顺序分配，即从/dev/xvdb到/dev/xvdz。|
|DeleteWithInstance|Boolean|否|否|磁盘是否随实例释放。|可选值：-   true：释放实例时，该云盘随实例一起释放。
-   false：释放实例时，保留该云盘，不随实例一起释放。

|

## 返回值 {#section_ulz_fyd_lfb .section}

**Fn::GetAtt**

-   DiskId：新建磁盘的 ID。
-   Status：新建磁盘的状态。
-   Device：磁盘设备名。

## 示例 {#section_vs5_3yd_lfb .section}

```language-json
{
  "ROSTemplateFormatVersion" : "2015-09-01",
  "Resources" : {
    "DataDisk": {
      "Type": "ALIYUN::ECS::Disk",
      "Properties": {
        "Size": 10,
        "ZoneId": "cn-beijing-a"
      }
    },
    "AttachDisk": {
      "Type": "ALIYUN::ECS::DiskAttachment",
      "Properties": {
        "DiskId": { "Fn::GetAtt" : [ "DataDisk", "DiskId" ] },
        "InstanceId": "i-250doz5fs"
      }
    }
  }
}

```

