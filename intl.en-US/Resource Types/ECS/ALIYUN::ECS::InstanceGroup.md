# ALIYUN::ECS::InstanceGroup

ALIYUN::ECS::InstanceGroup is used to create a group of ECS instances that have the same configurations.

## Syntax

```
{
  "Type": "ALIYUN::ECS::InstanceGroup",
  "Properties": {
    "DedicatedHostId": String,
    "ResourceGroupId": String,
    "SystemDiskDescription": String,
    "InstanceChargeType": String,
    "RamRoleName": String,
    "SystemDiskPerformanceLevel": String,
    "ImageId": String,
    "SystemDiskDiskName": String,
    "Tags": List,
    "HostName": String,
    "LaunchTemplateName": String,
    "VSwitchId": String,
    "Period": Number,
    "LaunchTemplateId": String,
    "DeletionProtection": "Boolean",
    "SecurityGroupIds": List,
    "SecurityEnhancementStrategy": String,
    "InternetChargeType": String,
    "InstanceName": String,
    "DeploymentSetId": String,
    "InternetMaxBandwidthOut": Integer,
    "VpcId": String,
    "LaunchTemplateVersion": String,
    "PeriodUnit": String,
    "AutoReleaseTime": String,
    "PrivateIpAddress": String,
    "Description": String,
    "DiskMappings": List,
    "SystemDiskSize": Number,
    "UserData": String,
    "AutoRenew": String,
    "Ipv6Addresses": List,
    "MaxAmount": Integer,
    "SystemDiskAutoSnapshotPolicyId": String,
    "Ipv6AddressCount": Integer,
    "NetworkType": String,
    "SpotPriceLimit": String,
    "InstanceType": String,
    "AllocatePublicIP": "Boolean",
    "SpotStrategy": String,
    "Password": String,
    "PasswordInherit": Boolean,
    "AutoRenewPeriod": Number,
    "KeyPairName": String,
    "IoOptimized": String,
    "ZoneId": String,
    "HpcClusterId": String,
    "SecurityGroupId": String,
    "SystemDiskCategory": String,
    "EniMappings": List,
    "InternetMaxBandwidthIn": Integer
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ResourceGroupId|String|No|Yes|The ID of the resource group to which the instance belongs.|None|
|HpcClusterId|String|No|Yes|The ID of the HPC cluster to which the instance belongs.|None|
|MaxAmount|Integer|Yes|Yes|The maximum number of instances that can be created at a time.|Valid values: 1 to 100.|
|Description|String|No|Yes|The description of the instance.|The description can be up to 256 characters in length.|
|InstanceType|String|Yes|Yes|The instance type.|For more information, see [Instance families](/intl.en-US/Instance/Instance families.md).|
|ImageId|String|Yes|Yes|The ID of the image that is used to start the instance. You can use a public image, a custom image, or an Alibaba Cloud Marketplace image.|You can specify a partial public image ID instead of providing the complete ID. Examples: -   If you enter ubuntu, the system matches it with the following ID: ubuntu16\_0402\_64\_20G\_alibase\_20170818.vhd
-   If you enter ubuntu\*14\*32, the system matches it with the following ID: ubuntu\_14\_0405\_32\_40G\_alibase\_20170711.vhd

For more information, see [Request parameters](/intl.en-US/API Reference/Instances/RunInstances.md).|
|SecurityGroupId|String|No|No|The ID of the security group to which the instance belongs.|You cannot specify both the SecurityGroupId and SecurityGroupIds parameters.|
|SecurityGroupIds|List|No|No|The IDs of multiple security groups to which the instance belongs. For information about the quota for security groups to which an instance can belong, see [Security group limits](/intl.en-US/Product Introduction/Limits.md).|You cannot specify both the SecurityGroupId and SecurityGroupIds parameters.|
|SecurityEnhancementStrategy|String|No|No|Specifies whether to enable security hardening.|Valid values:-   Active: enables security hardening. This value is applicable only to public images.
-   Deactive: disables security hardening. This value is applicable to all image types. |
|InstanceName|String|No|No|The name of the instance.|The name can be up to 128 characters in length and can contain letters, digits, underscores \(\_\), periods \(.\), and hyphens \(-\). The instance name must be in the `name_prefix[begin_number,bits]name_suffix` format. For more information, see [Request parameters](/intl.en-US/API Reference/Instances/RunInstances.md). |
|Password|String|No|Yes|The password that is used to log on to the instance.|The password must be 8 to 30 characters in length and must contain at least three of the following character types: uppercase letters, lowercase letters, digits, and special characters. Special characters include```
: ( ) ` ~ ! @ # $ % ^ & * - + = | { } [ ] : ; ' < > , . ? /
```

If you specify this parameter in the API request, use HTTPS to secure the API and protect your password.|
|PasswordInherit|Boolean|No|No|Specifies whether to use the preset password in the image.|Valid values:-   true: The preset password is used.
-   false: The preset password is not used.

**Note:** If you set the PasswordInherit parameter to true, leave the Password parameter empty and make sure that the selected image has a password preset. |
|HostName|String|No|No|The hostname of the instance.|The hostname must be at least 2 characters in length and cannot contain consecutive periods \(.\) or hyphens \(-\). It cannot start or end with a period \(.\) or a hyphen \(-\). For more information, see [Request parameters](/intl.en-US/API Reference/Instances/RunInstances.md).|
|AllocatePublicIP|Boolean|No|No|Specifies whether to assign a public IP address to the ECS instance.|If the InternetMaxBandwidthOut parameter is set to 0, no public IP address is assigned. Default value: true. Valid values:

-   true
-   false |
|AutoReleaseTime|String|No|No|The time scheduled for the instances to be automatically released.|Specify the time in the ISO 8601 standard in the `yyyy-MM-ddTHH:mm:ssZ` format. The time must be in UTC. The maximum release time must be within three years from the time when the instance is created.|
|PrivateIpAddress|String|No|No|The private IP address of the instance.|To assign a private IP address to a VPC-type instance, make sure that the IP address is an idle IP address within the CIDR block of the vSwitch. **Note:** If you specify the PrivateIpAddress parameter, the MaxAmount parameter must be set to 1. |
|DiskMappings|List|No|Yes|The list of one or more data disks to be attached to the instance.|A maximum of 16 data disks can be specified. If you modify the value of this parameter, existing instances are not affected. The modified value takes effect for the new instance.

For more information, see [DiskMappings properties](#section_39d_e40_xo6). |
|InternetChargeType|String|No|No|The billing method for network usage.|Default value: PayByTraffic. Valid values: -   PayByBandwidth
-   PayByTraffic |
|InternetMaxBandwidthIn|Integer|No|No|The maximum inbound public bandwidth.|Valid values: 1 to 100.

Unit: Mbit/s.

Default value: 100 |
|InternetMaxBandwidthOut|Integer|No|No|The maximum outbound public bandwidth.|Valid values: 0 to 100.

Unit: Mbit/s.

Default value: 0. |
|IoOptimized|String|No|No|Specifies whether the instance is I/O optimized.|Default value: optimized. Valid values: -   none: The instance is not I/O optimized.
-   optimized: The instance is I/O optimized. |
|SystemDiskCategory|String|No|Yes|The category of the system disk.|Valid values: -   cloud: basic disk
-   cloud\_efficiency: ultra disk
-   cloud\_ssd: standard SSD
-   cloud\_essd: enhanced SSD \(ESSD\)
-   ephemeral\_ssd: local SSD |
|SystemDiskDescription|String|No|Yes|The description of the system disk.|None|
|SystemDiskDiskName|String|No|Yes|The name of the system disk.|None|
|SystemDiskSize|Number|No|Yes|The size of the system disk.|Valid values: 40 to 500. Unit: GB.

If a custom image is used to create a system disk, make sure that the size of the system disk is larger than that of the custom image. |
|Tags|List|No|Yes|The custom tags of the instance.|A maximum of 20 tags can be specified in the `[{"Key":"tagKey","Value":"tagValue"},{"Key":"tagKey2","Value":"tagValue2"}]` format. For more information, see [Tags properties](#section_668_3ad_arl). |
|UserData|String|No|Yes|The user data that you provide when you create the instance.|The user data can be up to 16 KB in size. You do not need to convert the data into Base64-encoded strings. If the data contains special characters, add a backslash \(\\\) immediately before each special character.|
|ZoneId|String|No|No|The zone ID of the instance.|None|
|VpcId|String|No|No|The ID of the VPC.|None|
|VSwitchId|String|No|No|The ID of the vSwitch.|None|
|KeyPairName|String|No|Yes|The name of the key pair that is used to connect to the instance.|For a Windows ECS instance, this parameter is ignored and is empty by default.

For a Linux ECS instance, the Password parameter still takes effect if this parameter is specified. However, logon by password is disabled, and the KeyPairName value is used.|
|RamRoleName|String|No|Yes|The RAM role name of the instance.|You can call the ListRoles operation to query the RAM role name. For more information, see [CreateRole](/intl.en-US/API Reference/API Reference (RAM)/Role management APIs/CreateRole.md)and [ListRoles](/intl.en-US/API Reference/API Reference (RAM)/Role management APIs/ListRoles.md).|
|SpotPriceLimit|String|No|No|The maximum hourly price of the instance.|Three decimal places are allowed at most. This parameter takes effect only when the SpotStrategy parameter is set to SpotWithPriceLimit.|
|SpotStrategy|String|No|No|The bidding policy for pay-as-you-go instances.|This parameter takes effect only when the InstanceChargeType parameter is set to PostPaid. Default value: NoSpot. Valid values: -   NoSpot: applies to regular pay-as-you-go instances.
-   SpotWithPriceLimit: applies to preemptible instances with a maximum hourly price.
-   SpotAsPriceGo: applies to pay-as-you-go instances priced at the market price at the time of purchase. |
|DedicatedHostId|String|No|No|The ID of the dedicated host.|None|
|LaunchTemplateName|String|No|Yes|The name of the launch template.|None|
|PeriodUnit|String|No|Yes|The unit of the subscription period.|Default value: Month. Valid values: -   Week
-   Month |
|AutoRenewPeriod|Number|No|Yes|The auto-renewal period for the instance.|This parameter is required when the AutoRenew parameter is set to True. Default value: 1. Valid values:

-   1
-   2
-   3
-   6
-   12 |
|AutoRenew|String|No|Yes|Specifies whether to enable auto-renewal for the instance.|This parameter takes effect only when the InstanceChargeType parameter is set to PrePaid. Default value: False. Valid values: -   True: enables auto-renewal.
-   False: disables auto-renewal. |
|InstanceChargeType|String|No|Yes|The billing method of the instance.|Default value: Postpaid. Valid values: -   PrePaid: subscription

**Note:** If this parameter is set to PrePaid, you must make sure that your payment account has sufficient balance or credit. Otherwise, an InvalidPayMethod error is returned.

-   PostPaid: pay-as-you-go |
|EniMappings|List|No|Yes|The elastic network interface \(ENI\) to be bound to the instance.|Only one ENI can be bound to each instance. For more information, see [EniMappings properties](#section_qf5_2mx_o68). |
|LaunchTemplateId|String|No|Yes|The ID of the launch template.|None|
|LaunchTemplateVersion|String|No|Yes|The version of the launch template.|If you do not specify a version, the default version is used.|
|Period|Number|No|Yes|The subscription period of the instance.|This parameter is required when the InstanceChargeType parameter is set to PrePaid. If the DedicatedHostId parameter is specified, values of this parameter must be within the subscription period of the dedicated host. -   Valid values when PeriodUnit is set to Week: 1, 2, 3, and 4.
-   Valid values when PeriodUnit is set to Month: 1, 2, 3, 4, 5, 6, 7, 8, 9, 12, 24, 36, 48, and 60. |
|NetworkType|String|No|No|The network type of the instance.|Default value: classic. Valid values: -   vpc
-   classic |
|DeletionProtection|Boolean|No|No|The deletion protection property of the instance. It specifies whether to release the instances by using the ECS console or calling the [DeleteInstance](/intl.en-US/API Reference/Instances/DeleteInstance.md) operation.|Valid values: -   true
-   false |
|DeploymentSetId|String|No|Yes|The ID of the deployment set.|None|
|Ipv6AddressCount|Integer|No|Yes|The number of randomly generated IPv6 addresses that are assigned to the ENI.|You cannot specify both the Ipv6Addresses and Ipv6AddressCount parameters.|
|Ipv6Addresses|List|No|Yes|The list of one or more IPv6 addresses assigned to the ENI.|Only one IPv6 address can be specified. Property modification does not affect existing instances. You cannot specify both the Ipv6Addresses and Ipv6AddressCount parameters.|
|SystemDiskAutoSnapshotPolicyId|String|No|Yes|The ID of the automatic snapshot policy for the system disk.|None|
|SystemDiskPerformanceLevel|String|No|No|The performance level of the ESSD that is used as the system disk.|Default value: PL1. Valid values: -   PL1: A single ESSD delivers up to 50,000 random read/write IOPS.
-   PL2: A single ESSD delivers up to 100,000 random read/write IOPS.
-   PL3: A single ESSD delivers up to 1,000,000 random read/write IOPS.

For more information about performance levels of ESSDs, see [ESSDs](/intl.en-US/Block Storage/Block Storage overview/ESSDs.md).|

## DiskMappings syntax

```
"DiskMappings": [
  {
    "Category": String,
    "DiskName": String,
    "Description": String,
    "Device": String,
    "SnapshotId": String,
    "Size": String,
    "Encrypted": String,
    "KMSKeyId": String,
    "PerformanceLevel": String,
    "AutoSnapshotPolicyId": String
  }
]
```

## DiskMappings properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Size|String|Yes|No|The size of the data disk.|Unit: GB.|
|Category|String|No|No|The category of the data disk.|Valid values: -   cloud
-   cloud\_efficiency
-   cloud\_ssd
-   cloud\_essd
-   ephemeral\_ssd

For I/O optimized instances, the default value is cloud\_efficiency. For non-I/O optimized instances, the default value is cloud.|
|DiskName|String|No|No|The name of the data disk.|The name must be 2 to 128 characters in length and can contain letters, digits, underscores \(\_\), colons \(:\), and hyphens \(-\). It must start with a letter and cannot start with `http://` or `https://`.|
|Description|String|No|No|The description of the data disk.|The description must be 2 to 256 characters in length. It cannot start with `http://` or `https://`.|
|Device|String|No|No|The device name of the data disk.|**Note:** This parameter will be removed in the future. We recommend that you use other parameters to ensure future compatibility. |
|SnapshotId|String|No|No|The ID of the snapshot.|None|
|Encrypted|String|No|No|Specifies whether to encrypt the data disk.|Default value: false. Valid values: -   true
-   false |
|KMSKeyId|String|No|No|The ID of the KMS key corresponding to the data disk.|None|
|AutoSnapshotPolicyId|String|No|No|The ID of the automatic snapshot policy.|None|
|PerformanceLevel|String|No|No|The performance level of the ESSD that is used as the data disk.|Default value: PL1. Valid values: -   PL1: A single ESSD delivers up to 50,000 random read/write IOPS.
-   PL2: A single ESSD delivers up to 100,000 random read/write IOPS.
-   PL3: A single ESSD delivers up to 1,000,000 random read/write IOPS.

For more information about performance levels of ESSDs, see [ESSDs](/intl.en-US/Block Storage/Block Storage overview/ESSDs.md).|

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
|Key|String|Yes|No|The tag key.|The tag key must be 1 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|
|Value|String|No|No|The tag value.|The tag value must be 0 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|

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
|SecurityGroupId|String|Yes|Yes|The ID of the security group.|The security group and the instance must be in one VPC.|
|VSwitchId|String|Yes|No|The ID of the vSwitch.|None|
|Description|String|No|Yes|The description of the ENI.|The description must be 2 to 256 characters in length. It cannot start with `http://` or `https://`.|
|NetworkInterfaceName|String|No|Yes|The name of the ENI.|The name must be 2 to 128 characters in length and can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with `http://` or `https://`.|
|PrimaryIpAddress|String|No|No|The primary private IP address of the ENI.|The IP address must be an idle IP address within the CIDR block of the vSwitch. If this parameter is not specified, an idle IP address within the CIDR block of the vSwitch is assigned at random.|

## Response parameters

Fn::GetAtt

-   InstanceIds: the IDs of one or more instances. An instance ID is a system-generated globally unique identifier \(GUID\) for an instance.
-   PrivateIps: the private IP addresses of one or more VPC-type instances. This parameter takes effect only when the NetworkType parameter is set to VPC. Example:`["172.16.XX.XX", "172.16. XX.XX", ... "172.16. XX.XX"]`. In this example, the list is a JSON array that can contain up to 100 IP addresses separated by commas \(,\).
-   InnerIps: the private IP addresses of one or more classic network-type instances. This parameter takes effect only when the NetworkType parameter is set to Classic. Example:`["10.1.XX.XX", "10.1. XX.XX", ... "10.1. XX.XX"]`. In this example, the list is a JSON array that can contain up to 100 IP addresses separated by commas \(,\).
-   PublicIps: the public IP addresses of one or more classic network-type instances. This parameter takes effect only when the NetworkType parameter is set to Classic. Example:`["42.1.XX.XX", "42.1. XX.XX", ... "42.1. XX.XX"]`. In this example, the list is a JSON array that can contain up to 100 IP addresses separated by commas \(,\).
-   HostNames: the hostnames of one or more instances.
-   OrderId: the order IDs of one or more instances.
-   ZoneIds: the zone IDs of one or more instances.

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
    "ResourceGroupId": {
      "Type": "String",
      "Description": "Resource group id."
    },
    "SystemDiskDescription": {
      "Type": "String",
      "Description": "Description of created system disk.Old instances will not be changed."
    },
    "InstanceChargeType": {
      "Type": "String",
      "Description": "Instance Charge type, allowed value: Prepaid and Postpaid. If specified Prepaid, please ensure you have sufficient balance in your account. Or instance creation will be failure. Default value is Postpaid.Old instances will not be changed.",
      "AllowedValues": [
        "PrePaid",
        "PostPaid"
      ],
      "Default": "PostPaid"
    },
    "RamRoleName": {
      "Type": "String",
      "Description": "Instance RAM role name. The name is provided and maintained by Resource Access Management (RAM) and can be queried using ListRoles. For more information, see RAM API CreateRole and ListRoles."
    },
    "SystemDiskPerformanceLevel": {
      "Type": "String",
      "Description": "The performance level of the enhanced SSD used as the system disk.Default value: PL1. Valid values:PL0: A single enhanced SSD delivers up to 10,000 random read/write IOPS.PL1: A single enhanced SSD delivers up to 50,000 random read/write IOPS.PL2: A single enhanced SSD delivers up to 100,000 random read/write IOPS.PL3: A single enhanced SSD delivers up to 1,000,000 random read/write IOPS."
    },
    "ImageId": {
      "Type": "String",
      "Description": "Image ID to create ecs instance."
    },
    "SystemDiskDiskName": {
      "Type": "String",
      "Description": "Name of created system disk.Old instances will not be changed."
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to instance. Max support 20 tags to add during create instance. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
    },
    "HostName": {
      "Type": "String",
      "Description": "Host name of created ecs instance. at least 2 characters, and '.' '-' Is not the first and last characters as hostname, not continuous use. Windows platform can be up to 15 characters, allowing letters (without limiting case), numbers and '-', and does not support the number of points, not all is digital ('.').Other (Linux, etc.) platform up to 30 characters, allowing support number multiple points for the period between the points, each permit letters (without limiting case), numbers and '-' components. \nSupport to use the regular expression to set the different instance name for each ECS instance. HostName could be specified as 'name_prefix[begin_number,bits]name_suffix', such as 'host[123,4]tail'. If you creates 3 instances with hostname 'host[123,4]tail', all the host names of instances are host0123tail, host0124tail, host0125tail. The 'name_prefix[begin_number,bits]name_suffix' should follow those rules: \n1. 'name_prefix' is required. \n2. 'name_suffix' is optional. \n3. The name regular expression can't include any spaces. \n4. The 'bits' must be in range [1, 6]. \n5. The 'begin_number' must be in range [0, 999999]. \n6. You could only specify 'begin_number'. The 'bits' will be set as 6 by default. \n7. You also could only specify the [] or [,]. The 'begin_number' will be set as 0 by default, the 'bits' will be set as 6 by default. \n8. If the bits of 'begin_number' is less than the 'bits' you specified, like [1234,1], the 'bits' will be set as 6 by default. \nThe host name is specified by regular expression works after restart instance manually."
    },
    "LaunchTemplateName": {
      "Type": "String",
      "Description": "Name of launch template. Launch template id or name must be specified to use launch template"
    },
    "VSwitchId": {
      "Type": "String",
      "Description": "The vSwitch Id to create ecs instance."
    },
    "Period": {
      "Type": "Number",
      "Description": "Prepaid time period. Unit is month, it could be from 1 to 9 or 12, 24, 36, 48, 60. Default value is 1.Old instances will not be changed.",
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
      "Description": "Whether an instance can be released manually through the console or API, deletion protection only support postPaid instance",
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
    "InternetChargeType": {
      "Type": "String",
      "Description": "Instance internet access charge type.Support 'PayByBandwidth' and 'PayByTraffic' only. Default is PayByTraffic",
      "AllowedValues": [
        "PayByBandwidth",
        "PayByTraffic"
      ],
      "Default": "PayByTraffic"
    },
    "DeploymentSetId": {
      "Type": "String",
      "Description": "Deployment set ID. The change of the property does not affect existing instances."
    },
    "InstanceName": {
      "Type": "String",
      "Description": "Display name of the instance, [2, 128] English or Chinese characters, must start with a letter or Chinese in size, can contain numbers, '_' or '.', '-'. \nSupport to use the regular expression to set the different instance name for each ECS instance. InstanceName could be specified as 'name_prefix[begin_number,bits]name_suffix', such as 'testinstance[123,4]tail'. If you creates 3 instances with the instance name 'testinstance[123,4]tail', all the instances' names are testinstance0123tail, testinstance0124tail, testinstance0125tail. \nThe 'name_prefix[begin_number,bits]name_suffix' should follow those rules: \n1. 'name_prefix' is required. \n2. 'name_suffix' is optional. \n3. The name regular expression can't include any spaces. \n4. The 'bits' must be in range [1, 6]. \n5. The 'begin_number' must be in range [0, 999999]. \n6. You could only specify 'begin_number'. The 'bits' will be set as 6 by default. \n7. You also could only specify the [] or [,]. The 'begin_number' will be set as 0 by default, the 'bits' will be set as 6 by default. \n8. If the bits of 'begin_number' is less than the 'bits' you specified, like [1234,1], the 'bits' will be set as 6 by default."
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
    "LaunchTemplateVersion": {
      "Type": "String",
      "Description": "Version of launch template. Default version is used if version is not specified.",
      "AllowedPattern": "^[1-9]\\d*$"
    },
    "SecurityEnhancementStrategy": {
      "Type": "String",
      "Description": "",
      "AllowedValues": [
        "Active",
        "Deactive"
      ]
    },
    "AutoReleaseTime": {
      "Type": "String",
      "Description": "Auto release time for created instance, Follow ISO8601 standard using UTC time. format is 'yyyy-MM-ddTHH:mm:ssZ'. Not bigger than 3 years from this day onwards"
    },
    "PeriodUnit": {
      "Type": "String",
      "Description": "Unit of prepaid time period, it could be Week/Month. Default value is Month.Old instances will not be changed.",
      "AllowedValues": [
        "Week",
        "Month"
      ],
      "Default": "Month"
    },
    "PrivateIpAddress": {
      "Type": "String",
      "Description": "Private IP for the instance created. Only works for VPC instance and cannot duplicated with existing instance."
    },
    "Description": {
      "Type": "String",
      "Description": "Description of the instance, [2, 256] characters. Do not fill or empty, the default is empty. Old instances will not be changed."
    },
    "DiskMappings": {
      "Type": "Json",
      "Description": "Disk mappings to attach to instance. Max support 16 disks.\nIf the image contains a data disk, you can specify other parameters of the data disk via the same value of parameter \"Device\". If parameter \"Category\" is not specified, it will be cloud_efficiency instead of \"Category\" of data disk in the image.Old instances will not be changed.",
      "MaxLength": 16
    },
    "UserData": {
      "Type": "String",
      "Description": "User data to pass to instance. [1, 16KB] characters.User data should not be base64 encoded. If you want to pass base64 encoded string to the property, use function Fn::Base64Decode to decode the base64 string first."
    },
    "SystemDiskSize": {
      "Type": "Number",
      "Description": "Disk size of the system disk, range from 20 to 500 GB. If you specify with your own image, make sure the system disk size bigger than image size. ",
      "MinValue": 20
    },
    "AutoRenew": {
      "Type": "String",
      "Description": "Whether renew the fee automatically? When the parameter InstanceChargeType is PrePaid, it will take effect. Range of value:True: automatic renewal.False: no automatic renewal. Default value is False.Old instances will not be changed.",
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
    "NetworkType": {
      "Type": "String",
      "Description": "Instance network type. Support 'vpc' and 'classic', for compatible reason, default is 'classic'. If vswitch id and vpc id is specified, the property will be forced to be set to 'vpc'  ",
      "AllowedValues": [
        "vpc",
        "classic"
      ],
      "Default": "classic"
    },
    "Ipv6AddressCount": {
      "Type": "Number",
      "Description": "Specifies the number of randomly generated IPv6 addresses for the elastic NIC.\nNote You cannot specify the parameters Ipv6Addresses and Ipv6AddressCount at the same time.\nThe change of the property does not affect existing instances.",
      "MinValue": 0
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
      "Description": "The time period of auto renew. When the parameter InstanceChargeType is PrePaid, it will take effect.It could be 1, 2, 3, 6, 12. Default value is 1.Old instances will not be changed.",
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
      "Description": "SSH key pair name.Old instances will not be changed."
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
      "Description": "The ID of the zone to which the instance belongs. For more information, \ncall the DescribeZones operation to query the most recent zone list. \nDefault value is empty, which means random selection."
    },
    "HpcClusterId": {
      "Type": "String",
      "Description": "The HPC cluster ID to which the instance belongs.The change of the property does not affect existing instances."
    },
    "SecurityGroupId": {
      "Type": "String",
      "Description": "Security group to create ecs instance. For classic instance need the security group not belong to VPC, for VPC instance, please make sure the security group belong to specified VPC."
    },
    "SystemDiskCategory": {
      "Type": "String",
      "Description": "Category of system disk. Default is cloud_efficiency. support cloud|cloud_efficiency|cloud_ssd|cloud_essd|ephemeral_ssd.Old instances will not be changed.",
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
    "InternetMaxBandwidthIn": {
      "Type": "Number",
      "Description": "Max internet out band width setting, unit in Mbps(Mega bit per second). The range is [1,200], default is 200 Mbps.",
      "MinValue": 1,
      "MaxValue": 200,
      "Default": 200
    }
  },
  "Resources": {
    "InstanceGroup": {
      "Type": "ALIYUN::ECS::InstanceGroup",
      "Properties": {
        "DedicatedHostId": {
          "Ref": "DedicatedHostId"
        },
        "ResourceGroupId": {
          "Ref": "ResourceGroupId"
        },
        "SystemDiskDescription": {
          "Ref": "SystemDiskDescription"
        },
        "InstanceChargeType": {
          "Ref": "InstanceChargeType"
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
        "Tags": {
          "Ref": "Tags"
        },
        "HostName": {
          "Ref": "HostName"
        },
        "LaunchTemplateName": {
          "Ref": "LaunchTemplateName"
        },
        "VSwitchId": {
          "Ref": "VSwitchId"
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
        "InternetChargeType": {
          "Ref": "InternetChargeType"
        },
        "DeploymentSetId": {
          "Ref": "DeploymentSetId"
        },
        "InstanceName": {
          "Ref": "InstanceName"
        },
        "InternetMaxBandwidthOut": {
          "Ref": "InternetMaxBandwidthOut"
        },
        "VpcId": {
          "Ref": "VpcId"
        },
        "LaunchTemplateVersion": {
          "Ref": "LaunchTemplateVersion"
        },
        "SecurityEnhancementStrategy": {
          "Ref": "SecurityEnhancementStrategy"
        },
        "AutoReleaseTime": {
          "Ref": "AutoReleaseTime"
        },
        "PeriodUnit": {
          "Ref": "PeriodUnit"
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
        "UserData": {
          "Ref": "UserData"
        },
        "SystemDiskSize": {
          "Ref": "SystemDiskSize"
        },
        "AutoRenew": {
          "Ref": "AutoRenew"
        },
        "Ipv6Addresses": {
          "Ref": "Ipv6Addresses"
        },
        "MaxAmount": {
          "Ref": "MaxAmount"
        },
        "SystemDiskAutoSnapshotPolicyId": {
          "Ref": "SystemDiskAutoSnapshotPolicyId"
        },
        "NetworkType": {
          "Ref": "NetworkType"
        },
        "Ipv6AddressCount": {
          "Ref": "Ipv6AddressCount"
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
        "SecurityGroupId": {
          "Ref": "SecurityGroupId"
        },
        "SystemDiskCategory": {
          "Ref": "SystemDiskCategory"
        },
        "EniMappings": {
          "Ref": "EniMappings"
        },
        "InternetMaxBandwidthIn": {
          "Ref": "InternetMaxBandwidthIn"
        }
      }
    }
  },
  "Outputs": {
    "PublicIps": {
      "Description": "Public IP address list of created ecs instance.",
      "Value": {
        "Fn::GetAtt": [
          "InstanceGroup",
          "PublicIps"
        ]
      }
    },
    "PrivateIps": {
      "Description": "Private IP address list of created ecs instance. Only for VPC instance.",
      "Value": {
        "Fn::GetAtt": [
          "InstanceGroup",
          "PrivateIps"
        ]
      }
    },
    "HostNames": {
      "Description": "Host names of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "InstanceGroup",
          "HostNames"
        ]
      }
    },
    "InnerIps": {
      "Description": "Inner IP address list of the specified instance. Only for classical instance.",
      "Value": {
        "Fn::GetAtt": [
          "InstanceGroup",
          "InnerIps"
        ]
      }
    },
    "ZoneIds": {
      "Description": "Zone id of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "InstanceGroup",
          "ZoneIds"
        ]
      }
    },
    "OrderId": {
      "Description": "The order id list of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "InstanceGroup",
          "OrderId"
        ]
      }
    },
    "InstanceIds": {
      "Description": "The instance id list of created ecs instance",
      "Value": {
        "Fn::GetAtt": [
          "InstanceGroup",
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
  DedicatedHostId:
    Type: String
    Description: which dedicated host will be deployed
  ResourceGroupId:
    Type: String
    Description: Resource group id.
  SystemDiskDescription:
    Type: String
    Description: Description of created system disk.Old instances will not be changed.
  InstanceChargeType:
    Type: String
    Description: >-
      Instance Charge type, allowed value: Prepaid and Postpaid. If specified
      Prepaid, please ensure you have sufficient balance in your account. Or
      instance creation will be failure. Default value is Postpaid.Old instances
      will not be changed.
    AllowedValues:
      - PrePaid
      - PostPaid
    Default: PostPaid
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
  ImageId:
    Type: String
    Description: Image ID to create ecs instance.
  SystemDiskDiskName:
    Type: String
    Description: Name of created system disk.Old instances will not be changed.
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

      Support to use the regular expression to set the different instance name
      for each ECS instance. HostName could be specified as
      'name_prefix[begin_number,bits]name_suffix', such as 'host[123,4]tail'. If
      you creates 3 instances with hostname 'host[123,4]tail', all the host
      names of instances are host0123tail, host0124tail, host0125tail. The
      'name_prefix[begin_number,bits]name_suffix' should follow those rules: 

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

      The host name is specified by regular expression works after restart
      instance manually.
  LaunchTemplateName:
    Type: String
    Description: >-
      Name of launch template. Launch template id or name must be specified to
      use launch template
  VSwitchId:
    Type: String
    Description: The vSwitch Id to create ecs instance.
  Period:
    Type: Number
    Description: >-
      Prepaid time period. Unit is month, it could be from 1 to 9 or 12, 24, 36,
      48, 60. Default value is 1.Old instances will not be changed.
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
  InternetChargeType:
    Type: String
    Description: >-
      Instance internet access charge type.Support 'PayByBandwidth' and
      'PayByTraffic' only. Default is PayByTraffic
    AllowedValues:
      - PayByBandwidth
      - PayByTraffic
    Default: PayByTraffic
  DeploymentSetId:
    Type: String
    Description: >-
      Deployment set ID. The change of the property does not affect existing
      instances.
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
  LaunchTemplateVersion:
    Type: String
    Description: >-
      Version of launch template. Default version is used if version is not
      specified.
    AllowedPattern: '^[1-9]\d*$'
  SecurityEnhancementStrategy:
    Type: String
    Description: ''
    AllowedValues:
      - Active
      - Deactive
  AutoReleaseTime:
    Type: String
    Description: >-
      Auto release time for created instance, Follow ISO8601 standard using UTC
      time. format is 'yyyy-MM-ddTHH:mm:ssZ'. Not bigger than 3 years from this
      day onwards
  PeriodUnit:
    Type: String
    Description: >-
      Unit of prepaid time period, it could be Week/Month. Default value is
      Month.Old instances will not be changed.
    AllowedValues:
      - Week
      - Month
    Default: Month
  PrivateIpAddress:
    Type: String
    Description: >-
      Private IP for the instance created. Only works for VPC instance and
      cannot duplicated with existing instance.
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
      "Category" of data disk in the image.Old instances will not be changed.
    MaxLength: 16
  UserData:
    Type: String
    Description: >-
      User data to pass to instance. [1, 16KB] characters.User data should not
      be base64 encoded. If you want to pass base64 encoded string to the
      property, use function Fn::Base64Decode to decode the base64 string first.
  SystemDiskSize:
    Type: Number
    Description: >-
      Disk size of the system disk, range from 20 to 500 GB. If you specify with
      your own image, make sure the system disk size bigger than image size. 
    MinValue: 20
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
  NetworkType:
    Type: String
    Description: >-
      Instance network type. Support 'vpc' and 'classic', for compatible reason,
      default is 'classic'. If vswitch id and vpc id is specified, the property
      will be forced to be set to 'vpc'  
    AllowedValues:
      - vpc
      - classic
    Default: classic
  Ipv6AddressCount:
    Type: Number
    Description: >-
      Specifies the number of randomly generated IPv6 addresses for the elastic
      NIC.

      Note You cannot specify the parameters Ipv6Addresses and Ipv6AddressCount
      at the same time.

      The change of the property does not affect existing instances.
    MinValue: 0
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
      PrePaid, it will take effect.It could be 1, 2, 3, 6, 12. Default value is
      1.Old instances will not be changed.
    AllowedValues:
      - 1
      - 2
      - 3
      - 6
      - 12
    Default: 1
  KeyPairName:
    Type: String
    Description: SSH key pair name.Old instances will not be changed.
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
    Description: |-
      The ID of the zone to which the instance belongs. For more information, 
      call the DescribeZones operation to query the most recent zone list. 
      Default value is empty, which means random selection.
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
  InternetMaxBandwidthIn:
    Type: Number
    Description: >-
      Max internet out band width setting, unit in Mbps(Mega bit per second).
      The range is [1,200], default is 200 Mbps.
    MinValue: 1
    MaxValue: 200
    Default: 200
Resources:
  InstanceGroup:
    Type: 'ALIYUN::ECS::InstanceGroup'
    Properties:
      DedicatedHostId:
        Ref: DedicatedHostId
      ResourceGroupId:
        Ref: ResourceGroupId
      SystemDiskDescription:
        Ref: SystemDiskDescription
      InstanceChargeType:
        Ref: InstanceChargeType
      RamRoleName:
        Ref: RamRoleName
      SystemDiskPerformanceLevel:
        Ref: SystemDiskPerformanceLevel
      ImageId:
        Ref: ImageId
      SystemDiskDiskName:
        Ref: SystemDiskDiskName
      Tags:
        Ref: Tags
      HostName:
        Ref: HostName
      LaunchTemplateName:
        Ref: LaunchTemplateName
      VSwitchId:
        Ref: VSwitchId
      Period:
        Ref: Period
      LaunchTemplateId:
        Ref: LaunchTemplateId
      DeletionProtection:
        Ref: DeletionProtection
      SecurityGroupIds:
        Ref: SecurityGroupIds
      InternetChargeType:
        Ref: InternetChargeType
      DeploymentSetId:
        Ref: DeploymentSetId
      InstanceName:
        Ref: InstanceName
      InternetMaxBandwidthOut:
        Ref: InternetMaxBandwidthOut
      VpcId:
        Ref: VpcId
      LaunchTemplateVersion:
        Ref: LaunchTemplateVersion
      SecurityEnhancementStrategy:
        Ref: SecurityEnhancementStrategy
      AutoReleaseTime:
        Ref: AutoReleaseTime
      PeriodUnit:
        Ref: PeriodUnit
      PrivateIpAddress:
        Ref: PrivateIpAddress
      Description:
        Ref: Description
      DiskMappings:
        Ref: DiskMappings
      UserData:
        Ref: UserData
      SystemDiskSize:
        Ref: SystemDiskSize
      AutoRenew:
        Ref: AutoRenew
      Ipv6Addresses:
        Ref: Ipv6Addresses
      MaxAmount:
        Ref: MaxAmount
      SystemDiskAutoSnapshotPolicyId:
        Ref: SystemDiskAutoSnapshotPolicyId
      NetworkType:
        Ref: NetworkType
      Ipv6AddressCount:
        Ref: Ipv6AddressCount
      SpotPriceLimit:
        Ref: SpotPriceLimit
      InstanceType:
        Ref: InstanceType
      AllocatePublicIP:
        Ref: AllocatePublicIP
      SpotStrategy:
        Ref: SpotStrategy
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
      SecurityGroupId:
        Ref: SecurityGroupId
      SystemDiskCategory:
        Ref: SystemDiskCategory
      EniMappings:
        Ref: EniMappings
      InternetMaxBandwidthIn:
        Ref: InternetMaxBandwidthIn
Outputs:
  PublicIps:
    Description: Public IP address list of created ecs instance.
    Value:
      'Fn::GetAtt':
        - InstanceGroup
        - PublicIps
  PrivateIps:
    Description: Private IP address list of created ecs instance. Only for VPC instance.
    Value:
      'Fn::GetAtt':
        - InstanceGroup
        - PrivateIps
  HostNames:
    Description: Host names of created instance.
    Value:
      'Fn::GetAtt':
        - InstanceGroup
        - HostNames
  InnerIps:
    Description: >-
      Inner IP address list of the specified instance. Only for classical
      instance.
    Value:
      'Fn::GetAtt':
        - InstanceGroup
        - InnerIps
  ZoneIds:
    Description: Zone id of created instance.
    Value:
      'Fn::GetAtt':
        - InstanceGroup
        - ZoneIds
  OrderId:
    Description: The order id list of created instance.
    Value:
      'Fn::GetAtt':
        - InstanceGroup
        - OrderId
  InstanceIds:
    Description: The instance id list of created ecs instance
    Value:
      'Fn::GetAtt':
        - InstanceGroup
        - InstanceIds
```

