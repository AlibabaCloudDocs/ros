# ALIYUN::ECS::CustomImage {#concept_55980_zh .concept}

ALIYUN::ECS::CustomImage is used to create a custom image.

## Syntax { .section}

```language-json
{
  "Type": "ALIYUN::ECS::CustomImage",
  "Properties": {
    "Description": String,
    "InstanceId": String,
    "ImageName": String,
    "ImageVersion": String,
    "SnapshotId": String,
    "Tag": List,
    "ResourceGroupId": String,
    "Platform": String,
    "DiskDeviceMapping": List,
    "Architecture": String
  }
}
```

## Properties { .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Description|String|No|No|The description of the image.|The description can be up to 256 characters in length. Default value: null. The description cannot start with http:// or https://.|
|InstanceId|String|No|No|The ID of the ECS instance used to create the image.|For more information about how to use an instance to create an image, see [Create a custom image by using an instance](https://partners-intl.aliyun.com/help/doc-detail/35109.htm).|
|ImageName|String|No|No|The name of the image.|The name must be 2 to 128 characters in length and can contain letters, digits, underscores \(\_\), and hyphens\(-\). It must start with a letter and cannot start with http:// or https://.|
|ImageVersion|String|No|No|The version of the image.|The image version must be 1 to 40 characters in length.|
|SnapshotId|String|No|No|The ID of the snapshot used to create the image.| -   For more information about how to use a snapshot to create an image, see [Create a custom image by using a snapshot](https://partners-intl.aliyun.com/help/doc-detail/25460.htm).

 -   If both this parameter and InstanceId are set, this parameter does not take effect. In this case, the system will use an instance to create a custom image.

 |
|Tag|List|No|No|The tags of the image.|None|
|ResourceGroupId|String|No|No|The ID of the resource group to which the custom image will belong.|None|
|Platform|String|No|No|When you specify a data disk snapshot to be used to create the system disk of the custom image, you must use the Platform parameter to determine the release version of the operating system for the system disk.|None|
|DiskDeviceMapping|List|No|No|The list of mappings between images and snapshots.|None|
|Architecture|String|No|No|When you specify a data disk snapshot to be used to create the system disk of the custom image, you must use the Architecture parameter to determine the architecture of the system disk. Default value: x86\_64.|Valid values: -   i386
-   x86\_64

 |

## Tag syntax {#section_0mx_ilv_77x .section}

``` {#codeblock_8k8_q7m_kv3 .language-json}
"Tag": [
  {
    "Key": String,
    "Value": String
  }
]
```

## Tag properties { .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Key|String|No|No|The tag key of the image.|The tag key cannot be a null string. It can be up to 64 characters in length. It cannot start with aliyun or acs: and cannot contain http:// or https://.|
|Value|String|No|No|The tag value of the image.|The tag value can be a null string. It can be up to 128 characters in length. It cannot start with aliyun or acs: and cannot contain http:// or https://.|

## DiskDeviceMapping { .section}

```language-json
"DiskDeviceMapping": [
  {
    "Device": String,
    "SnapshotId": String,
    "Size": Integer,
    "DiskType": String
  }
]
```

## DiskDeviceMapping properties { .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Device|String|No|No|The device name of a disk in the custom image.|The system allocates a device name in the alphabetical order from /dev/xvda to /dev/xvdz by default.|
|SnapshotId|String|No|No|The ID of the snapshot that is used to create the custom image.|None|
|Size|Integer|No|No| The size of a disk in the custom image. Unit: GiB.

 | Valid values: 5 to 2000

-   The default value is the size of the snapshot specified by the DiskDeviceMapping.N.SnapshotId parameter.
-   If the DiskDeviceMapping.N.SnapshotId parameter is not set, the disk size is 5 GiB.
-   The disk size must be greater than or equal to the size of the snapshot specified by the DiskDeviceMapping.N.SnapshotId parameter.

 |
|DiskType|String|No|No|The type of a disk in the custom image. You can set this parameter to create the system disk of the custom image from a data disk snapshot. If you do not set this parameter, the disk type is determined by the corresponding snapshot.| Valid values:

 -   system: indicates a system disk.
-   data: indicates a data disk.

 |

## Response parameters { .section}

 **Fn::GetAtt** 

ImageId: the ID of the custom image.

## Examples { .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "WebServer": {
      "Type": "ALIYUN::ECS::InstanceGroup",
      "Properties": {
        "VpcId": "vpc-2zevx9ios1rszqv0a****",
        "MinAmount": 1,
        "SecurityGroupId": "sg-2ze7pxymaix640qr****",
        "ImageId": {
          "Ref": "CustomImage"
        },
        "IoOptimized": "optimized",
        "SystemDisk_Description": "SystemDisk.Description",
        "SystemDisk_DiskName": "SystemDisk.DiskName",
        "SystemDisk_Category": "cloud_ssd",
        "VSwitchId": "vsw-2zei67xd9nhcqxzec****",
        "Password": "Wenqiao****",
        "InstanceType": "ecs.n1.medium",
        "MaxAmount": 1
      }
    },
    "CustomImage": {
      "Type": "ALIYUN::ECS::CustomImage",
      "Properties": {
        "InstanceId": "i-2zefq1f3ynnrr89q****",
        "SnapshotId": "s-2ze0ibk1pvak4mw6****",
        "ImageName": "image-test-****",
        "ImageVersion": "verison-6-1"
      }
    }
  },
  "Outputs": {
    "CustomImage": {
      "Value": {
        "Fn::GetAtt": [
          "CustomImage",
          "ImageId"
        ]
      }
    },
    "InstanceIds": {
      "Value": {
        "Fn::GetAtt": [
          "WebServer",
          "InstanceIds"
        ]
      }
    }
  }
}            
```

