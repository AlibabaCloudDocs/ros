# ALIYUN::ECS::DiskAttachment {#concept_51188_zh .concept}

挂载 ECS 磁盘。

## 语法 {#section_n3l_xxd_lfb .section}

``` {#codeblock_125_p2l_dce .language-json}
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
|InstanceId|String|是|否|需挂载磁盘的实例 ID|无|
|DiskId|String|是|否|磁盘 ID|磁盘和 ECS 实例必须在同一个可用区。|
|Device|String|否|否|磁盘设备名|如不指定，则默认由系统按顺序分配，即从/dev/xvdb到/dev/xvdz。|
|DeleteWithInstance|Boolean|否|否|磁盘是否随实例释放。|取值范围： -   true：释放实例时，该云盘随实例一起释放。
-   false：释放实例时，保留该云盘，不随实例一起释放。

 |

## 返回值 {#section_ulz_fyd_lfb .section}

Fn::GetAtt

-   DiskId：新建磁盘的 ID
-   Status：新建磁盘的状态
-   Device：磁盘设备名

## 示例 {#section_vs5_3yd_lfb .section}

``` {#codeblock_znp_1av_qh0 .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "DiskAttachment": {
      "Type": "ALIYUN::ECS::DiskAttachment",
      "Properties": {
        "InstanceId": {
          "Ref": "InstanceId"
        },
        "Device": {
          "Ref": "Device"
        },
        "DeleteWithInstance": {
          "Ref": "DeleteWithInstance"
        },
        "DiskId": {
          "Ref": "DiskId"
        }
      }
    }
  },
  "Parameters": {
    "InstanceId": {
      "Type": "String",
      "Description": "The instanceId to attach the disk."
    },
    "Device": {
      "Type": "String",
      "Description": "The device where the volume is exposed on the instance. could be /dev/xvd[a-z]. If not specification, will use default value."
    },
    "DeleteWithInstance": {
      "Type": "Boolean",
      "Description": "If property is true, the disk will be deleted while instance is deleted, if property is false, the disk will be retain after instance is deleted.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "DiskId": {
      "Type": "String",
      "Description": "The disk id to attached."
    }
  },
  "Outputs": {
    "Status": {
      "Description": "The disk status now.",
      "Value": {
        "Fn::GetAtt": [
          "DiskAttachment",
          "Status"
        ]
      }
    },
    "Device": {
      "Description": "The device where the volume is exposed on ecs instance.",
      "Value": {
        "Fn::GetAtt": [
          "DiskAttachment",
          "Device"
        ]
      }
    },
    "DiskId": {
      "Description": "The disk id of created disk",
      "Value": {
        "Fn::GetAtt": [
          "DiskAttachment",
          "DiskId"
        ]
      }
    }
  }
}
```

