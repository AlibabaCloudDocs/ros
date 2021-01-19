# ALIYUN::ECS::InstanceGroupClone

ALIYUN::ECS::InstanceGroupClone is used to clone an ECS instance group.

## Syntax

```
{
  "Type": "ALIYUN::ECS::InstanceGroupClone",
  "Properties": {
    "BackendServerWeight": Integer,
    "SystemDiskAutoSnapshotPolicyId": String,
    "DiskMappings": List,
    "Period": Number,
    "LaunchTemplateName": String,
    "RamRoleName": String,
    "ResourceGroupId": String,
    "KeyPairName": String,
    "SystemDiskDiskName": String,
    "PeriodUnit": String,
    "Description": String,
    "Tags": List,
    "AutoRenewPeriod": Number,
    "ImageId": String,
    "AutoRenew": String,
    "SpotStrategy": String,
    "SourceInstanceId": String,
    "EniMappings": List,
    "Password": String,
    "PasswordInherit": Boolean,
    "MaxAmount": Integer,
    "AutoReleaseTime": String,
    "SystemDiskCategory": String,
    "LoadBalancerIdToAttach": String,
    "LaunchTemplateId": String,
    "LaunchTemplateVersion": String,
    "ZoneId": String,
    "InternetMaxBandwidthOut": Integer,
    "InstanceName": String,
    "InternetMaxBandwidthIn": Integer,
    "DeletionProtection": Boolean,
    "DeploymentSetId": String,
    "Ipv6AddressCount": Integer,
    "SecurityGroupId": String,
    "SecurityGroupIds": List,
    "SpotPriceLimit": String,
    "HpcClusterId": String,
    "SystemDiskDescription": String,
    "Ipv6Addresses": List
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ResourceGroupId|String|No|No|The ID of the enterprise resource group to which the created instances belong.|None|
|HpcClusterId|String|No|Yes|The ID of the E-HPC cluster to which the created instances belong.|None|
|SourceInstanceId|String|Yes|No|The ID of the source ECS instance to be cloned.|The clone operation clones the specified instance, including its instance type, image, billing method for network usage, bandwidth limit, and network type. If the source ECS instance belongs to multiple security groups, the cloned instance is added only to the first of these security groups.|
|MaxAmount|Integer|Yes|Yes|The maximum number of ECS instances that can be created at a time.|Valid values: 1 to 100.|
|BackendServerWeight|Integer|No|No|The weight assigned to the created ECS instances in the SLB instance.|Valid values: 0 to 100. Default value: 100. |
|LoadBalancerIdToAttach|String|No|No|The ID of the SLB instance to which you want to attach the created ECS instances.|None|
|Description|String|No|Yes|The description of the created instances.|The description can be up to 256 characters in length.|
|ImageId|String|No|Yes|The ID of the image used to start the created ECS instances. You can use a public image, a custom image, or an Alibaba Cloud Marketplace image.|You can specify a partial public image ID instead of providing the complete ID. Example: -   If you enter ubuntu, the system matches it with the following ID: ubuntu16\_0402\_64\_20G\_alibase\_20170818.vhd
-   If you enter ubuntu\_14, the system matches it with the following ID: ubuntu\_14\_0405\_64\_20G\_alibase\_20170824.vhd
-   If you enter ubuntu\*14\*32, the system matches it with the following ID: ubuntu\_14\_0405\_32\_40G\_alibase\_20170711.vhd
-   If you enter ubuntu\_16\_0402\_32, the system matches it with the following ID: ubuntu\_16\_0402\_32\_40G\_alibase\_20170711.vhd |
|InternetMaxBandwidthOut|Integer|No|No|The maximum outbound public bandwidth.|Unit: Mbit/s. -   Valid values for the PayByBandwidth mode: 0 to 200.
-   Valid values for the PayByTraffic mode: 1 to 200. |
|SecurityGroupId|String|No|No|The ID of the security group to which the created instances belong.|You cannot specify both SecurityGroupId and SecurityGroupIds.|
|SecurityGroupIds|List|No|No|The IDs of multiple security groups to which the created ECS instances belong. For information about the quota for security groups to which an ECS instance can belong, see [Security group limits](/intl.en-US/Product Introduction/Limits.md).|You cannot specify both SecurityGroupId and SecurityGroupIds.|
|InstanceName|String|No|No|The names of the created ECS instances.|The name can be up to 128 characters in length and can contain letters, digits, underscores \(\_\), periods \(.\), and hyphens \(-\).|
|Password|String|No|Yes|The password that is used to log on to the created ECS instances.|The password must be 8 to 30 characters in length and must contain at least one letter, digit, and special character at the same time. Special characters include ```
( ) ~ ! @ # $ % ^ & * - + = | { } [ ] : ; ' < > , . ? / -
```

If you specify this parameter in the API request, use HTTPS to secure the API and protect your password.|
|PasswordInherit|Boolean|No|No|Specifies whether to use the password preset in the image.|Valid values:-   true
-   false

**Note:** To use the PasswordInherit parameter, the Password parameter must be empty and you must make sure that the selected image has a password configured. |
|DiskMappings|List|No|Yes|The disks to be attached to the created ECS instances.|A maximum of 16 disks can be attached to each instance. For more information, see [DiskMappings properties](#section_1an_6zh_or9). |
|Period|Number|No|Yes|The billing cycle.|Valid values: 1, 2, 3, 4, 5, 6, 7, 8, 9, 12, 24, and 36. Unit: months.

This parameter is required when InstanceChargeType is set to PrePaid. This parameter is optional when InstanceChargeType is set to PostPaid.|
|Tags|List|No|Yes|The custom tags of the created instances.|A maximum of 20 tags can be specified in the `[{"Key": "tagKey", "Value": "tagValue"},{"Key": "tagKey2", "Value": "tagValue2"}]` format. For more information, see [Tags properties](#section_4pe_ycf_0op). |
|ZoneId|String|No|No|The ID of the zone.|None|
|KeyPairName|String|No|Yes|The name of the key pair that is used to connect to the created ECS instances.|For Windows instances, this parameter is ignored. For Linux instances, the Password parameter still takes effect if this parameter is specified. However, logon by password is disabled, and the value of this parameter is used.|
|RamRoleName|String|No|Yes|The RAM role name of the created instances.|You can call the ListRoles operation to query the RAM role name. For more information, see [CreateRole](/intl.en-US/API Reference/API Reference (RAM)/Role management APIs/CreateRole.md) and [ListRoles](/intl.en-US/API Reference/API Reference (RAM)/Role management APIs/ListRoles.md).|
|SpotPriceLimit|String|No|No|The maximum hourly price of the instance.|Three decimal places are allowed at most. This parameter takes effect only when the SpotStrategy parameter is set to SpotWithPriceLimit.|
|SpotStrategy|String|No|No|The bidding policy for pay-as-you-go instances.|This parameter takes effect only when the InstanceChargeType parameter is set to PostPaid. Default value: NoSpot. Valid values:

-   NoSpot: applies to regular pay-as-you-go instances.
-   SpotWithPriceLimit: applies to preemptible instances with a maximum hourly price.
-   SpotAsPriceGo: applies to pay-as-you-go instances priced at the market price at the time of purchase. |
|SystemDiskDiskName|String|No|Yes|The name of the system disk.|The name must be 2 to 128 characters in length and can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with `http://` or `https://`.|
|PeriodUnit|String|No|Yes|The unit of billing cycle for the created ECS instances.|Default value: Month. Valid values: -   Week

Valid values for the Period parameter when this parameter is set to Week: 1, 2, 3, and 4. Valid values for the AutoRenewPeriod parameter when this parameter is set to Week: 1, 2, and 3.

-   Month

Valid values for the Period parameter when this parameter is set to Month: 1, 2, 3, 4, 5, 6, 7, 8, 9, 12, 24, 36, 48, and 60. Valid values for the AutoRenewPeriod parameter when this parameter is set to Month: 1, 2, 3, 6, and 12. |
|AutoRenewPeriod|Number|No|Yes|The auto-renewal period for the created instances.|This parameter is required when the AutoRenew parameter is set to True. Default value: 1. Valid values:

-   1
-   2
-   3
-   6
-   12 |
|AutoRenew|String|No|Yes|Specifies whether to enable auto-renewal for the created instances.|Default value: False. Valid values: -   True: enables auto-renewal for the created instances.
-   False: disables auto-renewal for the created instances.

This parameter is required when the InstanceChargeType parameter is set to PrePaid.|
|EniMappings|List|No|Yes|The elastic network interfaces \(ENIs\) to be attached to the created ECS instances.|Only one ENI can be attached to each instance. For more information, see [EniMappings properties](#section_4pe_ycf_0rp). |
|AutoReleaseTime|String|No|No|The time scheduled for the created ECS instances to be automatically released.|Specify the time in the ISO 8601 standard in the `yyyy-MM-ddTHH:mm:ssZ` format. The maximum release time must be within three years from the current time.|
|SystemDiskCategory|String|No|Yes|The type of the system disk.|Valid values: -   cloud
-   cloud\_efficiency
-   cloud\_ssd
-   cloud\_essd |
|LaunchTemplateName|String|No|Yes|The name of the launch template.|None|
|LaunchTemplateVersion|String|No|Yes|The version of the launch template.|If you do not specify a version, the default version is used.|
|InternetMaxBandwidthIn|Integer|No|No|The maximum inbound public bandwidth.|Unit: Mbit/s. Valid values: 1 to 100.

Default value: 100.|
|LaunchTemplateId|String|No|Yes|The ID of the launch template.|None|
|SystemDiskDescription|String|No|Yes|The description of the system disk.|None|
|DeletionProtection|Boolean|No|No|The deletion protection properties of the ECS instances. It specifies whether the instances can be released by using the ECS console or the [DeleteInstance](/intl.en-US/API Reference/Instances/DeleteInstance.md) operation.|Valid values: -   true
-   false |
|DeploymentSetId|String|No|Yes|The ID of the deployment set.|None|
|Ipv6AddressCount|Integer|No|Yes|The number of randomly generated IPv6 addresses that are allocated to the ENI.|You can specify one of the Ipv6Addresses and Ipv6AddressCount parameters, but you cannot specify both of them.|
|Ipv6Addresses|List|No|Yes|The list of IPv6 addresses allocated to the ENI.|The list can contain only one IPv6 address. Property modification does not affect existing instances. You can specify one of the Ipv6Addresses and Ipv6AddressCount parameters, but you cannot specify both of them.|
|SystemDiskAutoSnapshotPolicyId|String|No|Yes|The ID of the automatic snapshot policy for the system disk.|None|

## DiskMappings syntax

```
"DiskMappings": [
  {
    "Category": String,
    "DiskName": String,
    "Description": String,
    "Encrypted": String,
    "KMSKeyId": String,
    "Device": String,
    "SnapshotId": String,
    "Size": String,
    "PerformanceLevel": String,
    "AutoSnapshotPolicyId": String
  }
]
```

## DiskMappings properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Size|String|Yes|No|The size of the data disk.|Unit: GB.|
|Category|String|No|No|The type of the data disk.|Default value: cloud. Valid values: -   cloud: basic disk
-   cloud\_ssd: standard SSD
-   cloud\_essd: enhanced SSD \(ESSD\)
-   cloud\_efficiency: ultra disk |
|DiskName|String|No|No|The name of the data disk.|The name can be up to 128 characters in length and can contain letters, digits, underscores \(\_\), periods \(.\), and hyphens \(-\).|
|Description|String|No|No|The description of the data disk.|The description must be 2 to 256 characters in length. It cannot start with `http://` or `https://`.|
|Device|String|No|No|The device name of the data disk.|The system allocates a device name in alphabetical order. Example: `/dev/xvd[a-z]`.|
|SnapshotId|String|No|No|The ID of the snapshot.|None|
|Encrypted|String|No|No|Specifies whether to encrypt the data disk.|Default value: false. Valid values: -   true
-   false |
|KMSKeyId|String|No|No|The ID of the KMS key corresponding to the data disk.|None|
|AutoSnapshotPolicyId|String|No|No|The ID of the automatic snapshot policy.|None|
|PerformanceLevel|String|No|No|The performance level of the ESSD that is used as the system disk.|Default value: PL1. Valid values:-   PL1: A single ESSD delivers up to 50,000 random read/write IOPS.
-   PL2: A single ESSD delivers up to 100,000 random read/write IOPS.
-   PL3: A single ESSD delivers up to 1,000,000 random read/write IOPS.

For more information about performance levels of ESSDs, see [Enhanced SSDs](/intl.en-US/Block Storage/Block Storage overview/Enhanced SSDs.md).|

## EniMappings syntax

```
"EniMappings": [
  {
    "SecurityGroupId": String,
    "VSwitchId": String,
    "Description": String,
    "NetworkInterfaceName": String,
    "PrimaryIpAddress": String
  }
]
```

## EniMappings properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|SecurityGroupId|String|Yes|Yes|The ID of the security group to which the ENI belongs.|None|
|VSwitchId|String|Yes|No|The ID of the VSwitch to which the ENI belongs.|None|
|Description|String|No|Yes|The description of the ENI.|The description must be 2 to 256 characters in length. It cannot start with `http://` or `https://`.|
|NetworkInterfaceName|String|No|Yes|The name of the ENI.|None|
|PrimaryIpAddress|String|No|No|The primary IP address of the ENI.|None|

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

-   InstanceIds: the IDs of the created instances in the ECS instance group. An ID is a system-generated globally unique identifier \(GUID\) for an instance.
-   PrivateIps: the list of private IP addresses of instances in a VPC. This parameter takes effect only when the NetworkType parameter is set to VPC. The list is a JSON array that contains up to 100 IP addresses separated with commas \(,\). Example: \["172.16.XX.XX", "172.16. XX.XX", ... "172.16. XX.XX"\].
-   InnerIps: the list of private IP addresses of instances in the classic network. This parameter takes effect only when the NetworkType parameter is set to Classic. The list is a JSON array that contains up to 100 IP addresses separated with commas \(,\). Example: \["10.1.XX.XX", "10.1. XX.XX", ... "10.1. XX.XX"\].
-   PublicIps: the list of public IP addresses of instances in the classic network. This parameter takes effect only when the NetworkType parameter is set to Classic. The list is a JSON array that contains up to 100 IP addresses separated with commas \(,\). Example: \["42.1.XX.XX", "42.1. XX.XX", ... "42.1. XX.XX"\].
-   HostNames: the list of hostnames of all instances.
-   OrderId: the order IDs of all instances.
-   ZoneIds: the IDs of the zones.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Description": {
      "Type": "String",
      "Description": "Description of the instance, [2, 256] characters. Do not fill or empty, the default is empty. Old instances will not be changed."
    },
    "DiskMappings": {
      "Type": "Json",
      "Description": "Disk mappings to attach to instance. Max support 16 disks.\nIf the image contains a data disk, you can specify other parameters of the data disk via the same value of parameter \"Device\". If parameter \"Category\" is not specified, it will be cloud_efficiency instead of \"Category\" of data disk in the image. Old instances will not be changed.",
      "MaxLength": 16
    },
    "ResourceGroupId": {
      "Type": "String",
      "Description": "Resource group id."
    },
    "SystemDiskDescription": {
      "Type": "String",
      "Description": "Description of created system disk. Old instances will not be changed."
    },
    "AutoRenew": {
      "Type": "String",
      "Description": "Whether renew the fee automatically? When the parameter InstanceChargeType is PrePaid, it will take effect. Range of value:True: automatic renewal.False: no automatic renewal. Default value is False. Old instances will not be changed.",
      "AllowedValues": [
        "True",
        "False"
      ],
      "Default": "False"
    },
    "Ipv6Addresses": {
      "Type": "CommaDelimitedList",
      "Description": "Specify one or more IPv6 addresses for the elastic NIC. Currently, the maximum list size is 1. Example value: 2001:db8:1234:1a00::*** .\nNote You cannot specify the parameters Ipv6Addresses and Ipv6AddressCount at the same time.\nThe change of the property does not affect existing instances.",
      "MaxLength": 1
    },
    "SourceInstanceId": {
      "Type": "String",
      "Description": "Source ecs instance used to copy properties to clone new ecs instance. It will copy the InstanceType, ImageId, InternetChargeType, InternetMaxBandwidthIn, InternetMaxBandwidthOut and the system disk and data disk configurations. If the instance network is VPC, it will also clone the relative properties. If specified instance with more than one security group, it will use the first security group to create instance. you can also specify the SecurityGroupId to override it."
    },
    "MaxAmount": {
      "Type": "Number",
      "Description": "Max number of instances to create, should be bigger than 'MinAmount' and smaller than 1000.",
      "MinValue": 0,
      "MaxValue": 1000
    },
    "SystemDiskAutoSnapshotPolicyId": {
      "Type": "String",
      "Description": "Auto snapshot policy ID."
    },
    "RamRoleName": {
      "Type": "String",
      "Description": "Instance RAM role name. The name is provided and maintained by Resource Access Management (RAM) and can be queried using ListRoles. For more information, see RAM API CreateRole and ListRoles."
    },
    "Ipv6AddressCount": {
      "Type": "Number",
      "Description": "Specifies the number of randomly generated IPv6 addresses for the elastic NIC.\nNote You cannot specify the parameters Ipv6Addresses and Ipv6AddressCount at the same time.\nThe change of the property does not affect existing instances.",
      "MinValue": 0
    },
    "ImageId": {
      "Type": "String",
      "Description": "Image ID to create ecs instance."
    },
    "SystemDiskDiskName": {
      "Type": "String",
      "Description": "Name of created system disk. Old instances will not be changed."
    },
    "SpotPriceLimit": {
      "Type": "String",
      "Description": "The hourly price threshold of a instance, and it takes effect only when parameter InstanceChargeType is PostPaid. Three decimals is allowed at most. "
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to instance. Max support 20 tags to add during create instance. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
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
      "Description": "The time period of auto renew. When the parameter InstanceChargeType is PrePaid, it will take effect. It could be 1, 2, 3, 6, 12. Default value is 1. Old instances will not be changed.",
      "AllowedValues": [
        1,
        2,
        3,
        6,
        12
      ],
      "Default": 1
    },
    "BackendServerWeight": {
      "Type": "Number",
      "Description": "The weight of backend server of load balancer. From 0 to 100, 0 means offline. Default is 100.",
      "MinValue": 0,
      "MaxValue": 100,
      "Default": 100
    },
    "KeyPairName": {
      "Type": "String",
      "Description": "SSH key pair name. Old instances will not be changed."
    },
    "LaunchTemplateName": {
      "Type": "String",
      "Description": "Name of launch template. Launch template id or name must be specified to use launch template"
    },
    "ZoneId": {
      "Type": "String",
      "Description": "current zone to create the instance."
    },
    "HpcClusterId": {
      "Type": "String",
      "Description": "The HPC cluster ID to which the instance belongs.The change of the property does not affect existing instances."
    },
    "SecurityGroupId": {
      "Type": "String",
      "Description": "Security group to create ecs instance. For classic instance need the security group not belong to VPC, for VPC instance, please make sure the security group belong to specified VPC."
    },
    "Period": {
      "Type": "Number",
      "Description": "Prepaid time period. Unit is month, it could be from 1 to 9 or 12, 24, 36, 48, 60. Default value is 1. Old instances will not be changed.",
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
    "LaunchTemplateId": {
      "Type": "String",
      "Description": "ID of launch template. Launch template id or name must be specified to use launch template"
    },
    "DeletionProtection": {
      "Type": "Boolean",
      "Description": "Whether an instance can be released manually through the console or API, deletion protection only support postPaid instance ",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "SecurityGroupIds": {
      "Type": "CommaDelimitedList",
      "Description": "The IDs of security groups N to which the instance belongs. The valid values of N are based on the maximum number of security groups to which an instance can belong. For more information, see Security group limits.Note: You cannot specify both SecurityGroupId and SecurityGroupIds at the same time."
    },
    "LoadBalancerIdToAttach": {
      "Type": "String",
      "Description": "After the instance is created. Automatic attach it to the load balancer."
    },
    "SystemDiskCategory": {
      "Type": "String",
      "Description": "Category of system disk. Default is cloud_efficiency. support cloud|cloud_efficiency|cloud_ssd|cloud_essd|ephemeral_ssd. Old instances will not be changed.",
      "AllowedValues": [
        "cloud",
        "cloud_efficiency",
        "cloud_ssd",
        "cloud_essd",
        "ephemeral_ssd"
      ],
      "Default": "cloud_efficiency"
    },
    "EniMappings": {
      "Type": "Json",
      "Description": "NetworkInterface to attach to instance. Max support 1 ENI.",
      "MaxLength": 1
    },
    "InstanceName": {
      "Type": "String",
      "Description": "Display name of the instance, [2, 128] English or Chinese characters, must start with a letter or Chinese in size, can contain numbers, '_' or '.', '-'. \nSupport to use the regular expression to set the different instance name for each ECS instance. InstanceName could be specified as 'name_prefix[begin_number,bits]name_suffix', such as 'testinstance[123,4]tail'. If you creates 3 instances with the instance name 'testinstance[123,4]tail', all the instances' names are testinstance0123tail, testinstance0124tail, testinstance0125tail. \nThe 'name_prefix[begin_number,bits]name_suffix' should follow those rules: \n1. 'name_prefix' is required. \n2. 'name_suffix' is optional. \n3. The name regular expression can't include any spaces. \n4. The 'bits' must be in range [1, 6]. \n5. The 'begin_number' must be in range [0, 999999]. \n6. You could only specify 'begin_number'. The 'bits' will be set as 6 by default. \n7. You also could only specify the [] or [,]. The 'begin_number' will be set as 0 by default, the 'bits' will be set as 6 by default. \n8. If the bits of 'begin_number' is less than the 'bits' you specified, like [1234,1], the 'bits' will be set as 6 by default."
    },
    "DeploymentSetId": {
      "Type": "String",
      "Description": "Deployment set ID. The change of the property does not affect existing instances."
    },
    "InternetMaxBandwidthOut": {
      "Type": "Number",
      "Description": "Set internet output bandwidth of instance. Unit is Mbps(Mega bit per second). Range is [0,200]. Default is 1.While the property is not 0, public ip will be assigned for instance.",
      "MinValue": 0,
      "MaxValue": 200
    },
    "InternetMaxBandwidthIn": {
      "Type": "Number",
      "Description": "Max internet out band width setting, unit in Mbps(Mega bit per second). The range is [1,200], default is 200 Mbps.",
      "MinValue": 1,
      "MaxValue": 200,
      "Default": 200
    },
    "LaunchTemplateVersion": {
      "Type": "String",
      "Description": "Version of launch template. Default version is used if version is not specified.",
      "AllowedPattern": "^[1-9]\\d*$"
    },
    "PeriodUnit": {
      "Type": "String",
      "Description": "Unit of prepaid time period, it could be Week/Month. Default value is Month. Old instances will not be changed.",
      "AllowedValues": [
        "Week",
        "Month"
      ],
      "Default": "Month"
    },
    "AutoReleaseTime": {
      "Type": "String",
      "Description": "Auto release time for created instance, Follow ISO8601 standard using UTC time. format is 'yyyy-MM-ddTHH:mm:ssZ'. Not bigger than 3 years from this day onwards"
    }
  },
  "Resources": {
    "InstanceGroupClone": {
      "Type": "ALIYUN::ECS::InstanceGroupClone",
      "Properties": {
        "Description": {
          "Ref": "Description"
        },
        "DiskMappings": {
          "Ref": "DiskMappings"
        },
        "ResourceGroupId": {
          "Ref": "ResourceGroupId"
        },
        "SystemDiskDescription": {
          "Ref": "SystemDiskDescription"
        },
        "AutoRenew": {
          "Ref": "AutoRenew"
        },
        "Ipv6Addresses": {
          "Ref": "Ipv6Addresses"
        },
        "SourceInstanceId": {
          "Ref": "SourceInstanceId"
        },
        "MaxAmount": {
          "Ref": "MaxAmount"
        },
        "SystemDiskAutoSnapshotPolicyId": {
          "Ref": "SystemDiskAutoSnapshotPolicyId"
        },
        "RamRoleName": {
          "Ref": "RamRoleName"
        },
        "Ipv6AddressCount": {
          "Ref": "Ipv6AddressCount"
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
        "Tags": {
          "Ref": "Tags"
        },
        "SpotStrategy": {
          "Ref": "SpotStrategy"
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
        "BackendServerWeight": {
          "Ref": "BackendServerWeight"
        },
        "KeyPairName": {
          "Ref": "KeyPairName"
        },
        "LaunchTemplateName": {
          "Ref": "LaunchTemplateName"
        },
        "ZoneId": {
          "Ref": "ZoneId"
        },
        "HpcClusterId": {
          "Ref": "HpcClusterId"
        },
        "SecurityGroupId": {
          "Ref": "SecurityGroupId"
        },
        "Period": {
          "Ref": "Period"
        },
        "LaunchTemplateId": {
          "Ref": "LaunchTemplateId"
        },
        "DeletionProtection": {
          "Ref": "DeletionProtection"
        },
        "SecurityGroupIds": {
          "Ref": "SecurityGroupIds"
        },
        "LoadBalancerIdToAttach": {
          "Ref": "LoadBalancerIdToAttach"
        },
        "SystemDiskCategory": {
          "Ref": "SystemDiskCategory"
        },
        "EniMappings": {
          "Ref": "EniMappings"
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
        },
        "LaunchTemplateVersion": {
          "Ref": "LaunchTemplateVersion"
        },
        "PeriodUnit": {
          "Ref": "PeriodUnit"
        },
        "AutoReleaseTime": {
          "Ref": "AutoReleaseTime"
        }
      }
    }
  },
  "Outputs": {
    "PublicIps": {
      "Description": "Public IP address list of created ecs instance.",
      "Value": {
        "Fn::GetAtt": [
          "InstanceGroupClone",
          "PublicIps"
        ]
      }
    },
    "PrivateIps": {
      "Description": "Private IP address list of created ecs instance. Only for VPC instance.",
      "Value": {
        "Fn::GetAtt": [
          "InstanceGroupClone",
          "PrivateIps"
        ]
      }
    },
    "HostNames": {
      "Description": "Host names of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "InstanceGroupClone",
          "HostNames"
        ]
      }
    },
    "InnerIps": {
      "Description": "Inner IP address list of the specified instance. Only for classical instance.",
      "Value": {
        "Fn::GetAtt": [
          "InstanceGroupClone",
          "InnerIps"
        ]
      }
    },
    "ZoneIds": {
      "Description": "Zone id of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "InstanceGroupClone",
          "ZoneIds"
        ]
      }
    },
    "OrderId": {
      "Description": "The order id list of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "InstanceGroupClone",
          "OrderId"
        ]
      }
    },
    "InstanceIds": {
      "Description": "The instance id list of created ecs instance",
      "Value": {
        "Fn::GetAtt": [
          "InstanceGroupClone",
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
  Description:
    Type: String
    Description: >-
      Description of the instance, [2, 256] characters. Do not fill or empty,
      the default is empty. Old instances will not be changed.
  DiskMappings:
    Type: Json
    Description: >-
      Disk mappings to attach to instance. Max support 16 disks.

      If the image contains a data disk, you can specify other parameters of the
      data disk via the same value of parameter "Device". If parameter
      "Category" is not specified, it will be cloud_efficiency instead of
      "Category" of data disk in the image. Old instances will not be changed.
    MaxLength: 16
  ResourceGroupId:
    Type: String
    Description: Resource group id.
  SystemDiskDescription:
    Type: String
    Description: Description of created system disk. Old instances will not be changed.
  AutoRenew:
    Type: String
    Description: >-
      Whether renew the fee automatically? When the parameter InstanceChargeType
      is PrePaid, it will take effect. Range of value:True: automatic
      renewal.False: no automatic renewal. Default value is False.Old instances
      will not be changed.
    AllowedValues:
      - 'True'
      - 'False'
    Default: 'False'
  Ipv6Addresses:
    Type: CommaDelimitedList
    Description: >-
      Specify one or more IPv6 addresses for the elastic NIC. Currently, the
      maximum list size is 1. Example value: 2001:db8:1234:1a00::*** .

      Note You cannot specify the parameters Ipv6Addresses and Ipv6AddressCount
      at the same time.

      The change of the property does not affect existing instances.
    MaxLength: 1
  SourceInstanceId:
    Type: String
    Description: >-
      Source ecs instance used to copy properties to clone new ecs instance. It
      will copy the InstanceType, ImageId, InternetChargeType,
      InternetMaxBandwidthIn, InternetMaxBandwidthOut and the system disk and
      data disk configurations. If the instance network is VPC, it will also
      clone the relative properties. If specified instance with more than one
      security group, it will use the first security group to create instance.
      you can also specify the SecurityGroupId to override it.
  MaxAmount:
    Type: Number
    Description: >-
      Max number of instances to create, should be bigger than 'MinAmount' and
      smaller than 1000.
    MinValue: 0
    MaxValue: 1000
  SystemDiskAutoSnapshotPolicyId:
    Type: String
    Description: Auto snapshot policy ID.
  RamRoleName:
    Type: String
    Description: >-
      Instance RAM role name. The name is provided and maintained by Resource
      Access Management (RAM) and can be queried using ListRoles. For more
      information, see RAM API CreateRole and ListRoles.
  Ipv6AddressCount:
    Type: Number
    Description: >-
      Specifies the number of randomly generated IPv6 addresses for the elastic
      NIC.

      Note You cannot specify the parameters Ipv6Addresses and Ipv6AddressCount
      at the same time.

      The change of the property does not affect existing instances.
    MinValue: 0
  ImageId:
    Type: String
    Description: Image ID to create ecs instance.
  SystemDiskDiskName:
    Type: String
    Description: Name of created system disk. Old instances will not be changed.
  SpotPriceLimit:
    Type: String
    Description: >-
      The hourly price threshold of a instance, and it takes effect only when
      parameter InstanceChargeType is PostPaid. Three decimals is allowed at
      most.
  Tags:
    Type: Json
    Description: >-
      Tags to attach to instance. Max support 20 tags to add during create
      instance. Each tag with two properties Key and Value, and Key is required.
    MaxLength: 20
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
      PrePaid, it will take effect. It could be 1, 2, 3, 6, 12. Default value is
      1. Old instances will not be changed.
    AllowedValues:
      - 1
      - 2
      - 3
      - 6
      - 12
    Default: 1
  BackendServerWeight:
    Type: Number
    Description: >-
      The weight of backend server of load balancer. From 0 to 100, 0 means
      offline. Default is 100.
    MinValue: 0
    MaxValue: 100
    Default: 100
  KeyPairName:
    Type: String
    Description: SSH key pair name. Old instances will not be changed.
  LaunchTemplateName:
    Type: String
    Description: >-
      Name of launch template. Launch template id or name must be specified to
      use launch template
  ZoneId:
    Type: String
    Description: current zone to create the instance.
  HpcClusterId:
    Type: String
    Description: >-
      The HPC cluster ID to which the instance belongs.The change of the
      property does not affect existing instances.
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
      48, 60. Default value is 1. Old instances will not be changed.
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
  LaunchTemplateId:
    Type: String
    Description: >-
      ID of launch template. Launch template id or name must be specified to use
      launch template
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
  SecurityGroupIds:
    Type: CommaDelimitedList
    Description: >-
      The IDs of security groups N to which the instance belongs. The valid
      values of N are based on the maximum number of security groups to which an
      instance can belong. For more information, see Security group limits.Note:
      You cannot specify both SecurityGroupId and SecurityGroupIds at the same
      time.
  LoadBalancerIdToAttach:
    Type: String
    Description: After the instance is created. Automatic attach it to the load balancer.
  SystemDiskCategory:
    Type: String
    Description: >-
      Category of system disk. Default is cloud_efficiency. support
      cloud|cloud_efficiency|cloud_ssd|cloud_essd|ephemeral_ssd.Old instances
      will not be changed.
    AllowedValues:
      - cloud
      - cloud_efficiency
      - cloud_ssd
      - cloud_essd
      - ephemeral_ssd
    Default: cloud_efficiency
  EniMappings:
    Type: Json
    Description: NetworkInterface to attach to instance. Max support 1 ENI.
    MaxLength: 1
  InstanceName:
    Type: String
    Description: >-
      Display name of the instance, [2, 128] English or Chinese characters, must
      start with a letter or Chinese in size, can contain numbers, '_' or '.',
      '-'.

      Support to use the regular expression to set the different instance name
      for each ECS instance. InstanceName could be specified as
      'name_prefix[begin_number,bits]name_suffix', such as
      'testinstance[123,4]tail'. If you creates 3 instances with the instance
      name 'testinstance[123,4]tail', all the instances' names are
      testinstance0123tail, testinstance0124tail, testinstance0125tail.

      The 'name_prefix[begin_number,bits]name_suffix' should follow those
      rules:

      1. 'name_prefix' is required.

      2. 'name_suffix' is optional.

      3. The name regular expression can't include any spaces.

      4. The 'bits' must be in range [1, 6].

      5. The 'begin_number' must be in range [0, 999999].

      6. You could only specify 'begin_number'. The 'bits' will be set as 6 by
      default.

      7. You also could only specify the [] or [,]. The 'begin_number' will be
      set as 0 by default, the 'bits' will be set as 6 by default.

      8. If the bits of 'begin_number' is less than the 'bits' you specified,
      like [1234,1], the 'bits' will be set as 6 by default.
  DeploymentSetId:
    Type: String
    Description: >-
      Deployment set ID. The change of the property does not affect existing
      instances.
  InternetMaxBandwidthOut:
    Type: Number
    Description: >-
      Set internet output bandwidth of instance. Unit is Mbps(Mega bit per
      second). Range is [0,200]. Default is 1.While the property is not 0,
      public ip will be assigned for instance.
    MinValue: 0
    MaxValue: 200
  InternetMaxBandwidthIn:
    Type: Number
    Description: >-
      Max internet out band width setting, unit in Mbps(Mega bit per second).
      The range is [1,200], default is 200 Mbps.
    MinValue: 1
    MaxValue: 200
    Default: 200
  LaunchTemplateVersion:
    Type: String
    Description: >-
      Version of launch template. Default version is used if version is not
      specified.
    AllowedPattern: '^[1-9]\d*$'
  PeriodUnit:
    Type: String
    Description: >-
      Unit of prepaid time period, it could be Week/Month. Default value is
      Month. Old instances will not be changed.
    AllowedValues:
      - Week
      - Month
    Default: Month
  AutoReleaseTime:
    Type: String
    Description: >-
      Auto release time for created instance, Follow ISO8601 standard using UTC
      time. format is 'yyyy-MM-ddTHH:mm:ssZ'. Not bigger than 3 years from this
      day onwards
Resources:
  InstanceGroupClone:
    Type: 'ALIYUN::ECS::InstanceGroupClone'
    Properties:
      Description:
        Ref: Description
      DiskMappings:
        Ref: DiskMappings
      ResourceGroupId:
        Ref: ResourceGroupId
      SystemDiskDescription:
        Ref: SystemDiskDescription
      AutoRenew:
        Ref: AutoRenew
      Ipv6Addresses:
        Ref: Ipv6Addresses
      SourceInstanceId:
        Ref: SourceInstanceId
      MaxAmount:
        Ref: MaxAmount
      SystemDiskAutoSnapshotPolicyId:
        Ref: SystemDiskAutoSnapshotPolicyId
      RamRoleName:
        Ref: RamRoleName
      Ipv6AddressCount:
        Ref: Ipv6AddressCount
      ImageId:
        Ref: ImageId
      SystemDiskDiskName:
        Ref: SystemDiskDiskName
      SpotPriceLimit:
        Ref: SpotPriceLimit
      Tags:
        Ref: Tags
      SpotStrategy:
        Ref: SpotStrategy
      PasswordInherit:
        Ref: PasswordInherit
      Password:
        Ref: Password
      AutoRenewPeriod:
        Ref: AutoRenewPeriod
      BackendServerWeight:
        Ref: BackendServerWeight
      KeyPairName:
        Ref: KeyPairName
      LaunchTemplateName:
        Ref: LaunchTemplateName
      ZoneId:
        Ref: ZoneId
      HpcClusterId:
        Ref: HpcClusterId
      SecurityGroupId:
        Ref: SecurityGroupId
      Period:
        Ref: Period
      LaunchTemplateId:
        Ref: LaunchTemplateId
      DeletionProtection:
        Ref: DeletionProtection
      SecurityGroupIds:
        Ref: SecurityGroupIds
      LoadBalancerIdToAttach:
        Ref: LoadBalancerIdToAttach
      SystemDiskCategory:
        Ref: SystemDiskCategory
      EniMappings:
        Ref: EniMappings
      InstanceName:
        Ref: InstanceName
      DeploymentSetId:
        Ref: DeploymentSetId
      InternetMaxBandwidthOut:
        Ref: InternetMaxBandwidthOut
      InternetMaxBandwidthIn:
        Ref: InternetMaxBandwidthIn
      LaunchTemplateVersion:
        Ref: LaunchTemplateVersion
      PeriodUnit:
        Ref: PeriodUnit
      AutoReleaseTime:
        Ref: AutoReleaseTime
Outputs:
  PublicIps:
    Description: Public IP address list of created ecs instance.
    Value:
      'Fn::GetAtt':
        - InstanceGroupClone
        - PublicIps
  PrivateIps:
    Description: Private IP address list of created ecs instance. Only for VPC instance.
    Value:
      'Fn::GetAtt':
        - InstanceGroupClone
        - PrivateIps
  HostNames:
    Description: Host names of created instance.
    Value:
      'Fn::GetAtt':
        - InstanceGroupClone
        - HostNames
  InnerIps:
    Description: >-
      Inner IP address list of the specified instance. Only for classical
      instance.
    Value:
      'Fn::GetAtt':
        - InstanceGroupClone
        - InnerIps
  ZoneIds:
    Description: Zone id of created instance.
    Value:
      'Fn::GetAtt':
        - InstanceGroupClone
        - ZoneIds
  OrderId:
    Description: The order id list of created instance.
    Value:
      'Fn::GetAtt':
        - InstanceGroupClone
        - OrderId
  InstanceIds:
    Description: The instance id list of created ecs instance
    Value:
      'Fn::GetAtt':
        - InstanceGroupClone
        - InstanceIds
```

