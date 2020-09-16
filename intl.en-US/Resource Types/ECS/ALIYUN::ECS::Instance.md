# ALIYUN::ECS::Instance

ALIYUN::ECS::Instance is used to create an ECS instance.

## Syntax

```
{
  "Type": "ALIYUN::ECS::Instance",
  "Properties": {
    "DedicatedHostId": String,
    "Period": Number,
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
    "HostName": String,
    "AutoRenewPeriod": Number,
    "ImageId": String,
    "ResourceGroupId": String,
    "InstanceChargeType": String,
    "VSwitchId": String,
    "Password": String,
    "InstanceType": String,
    "SystemDiskCategory": String,
    "UserData": String,
    "SystemDiskSize": Number,
    "ZoneId": String,
    "InternetMaxBandwidthOut": Integer,
    "VpcId": String,
    "SpotStrategy": String,
    "InstanceName": String,
    "InternetMaxBandwidthIn": Integer,
    "DeletionProtection": Boolean,
    "DeploymentSetId": String,
    "SecurityGroupId": String,
    "SpotPriceLimit": String,
    "HpcClusterId": String,
    "AllocatePublicIP": Boolean,
    "SystemDiskDescription": String,
    "SystemDiskPerformanceLevel": String,
    "DiskMappings": List
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ResourceGroupId|String|No|No|The ID of the resource group to which the created ECS instance belongs.|None|
|ImageId|String|Yes|Yes|The ID of the image that is used to create the ECS instance. You can use a public image, a custom image, or an Alibaba Cloud Marketplace image.|You can specify a partial public image ID instead of providing the complete ID. Example: -   If you enter ubuntu, the system matches it with the following ID: ubuntu16\_0402\_64\_20G\_alibase\_20170818.vhd
-   If you enter ubuntu\_14, the system matches it with the following ID: ubuntu\_14\_0405\_64\_20G\_alibase\_20170824.vhd
-   If you enter ubuntu\*14\*32, the system matches it with the following ID: ubuntu\_14\_0405\_32\_40G\_alibase\_20170711.vhd
-   If you enter ubuntu\_16\_0402\_32, the system matches it with the following ID: ubuntu\_16\_0402\_32\_40G\_alibase\_20170711.vhd |
|InstanceType|String|Yes|No|The type of the created ECS instance.|For more information, see [Instance families](/intl.en-US/Instance/Instance families.md).|
|SecurityGroupId|String|No|No|The ID of the security group to which the created ECS instance belongs.|None|
|Description|String|No|Yes|The description of the created ECS instance.|The description must be 2 to 256 characters in length.|
|InstanceName|String|No|No|The name of the created ECS instance.|The name must be 2 to 128 characters in length and can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with `http://` or `https://`. If this parameter is not specified, the name is set to the instance ID by default. |
|Password|String|No|Yes|The password that is used to log on to the created ECS instance.|The password must be 8 to 30 characters in length and must contain at least three of the following character types: uppercase letters, lowercase letters, digits, and special characters. Special characters include ```
( ) ~ ! @ # $ % ^ & * - + = | { } [ ] : ; ' < > , . ? / -
```

If you specify this parameter in the API request, use HTTPS to secure the API and protect your password.|
|HostName|String|No|No|The hostname of the created ECS instance.|The hostname must be at least 2 characters in length and cannot contain consecutive periods \(.\) or hyphens \(-\). It cannot start or end with a period \(.\) or hyphen \(-\). -   For Windows instances, the hostname can be up to 15 characters in length and can contain letters, digits, and hyphens \(-\). It cannot contain periods \(.\) or contain only digits.
-   For other instances such as Linux instances, the hostname can be up to 30 characters in length and can contain letters, digits, and hyphens \(-\). You can use periods \(.\) to separate a name into several segments. |
|AllocatePublicIP|Boolean|No|No|Specifies whether to allocate a public IP address to the created ECS instance.|If the InternetMaxBandwidthOut parameter is set to 0, no public IP addresses are allocated. Default value: true. Valid values:

-   true
-   false |
|PrivateIpAddress|String|No|No|The private IP address of an ECS instance in a VPC.|The specified IP address must not be used by other instances in the VPC.|
|InternetChargeType|String|No|No|The billing method for network usage.|Default value: PayByTraffic. Valid values: -   PayByBandwidth
-   PayByTraffic |
|InternetMaxBandwidthIn|Integer|No|No|The maximum inbound bandwidth from the Internet.|Unit: Mbit/s. Valid values: 1 to 200.

Default value: 200. |
|InternetMaxBandwidthOut|Integer|No|No|The maximum outbound bandwidth to the Internet.|Unit: Mbit/s. Valid values: 0 to 100.

Default value: 0. |
|IoOptimized|String|No|No|Specifies whether the created ECS instance is I/O optimized.|Default value: optimized. Valid values:-   none: The instance is not I/O optimized.
-   optimized: The instance is I/O optimized. |
|DiskMappings|List|No|No|The data disks to be attached to the created ECS instance.|A maximum of 16 disks can be attached. For more information, see [DiskMappings properties](#section_8il_fs8_t3z). |
|SystemDiskCategory|String|No|No|The type of the system disk.|Valid values: -   cloud: basic disk.
-   cloud\_ssd: standard SSD.
-   cloud\_efficiency: ultra disk.

For non-I/O optimized instances of phased-out instance types, the default value is cloud. For other instances, the default value is cloud\_efficiency.|
|SystemDiskDescription|String|No|No|The description of the system disk.|None|
|SystemDiskDiskName|String|No|No|The name of the system disk.|The name must be 2 to 128 characters in length and can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). The name must start with a letter and cannot start with `http://` or `https://`.|
|SystemDiskSize|Number|No|Yes|The size of the system disk.|Valid values: 20 to 500. Unit: GB.

If a custom image is used to create a system disk, make sure that the size of the system disk is greater than that of the custom image.|
|Tags|List|No|Yes|The custom tags of the created ECS instance.|A maximum of 20 tags can be specified in the `[{"Key": "tagKey", "Value": "tagValue"},{"Key": "tagKey2", "Value": "tagValue2"}]` format. For more information, see [Tags properties](#section_fes_3kc_798). |
|UserData|String|No|Yes|The user data that you provide when you create the ECS instance.|The user data can be up to 16 KB in size. You do not need to convert the data into Base64-encoded strings. If the data contains special characters, add a backslash \(\\\) immediately before each special character.|
|ZoneId|String|No|No|The ID of the zone.|None|
|HpcClusterId|String|No|No|The ID of the HPC cluster to which the created ECS instance belongs.|None|
|VpcId|String|No|No|The ID of the VPC to which the created ECS instance belongs.|None|
|VSwitchId|String|No|No|The ID of the VSwitch for the created ECS instance.|None|
|InstanceChargeType|String|No|No|The billing method of the ECS instance.|Default value: PostPaid. Valid values: -   PrePaid: the subscription billing method.

**Note:** If you set this parameter to PrePaid, make sure that you have sufficient balance in your account. Otherwise, the instance fails to be created.

-   PostPaid: the pay-as-you-go billing method. |
|Period|Number|No|No|The billing cycle of the created ECS instance.|Valid values: 1, 2, 3, 4, 5, 6, 7, 8, 9, 12, 24, and 36. Unit: months.

This parameter is required when the InstanceChargeType parameter is set to PrePaid. This parameter is optional when the InstanceChargeType parameter is set to PostPaid.|
|KeyPairName|String|No|No|The name of the key pair that is used to connect to the created ECS instance.|For Windows instances, this parameter is ignored by default. For Linux ECS instances, logon by password is disabled by default. To enhance instance security, we recommend that you use the SSH key pair for connection.|
|RamRoleName|String|No|No|The RAM role name of the created ECS instance.|For more information, see [CreateRole](/intl.en-US/API Reference (RAM)/Role management APIs/CreateRole.md) and [ListRoles](/intl.en-US/API Reference (RAM)/Role management APIs/ListRoles.md).|
|SpotPriceLimit|String|No|No|The maximum hourly price of the instance.|Three decimal places are allowed at most. This parameter takes effect only when the SpotStrategy parameter is set to SpotWithPriceLimit.|
|SpotStrategy|String|No|No|The bidding policy for the pay-as-you-go instance.|This parameter takes effect only when the InstanceChargeType parameter is set to PostPaid. Default value: NoSpot. Valid values:

-   NoSpot: applies to regular pay-as-you-go instances.
-   SpotWithPriceLimit: applies to preemptible instances with a maximum hourly price.
-   SpotAsPriceGo: applies to pay-as-you-go instances priced at the market price at the time of purchase. |
|DedicatedHostId|String|No|No|The ID of the dedicated host for the created ECS instance.|You can call the [DescribeDedicatedHosts](/intl.en-US/API Reference/Dedicated hosts/DescribeDedicatedHosts.md) operation to query the list of dedicated host IDs. If this parameter is specified, the SpotStrategy and SpotPriceLimit parameters are ignored. This is because preemptible instances cannot be created on dedicated hosts.|
|PeriodUnit|String|No|No|The unit of billing cycle for the created ECS instance.|Default value: Month. Valid values: -   Week
-   Month

Valid values of the Period parameter when this parameter is set to Week: 1, 2, 3, and 4. Valid values of the AutoRenewPeriod parameter when this parameter is set to Week: 1, 2, and 3. Valid values of the Period parameter when this parameter is set to Month: 1, 2, 3, 4, 5, 6, 7, 8, 9, 12, 24, 36, 48, and 60. Valid values of the AutoRenewPeriod parameter when this parameter is set to Month: 1, 2, 3, 6, and 12.|
|AutoRenewPeriod|Number|No|No|The auto-renewal period for the created ECS instance.|This parameter is required when the AutoRenew parameter is set to True. Valid values: 1, 2, 3, 6, and 12.|
|AutoRenew|String|No|No|Specifies whether to enable auto-renewal for the created ECS instance.|Default value: False. Valid values: -   True: enables auto renewal for the created ECS instance.
-   False: disables auto-renewal for the created ECS instance.

This parameter is required when the InstanceChargeType parameter is set to PrePaid.|
|DeletionProtection|Boolean|No|No|The deletion protection property of the ECS instance. It specifies whether the instance can be released by using the ECS console or by calling the [DeleteInstance](/intl.en-US/API Reference/Instances/DeleteInstance.md) operation.|Valid values: -   true
-   false |
|DeploymentSetId|String|No|No|The ID of the deployment set.|None|
|SystemDiskPerformanceLevel|String|No|No|The performance level of the enhanced SSD \(ESSD\) that is used as the system disk.|Default value: PL1. Valid values: -   PL1: A single ESSD delivers up to 50,000 random read/write IOPS.
-   PL2: A single ESSD delivers up to 100,000 random read/write IOPS.
-   PL3: A single ESSD delivers up to 1,000,000 random read/write IOPS.

For more information about performance levels of ESSDs, see [Enhanced SSDs](/intl.en-US/Block Storage/Block Storage overview/Enhanced SSDs.md).|

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
|Size|String|Yes|No|The size of the data disk.|Valid values: 20 to 500. Unit: GB. |
|Category|String|No|No|The type of the data disk.|Valid values: -   cloud: basic disk.
-   cloud\_ssd: standard SSD.
-   cloud\_essd: ESSD.
-   cloud\_efficiency: ultra disk.
-   ephemeral\_ssd: local SSD.

For I/O optimized instances, the default value is cloud\_efficiency. For non-I/O optimized instances, the default value is cloud.|
|DiskName|String|No|No|The name of the data disk.|The name must be 2 to 128 characters in length and can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). The name must start with a letter and cannot start with `http://` or `https://`.|
|Description|String|No|No|The description of the data disk.|The description must be 2 to 256 characters in length and cannot start with `http://` or `https://`.|
|Device|String|No|No|The mount point of the data disk.|**Note:** This parameter will be removed in the future. We recommend that you use other parameters to ensure compatibility. |
|PerformanceLevel|String|No|No|The performance level of the ESSD that is used as the data disk.|Default value: PL1. Valid values:-   PL1: A single ESSD delivers up to 50,000 random read/write IOPS.
-   PL2: A single ESSD delivers up to 100,000 random read/write IOPS.
-   PL3: A single ESSD delivers up to 1,000,000 random read/write IOPS.

For more information about performance levels of ESSDs, see [Enhanced SSDs](/intl.en-US/Block Storage/Block Storage overview/Enhanced SSDs.md).|
|SnapshotId|String|No|No|The ID of the snapshot that is used to create the data disk.|None|

## Tags syntax

```
"Tags": [
  {
    "Value": String,
    "Key": String
  }
]
```

## Tags properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Key|String|Yes|No|The key of the tag.|The tag key must be 1 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|
|Value|String|No|No|The value of the tag.|The tag value must be 0 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|

## Response parameters

Fn::GetAtt

-   InstanceId: the ID of the instance. The instance ID is a globally unique identifier \(GUID\) generated by the system for the instance.
-   PrivateIp: the private IP address of the VPC-type instance. This parameter takes effect only when the NetworkType parameter is set to VPC.
-   InnerIp: the private IP address of the instance in the classic network. This parameter takes effect only when the NetworkType parameter is set to Classic.
-   PublicIps: the public IP address of the instance in the classic network. This parameter takes effect only when the NetworkType parameter is set to Classic.
-   ZoneId: the ID of the zone.
-   HostName: the hostname of the instance.
-   PrimaryNetworkInterfaceId: the ID of the primary ENI.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
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
    "ResourceGroupId": {
      "Type": "String",
      "Description": "Resource group id."
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
      "Type": "String",
      "Description": "Whether renew the fee automatically? When the parameter InstanceChargeType is PrePaid, it will take effect. Range of value:True: automatic renewal.False: no automatic renewal. Default value is False.",
      "AllowedValues": [
        "True",
        "False"
      ],
      "Default": "False"
    },
    "RamRoleName": {
      "Type": "String",
      "Description": "Instance RAM role name. The name is provided and maintained by Resource Access Management (RAM) and can be queried using ListRoles. For more information, see RAM API CreateRole and ListRoles."
    },
    "SystemDiskPerformanceLevel": {
      "Type": "String",
      "Description": "The performance level of the enhanced SSD used as the system disk.Default value: PL1. Valid values:PL1: A single enhanced SSD delivers up to 50,000 random read/write IOPS.PL2: A single enhanced SSD delivers up to 100,000 random read/write IOPS.PL3: A single enhanced SSD delivers up to 1,000,000 random read/write IOPS."
    },
    "ImageId": {
      "Type": "String",
      "Description": "Image ID to create ecs instance."
    },
    "SystemDiskDiskName": {
      "Type": "String",
      "Description": "Name of created system disk."
    },
    "SpotPriceLimit": {
      "Type": "String",
      "Description": "The hourly price threshold of a instance, and it takes effect only when parameter InstanceChargeType is PostPaid. Three decimals is allowed at most. "
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
    "SpotStrategy": {
      "Type": "String",
      "Description": "The spot strategy of a Pay-As-You-Go instance, and it takes effect only when parameter InstanceChargeType is PostPaid. Value range: \"NoSpot: A regular Pay-As-You-Go instance\", \"SpotWithPriceLimit: A price threshold for a spot instance, \"\"SpotAsPriceGo: A price that is based on the highest Pay-As-You-Go instance. \"Default value: NoSpot.",
      "AllowedValues": [
        "NoSpot",
        "SpotWithPriceLimit",
        "SpotAsPriceGo"
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
      "Type": "String",
      "Description": "The 'optimized' instance can provide better IO performance. Support 'none' and 'optimized' only, default is 'optimized'.",
      "AllowedValues": [
        "none",
        "optimized"
      ],
      "Default": "optimized"
    },
    "ZoneId": {
      "Type": "String",
      "Description": "current zone to create the instance."
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
      "Description": "Prepaid time period. Unit is month, it could be from 1 to 9 or 12, 24, 36, 48, 60. Default value is 1.",
      "AllowedValues": [
        1,
        2,
        3,
        4,
        5,
        6,
        7,
        8,
        9,
        12,
        24,
        36,
        48,
        60
      ],
      "Default": 1
    },
    "DeletionProtection": {
      "Type": "Boolean",
      "Description": "Whether an instance can be released manually through the console or API, deletion protection only support postPaid instance",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "InternetChargeType": {
      "Type": "String",
      "Description": "Instance internet access charge type.Support 'PayByBandwidth' and 'PayByTraffic' only. Default is PayByTraffic",
      "AllowedValues": [
        "PayByBandwidth",
        "PayByTraffic"
      ],
      "Default": "PayByTraffic"
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
    "Instance": {
      "Type": "ALIYUN::ECS::Instance",
      "Properties": {
        "DedicatedHostId": {
          "Ref": "DedicatedHostId"
        },
        "PrivateIpAddress": {
          "Ref": "PrivateIpAddress"
        },
        "Description": {
          "Ref": "Description"
        },
        "ResourceGroupId": {
          "Ref": "ResourceGroupId"
        },
        "DiskMappings": {
          "Ref": "DiskMappings"
        },
        "SystemDiskSize": {
          "Ref": "SystemDiskSize"
        },
        "UserData": {
          "Fn::Join": [
            "",
            [
              "[powershell] \r\n",
              "New-Item -Path \"C:\\Install_dir\" -Force -type directory\r\n",
              "cd C:\\Install_dir \r\n"
            ]
          ]
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
        "RamRoleName": {
          "Ref": "RamRoleName"
        },
        "SystemDiskPerformanceLevel": {
          "Ref": "SystemDiskPerformanceLevel"
        },
        "ImageId": {
          "Ref": "ImageId"
        },
        "SystemDiskDiskName": {
          "Ref": "SystemDiskDiskName"
        },
        "SpotPriceLimit": {
          "Ref": "SpotPriceLimit"
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
        "SpotStrategy": {
          "Ref": "SpotStrategy"
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
        "DeletionProtection": {
          "Ref": "DeletionProtection"
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
        "PeriodUnit": {
          "Ref": "PeriodUnit"
        }
      }
    }
  },
  "Outputs": {
    "PrimaryNetworkInterfaceId": {
      "Description": "Primary network interface id of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "PrimaryNetworkInterfaceId"
        ]
      }
    },
    "InnerIp": {
      "Description": "Inner IP address of the specified instance. Only for classical instance.",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "InnerIp"
        ]
      }
    },
    "ZoneId": {
      "Description": "Zone id of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "ZoneId"
        ]
      }
    },
    "InstanceId": {
      "Description": "The instance id of created ecs instance",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "InstanceId"
        ]
      }
    },
    "PrivateIp": {
      "Description": "Private IP address of created ecs instance. Only for VPC instance.",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "PrivateIp"
        ]
      }
    },
    "PublicIp": {
      "Description": "Public IP address of created ecs instance.",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "PublicIp"
        ]
      }
    },
    "HostName": {
      "Description": "Host name of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "HostName"
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
  ResourceGroupId:
    Type: String
    Description: Resource group id.
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
    Type: String
    Description: >-
      Whether renew the fee automatically? When the parameter InstanceChargeType
      is PrePaid, it will take effect. Range of value:True: automatic
      renewal.False: no automatic renewal. Default value is False.
    AllowedValues:
      - 'True'
      - 'False'
    Default: 'False'
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
      value: PL1. Valid values:PL1: A single enhanced SSD delivers up to 50,000
      random read/write IOPS.PL2: A single enhanced SSD delivers up to 100,000
      random read/write IOPS.PL3: A single enhanced SSD delivers up to 1,000,000
      random read/write IOPS.
  ImageId:
    Type: String
    Description: Image ID to create ecs instance.
  SystemDiskDiskName:
    Type: String
    Description: Name of created system disk.
  SpotPriceLimit:
    Type: String
    Description: >-
      The hourly price threshold of a instance, and it takes effect only when
      parameter InstanceChargeType is PostPaid. Three decimals is allowed at
      most.
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
  SpotStrategy:
    Type: String
    Description: >-
      The spot strategy of a Pay-As-You-Go instance, and it takes effect only
      when parameter InstanceChargeType is PostPaid. Value range: "NoSpot: A
      regular Pay-As-You-Go instance", "SpotWithPriceLimit: A price threshold
      for a spot instance, ""SpotAsPriceGo: A price that is based on the highest
      Pay-As-You-Go instance. "Default value: NoSpot.
    AllowedValues:
      - NoSpot
      - SpotWithPriceLimit
      - SpotAsPriceGo
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
    Type: String
    Description: >-
      The 'optimized' instance can provide better IO performance. Support 'none'
      and 'optimized' only, default is 'optimized'.
    AllowedValues:
      - none
      - optimized
    Default: optimized
  ZoneId:
    Type: String
    Description: current zone to create the instance.
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
      Prepaid time period. Unit is month, it could be from 1 to 9 or 12, 24, 36,
      48, 60. Default value is 1.
    AllowedValues:
      - 1
      - 2
      - 3
      - 4
      - 5
      - 6
      - 7
      - 8
      - 9
      - 12
      - 24
      - 36
      - 48
      - 60
    Default: 1
  DeletionProtection:
    Type: Boolean
    Description: >-
      Whether an instance can be released manually through the console or API,
      deletion protection only support postPaid instance
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
  InternetChargeType:
    Type: String
    Description: >-
      Instance internet access charge type.Support 'PayByBandwidth' and
      'PayByTraffic' only. Default is PayByTraffic
    AllowedValues:
      - PayByBandwidth
      - PayByTraffic
    Default: PayByTraffic
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
  Instance:
    Type: 'ALIYUN::ECS::Instance'
    Properties:
      DedicatedHostId:
        Ref: DedicatedHostId
      PrivateIpAddress:
        Ref: PrivateIpAddress
      Description:
        Ref: Description
      ResourceGroupId:
        Ref: ResourceGroupId
      DiskMappings:
        Ref: DiskMappings
      SystemDiskSize:
        Ref: SystemDiskSize
      UserData:
        'Fn::Join':
          - ''
          - - "[powershell] \r\n"
            - "New-Item -Path \"C:\\Install_dir\" -Force -type directory\r\n"
            - "cd C:\\Install_dir \r\n"
      SystemDiskDescription:
        Ref: SystemDiskDescription
      InstanceChargeType:
        Ref: InstanceChargeType
      AutoRenew:
        Ref: AutoRenew
      RamRoleName:
        Ref: RamRoleName
      SystemDiskPerformanceLevel:
        Ref: SystemDiskPerformanceLevel
      ImageId:
        Ref: ImageId
      SystemDiskDiskName:
        Ref: SystemDiskDiskName
      SpotPriceLimit:
        Ref: SpotPriceLimit
      InstanceType:
        Ref: InstanceType
      AllocatePublicIP:
        Ref: AllocatePublicIP
      Tags:
        Ref: Tags
      HostName:
        Ref: HostName
      SpotStrategy:
        Ref: SpotStrategy
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
      DeletionProtection:
        Ref: DeletionProtection
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
      PeriodUnit:
        Ref: PeriodUnit
Outputs:
  PrimaryNetworkInterfaceId:
    Description: Primary network interface id of created instance.
    Value:
      'Fn::GetAtt':
        - Instance
        - PrimaryNetworkInterfaceId
  InnerIp:
    Description: Inner IP address of the specified instance. Only for classical instance.
    Value:
      'Fn::GetAtt':
        - Instance
        - InnerIp
  ZoneId:
    Description: Zone id of created instance.
    Value:
      'Fn::GetAtt':
        - Instance
        - ZoneId
  InstanceId:
    Description: The instance id of created ecs instance
    Value:
      'Fn::GetAtt':
        - Instance
        - InstanceId
  PrivateIp:
    Description: Private IP address of created ecs instance. Only for VPC instance.
    Value:
      'Fn::GetAtt':
        - Instance
        - PrivateIp
  PublicIp:
    Description: Public IP address of created ecs instance.
    Value:
      'Fn::GetAtt':
        - Instance
        - PublicIp
  HostName:
    Description: Host name of created instance.
    Value:
      'Fn::GetAtt':
        - Instance
        - HostName
```

