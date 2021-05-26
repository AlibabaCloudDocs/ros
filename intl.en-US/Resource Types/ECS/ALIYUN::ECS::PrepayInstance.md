# ALIYUN::ECS::PrepayInstance

ALIYUN::ECS::PrepayInstance is used to create a subscription ECS instance.

## Syntax

```
{
  "Type": "ALIYUN::ECS::Instance",
  "Properties": {
    "DedicatedHostId": String,
    "AutoRenew": String,
    "RamRoleName": String,
    "IoOptimized": String,
    "InternetChargeType": String,
    "PrivateIpAddress": String,
    "KeyPairName": String,
    "SystemDiskDiskName": String,
    "PeriodUnit": String,
    "Description": String,
    "Tags": List,
    "SpotPriceLimit": String,
    "HostName": String,
    "AutoRenewPeriod": Number,
    "ImageId": String,
    "ResourceGroupId": String,
    "InstanceChargeType": String,
    "VSwitchId": String,
    "Password": String,
    "PasswordInherit": Boolean,
    "InstanceType": String,
    "SystemDiskCategory": String,
    "DeletionProtection": Boolean,
    "SystemDiskSize": Number,
    "ZoneId": String,
    "InternetMaxBandwidthOut": Integer,
    "VpcId": String,
    "SpotStrategy": String,
    "InstanceName": String,
    "InternetMaxBandwidthIn": Integer,
    "UserData": String,
    "DeploymentSetId": String,
    "SecurityGroupId": String,
    "SecurityEnhancementStrategy": String,
    "Period": Number,
    "HpcClusterId": String,
    "AllocatePublicIP": Boolean,
    "SystemDiskDescription": String,
    "DiskMappings": List,
    "SystemDiskPerformanceLevel": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|HpcClusterId|String|No|No|The ID of the E-HPC cluster to which the ECS instance belongs.|None|
|PeriodType|String|Yes|No|The type of billing cycle for the ECS instance.|Valid values: -   Monthly
-   Yearly |
|DedicatedHostId|String|No|No|The ID of the dedicated host on which to create the instance.|None|
|RamRoleName|String|No|No|The RAM role name of the ECS instance.|You can call the ListRoles operation to query the role name. For more information, see [CreateRole](https://www.alibabacloud.com/help/doc-detail/28710.htm) and [ListRoles](https://www.alibabacloud.com/help/doc-detail/28713.htm).|
|IoOptimized|Boolean|No|No|Specifies whether the instance is I/O optimized.|Valid values: -   none: The instance is not I/O optimized.
-   optimized: The instance is I/O optimized.

For instances of retired instance types, the default value is none. For other instances, the default value is optimized. |
|InternetChargeType|String|No|No|The billing method for network usage.|Default value: PayByBandwidth. Valid values: -   PayByBandwidth
-   PayByTraffic |
|PrivateIpAddress|String|No|No|The private IP address to be assigned to the instance.|The private IP address must be selected from the CIDR block of the vSwitch specified by VSwitchId.|
|KeyPairName|String|No|Yes|The name of the SSH key pair.|For Windows instances, this parameter is ignored and is empty by default. The Password parameter takes effect even if this parameter is specified.

For Linux instances, if this parameter is specified, logon by password is disabled, and the value of this parameter is used. |
|SystemDiskDiskName|String|No|No|The name of the system disk attached to the instance.|None|
|PeriodUnit|String|No|No|The unit of billing cycle for the ECS instance.|Default value: Month. Valid values: -   Week

When this parameter is set to Week, valid values of the Period parameters are 1, 2, 3, and 4, and valid values of the AutoRenewPeriod parameter are 1, 2, and 3.

-   Month

When this parameter is set to Month, valid values of the Period parameters are 1, 2, 3, 4, 5, 6, 7, 8, 9, 12, 24, 36, 48, and 60, and valid values of the AutoRenewPeriod parameter are 1, 2, 3, 6, and 12. |
|Description|String|No|Yes|The description of the ECS instance.

|The description must be 2 to 256 characters in length. It cannot start with `http://` or `https://`.|
|Tags|List|No|No|The tags of the ECS instance.|A maximum of 20 tags can be specified in the `[{"Key": "tagKey", "Value": "tagValue"},{"Key": "tagKey2", "Value": "tagValue2"}]` format. For more information, see the [Tags properties](#section_ffh_ccm_70r) section in this topic. |
|MinAmount|Integer|Yes|No|The minimum number of ECS instances that can be created.|Valid values: 1 to 100. Default value: 1. |
|HostName|String|No|No|The hostname of the ECS instance.|The hostname cannot start or end with a period \(.\) or hyphen \(-\). It cannot contain consecutive periods \(.\) or hyphens \(-\). -   For Windows instances, the hostname must be 2 to 15 characters in length and can contain letters, digits, and hyphens \(-\). It cannot contain periods \(.\) or contain only digits.
-   For other types of instances such as Linux instances, the hostname must be 2 to 64 characters in length and can contain letters, digits, hyphens \(-\), and period \(.\). Separate a name into multiple segments with periods \(.\). Each segment can contain letters, digits, and hyphens \(-\). |
|AutoRenewPeriod|Number|No|No|The auto-renewal period for the ECS instance.|Valid values:-   1
-   2
-   3
-   6
-   12

This parameter is required when the AutoRenew parameter is set to True. |
|ImageId|String|Yes|Yes|The ID of the image file used to create the instance.

|You can call the [DescribeImages](/intl.en-US/API Reference/Images/DescribeImages.md) operation to query the available image resources. For Alibaba Cloud Marketplace images, you can view the image ID of a specific image on its Product Details page at Alibaba Cloud Marketplace. |
|AutoRenew|Boolean|No|No|Specifies whether to enable auto-renewal for the ECS instance.|This parameter takes effect only when the InstanceChargeType parameter is set to PrePaid. Default value: False. Valid values:

-   True: Auto-renewal is enabled for the instance.
-   False: Auto-renewal is disabled for the instance. |
|InstanceChargeType|String|No|No|The billing method of the ECS instance.|Default value: PostPaid. Valid values: -   PrePaid: subscription. If you set this parameter to PrePaid, make sure that you have sufficient balance or credit in your account. Otherwise, an `InvalidPayMethod` error is returned.
-   PostPaid: pay-as-you-go |
|VSwitchId|String|No|No|The ID of the vSwitch. This parameter is required when you create an ECS instance in a VPC.|None|
|Password|String|No|Yes|The password that is used to log on to the instance.|The password must be 8 to 30 characters in length and must contain uppercase letters, lowercase letters, digits, and special characters. Special characters include `( ) ' ~ ! @ # $ % ^ & * - _ + = | { } [ ] : ; < > , . ? /` **Note:** Passwords of Windows instances cannot start with a forward slash \(/\). |
|PasswordInherit|Boolean|No|No|Specifies whether to use the preset password in the image.|Valid values:-   true
-   false

**Note:** If you set the PasswordInherit parameter to true, you must leave the Password parameter empty and make sure that the selected image has a preset password. |
|InstanceType|String|Yes|No|The instance type of the ECS instance.|For more information, see [Instance families](/intl.en-US/Instance/Instance families.md). You can call the [DescribeInstanceTypes](/intl.en-US/API Reference/Instances/DescribeInstanceTypes.md) operation to query the most recent instance type list.|
|MaxAmount|Integer|Yes|No|The maximum number of instances that can be created.|Valid values: 1 to 100.|
|SystemDiskCategory|String|No|No|The type of the system disk.

|Valid values: -   cloud: basic disk
-   cloud\_efficiency: ultra disk
-   cloud\_ssd: standard SSD
-   ephemeral\_ssd: local SSD

**Note:** For instances that are not I/O optimized and belong to retired instance types, the default value is cloud. For other instances, the default value is cloud\_efficiency. |
|SystemDiskSize|Number|No|Yes|The size of the system disk. Unit: GB.|Valid values: 20 to 500. Unit: GiB.

The value of the parameter must be at least 20 and greater than or equal to the size of the image.

Default value: max\{40, ImageSize\}. |
|ZoneId|String|No|No|The ID of the zone to which the ECS instance belongs.|For more information, see [DescribeZones](/intl.en-US/API Reference/Regions/DescribeZones.md). You can call this operation to query the zones.

If you do not specify this parameter, the system selects a zone. This parameter is empty by default.|
|InternetMaxBandwidthOut|Integer|No|No|The maximum outbound public bandwidth.|-   Valid values for the PayByBandwidth mode: 0 to 200. Default value: 0.
-   Valid values for the PayByTraffic mode: 1 to 200. This parameter is required if the InternetChargeType parameter is set to PayByTraffic.

Unit: Mbit/s. |
|VpcId|String|No|No|The ID of the VPC.|None|
|InstanceName|String|No|No|The name of the ECS instance.|The name can be up to 128 characters in length and can contain letters, digits, underscores \(\_\), periods \(.\), and hyphens \(-\).|
|InternetMaxBandwidthIn|Integer|No|No|The maximum inbound public bandwidth.|Valid values: 1 to 200. Unit: Mbit/s.

Default value: 200. |
|UserData|String|No|Yes|The user data that you provide when you create an ECS instance.|The user data can be up to 16 KB in size. You do not need to convert the data into Base64-encoded strings. If the data contains special characters, add a backslash \(\\\) immediately before each special character.|
|SecurityGroupId|String|No|No|The ID of the security group to which the ECS instance belongs.|Instances in the same security group can communicate with each other.|
|SecurityEnhancementStrategy|String|No|No|Specifies whether to enable security hardening.|Valid values:-   Active: Security hardening is enabled. This value is applicable only to public images.
-   Deactive: Security hardening is disabled. This value is applicable to all image types. |
|Period|Number|Yes|No|The subscription duration of the instance.|-   Valid values when the PeriodUnit parameter is set to Week: 1, 2, 3, and 4.
-   Valid values when the PeriodUnit parameter is set to Month: 1, 2, 3, 4, 5, 6, 7, 8, 9, 12, 24, 36, 48, and 60.

Unit: months.

This parameter takes effect and is required only when the InstanceChargeType parameter is set to PrePaid.

If the DedicatedHostId parameter is specified, the subscription duration of the instances must be no longer than that of the dedicated host.|
|AllocatePublicIP|Boolean|No|No|Specifies whether to assign a public IP address to the instance.|Default value: True. Valid values:-   True
-   False

If the InternetMaxBandwidthOut parameter is set to 0, no public IP addresses are assigned.|
|SystemDiskDescription|String|No|No|The description of the system disk.|None|
|DiskMappings|List|No|No|The data disks to be attached to the ECS instance.|A maximum of 16 data disks can be attached. For more information, see the [DiskMappings properties](#section_o6l_y34_56i) section in this topic. |
|DeploymentSetId|String|No|No|The ID of the deployment set.|None|
|SystemDiskPerformanceLevel|String|No|No|The performance level of the enhanced SSD \(ESSD\) that is used as the system disk.|Default value: PL1. Valid values: -   PL1: A single ESSD delivers up to 50,000 random read/write IOPS.
-   PL2: A single ESSD delivers up to 100,000 random read/write IOPS.
-   PL3: A single ESSD delivers up to 1,000,000 random read/write IOPS.

For more information about performance levels of ESSDs, see [ESSDs](/intl.en-US/Block Storage/Block Storage overview/ESSDs.md). |

## Tags syntax

```
"Tags": [
  {
    "Key": String,
    "Value": String
  }
]
```

## Tags properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Key|String|Yes|No|The tag key.|The tag key must be 1 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|
|Value|String|No|No|The tag value.|The tag value must be 0 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|

## DiskMappings syntax

```
"DiskMappings": [
  {
    "Category": String,
    "DiskName": String,
    "Description": String,
    "Device": String,
    "SnapshotId": String,
    "PerformanceLevel": String,
    "Size": String
  }
]
```

## DiskMappings properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Category|String|No|No|The type of the data disk.|Default value: cloud\_efficiency. Valid values:-   cloud: basic disk
-   cloud\_ssd: standard SSD
-   cloud\_efficiency: ultra disk
-   ephemeral\_ssd: local SSD |
|DiskName|String|No|No|The name of the data disk.|The name can be up to 128 characters in length and can contain letters, digits, underscores\(\_\), periods\(.\), and hyphens \(-\).|
|Description|String|No|No|The description of the data disk.|The description must be 2 to 256 characters in length. This parameter is empty by default. |
|Device|String|No|No|The device name of the data disk.|The system allocates a device name in alphabetical order. Example: `/dev/xvd[a-z]`.|
|SnapshotId|String|No|No|The ID of the snapshot that is used to create the data disk.|None|
|PerformanceLevel|String|No|No|The performance level of the ESSD that is used as the data disk.|Default value: PL1. Valid values: -   PL1: A single ESSD delivers up to 50,000 random read/write IOPS.
-   PL2: A single ESSD delivers up to 100,000 random read/write IOPS.
-   PL3: A single ESSD delivers up to 1,000,000 random read/write IOPS.

For more information about performance levels of ESSDs, see [ESSDs](/intl.en-US/Block Storage/Block Storage overview/ESSDs.md). |
|Size|String|Yes|No|The size of the data disk.|Unit: GB|

## Response parameters

Fn::GetAtt

-   OrderId: the ID of the order.
-   InnerIps: the private IP addresses of the classic network-typed instance. This parameter takes effect only when the NetworkType parameter is set to classic.
-   PrivateIps: the private IP addresses of the VPC-typed instances. This parameter takes effect only when the NetworkType parameter is set to VPC.
-   ZoneIds: the IDs of the zones.
-   PublicIps: the public IP addresses of the classic network-typed instances. This parameter takes effect only when the NetworkType parameter is set to classic.
-   HostNames: the hostnames of the ECS instances.
-   RelatedOrderIds: the related order IDs.
-   InstanceIds: the IDs of the ECS instances. An ID is a globally unique identifier \(GUID\) generated by the system for an instance.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "PeriodType": {
      "Type": "String",
      "Description": "Charge period for created instances.",
      "AllowedValues": [
        "Monthly",
        "Yearly"
      ]
    },
    "DedicatedHostId": {
      "Type": "String",
      "Description": "which dedicated host will be deployed"
    },
    "PrivateIpAddress": {
      "Type": "String",
      "Description": "Private IP for the instance created. Only works for VPC instance and cannot duplicated with existing instance."
    },
    "Description": {
      "Type": "String",
      "Description": "Description of the instance, [2, 256] characters. Do not fill or empty, the default is empty."
    },
    "DiskMappings": {
      "Type": "Json",
      "Description": "Disk mappings to attach to instance. Max support 16 disks.\nIf the image contains a data disk, you can specify other parameters of the data disk via the same value of parameter \"Device\". If parameter \"Category\" is not specified, it will be cloud_efficiency instead of \"Category\" of data disk in the image.",
      "MaxLength": 16
    },
    "SystemDiskSize": {
      "Type": "Number",
      "Description": "Disk size of the system disk, range from 20 to 500 GB. If you specify with your own image, make sure the system disk size bigger than image size. ",
      "MinValue": 20
    },
    "UserData": {
      "Type": "String",
      "Description": "User data to pass to instance. [1, 16KB] characters.User data should not be base64 encoded. If you want to pass base64 encoded string to the property, use function Fn::Base64Decode to decode the base64 string first."
    },
    "SystemDiskDescription": {
      "Type": "String",
      "Description": "Description of created system disk."
    },
    "InstanceChargeType": {
      "Type": "String",
      "Description": "Instance Charge type, allowed value: Prepaid and Postpaid. If specified Prepaid, please ensure you have sufficient balance in your account. Or instance creation will be failure. Default value is Postpaid.",
      "AllowedValues": [
        "PrePaid",
        "PostPaid"
      ],
      "Default": "PostPaid"
    },
    "AutoRenew": {
      "Type": "Boolean",
      "Description": "Auto renew the prepay instance. If the period type is by year, it will renew by year, else it will renew by month.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ],
      "Default": false
    },
    "MaxAmount": {
      "Type": "Number",
      "Description": "Max number of instances to create, should be smaller than 'MaxAmount' and smaller than 100.",
      "MinValue": 1,
      "MaxValue": 100
    },
    "RamRoleName": {
      "Type": "String",
      "Description": "Instance RAM role name. The name is provided and maintained by Resource Access Management (RAM) and can be queried using ListRoles. For more information, see RAM API CreateRole and ListRoles."
    },
    "SystemDiskPerformanceLevel": {
      "Type": "String",
      "Description": "The performance level of the enhanced SSD used as the system disk.Default value: PL1. Valid values:PL0: A single enhanced SSD delivers up to 10,000 random read/write IOPS.PL1: A single enhanced SSD delivers up to 50,000 random read/write IOPS.PL2: A single enhanced SSD delivers up to 100,000 random read/write IOPS.PL3: A single enhanced SSD delivers up to 1,000,000 random read/write IOPS."
    },
    "MinAmount": {
      "Type": "Number",
      "Description": "Max number of instances to create, should be bigger than 'MinAmount' and smaller than 100.",
      "MinValue": 1,
      "MaxValue": 100,
      "Default": 1
    },
    "ImageId": {
      "Type": "String",
      "Description": "Image ID to create ecs instance."
    },
    "SystemDiskDiskName": {
      "Type": "String",
      "Description": "Name of created system disk."
    },
    "InstanceType": {
      "Type": "String",
      "Description": "Ecs instance supported instance type, make sure it should be correct."
    },
    "AllocatePublicIP": {
      "Type": "Boolean",
      "Description": "The public ip for ecs instance, if properties is true, will allocate public ip. If property InternetMaxBandwidthOut set to 0, it will not assign public ip.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ],
      "Default": true
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to instance. Max support 20 tags to add during create instance. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
    },
    "HostName": {
      "Type": "String",
      "Description": "Host name of created ecs instance. at least 2 characters, and '.' '-' Is not the first and last characters as hostname, not continuous use. Windows platform can be up to 15 characters, allowing letters (without limiting case), numbers and '-', and does not support the number of points, not all is digital ('.').Other (Linux, etc.) platform up to 30 characters, allowing support number multiple points for the period between the points, each permit letters (without limiting case), numbers and '-' components."
    },
    "PasswordInherit": {
      "Type": "Boolean",
      "Description": "Specifies whether to use the password preset in the image. To use the PasswordInherit parameter, the Password parameter must be empty and you must make sure that the selected image has a password configured.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "Password": {
      "Type": "String",
      "Description": "Password of created ecs instance. Must contain at least 3 types of special character, lower character, upper character, number."
    },
    "AutoRenewPeriod": {
      "Type": "Number",
      "Description": "The time period of auto renew. When the parameter InstanceChargeType is PrePaid, it will take effect.It could be 1, 2, 3, 6, 12. Default value is 1.",
      "AllowedValues": [
        1,
        2,
        3,
        6,
        12
      ],
      "Default": 1
    },
    "KeyPairName": {
      "Type": "String",
      "Description": "SSH key pair name."
    },
    "IoOptimized": {
      "Type": "Boolean",
      "Description": "The 'optimized' instance can provide better IO performance. Support true or false, Default is true. ",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ],
      "Default": true
    },
    "ZoneId": {
      "Type": "String",
      "Description": "The ID of the zone to which the instance belongs. For more information, \ncall the DescribeZones operation to query the most recent zone list. \nDefault value is empty, which means random selection."
    },
    "HpcClusterId": {
      "Type": "String",
      "Description": "The HPC cluster ID to which the instance belongs."
    },
    "VSwitchId": {
      "Type": "String",
      "Description": "The vSwitch Id to create ecs instance."
    },
    "SecurityGroupId": {
      "Type": "String",
      "Description": "Security group to create ecs instance. For classic instance need the security group not belong to VPC, for VPC instance, please make sure the security group belong to specified VPC."
    },
    "Period": {
      "Type": "Number",
      "Description": "Prepaid time period. While choose by pay by month, it could be from 1 to 9. While choose pay by year, it could be from 1 to 3.",
      "MinValue": 1,
      "MaxValue": 9,
      "Default": 1
    },
    "InternetChargeType": {
      "Type": "String",
      "Description": "Instance internet access charge type.Support 'PayByBandwidth' and 'PayByTraffic' only. For AfterPay instance, default is 'PayByBandwidth'.",
      "AllowedValues": [
        "PayByBandwidth",
        "PayByTraffic"
      ],
      "Default": "PayByBandwidth"
    },
    "SystemDiskCategory": {
      "Type": "String",
      "Description": "Category of system disk. Default is cloud_efficiency. support cloud|cloud_efficiency|cloud_ssd|cloud_essd|ephemeral_ssd",
      "AllowedValues": [
        "cloud",
        "cloud_efficiency",
        "cloud_ssd",
        "cloud_essd",
        "ephemeral_ssd"
      ],
      "Default": "cloud_efficiency"
    },
    "InstanceName": {
      "Type": "String",
      "Description": "Display name of the instance, [2, 128] English or Chinese characters, must start with a letter or Chinese in size, can contain numbers, '_' or '.', '-'"
    },
    "DeploymentSetId": {
      "Type": "String",
      "Description": "Deployment set ID."
    },
    "InternetMaxBandwidthOut": {
      "Type": "Number",
      "Description": "Set internet output bandwidth of instance. Unit is Mbps(Mega bit per second). Range is [0,200]. Default is 1.While the property is not 0, public ip will be assigned for instance.",
      "MinValue": 0,
      "MaxValue": 200,
      "Default": 1
    },
    "VpcId": {
      "Type": "String",
      "Description": "The VPC id to create ecs instance."
    },
    "InternetMaxBandwidthIn": {
      "Type": "Number",
      "Description": "Max internet out band width setting, unit in Mbps(Mega bit per second). The range is [1,200], default is 200 Mbps.",
      "MinValue": 1,
      "MaxValue": 200,
      "Default": 200
    },
    "SecurityEnhancementStrategy": {
      "Type": "String",
      "Description": "",
      "AllowedValues": [
        "Active",
        "Deactive"
      ]
    },
    "PeriodUnit": {
      "Type": "String",
      "Description": "Unit of prepaid time period, it could be Week/Month/Year. Default value is Month.",
      "AllowedValues": [
        "Week",
        "Month",
        "Year"
      ],
      "Default": "Month"
    }
  },
  "Resources": {
    "PrepayInstance": {
      "Type": "ALIYUN::ECS::PrepayInstance",
      "Properties": {
        "PeriodType": {
          "Ref": "PeriodType"
        },
        "DedicatedHostId": {
          "Ref": "DedicatedHostId"
        },
        "PrivateIpAddress": {
          "Ref": "PrivateIpAddress"
        },
        "Description": {
          "Ref": "Description"
        },
        "DiskMappings": {
          "Ref": "DiskMappings"
        },
        "SystemDiskSize": {
          "Ref": "SystemDiskSize"
        },
        "UserData": {
          "Ref": "UserData"
        },
        "SystemDiskDescription": {
          "Ref": "SystemDiskDescription"
        },
        "InstanceChargeType": {
          "Ref": "InstanceChargeType"
        },
        "AutoRenew": {
          "Ref": "AutoRenew"
        },
        "MaxAmount": {
          "Ref": "MaxAmount"
        },
        "RamRoleName": {
          "Ref": "RamRoleName"
        },
        "SystemDiskPerformanceLevel": {
          "Ref": "SystemDiskPerformanceLevel"
        },
        "MinAmount": {
          "Ref": "MinAmount"
        },
        "ImageId": {
          "Ref": "ImageId"
        },
        "SystemDiskDiskName": {
          "Ref": "SystemDiskDiskName"
        },
        "InstanceType": {
          "Ref": "InstanceType"
        },
        "AllocatePublicIP": {
          "Ref": "AllocatePublicIP"
        },
        "Tags": {
          "Ref": "Tags"
        },
        "HostName": {
          "Ref": "HostName"
        },
        "PasswordInherit": {
          "Ref": "PasswordInherit"
        },
        "Password": {
          "Ref": "Password"
        },
        "AutoRenewPeriod": {
          "Ref": "AutoRenewPeriod"
        },
        "KeyPairName": {
          "Ref": "KeyPairName"
        },
        "IoOptimized": {
          "Ref": "IoOptimized"
        },
        "ZoneId": {
          "Ref": "ZoneId"
        },
        "HpcClusterId": {
          "Ref": "HpcClusterId"
        },
        "VSwitchId": {
          "Ref": "VSwitchId"
        },
        "SecurityGroupId": {
          "Ref": "SecurityGroupId"
        },
        "Period": {
          "Ref": "Period"
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
        "VpcId": {
          "Ref": "VpcId"
        },
        "InternetMaxBandwidthIn": {
          "Ref": "InternetMaxBandwidthIn"
        },
        "SecurityEnhancementStrategy": {
          "Ref": "SecurityEnhancementStrategy"
        },
        "PeriodUnit": {
          "Ref": "PeriodUnit"
        }
      }
    }
  },
  "Outputs": {
    "PublicIps": {
      "Description": "Public IP address list of created ecs instance.",
      "Value": {
        "Fn::GetAtt": [
          "PrepayInstance",
          "PublicIps"
        ]
      }
    },
    "RelatedOrderIds": {
      "Description": "The related order id list of created ecs instances",
      "Value": {
        "Fn::GetAtt": [
          "PrepayInstance",
          "RelatedOrderIds"
        ]
      }
    },
    "PrivateIps": {
      "Description": "Private IP address list of created ecs instance. Only for VPC instance.",
      "Value": {
        "Fn::GetAtt": [
          "PrepayInstance",
          "PrivateIps"
        ]
      }
    },
    "HostNames": {
      "Description": "Host names of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "PrepayInstance",
          "HostNames"
        ]
      }
    },
    "InnerIps": {
      "Description": "Inner IP address list of the specified instance. Only for classical instance.",
      "Value": {
        "Fn::GetAtt": [
          "PrepayInstance",
          "InnerIps"
        ]
      }
    },
    "ZoneIds": {
      "Description": "Zone id of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "PrepayInstance",
          "ZoneIds"
        ]
      }
    },
    "OrderId": {
      "Description": "The order id list of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "PrepayInstance",
          "OrderId"
        ]
      }
    },
    "InstanceIds": {
      "Description": "The instance id list of created ecs instance",
      "Value": {
        "Fn::GetAtt": [
          "PrepayInstance",
          "InstanceIds"
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
  PeriodType:
    Type: String
    Description: Charge period for created instances.
    AllowedValues:
      - Monthly
      - Yearly
  DedicatedHostId:
    Type: String
    Description: which dedicated host will be deployed
  PrivateIpAddress:
    Type: String
    Description: >-
      Private IP for the instance created. Only works for VPC instance and
      cannot duplicated with existing instance.
  Description:
    Type: String
    Description: >-
      Description of the instance, [2, 256] characters. Do not fill or empty,
      the default is empty.
  DiskMappings:
    Type: Json
    Description: >-
      Disk mappings to attach to instance. Max support 16 disks.

      If the image contains a data disk, you can specify other parameters of the
      data disk via the same value of parameter "Device". If parameter
      "Category" is not specified, it will be cloud_efficiency instead of
      "Category" of data disk in the image.
    MaxLength: 16
  SystemDiskSize:
    Type: Number
    Description: >-
      Disk size of the system disk, range from 20 to 500 GB. If you specify with
      your own image, make sure the system disk size bigger than image size. 
    MinValue: 20
  UserData:
    Type: String
    Description: >-
      User data to pass to instance. [1, 16KB] characters.User data should not
      be base64 encoded. If you want to pass base64 encoded string to the
      property, use function Fn::Base64Decode to decode the base64 string first.
  SystemDiskDescription:
    Type: String
    Description: Description of created system disk.
  InstanceChargeType:
    Type: String
    Description: >-
      Instance Charge type, allowed value: Prepaid and Postpaid. If specified
      Prepaid, please ensure you have sufficient balance in your account. Or
      instance creation will be failure. Default value is Postpaid.
    AllowedValues:
      - PrePaid
      - PostPaid
    Default: PostPaid
  AutoRenew:
    Type: Boolean
    Description: >-
      Auto renew the prepay instance. If the period type is by year, it will
      renew by year, else it will renew by month.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
    Default: false
  MaxAmount:
    Type: Number
    Description: >-
      Max number of instances to create, should be smaller than 'MaxAmount' and
      smaller than 100.
    MinValue: 1
    MaxValue: 100
  RamRoleName:
    Type: String
    Description: >-
      Instance RAM role name. The name is provided and maintained by Resource
      Access Management (RAM) and can be queried using ListRoles. For more
      information, see RAM API CreateRole and ListRoles.
  SystemDiskPerformanceLevel:
    Type: String
    Description: >-
      The performance level of the enhanced SSD used as the system disk.Default
      value: PL1. Valid values:PL0: A single enhanced SSD delivers up to 10,000
      random read/write IOPS.PL1: A single enhanced SSD delivers up to 50,000
      random read/write IOPS.PL2: A single enhanced SSD delivers up to 100,000
      random read/write IOPS.PL3: A single enhanced SSD delivers up to 1,000,000
      random read/write IOPS.
  MinAmount:
    Type: Number
    Description: >-
      Max number of instances to create, should be bigger than 'MinAmount' and
      smaller than 100.
    MinValue: 1
    MaxValue: 100
    Default: 1
  ImageId:
    Type: String
    Description: Image ID to create ecs instance.
  SystemDiskDiskName:
    Type: String
    Description: Name of created system disk.
  InstanceType:
    Type: String
    Description: 'Ecs instance supported instance type, make sure it should be correct.'
  AllocatePublicIP:
    Type: Boolean
    Description: >-
      The public ip for ecs instance, if properties is true, will allocate
      public ip. If property InternetMaxBandwidthOut set to 0, it will not
      assign public ip.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
    Default: true
  Tags:
    Type: Json
    Description: >-
      Tags to attach to instance. Max support 20 tags to add during create
      instance. Each tag with two properties Key and Value, and Key is required.
    MaxLength: 20
  HostName:
    Type: String
    Description: >-
      Host name of created ecs instance. at least 2 characters, and '.' '-' Is
      not the first and last characters as hostname, not continuous use. Windows
      platform can be up to 15 characters, allowing letters (without limiting
      case), numbers and '-', and does not support the number of points, not all
      is digital ('.').Other (Linux, etc.) platform up to 30 characters,
      allowing support number multiple points for the period between the points,
      each permit letters (without limiting case), numbers and '-' components.
  PasswordInherit:
    Type: Boolean
    Description: >-
      Specifies whether to use the password preset in the image. To use the
      PasswordInherit parameter, the Password parameter must be empty and you
      must make sure that the selected image has a password configured.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
  Password:
    Type: String
    Description: >-
      Password of created ecs instance. Must contain at least 3 types of special
      character, lower character, upper character, number.
  AutoRenewPeriod:
    Type: Number
    Description: >-
      The time period of auto renew. When the parameter InstanceChargeType is
      PrePaid, it will take effect.It could be 1, 2, 3, 6, 12. Default value is
      1.
    AllowedValues:
      - 1
      - 2
      - 3
      - 6
      - 12
    Default: 1
  KeyPairName:
    Type: String
    Description: SSH key pair name.
  IoOptimized:
    Type: Boolean
    Description: >-
      The 'optimized' instance can provide better IO performance. Support true
      or false, Default is true. 
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
    Default: true
  ZoneId:
    Type: String
    Description: |-
      The ID of the zone to which the instance belongs. For more information, 
      call the DescribeZones operation to query the most recent zone list. 
      Default value is empty, which means random selection.
  HpcClusterId:
    Type: String
    Description: The HPC cluster ID to which the instance belongs.
  VSwitchId:
    Type: String
    Description: The vSwitch Id to create ecs instance.
  SecurityGroupId:
    Type: String
    Description: >-
      Security group to create ecs instance. For classic instance need the
      security group not belong to VPC, for VPC instance, please make sure the
      security group belong to specified VPC.
  Period:
    Type: Number
    Description: >-
      Prepaid time period. While choose by pay by month, it could be from 1 to
      9. While choose pay by year, it could be from 1 to 3.
    MinValue: 1
    MaxValue: 9
    Default: 1
  InternetChargeType:
    Type: String
    Description: >-
      Instance internet access charge type.Support 'PayByBandwidth' and
      'PayByTraffic' only. For AfterPay instance, default is 'PayByBandwidth'.
    AllowedValues:
      - PayByBandwidth
      - PayByTraffic
    Default: PayByBandwidth
  SystemDiskCategory:
    Type: String
    Description: >-
      Category of system disk. Default is cloud_efficiency. support
      cloud|cloud_efficiency|cloud_ssd|cloud_essd|ephemeral_ssd
    AllowedValues:
      - cloud
      - cloud_efficiency
      - cloud_ssd
      - cloud_essd
      - ephemeral_ssd
    Default: cloud_efficiency
  InstanceName:
    Type: String
    Description: >-
      Display name of the instance, [2, 128] English or Chinese characters, must
      start with a letter or Chinese in size, can contain numbers, '_' or '.',
      '-'
  DeploymentSetId:
    Type: String
    Description: Deployment set ID.
  InternetMaxBandwidthOut:
    Type: Number
    Description: >-
      Set internet output bandwidth of instance. Unit is Mbps(Mega bit per
      second). Range is [0,200]. Default is 1.While the property is not 0,
      public ip will be assigned for instance.
    MinValue: 0
    MaxValue: 200
    Default: 1
  VpcId:
    Type: String
    Description: The VPC id to create ecs instance.
  InternetMaxBandwidthIn:
    Type: Number
    Description: >-
      Max internet out band width setting, unit in Mbps(Mega bit per second).
      The range is [1,200], default is 200 Mbps.
    MinValue: 1
    MaxValue: 200
    Default: 200
  SecurityEnhancementStrategy:
    Type: String
    Description: ''
    AllowedValues:
      - Active
      - Deactive
  PeriodUnit:
    Type: String
    Description: >-
      Unit of prepaid time period, it could be Week/Month/Year. Default value is
      Month.
    AllowedValues:
      - Week
      - Month
      - Year
    Default: Month
Resources:
  PrepayInstance:
    Type: 'ALIYUN::ECS::PrepayInstance'
    Properties:
      PeriodType:
        Ref: PeriodType
      DedicatedHostId:
        Ref: DedicatedHostId
      PrivateIpAddress:
        Ref: PrivateIpAddress
      Description:
        Ref: Description
      DiskMappings:
        Ref: DiskMappings
      SystemDiskSize:
        Ref: SystemDiskSize
      UserData:
        Ref: UserData
      SystemDiskDescription:
        Ref: SystemDiskDescription
      InstanceChargeType:
        Ref: InstanceChargeType
      AutoRenew:
        Ref: AutoRenew
      MaxAmount:
        Ref: MaxAmount
      RamRoleName:
        Ref: RamRoleName
      SystemDiskPerformanceLevel:
        Ref: SystemDiskPerformanceLevel
      MinAmount:
        Ref: MinAmount
      ImageId:
        Ref: ImageId
      SystemDiskDiskName:
        Ref: SystemDiskDiskName
      InstanceType:
        Ref: InstanceType
      AllocatePublicIP:
        Ref: AllocatePublicIP
      Tags:
        Ref: Tags
      HostName:
        Ref: HostName
      PasswordInherit:
        Ref: PasswordInherit
      Password:
        Ref: Password
      AutoRenewPeriod:
        Ref: AutoRenewPeriod
      KeyPairName:
        Ref: KeyPairName
      IoOptimized:
        Ref: IoOptimized
      ZoneId:
        Ref: ZoneId
      HpcClusterId:
        Ref: HpcClusterId
      VSwitchId:
        Ref: VSwitchId
      SecurityGroupId:
        Ref: SecurityGroupId
      Period:
        Ref: Period
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
      VpcId:
        Ref: VpcId
      InternetMaxBandwidthIn:
        Ref: InternetMaxBandwidthIn
      SecurityEnhancementStrategy:
        Ref: SecurityEnhancementStrategy
      PeriodUnit:
        Ref: PeriodUnit
Outputs:
  PublicIps:
    Description: Public IP address list of created ecs instance.
    Value:
      'Fn::GetAtt':
        - PrepayInstance
        - PublicIps
  RelatedOrderIds:
    Description: The related order id list of created ecs instances
    Value:
      'Fn::GetAtt':
        - PrepayInstance
        - RelatedOrderIds
  PrivateIps:
    Description: Private IP address list of created ecs instance. Only for VPC instance.
    Value:
      'Fn::GetAtt':
        - PrepayInstance
        - PrivateIps
  HostNames:
    Description: Host names of created instance.
    Value:
      'Fn::GetAtt':
        - PrepayInstance
        - HostNames
  InnerIps:
    Description: >-
      Inner IP address list of the specified instance. Only for classical
      instance.
    Value:
      'Fn::GetAtt':
        - PrepayInstance
        - InnerIps
  ZoneIds:
    Description: Zone id of created instance.
    Value:
      'Fn::GetAtt':
        - PrepayInstance
        - ZoneIds
  OrderId:
    Description: The order id list of created instance.
    Value:
      'Fn::GetAtt':
        - PrepayInstance
        - OrderId
  InstanceIds:
    Description: The instance id list of created ecs instance
    Value:
      'Fn::GetAtt':
        - PrepayInstance
        - InstanceIds
```

For more examples, visit [PrepayInstance.json](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ECS/JSON/PrepayInstance.json) and [PrepayInstance.yml](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ECS/YAML/PrepayInstance.yml). In the examples, the ALIYUN::ECS::PrepayInstance and ALIYUN::ECS::PrepayInstanceGroupClone resource types are involved.

