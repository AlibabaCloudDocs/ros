# ALIYUN::ESS::ScalingConfiguration

ALIYUN::ESS::ScalingConfiguration is used to create a scaling configuration for a scaling group.

## Syntax

```
{
  "Type": "ALIYUN::ESS::ScalingConfiguration",
  "Properties": {
    "PasswordInherit": Boolean,
    "DiskMappings": List,
    "RamRoleName": String,
    "IoOptimized": String,
    "InternetChargeType": String,
    "KeyPairName": String,
    "InstanceId": String,
    "InstanceTypes": List,
    "ImageId": String,
    "ResourceGroupId": String,
    "SpotStrategy": String,
    "InstanceType": String,
    "SystemDiskCategory": String,
    "SystemDiskSize": Integer,
    "SystemDiskAutoSnapshotPolicyId": String,
    "SystemDiskPerformanceLevel": String,
    "InternetMaxBandwidthOut": Integer,
    "InstanceName": String,
    "InternetMaxBandwidthIn": Integer,
    "ScalingConfigurationName": String,
    "UserData": String,
    "DeploymentSetId": String,
    "SecurityGroupId": String,
    "SpotPriceLimit": Number,
    "HpcClusterId": String,
    "ScalingGroupId": String,
    "SpotPriceLimitForInstanceType": Map,
    "TagList": List
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ResourceGroupId|String|No|Yes|The ID of the resource group to which the instance belongs.|None|
|DeploymentSetId|String|No|No|The ID of the deployment set.|None|
|HpcClusterId|String|No|No|The ID of the E-HPC cluster to which the instance belongs.|None|
|ScalingGroupId|String|Yes|No|The ID of the scaling group to which the scaling configuration belongs.|None|
|DiskMappings|List|No|Yes|The disks to be attached to the instance.|A maximum of 16 data disks can be attached. For more information, see [DiskMappings properties](#section_ej4_e8i_zho). |
|InternetChargeType|String|No|Yes|The billing method for network usage.|Default value: PayByTraffic. Valid values: -   PayByBandwidth
-   PayByTraffic |
|InternetMaxBandwidthIn|Integer|No|No|The maximum inbound public bandwidth.|Unit: Mbit/s.

Valid values: 1 to 200.

Default value: 200. |
|InternetMaxBandwidthOut|Integer|No|Yes|The maximum outbound public bandwidth.|Valid values: -   Valid values when InternetChargeType is set to PayByBandwidth: 0 to 100. Default value: 0.
-   Valid values when InternetChargeType is set to PayByTraffic: 1 to 200. This parameter is required when the InternetChargeType parameter is set to PayByTraffic.

Unit: Mbit/s. |
|InstanceId|String|No|No|The ID of the instance whose properties are used to create the scaling configuration.|None|
|SystemDiskCategory|String|No|Yes|The category of the system disk.|Valid values: -   cloud: basic disk
-   cloud\_efficiency: ultra disk
-   cloud\_ssd: standard SSD.
-   ephemeral\_ssd: local SSD.
-   cloud\_essd: enhanced SSD \(ESSD\)

The default value is cloud for non-I/O optimized instances of the Generation I instance types. The default value is cloud\_efficiency for other types of instances. |
|ImageId|String|No|Yes|The ID of the image that is used to create the instance. You can use a public image, a custom image, or an Alibaba Cloud Marketplace image.|For more information, see [Overview](/intl.en-US/Images/Public image/Overview.md).|
|InstanceType|String|No|Yes|The instance type.|For more information, see [Instance families](/intl.en-US/Instance/Instance families.md).|
|SecurityGroupId|String|No|Yes|The ID of the security group to which the instance belongs.|None|
|IoOptimized|String|No|Yes|Specifies whether the instance is I/O optimized.|Default value: none. Valid values: -   none
-   optimized |
|ScalingConfigurationName|String|No|Yes|The name of the scaling configuration.|The name must be 2 to 64 characters in length and can contain letters, digits, underscores \(\_\), hyphens \(-\), and periods \(.\). It must start with a letter or digit.

The name of the scaling configuration must be unique within a scaling group in a specific region.

If you do not specify this parameter, the system uses the ID of the scaling configuration. |
|KeyPairName|String|No|Yes|The name of the key pair that is used to connect to the instance.|-   For Windows instances, this parameter is ignored and is empty by default.
-   For Linux instances, the password logon method is disabled during initialization. |
|RamRoleName|String|No|Yes|The RAM role name of the instance.|You can call the ListRoles operation to query the role name. For more information, see [CreateRole](/intl.en-US/API Reference/API Reference (RAM)/Role management APIs/CreateRole.md) and [ListRoles](/intl.en-US/API Reference/API Reference (RAM)/Role management APIs/ListRoles.md).|
|SystemDiskSize|Integer|No|Yes|The size of the system disk.|Valid values: 20 to 500.

Default value: 40.

Unit: GiB.

If a custom image is used to create a system disk, make sure that the size of the system disk is greater than or equal to that of the custom image. |
|SystemDiskPerformanceLevel|String|No|Yes|The performance level of the ESSD that is used as the system disk.|Default value: PL1. Valid values: -   PL1: A single ESSD can deliver up to 50,000 random read/write IOPS.
-   PL2: A single ESSD can deliver up to 100,000 random read/write IOPS.
-   PL3: A single ESSD can deliver up to 1,000,000 random read/write IOPS.

For more information about performance levels of ESSDs, see [Enhanced SSDs](/intl.en-US/Block Storage/Block Storage overview/Enhanced SSDs.md).|
|UserData|String|No|Yes|The user data that you provide when you create the instance.|The user data can be up to 16 KB in size. You do not need to convert the data into Base64-encoded strings. If the data contains special characters, add a backslash \(\\\) immediately before each special character.|
|InstanceTypes|List|No|Yes|The instance types from which instances can be created. If you specify this parameter, the InstanceType parameter is ignored.|A maximum of 10 instance types can be specified. The priority is determined in descending order of instance types in the list. Auto Scaling creates instances in order of priority. When an instance type that has the highest priority cannot be used to create an instance, the instance type that has the next highest priority is used.|
|PasswordInherit|Boolean|No|Yes|Specifies whether to use the password preset in the image.|To use this parameter, make sure that a password is preset in the specified image.|
|TagList|List|No|Yes|The tags of the instance.|A tag is a key-value pair. You can specify a maximum of five tags in the `{"key1": "value1", "key2": "value2", ... "key5": "value5"}` format. For more information, see the [TagList properties](#section_sua_kck_w4z) section. |
|SpotStrategy|String|No|Yes|The preemption policy to be applied to pay-as-you-go instances.|Default value: NoSpot. Valid values: -   NoSpot: applies to regular pay-as-you-go instances.
-   SpotWithPriceLimit: applies to preemptible instances that have user-defined maximum hourly prices.
-   SpotAsPriceGo: applies to pay-as-you-go instances that are of the market price at the time of purchase. |
|InstanceName|String|No|Yes|The name of the instance that is created based on the current scaling configuration.|None|
|SpotPriceLimit|Number|No|Yes|The maximum hourly price for the instance.|A maximum of three decimal places can be specified. This parameter takes effect only when the SpotStrategy parameter is set to SpotWithPriceLimit. The value of this parameter can be overwritten by the value of SpotPriceLimitForInstanceType.|
|SpotPriceLimitForInstanceType|Map|No|Yes|The maximum spot price for each instance type.|Specify the value in the `{"<instance_type_1>": <price_limit_1>, ..., {"<instance_type_10>": <price_limit_10>}` format. This parameter takes effect only when the SpotStrategy parameter is set to SpotWithPriceLimit. You can configure up to 10 pairs of instance types and spot prices. |
|SystemDiskAutoSnapshotPolicyId|String|No|Yes|The ID of the automatic snapshot policy applied to the system disk.|None|

## DiskMappings syntax

```
"DiskMappings": [
  {
    "Category": String,
    "DiskName": String,
    "Description": String,
    "AutoSnapshotPolicyId": String,
    "PerformanceLevel": String,
    "Encrypted": String,
    "KMSKeyId": String,
    "Device": String,
    "SnapshotId": String,
    "Size": String
  }
]
```

## DiskMappings properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Size|String|No|No|The size of the data disk.|Valid values: -   Valid values when Category is set to cloud: 5 to 2000
-   Valid values when Category is set to cloud\_efficiency: 20 to 32768
-   Valid values when Category is set to cloud\_ssd: 20 to 32768
-   Valid values when Category is set to cloud\_essd: 20 to 32768
-   Valid values when Category is set to ephemeral\_ssd: 5 to 800

Unit: GB.

If you specify this parameter, the data disk size must be greater than or equal to the size of the snapshot that is specified by SnapshotId. |
|Category|String|No|No|The category of the data disk.|Default value: cloud\_efficiency. Valid values: -   cloud: basic disk
-   cloud\_efficiency: ultra disk
-   cloud\_ssd: standard SSD
-   ephemeral\_ssd: local SSD
-   cloud\_essd: ESSD

For I/O optimized instances, the default value is cloud\_efficiency. For non-I/O optimized instances, the default value is cloud. |
|DiskName|String|No|No|The name of the data disk.|The name must be 2 to 128 characters in length. It must start with a letter and cannot start with `http://` or `https://`.

It can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\).|
|PerformanceLevel|String|No|No|The performance level of the ESSD that is used as the data disk.|Default value: PL1. Valid values:-   PL1: A single ESSD can deliver up to 50,000 random read/write IOPS.
-   PL2: A single ESSD can deliver up to 100,000 random read/write IOPS.
-   PL3: A single ESSD can deliver up to 1,000,000 random read/write IOPS.

For more information about performance levels of ESSDs, see [Enhanced SSDs](/intl.en-US/Block Storage/Block Storage overview/Enhanced SSDs.md).|
|Description|String|No|No|The description of the data disk.|The description must be 2 to 256 characters in length. It cannot start with `http://` or `https://`.|
|Device|String|No|No|The device name of the data disk.|If you do not specify this parameter, the system automatically allocates a device name in alphabetical order from /dev/xvdb to /dev/xvdz.|
|SnapshotId|String|No|No|The ID of the snapshot that is used to create the data disk.|If you specify this parameter, the Size parameter is ignored. The actual size of the created disk is the size of the specified snapshot. If you specify a snapshot that was created on or before July 15, 2013, the operation fails and returns InvalidSnapshot.TooOld.|
|Encrypted|String|No|No|Specifies whether the data disk is encrypted.|Default value: false. Valid values:-   true: The data disk is encrypted.
-   false: The data disk is not encrypted. |
|KMSKeyId|String|No|No|The ID of the KMS key corresponding to the data disk.|None|
|AutoSnapshotPolicyId|String|No|No|The ID of the automatic snapshot policy applied to the data disk.|None|

## TagList syntax

```
"TagList": [
  {
    "Key": String,
    "Value": String
  }
]
```

## TagList properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Key|String|Yes|No|The key of the tag.|The tag key must be 1 to 64 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|
|Value|String|No|No|The value of the tag.|The tag value can be up to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|

## Response parameters

Fn::GetAtt

ScalingConfigurationId: the ID of the scaling configuration. This ID is a globally unique identifier \(GUID\) that is generated by the system.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "ScalingConfigurationName": {
      "Type": "String",
      "Description": "Name of created scaling configuration."
    },
    "DiskMappings": {
      "Type": "Json",
      "Description": "Disk mappings to attach to instance."
    },
    "ResourceGroupId": {
      "Type": "String",
      "Description": "Resource group id."
    },
    "SystemDiskSize": {
      "Type": "Number",
      "Description": "Size of system disk. Unit is GB.",
      "MinValue": 20
    },
    "UserData": {
      "Type": "String",
      "Description": "User data to pass to instance. [1, 16KB] characters.User data should not be base64 encoded. If you want to pass base64 encoded string to the property, use function Fn::Base64Decode to decode the base64 string first."
    },
    "SystemDiskAutoSnapshotPolicyId": {
      "Type": "String",
      "Description": "Auto snapshot policy ID."
    },
    "RamRoleName": {
      "Type": "String",
      "Description": "Instance RAM role name. The name is provided and maintained by Resource Access Management (RAM) and can be queried using ListRoles. For more information, see RAM API CreateRole and ListRoles."
    },
    "SystemDiskPerformanceLevel": {
      "Type": "String",
      "Description": "The performance level of an ESSD."
    },
    "SpotPriceLimitForInstanceType": {
      "Type": "Json",
      "Description": "Set the hourly maximum price for the instance of specified instance type.\nThe parameter takes effect only when the value of SpotStrategy is SpotWithPriceLimit.\nYou should input the information of the tag with the format of the Key-Value, such as {\"key1\":\"value1\",\"key2\":\"value2\", ... \"key5\":\"value5\"}.\nAt most 50 items can be specified.\nKey\n\tecs instance type\nValue\n\tSupports a maximum of 3 decimal places."
    },
    "ImageId": {
      "Type": "String",
      "Description": "Image ID to create ecs instance ."
    },
    "SpotPriceLimit": {
      "Type": "Number",
      "Description": "Set the hourly maximum price for the instance. Supports a maximum of 3 decimal places, and the parameter takes effect only when the value of SpotStrategy is SpotWithPriceLimit.It is a default value for all instance types, and can be overwrite by SpotPriceLimitForInstanceType"
    },
    "TagList": {
      "Type": "Json",
      "Description": "The tags of an instance in list format.\nDo not use with Tags at the same time.\nYou should input the information of the tag with the format of Key-Value list, such as [{\"Key\":\"key1\",\"Value\":\"value1\"}, ...].\nAt most 20 tags can be specified.\nKey\nIt can be up to 64 characters in length.\nCannot begin with aliyun.\nCannot begin with http:// or https://.\nCannot be a null string.\nValue\nIt can be up to 128 characters in length.\nCannot begin with aliyun.\nCannot begin with http:// or https://.\nCan be a null string. If less then 20 tags are specified, ros will add a tag(Key: \"ros-aliyun-created\", Value:\"<resource_name>_stack_<stack_id>\") if possible.",
      "MaxLength": 20
    },
    "InstanceTypes": {
      "Type": "CommaDelimitedList",
      "Description": "ecs supported instance types. Length [1,10]. If InstanceTypes is specified,the InstanceType will be ignored.",
      "MinLength": 1,
      "MaxLength": 10
    },
    "InstanceType": {
      "Type": "String",
      "Description": "ecs supported instance type."
    },
    "SpotStrategy": {
      "Type": "String",
      "Description": "Preemption strategy for post-paid instances. It takes effect when the parameter InstanceChargeType takes the value of PostPaid. Ranges:\nNoSpot: Normal pay-per-use instance\nSpotWithPriceLimit: Set a preemptive instance of the cap price\nSpotAsPriceGo: System automatic bidding, following the current market actual price\nDefault: NoSpot.",
      "AllowedValues": [
        "NoSpot",
        "SpotWithPriceLimit",
        "SpotAsPriceGo"
      ]
    },
    "PasswordInherit": {
      "Type": "Boolean",
      "Description": "Whether to use the password pre-configured in the image you select or not. When PasswordInherit is specified, the Password must be null. For a secure access, make sure that the selected image has password configured.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "KeyPairName": {
      "Type": "String",
      "Description": "SSH key pair name."
    },
    "IoOptimized": {
      "Type": "String",
      "Description": "The 'optimized' instance can provide better IO performance. Support 'none' and 'optimized' only, default is 'none'.",
      "AllowedValues": [
        "none",
        "optimized"
      ]
    },
    "InstanceId": {
      "Type": "String",
      "Description": "Source ECS instance to copy configuration, if the properties is setting, Which will copy the InstanceType, ImageId, InternetChargeType, IoOptimized,UserData, KeyPairName, RamRoleName, InternetMaxBandwidthIn,InternetMaxBandwidthOut, and first security group id from source instance, you can also specify the relative properties to overwrite the properties copy from source instance id."
    },
    "HpcClusterId": {
      "Type": "String",
      "Description": "The HPC cluster ID to which the instance belongs."
    },
    "ScalingGroupId": {
      "Type": "String",
      "Description": "Scaling group id to create the scaling configuration."
    },
    "SecurityGroupId": {
      "Type": "String",
      "Description": "Security Group to create ecs instance."
    },
    "InternetChargeType": {
      "Type": "String",
      "Description": "Instance internet access charge type.Support 'PayByBandwidth' and 'PayByTraffic' only.",
      "AllowedValues": [
        "PayByBandwidth",
        "PayByTraffic"
      ]
    },
    "SystemDiskCategory": {
      "Type": "String",
      "Description": "Category of system disk. Default is cloud.support cloud|cloud_efficiency|cloud_ssd|cloud_essd|ephemeral_ssd",
      "AllowedValues": [
        "cloud",
        "cloud_efficiency",
        "cloud_ssd",
        "cloud_essd",
        "ephemeral_ssd"
      ]
    },
    "InstanceName": {
      "Type": "String",
      "Description": "The name of the instance launched from the current scaling configuration."
    },
    "DeploymentSetId": {
      "Type": "String",
      "Description": "Deployment set ID."
    },
    "InternetMaxBandwidthOut": {
      "Type": "Number",
      "Description": "Maximum outgoing bandwidth from the public network, measured in Mbps (Mega bit per second).\nThe value range for PayByBandwidth is [0,100]. If this parameter value is not specified, AliyunAPI automatically sets the value to 0 Mbps.\nThe value range for PayByTraffic is [0,100]. If this parameter value is not specified, an error is reported",
      "MinValue": 0,
      "MaxValue": 100
    },
    "InternetMaxBandwidthIn": {
      "Type": "Number",
      "Description": "Maximum incoming bandwidth from the public network, measured in Mbps (Mega bit per second). The value range is [1,200]. If this parameter value is not specified, AliyunAPI automatically sets the value to 200 Mbps.",
      "MinValue": 1,
      "MaxValue": 200
    }
  },
  "Resources": {
    "ScalingConfiguration": {
      "Type": "ALIYUN::ESS::ScalingConfiguration",
      "Properties": {
        "ScalingConfigurationName": {
          "Ref": "ScalingConfigurationName"
        },
        "DiskMappings": {
          "Ref": "DiskMappings"
        },
        "ResourceGroupId": {
          "Ref": "ResourceGroupId"
        },
        "SystemDiskSize": {
          "Ref": "SystemDiskSize"
        },
        "UserData": {
          "Ref": "UserData"
        },
        "SystemDiskAutoSnapshotPolicyId": {
          "Ref": "SystemDiskAutoSnapshotPolicyId"
        },
        "RamRoleName": {
          "Ref": "RamRoleName"
        },
        "SystemDiskPerformanceLevel": {
          "Ref": "SystemDiskPerformanceLevel"
        },
        "SpotPriceLimitForInstanceType": {
          "Ref": "SpotPriceLimitForInstanceType"
        },
        "ImageId": {
          "Ref": "ImageId"
        },
        "SpotPriceLimit": {
          "Ref": "SpotPriceLimit"
        },
        "TagList": {
          "Ref": "TagList"
        },
        "InstanceTypes": {
          "Ref": "InstanceTypes"
        },
        "InstanceType": {
          "Ref": "InstanceType"
        },
        "SpotStrategy": {
          "Ref": "SpotStrategy"
        },
        "PasswordInherit": {
          "Ref": "PasswordInherit"
        },
        "KeyPairName": {
          "Ref": "KeyPairName"
        },
        "IoOptimized": {
          "Ref": "IoOptimized"
        },
        "InstanceId": {
          "Ref": "InstanceId"
        },
        "HpcClusterId": {
          "Ref": "HpcClusterId"
        },
        "ScalingGroupId": {
          "Ref": "ScalingGroupId"
        },
        "SecurityGroupId": {
          "Ref": "SecurityGroupId"
        },
        "InternetChargeType": {
          "Ref": "InternetChargeType"
        },
        "SystemDiskCategory": {
          "Ref": "SystemDiskCategory"
        },
        "InstanceName": {
          "Ref": "InstanceName"
        },
        "DeploymentSetId": {
          "Ref": "DeploymentSetId"
        },
        "InternetMaxBandwidthOut": {
          "Ref": "InternetMaxBandwidthOut"
        },
        "InternetMaxBandwidthIn": {
          "Ref": "InternetMaxBandwidthIn"
        }
      }
    }
  },
  "Outputs": {
    "ScalingConfigurationId": {
      "Description": "The scaling configuration id",
      "Value": {
        "Fn::GetAtt": [
          "ScalingConfiguration",
          "ScalingConfigurationId"
        ]
      }
    }
  }
}
```

`YAML` format

```
ROSTemplateFormatVersion: '2015-09-01'
Parameters:
  ScalingConfigurationName:
    Type: String
    Description: Name of created scaling configuration.
  DiskMappings:
    Type: Json
    Description: Disk mappings to attach to instance.
  ResourceGroupId:
    Type: String
    Description: Resource group id.
  SystemDiskSize:
    Type: Number
    Description: Size of system disk. Unit is GB.
    MinValue: 20
  UserData:
    Type: String
    Description: >-
      User data to pass to instance. [1, 16KB] characters.User data should not
      be base64 encoded. If you want to pass base64 encoded string to the
      property, use function Fn::Base64Decode to decode the base64 string first.
  SystemDiskAutoSnapshotPolicyId:
    Type: String
    Description: Auto snapshot policy ID.
  RamRoleName:
    Type: String
    Description: >-
      Instance RAM role name. The name is provided and maintained by Resource
      Access Management (RAM) and can be queried using ListRoles. For more
      information, see RAM API CreateRole and ListRoles.
  SystemDiskPerformanceLevel:
    Type: String
    Description: The performance level of an ESSD.
  SpotPriceLimitForInstanceType:
    Type: Json
    Description: "Set the hourly maximum price for the instance of specified instance type.\nThe parameter takes effect only when the value of SpotStrategy is SpotWithPriceLimit.\nYou should input the information of the tag with the format of the Key-Value, such as {\"key1\":\"value1\",\"key2\":\"value2\", ... \"key5\":\"value5\"}.\nAt most 50 items can be specified.\nKey\n\tecs instance type\nValue\n\tSupports a maximum of 3 decimal places."
  ImageId:
    Type: String
    Description: Image ID to create ecs instance .
  SpotPriceLimit:
    Type: Number
    Description: >-
      Set the hourly maximum price for the instance. Supports a maximum of 3
      decimal places, and the parameter takes effect only when the value of
      SpotStrategy is SpotWithPriceLimit.It is a default value for all instance
      types, and can be overwrite by SpotPriceLimitForInstanceType
  TagList:
    Type: Json
    Description: >-
      The tags of an instance in list format.

      Do not use with Tags at the same time.

      You should input the information of the tag with the format of Key-Value
      list, such as [{"Key":"key1","Value":"value1"}, ...].

      At most 20 tags can be specified.

      Key

      It can be up to 64 characters in length.

      Cannot begin with aliyun.

      Cannot begin with http:// or https://.

      Cannot be a null string.

      Value

      It can be up to 128 characters in length.

      Cannot begin with aliyun.

      Cannot begin with http:// or https://.

      Can be a null string. If less then 20 tags are specified, ros will add a
      tag(Key: "ros-aliyun-created", Value:"<resource_name>_stack_<stack_id>")
      if possible.
    MaxLength: 20
  InstanceTypes:
    Type: CommaDelimitedList
    Description: >-
      ecs supported instance types. Length [1,10]. If InstanceTypes is
      specified,the InstanceType will be ignored.
    MinLength: 1
    MaxLength: 10
  InstanceType:
    Type: String
    Description: ecs supported instance type.
  SpotStrategy:
    Type: String
    Description: >-
      Preemption strategy for post-paid instances. It takes effect when the
      parameter InstanceChargeType takes the value of PostPaid. Ranges:

      NoSpot: Normal pay-per-use instance

      SpotWithPriceLimit: Set a preemptive instance of the cap price

      SpotAsPriceGo: System automatic bidding, following the current market
      actual price

      Default: NoSpot.
    AllowedValues:
      - NoSpot
      - SpotWithPriceLimit
      - SpotAsPriceGo
  PasswordInherit:
    Type: Boolean
    Description: >-
      Whether to use the password pre-configured in the image you select or not.
      When PasswordInherit is specified, the Password must be null. For a secure
      access, make sure that the selected image has password configured.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
  KeyPairName:
    Type: String
    Description: SSH key pair name.
  IoOptimized:
    Type: String
    Description: >-
      The 'optimized' instance can provide better IO performance. Support 'none'
      and 'optimized' only, default is 'none'.
    AllowedValues:
      - none
      - optimized
  InstanceId:
    Type: String
    Description: >-
      Source ECS instance to copy configuration, if the properties is setting,
      Which will copy the InstanceType, ImageId, InternetChargeType,
      IoOptimized,UserData, KeyPairName, RamRoleName,
      InternetMaxBandwidthIn,InternetMaxBandwidthOut, and first security group
      id from source instance, you can also specify the relative properties to
      overwrite the properties copy from source instance id.
  HpcClusterId:
    Type: String
    Description: The HPC cluster ID to which the instance belongs.
  ScalingGroupId:
    Type: String
    Description: Scaling group id to create the scaling configuration.
  SecurityGroupId:
    Type: String
    Description: Security Group to create ecs instance.
  InternetChargeType:
    Type: String
    Description: >-
      Instance internet access charge type.Support 'PayByBandwidth' and
      'PayByTraffic' only.
    AllowedValues:
      - PayByBandwidth
      - PayByTraffic
  SystemDiskCategory:
    Type: String
    Description: >-
      Category of system disk. Default is cloud.support
      cloud|cloud_efficiency|cloud_ssd|cloud_essd|ephemeral_ssd
    AllowedValues:
      - cloud
      - cloud_efficiency
      - cloud_ssd
      - cloud_essd
      - ephemeral_ssd
  InstanceName:
    Type: String
    Description: The name of the instance launched from the current scaling configuration.
  DeploymentSetId:
    Type: String
    Description: Deployment set ID.
  InternetMaxBandwidthOut:
    Type: Number
    Description: >-
      Maximum outgoing bandwidth from the public network, measured in Mbps (Mega
      bit per second).

      The value range for PayByBandwidth is [0,100]. If this parameter value is
      not specified, AliyunAPI automatically sets the value to 0 Mbps.

      The value range for PayByTraffic is [0,100]. If this parameter value is
      not specified, an error is reported
    MinValue: 0
    MaxValue: 100
  InternetMaxBandwidthIn:
    Type: Number
    Description: >-
      Maximum incoming bandwidth from the public network, measured in Mbps (Mega
      bit per second). The value range is [1,200]. If this parameter value is
      not specified, AliyunAPI automatically sets the value to 200 Mbps.
    MinValue: 1
    MaxValue: 200
Resources:
  ScalingConfiguration:
    Type: 'ALIYUN::ESS::ScalingConfiguration'
    Properties:
      ScalingConfigurationName:
        Ref: ScalingConfigurationName
      DiskMappings:
        Ref: DiskMappings
      ResourceGroupId:
        Ref: ResourceGroupId
      SystemDiskSize:
        Ref: SystemDiskSize
      UserData:
        Ref: UserData
      SystemDiskAutoSnapshotPolicyId:
        Ref: SystemDiskAutoSnapshotPolicyId
      RamRoleName:
        Ref: RamRoleName
      SystemDiskPerformanceLevel:
        Ref: SystemDiskPerformanceLevel
      SpotPriceLimitForInstanceType:
        Ref: SpotPriceLimitForInstanceType
      ImageId:
        Ref: ImageId
      SpotPriceLimit:
        Ref: SpotPriceLimit
      TagList:
        Ref: TagList
      InstanceTypes:
        Ref: InstanceTypes
      InstanceType:
        Ref: InstanceType
      SpotStrategy:
        Ref: SpotStrategy
      PasswordInherit:
        Ref: PasswordInherit
      KeyPairName:
        Ref: KeyPairName
      IoOptimized:
        Ref: IoOptimized
      InstanceId:
        Ref: InstanceId
      HpcClusterId:
        Ref: HpcClusterId
      ScalingGroupId:
        Ref: ScalingGroupId
      SecurityGroupId:
        Ref: SecurityGroupId
      InternetChargeType:
        Ref: InternetChargeType
      SystemDiskCategory:
        Ref: SystemDiskCategory
      InstanceName:
        Ref: InstanceName
      DeploymentSetId:
        Ref: DeploymentSetId
      InternetMaxBandwidthOut:
        Ref: InternetMaxBandwidthOut
      InternetMaxBandwidthIn:
        Ref: InternetMaxBandwidthIn
Outputs:
  ScalingConfigurationId:
    Description: The scaling configuration id
    Value:
      'Fn::GetAtt':
        - ScalingConfiguration
        - ScalingConfigurationId
```

