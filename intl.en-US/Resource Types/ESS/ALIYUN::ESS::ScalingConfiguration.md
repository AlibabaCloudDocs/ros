# ALIYUN::ESS::ScalingConfiguration {#concept_51203_zh .concept}

ALIYUN::ESS::ScalingConfiguration is used to create a scaling configuration.

## Syntax {#section_k4p_5d1_mfb .section}

```language-json
{
  "Type": "ALIYUN::ESS::ScalingConfiguration",
  "Properties": {
    "DiskMappings": List,
    "InternetMaxBandwidthIn": Integer,
    "InstanceId": String,
    "SecurityGroupId": String,
    "SystemDiskCategory": String,
    "SystemDiskSize": Integer,
    "ImageId": String,
    "InternetMaxBandwidthOut": Integer,
    "IoOptimized": String,
    "ScalingGroupId": String,
    "InternetChargeType": String,
    "InstanceType": String,
    "ScalingConfigurationName": String,
    "InstanceTypes": List,
    "KeyPairName": String,
    "UserData": String,
    "RamRoleName": String,
    "TagList": List
  }
}
```

## Properties {#section_zvc_wd1_mfb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|ScalingGroupId|String|Yes|No|The ID of the scaling group to which the scaling configuration will belong.|None|
|DiskMappings|List|No|No|The data disks to be attached to ECS instances in the specified scaling group.|A maximum of 16 data disks can be attached to each ECS instance.|
|InternetChargeType|String|No|No|The billing method for Internet traffic.| Valid values: PayByBandwidth and PayByTraffic

 Default value: PayByTraffic

 |
|InternetMaxBandwidthIn|Integer|No|No|The maximum inbound bandwidth from the Internet. Unit: Mbit/s.| Valid values: 1 to 100

 Default value: 100

 |
|InternetMaxBandwidthOut|Integer|No|No|The maximum outbound bandwidth to the Internet. Unit: Mbit/s.| Valid values in PayByBandwidth mode: 0 to 200. Default value: 0.

 Valid values in PayByTraffic mode: 1 to 200. If you choose to use the PayByTraffic mode, you must specify this parameter.

 |
|InstanceId|String|No|No|The ID of the ECS instance whose properties are used to create the scaling configuration.|None|
|SystemDiskCategory|String|No|No|The system disk type of created instances.|Valid values: cloud, cloud\_efficiency, cloud\_ssd, and ephemeral\_ssd|
|ImageId|String|No|No|The ID of the image used to start an ECS instance. You can use a public image, custom image, or Alibaba Cloud Marketplace image.|For more information, see [Public images for ECS instances](https://ros.console.aliyun.com/#/product/cn-hangzhou/list/imageList).|
|InstanceType|String|No|No|The type of created ECS instances.|For more information, see [Instance type families](https://partners-intl.aliyun.com/help/doc-detail/25378.htm).|
|SecurityGroupId|String|No|No|The ID of the security group to which created instances will belong.|None|
|IoOptimized|String|No|No|Specifies whether created instances are I/O optimized.| Valid values: none \(non-I/O optimized\) and optimized \(I/O optimized\)

 Default value: none

 |
|ScalingConfigurationName|String|No|No|The display name of the scaling configuration.|The name must be 2 to 40 characters in length and can contain letters, digits, underscores \(\_\), hyphens \(-\), and periods \(.\). It must start with a letter or digit. The name must be unique in a scaling group. The default name is the ID of the scaling configuration.|
|KeyPairName|String|No|No|The name of the key pair used to connect to created ECS instances.|For Windows-based ECS instances, this parameter is ignored and is empty by default. For Linux-based ECS instances, the Password parameter will still take effect if the KeyPairName parameter is specified. However, logon by password is disabled, and the KeyPairName value is used.|
|RamRoleName|String|No|No|The name of the RAM role assigned to created instances.|You can call the ListRoles API to query the role name. For more information, see [CreateRole](https://partners-intl.aliyun.com/help/doc-detail/28710.htm) and [ListRoles](https://partners-intl.aliyun.com/help/doc-detail/28713.htm).|
|SystemDiskSize|Integer|No|Yes|The system disk size of created instances.|Valid values: 40 to 500. Unit: GB. If a custom image is used to create a system disk, make sure that the size of the system disk is greater than that of the custom image.|
|UserData|String|No|No|The user data you provide when you create an ECS instance.|The user data can be up to 16 KB in size. You must convert the data into Base64-encoded strings. If the data contains special characters, add a backslash \(\\\) immediately before each special character.|
|InstanceTypes|List|No|No|The ECS instance types that can be used in a scaling group.|A maximum of 10 ECS instance types can be specified. If this parameter is specified, the InstanceType parameter is ignored.|
|PasswordInherit|Boolean|No|Yes|Specifies whether to use the password predefined in the image you select. When you set this parameter, ensure that the selected image has a predefined password.|None|
|TagList|List|No|Yes|The tags of created ECS instances. Tags must be specified as key-value pairs. A maximum of 20 tags can be specified for each ECS instance. The following rules apply to keys and values: -   A key can contain a maximum of 64 characters and cannot start with aliyun, http://, or https://. You cannot specify an empty string as a key.
-   A value can contain a maximum of 128 characters and cannot start with aliyun, http://, or https://. You can specify an empty string as a value.

 |None|
|SpotStrategy|String|No|Yes|The preemption policy to be applied to pay-as-you-go instances. Valid values: -   NoSpot: specifies a regular pay-as-you-go instance.
-   SpotWithPriceLimit: specifies a pay-as-you-go instance with a maximum hourly price.
-   SpotAsPriceGo: specifies a pay-as-you-go instance priced at the market price at the time of purchase.

 Default value: NoSpot

 |Valid values: NoSpot, SpotWithPriceLimit, and SpotAsPriceGo|
|InstanceName|String|No|Yes|The name of the ECS instance that is created based on the current scaling configuration.|None|
|SpotPriceLimit|Number|No|Yes|The maximum hourly price for preemptible instances. This parameter is only valid when the SpotStrategy parameter is set to SpotWithPriceLimit. A maximum of three decimal places can be specified. The default value of InstanceTypes can be overridden by the value of SpotPriceLimitForInstanceType.|None|
|SpotPriceLimitForInstanceType|Map|No|Yes|The maximum spot price for each instance type. This parameter is only valid when the SpotStrategy parameter is set to SpotWithPriceLimit. Example: \{"key1":"value1","key2":"value2", ... "key5":"value5"\}. A key is an ECS instance type. A value can have a maximum of three decimal places.

 |None|

## DiskMappings syntax {#section_cvf_221_mfb .section}

```language-json
"DiskMappings": [
  {
    "Category": String,
    "Device": String,
    "SnapshotId": String,
    "Size": String,
    "Encrypted": String,
    "KMSKeyId": String,
    "Description": String,
    "DiskName": String
  }
]
```

## DiskMappings properties { .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Size|String|Yes|No|The size of a disk size. Unit: GB|None|
|Category|String|No|No|The type of a disk size.|Valid values: cloud, cloud\_efficiency, cloud\_ssd, and ephemeral\_ssd|
|DiskName|String|No|No|The name of a disk size.|The name must be 2 to 128 characters in length. It must start with a letter and cannot start with http:// or https://. It can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). Default value: null

 |
|Description|String|No|No|The description of a disk size.|The description must be 2 to 256 characters in length and cannot start with http:// or https://.|
|Device|String|No|No|The device name of a data disk to be attached to created instances.|The system allocates a device name in the alphabetical order from /dev/xvda to /dev/xvdz by default.|
|SnapshotId|String|No|No|The ID of the snapshot used to create a data disk.|None|
|Encrypted|String|No|No|Specifies whether to encrypt a data disk.|Default value: false|
|KMSKeyId|String|No|No|The ID of the KMS key corresponding to a data disk.|None|

## TagList syntax {#section_y5m_jod_yzj .section}

``` {#codeblock_7ys_9p9_3qd .language-json}
"TagList": [
  {
    "Value": String,
    "Key": String
  },
  .
  .
  .
]
```

## TagList properties {#section_46t_1x3_9fy .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Key|String|Yes|No|None|None|
|Value|String|Yes|No|None|None|

## Response parameters {#section_bsn_k21_mfb .section}

**Fn::GetAtt**

ScalingConfigurationId: the ID of the scaling configuration. This ID is a globally unique identifier \(GUID\) generated by the system.

## Examples {#section_ozp_n21_mfb .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "ScalingConfiguration": {
      "Type": "ALIYUN::ESS::ScalingConfiguration",
      "Properties": {
        "ImageId": "ubuntu1404_64_20G_aliaegis_20150325.vhd",
        "InstanceType": "ecs.t1.small",
        "InstanceId": "i-25xhh****",
        "InternetChargeType": "PayByTraffic",
        "InternetMaxBandwidthIn": 1,
        "InternetMaxBandwidthOut": 20,
        "SystemDisk_Category": "cloud",
        "ScalingGroupId": "bwhtvpcBcKYac9fe3vd0****",
        "SecurityGroupId": "sg-25zwc****",
        "DiskMappings": [
          {
            "Size": 10
          },
          {
            "Category": "cloud",
            "Size": 10
          }
        ]
      }
    }
  },
  "Outputs": {
    "ScalingConfiguration": {
      "Value": {"get_attr": ["ScalingConfigurationId"]}
    }
  }
}
```

