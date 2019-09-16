# ALIYUN::ECS::DiskAttachment {#concept_51188_zh .concept}

ALIYUN::ECS::DiskAttachment is used to attach a disk to an ECS instance.

## Syntax {#section_n3l_xxd_lfb .section}

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

## Properties {#section_mqw_zxd_lfb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|InstanceId|String|Yes|No|The ID of the ECS instance for which you want to attach a disk.|None|
|DiskId|String|Yes|No|The ID of the disk.|The disk and ECS instance must reside in the same zone.|
|Device|String|No|No|The device name of the disk.|If you do not set this parameter, the system will automatically allocate a device name in alphabetical order from /dev/xvdb to /dev/xvdz.|
|DeleteWithInstance|Boolean|No|No|Specifies whether the disk is to be released together with the instance.|Valid values: -   true: The disk will be released when the instance is released.
-   false: The disk will be retained when the instance is released.

 |

## Response parameters {#section_ulz_fyd_lfb .section}

Fn::GetAtt

-   DiskId: the ID of the disk.
-   Status: the status of the disk.
-   Device: the device name of the disk.

## Examples {#section_vs5_3yd_lfb .section}

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
      "Description": "The ID of the instance to attach the disk."
    },
    "Device": {
      "Type": "String",
      "Description": "The device where the volume is exposed on the instance. The device name could be /dev/xvd[a-z]. If this parameter is not specified, the default value will be used."
    },
    "DeleteWithInstance": {
      "Type": "Boolean",
      "Description": "If this parameter is set to true, the disk will be deleted while the instance is deleted. If this parameter is set to false, the disk will be retained after the instance is deleted.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "DiskId": {
      "Type": "String",
      "Description": "The ID of the disk to be attached."
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
      "Description": "The device where the volume is exposed on the ECS instance.",
      "Value": {
        "Fn::GetAtt": [
          "DiskAttachment",
          "Device"
        ]
      }
    },
    "DiskId": {
      "Description": "The ID of the created disk.",
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

