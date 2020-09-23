# ALIYUN::ECS::CustomImage

ALIYUN::ECS::CustomImage is used to create a custom image.

## Syntax

```
{
  "Type": "ALIYUN::ECS::CustomImage",
  "Properties": {
    "Description": String,
    "InstanceId": String,
    "ImageName": String,
    "SnapshotId": String,
    "Tag": List,
    "ResourceGroupId": String,
    "Platform": String,
    "DiskDeviceMapping": List,
    "Architecture": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Description|String|No|No|The description of the image.|The description can be up to 256 characters in length. It cannot start with `http://` or `https://`. This parameter is empty by default. |
|InstanceId|String|No|No|The ID of the instance.|If this parameter is specified, a custom image is created from an instance. For more information, see [Create a custom image from an instance](/intl.en-US/Images/Custom image/Create custom image/Create a custom image from an instance.md).|
|ImageName|String|No|No|The name of the image.|The name must be 2 to 128 characters in length. The name must start with a letter and cannot start with `http://` or `https://`. The name can contain letters, digits, underscores \(\_\), and hyphens \(-\).|
|SnapshotId|String|No|No|The ID of the snapshot.|If this parameter is specified, a custom image is created from a snapshot. For more information, see [Create a custom image from a snapshot](/intl.en-US/Images/Custom image/Create custom image/Create a custom image from a snapshot.md). If both this parameter and the InstanceId parameter are specified, ROS ignores this parameter and creates a custom image from an instance. |
|Tag|List|No|No|The tags of the image.|For more information, see [Tag properties](#section_jxz_qoz_9zs).|
|ResourceGroupId|String|No|No|The ID of the resource group to which the custom image belongs.|None|
|Platform|String|No|No|The distribution of the operating system for the system disk in the custom image. If you specify a data disk snapshot to create the system disk of the custom image, you must use the Platform parameter to determine the distribution of the operating system for the system disk.|None|
|DiskDeviceMapping|List|No|No|The mappings between images and snapshots.|For more information, see [DiskDeviceMapping properties](#section_w2m_3kf_bhs).|
|Architecture|String|No|No|The system architecture of the system disk. If you specify a data disk snapshot to create the system disk of the custom image, you must use the Architecture parameter to determine the system architecture of the system disk.|Default value: x86\_64. Valid values: -   i386
-   x86\_64 |

## Tag syntax

```
"Tag": [
  {
    "Key": String,
    "Value": String
  }
]
```

## Tag properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Key|String|No|No|The tag key.|The tag key must be 1 to 128 characters in length and cannot start with `acs:` or `aliyun`. It cannot contain `http://` or `https://`.|
|Value|String|No|No|The tag value.|The tag value must be 0 to 128 characters in length and cannot start with `acs:` or `aliyun`. It cannot contain `http://` or `https://`.|

## DiskDeviceMapping

```
"DiskDeviceMapping": [
  {
    "Device": String,
    "SnapshotId": String,
    "Size": Integer,
    "DiskType": String
  }
]
```

## DiskDeviceMapping properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Device|String|No|No|The device name of the disk in the custom image.|Valid values: -   For basic disks, the system allocates a device name in alphabetical order from /dev/xvda to /dev/xvdz.
-   For disk categories other than basic disks, the system allocates a device name in alphabetical order from /dev/vda to /dev/vdz. |
|SnapshotId|String|No|No|The ID of the snapshot from which the custom image is created.|None|
|Size|Integer|No|No|The size of the disk.

|Valid values:

-   If the SnapshotId parameter is not specified:
    -   Valid values for basic disks: 5 to 2000.

Default value: 5.

    -   Valid values for disk categories other than basic disks: 20 to 32768.

Default value: 20.

-   If the SnapshotId parameter is specified, the Size value must be greater than or equal to the SnapshotId value. The default value of the Size parameter is equal to the value of the SnapshotId parameter.

 Unit: GiB. |
|DiskType|String|No|No|The type of the disk in the custom image.|You can set this parameter to create the system disk of the custom image from a data disk snapshot. If you do not set this parameter, the disk type is determined by the corresponding snapshot. Valid values:

 -   system
-   data |

## Response parameters

Fn::GetAtt

ImageId: the ID of the custom image.

## Examples

```
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
        "ImageName": "image-test-****"
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

