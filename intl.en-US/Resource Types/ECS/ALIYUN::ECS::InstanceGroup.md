# ALIYUN::ECS::InstanceGroup {#concept_48278_zh .concept}

ALIYUN::ECS::InstanceGroup is used to create an ECS instance group.

## Syntax {#section_xyg_tn2_lfb .section}

``` {#codeblock_qwf_u6r_omx .language-json}
{
  "Type": "ALIYUN::ECS::InstanceGroup",
  "Properties": {
    "DedicatedHostId": String,
    "LaunchTemplateName": String,
    "RamRoleName": String,
    "IoOptimized": String,
    "InternetChargeType": String,
    "PrivateIpAddress": String,
    "KeyPairName": String,
    "SystemDiskDiskName": String,
    "PeriodUnit": String,
    "Description": String,
    "AutoRenew": String,
    "SpotPriceLimit": String,
    "HostName": String,
    "AutoRenewPeriod": Number,
    "ImageId": String,
    "ResourceGroupId": String,
    "InstanceChargeType": String,
    "VSwitchId": String,
    "EniMappings": List,
    "Password": String,
    "InstanceType": String,
    "MaxAmount": Integer,
    "AutoReleaseTime": String,
    "Tags": List,
    "SystemDiskCategory": String,
    "DeletionProtection": Boolean,
    "LaunchTemplateId": String,
    "LaunchTemplateVersion": String,
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
    "Period": Number,
    "HpcClusterId": String,
    "AllocatePublicIP": Boolean,
    "SystemDiskDescription": String,
    "NetworkType": String,
    "DiskMappings": List
  }
}
```

## Properties {#section_pzg_wn2_lfb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|ResourceGroupId|String|No|Yes|The ID of the resource group to which created instances belong.|None|
|HpcClusterId|String|No|Yes|The ID of the HPC cluster to which created instances belong.|None|
|MaxAmount|Integer|Yes|Yes|The maximum number of ECS instances that can be created in a single scaling operation.|Valid values: 1 to 100. The value of this parameter must be greater than or equal to that of the MinAmount parameter.|
|MinAmount|String|Yes|Yes|The minimum number of ECS instances that can be created in a single scaling operation.|Valid values: 1 to 100. The value of this parameter must be less than or equal to that of the MaxAmount parameter.|
|Description|String|No|No|The description of created ECS instances.|The description can be up to 256 characters in length.|
|InstanceType|String|Yes|No|The type of created ECS instances.|For more information, see [Instance families](https://partners-intl.aliyun.com/help/doc-detail/25378.htm).|
|ImageId|String|Yes|Yes|The ID of the image used to start an ECS instance. You can use a public image, custom image, or Alibaba Cloud Marketplace image.|For more information, see [Public images for ECS instances](https://ros.console.aliyun.com/#/product/cn-hangzhou/list/imageList). You can specify a partial public image ID instead of providing the complete ID. When editing a template used to deploy an ECS instance, you can specify either the image type and version or only the image type. ROS automatically selects an appropriate public image ID. You can use the wildcard character \(\*\) to represent part of an image ID. Take the Ubuntu public images provided by Alibaba Cloud as an example:

 ubuntu\_14\_0405\_32\_40G\_alibase\_20170711.vhd

 ubuntu\_14\_0405\_64\_20G\_alibase\_20170824.vhd

 ubuntu\_16\_0402\_32\_40G\_alibase\_20170711.vhd

 ubuntu\_16\_0402\_64\_20G\_alibase\_20170818.vhd

 You can use one of the following methods to specify a public image ID for the ECS instance:

 If you enter ubuntu,

 the system matches it with the following ID: ubuntu\_16\_0402\_64\_20G\_alibase\_20170818.vhd

 If you enter ubuntu\_14,

 the system matches it with the following ID: ubuntu\_14\_0405\_64\_20G\_alibase\_20170824.vhd

 If you enter ubuntu1432,

 the system matches it with the following ID: ubuntu\_14\_0405\_32\_40G\_alibase\_20170711.vhd If you enter ubuntu\_16\_0402\_32,

 the system matches it with the following ID: ubuntu\_16\_0402\_32\_40G\_alibase\_20170711.vhd|
|SecurityGroupId|String|No|No|The ID of the security group to which created instances belong.|None|
|InstanceName|String|No|No|The name of created ECS instances.|The name can be up to 128 characters in length and can contain letters, digits, underscores \(\_\), periods \(.\), and hyphens \(-\). Instance names must be in the name\_prefix\[begin\_number,bits\]name\_suffix format. The name\_prefix parameter specifies the prefix of an instance name. This parameter is required. The \[begin\_number,bits\] parameter specifies the part of an instance name that distinguishes a created instance from others. The begin\_number parameter specifies the number from which to start incrementing instance names. The bits parameter specifies the number of digits in the number for each instance name. The name\_suffix parameter specifies the suffix of each instance name. This parameter is optional. When specifying the \[begin\_number,bits\] parameter, you must pay attention to the following rules:

 Do not place spaces between the begin\_number and bits parameters.

 The value of bits can range from 1 to 6.

 The value of begin\_number can range from 0 to 999999.

 If you specify the begin\_number parameter without specifying the bits parameter, bits is set to 6.

 If neither the begin\_number parameter nor the bits parameter is specified, begin\_number is set to 0 and bits is set to 6.

 If the number of digits for begin\_number is greater than the specified value of bits, the specified value of bits will be overridden by the number of digits in the specified value of begin\_number. For example, if \[begin\_number,bits\] is set to \[123456,1\], the value of bits will be overridden by the number of digits in the specified value of begin\_number, which in this case is 6.

 |
|Password|String|No|No|The password used to log on to created ECS instances.|The password must contain characters from at least three of the following categories: uppercase letters, lowercase letters, digits, and special characters. Special characters include \( \) \` ~ ! @ \# $ % ^ & \* - + = | \{ \} \[ \] : ; ' < \> , . ? / If you specify the Password parameter in the API request, use HTTPS to secure the API and protect your password.|
|HostName|String|No|No|The hostname of created ECS instances.| The hostname must be at least 2 characters in length. It cannot start or end with a period \(.\) or a hyphen \(-\). It cannot contain consecutive periods \(.\) or hyphens \(-\).

 For Windows-based instances, the hostname must be 2 to 15 characters in length and can contain letters, digits, and hyphens \(-\). It cannot contain periods \(.\) and cannot be composed of only digits.

 For Linux-based instances, the hostname must be 2 to 30 characters in length and can contain letters, digits, hyphens \(-\), and periods \(.\). Use periods \(.\) to separate a name into multiple segments.

 Hostnames for created ECS instances must be in the name\_prefix\[begin\_number,bits\]name\_suffix format.

 The name\_prefix parameter specifies the prefix of each hostname. This parameter is required.

 The \[begin\_number,bits\] parameter specifies the part of a hostname that distinguishes a created instance from others. The begin\_number parameter specifies the number from which to start incrementing hostnames. The bits parameter specifies the number of digits in the number for each hostname.

 The name\_suffix parameter specifies the suffix of each hostname. This parameter is optional.

 When specifying the \[begin\_number,bits\] parameter, you must pay attention to the following rules: Do not place spaces between the begin\_number and bits parameters.

 The value of bits can range from 1 to 6.

 The value of begin\_number can range from 0 to 999999.

 If you specify the begin\_number parameter without specifying the bits parameter, bits is set to 6.

 If neither the begin\_number parameter nor the bits parameter is specified, begin\_number is set to 0 and bits is set to 6.

 If the number of digits for begin\_number is greater than the specified value of bits, the specified value of bits will be overridden by the number of digits in the specified value of begin\_number. For example, if \[begin\_number,bits\] is set to \[123456,1\], the value of bits will be overridden by the number of digits in the specified value of begin\_number, which in this case is 6.

 |
|AllocatePublicIP|Boolean|No|No|Specifies whether the system allocates a public IP address to an ECS instance. If the InternetMaxBandwidthOut parameter is set to 0, no public IP addresses will be allocated.|Default value: true|
|AutoReleaseTime|String|No|No|The time scheduled for created ECS instances to be automatically released.|Specify the time in the ISO 8601 standard in the yyyy-MM-ddTHH:mm:ssZ format. The specified release time must be within three years of the current time.|
|PrivateIpAddress|String|No|No|The private IP address of an ECS instance in a VPC. The specified IP address must not be in use by other instances in the VPC.|None|
|DiskMappings|List|No|No|The data disks to be attached to created ECS instances.|None|
|InternetChargeType|String|No|No|The billing method for Internet traffic.| Valid values: PayByBandwidth and PayByTraffic

 Default value: PayByTraffic

 |
|InternetMaxBandwidthIn|Integer|No|No|The maximum inbound bandwidth from the Internet. Unit: Mbit/s.|Valid values: 1 to 100. Default value: 100.|
|InternetMaxBandwidthOut|Integer|No|No|The maximum outbound bandwidth to the Internet. Unit: Mbit/s.|Valid values in PayByBandwidth mode: 0 to 200. Default value: 0. Valid values in PayByTraffic mode: 1 to 200. If you choose to use the PayByTraffic mode, you must specify this parameter.|
|IoOptimized|String|No|No|Specifies whether created ECS instances are I/O optimized.| Valid values: none \(non-I/O optimized\) and optimized \(I/O optimized\)

 Default value: none

 |
|SystemDiskCategory|String|No|No|The system disk type of created instances.|Valid values: cloud, cloud\_efficiency, cloud\_ssd, and ephemeral\_ssd|
|SystemDiskDescription|String|No|No|The system disk description of created instances.|None|
|SystemDiskDiskName|String|No|No|The system disk name of created instances.|None|
|SystemDiskSize|Number|No|Yes|The system disk size of created instances. Unit: GB.|Valid values: 40 to 500. If a custom image is used to create a system disk, make sure that the size of the system disk is greater than that of the custom image.|
|Tags|List|No|No|The custom tags of created instances.|For each ECS instance, a maximum of 20 tags can be specified in the \[\{"Key":"tagKey","Value":"tagValue"\},\{"Key":"tagKey2","Value":"tagValue2"\}\] format.|
|UserData|String|No|No|The user data you provide when you create an ECS instance.|The user data can be up to 16 KB in size. You must convert the data into Base64-encoded strings. If the data contains special characters, add a backslash \(\\\) immediately before each special character.|
|ZoneId|String|No|No|The ID of the zone where created instances reside.|None|
|VpcId|String|No|No|The ID of the VPC to which created instances belong.|None|
|VSwitchId|String|No|No|The ID of the VSwitch for created instances.|None|
|KeyPairName|String|No|No|The name of the key pair used to connect to created ECS instances. For Windows-based ECS instances, this parameter is ignored and is empty by default. For Linux-based ECS instances, the Password parameter will still take effect if the KeyPairName parameter is specified. However, logon by password is disabled, and the KeyPairName value is used.|None|
|RamRoleName|String|No|No|The name of the RAM role assigned to created instances.|You can call the ListRoles operation to query the role name. For more information, see [CreateRole](https://partners-intl.aliyun.com/help/doc-detail/28710.htm) and [ListRoles](https://partners-intl.aliyun.com/help/doc-detail/28713.htm).|
|SpotPriceLimit|String|No|No|The maximum hourly price of created instances.|This parameter is only valid when SpotStrategy is set to SpotWithPriceLimit. A maximum of three decimal places can be specified.|
|SpotStrategy|String|No|No|The spot strategy for pay-as-you-go instances.|This parameter is only valid when InstanceChargeType is set to PostPaid. Valid values:

 NoSpot: specifies a regular pay-as-you-go instance.

 SpotWithPriceLimit: specifies a pay-as-you-go instance with a maximum hourly price.

 SpotAsPriceGo: specifies a pay-as-you-go instance priced at the market price at the time of purchase.

 Default value: NoSpot

 |
|DedicatedHostId|String|No|No|The ID of the dedicated host for created instances.|None|
|LaunchTemplateName|String|No|No|The name of the launch template for created instances.|None|
|PeriodUnit|String|No|No|The unit of billing cycle for created instances. When the PeriodUnit parameter is set to Week:

 -   Valid values for the Period parameter: 1, 2, 3, and 4
-   Valid values for the AutoRenewPeriod parameter: 1, 2, and 3

 When the PeriodUnit parameter is set to Month: -   Valid values for the Period parameter: 1, 2, 3, 4, 5, 6, 7, 8, 9, 12, 24, 36, 48, and 60
-   Valid values for the AutoRenewPeriod parameter: 1, 2, 3, 6, and 12

 | Valid values: Week and Month

 Default value: Month

 |
|AutoRenewPeriod|Number|No|Yes|The automatic subscription renewal period for created instances. This parameter is required when AutoRenew is set to True.| Valid values: 1, 2, 3, 6, and 12

 Default value: 1

 |
|AutoRenew|String|No|Yes|Specifies whether to enable automatic renewal for created instances. Default value: False. This parameter is only valid when InstanceChargeType is set to PrePaid.|Valid values: -   True: specifies to enable automatic renewal for created instances.
-   False: specifies to disable automatic renewal for created instances.

 |
|InstanceChargeType|String|No|Yes|The billing method of created instances. Default value: PostPaid.|Valid values: -   PrePaid: specifies the subscription billing method, in which services are billed on a monthly or yearly basis. You must ensure that the balance of your account or credit balance can cover the cost of the subscription. Otherwise, you will receive an `InvalidPayMethod` error code.
-   PostPaid: specifies the pay-as-you-go billing method, in which services are billed by the amount of resources that you actually use.

 |
|EniMappings|List|No|Yes|The elastic network interfaces \(ENIs\) to be attached to created instances.|Only one ENI can be attached to an instance.|
|LaunchTemplateId|String|No|Yes|The ID of the launch template from which to create instances.|None|
|LaunchTemplateVersion|String|No|Yes|The version of the specified launch template. If you do not specify a version, the default version is used.|None|
|Period|Number|No|Yes|The subscription period of created instances. Unit: months. This parameter is only required when InstanceChargeType is set to PrePaid. If the DedicatedHostId parameter is specified, the subscription period of the instance must be shorter than that of the dedicated host.|Valid values: -   Valid values for the Period parameter in the case of `PeriodUnit=Week`: 1, 2, 3, and 4
-   Valid values for the Period parameter in the case of `PeriodUnit=Month`: 1, 2, 3, 4, 5, 6, 7, 8, 9, 12, 24, 36, 48, and 60

 |
|NetworkType|String|No|No|The network type of created ECS instances.| Valid values: vpc and classic

 Default value: classic

 |
|DeletionProtection|Boolean|No|No|The release protection property of created ECS instances. It specifies whether the instances can be released from the ECS console or through the DeleteInstance API operation.|Valid values: true and false|
|DeploymentSetId|String|No|Yes|The ID of the deployment set used to create ECS instances.|None|

## DiskMappings syntax {#section_tjh_kal_k6c .section}

``` {#codeblock_uoz_vdu_2d5 .language-json}
"DiskMappings": [
  {
    "Category": String,
    "DiskName": String,
    "Description": String,
    "Device": String,
    "SnapshotId": String,
    "Size": String,
    "Encrypted": String,
    "KMSKeyId": String
  }
]
```

## DiskMappings properties {#section_39d_e40_xo6 .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Size|String|Yes|No|The size of a data disk to be attached to a created instance. Unit: GB.|None|
|Category|String|No|No|The type of a data disk to be attached to a created instance.|Valid values: cloud, cloud\_efficiency, cloud\_ssd, and ephemeral\_ssd|
|DiskName|String|No|No|The name of a data disk to be attached to a created instance.|The name can be up to 128 characters in length and can contain letters, digits, underscores \(\_\), periods \(.\), and hyphens \(-\).|
|Description|String|No|No|The description of a data disk to be attached to a created instance.|The description must be 2 to 256 characters in length and cannot start with http:// or https://.|
|Device|String|No|No|The device name of a data disk to be attached to a created instance.|The system allocates a device name in the alphabetical order from /dev/xvda to /dev/xvdz by default.|
|SnapshotId|String|No|No|The ID of the snapshot used to create a data disk.|None|
|Encrypted|String|No|No|Specifies whether to encrypt a data disk.|Default value: false|
|KMSKeyId|String|No|No|The ID of the KMS key corresponding to a data disk.|None|

## Tags syntax {#section_yw8_jqs_gx1 .section}

``` {#codeblock_ha2_frx_24k .language-json}
"Tags": [
  {
    "Value": String,
    "Key": String
  }
]
```

## Tags properties {#section_qf5_2mx_o68 .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Key|String|Yes|No|None|None|
|Value|String|No|No|None|None|

## Response parameters {#section_ijt_fr2_lfb .section}

**Fn::GetAtt**

-   InstanceIds: the IDs of instances in the ECS instance group. An ID is a system-generated globally unique identifier \(GUID\) for an instance.
-   PrivateIps: the list of private IP addresses of VPC-connected instances. This parameter is only valid when the NetworkType parameter is set to VPC. The list is a JSON array, containing up to 100 IP addresses separated by commas \(,\). Example: \["172.16.XX.XX", "172.16. XX.XX", ... "172.16. XX.XX"\].
-   InnerIps: the list of private IP addresses of classic network-connected instances. This parameter is only valid when the NetworkType parameter is set to Classic. The list is a JSON array, containing up to 100 IP addresses separated by commas \(,\). Example: \["10.1.XX.XX", "10.1. XX.XX", ... "10.1. XX.XX"\].
-   PublicIps: the list of public IP addresses of classic network-connected instances. This parameter is only valid when the NetworkType parameter is set to Classic. The list is a JSON array, containing up to 100 IP addresses separated by commas \(,\). Example: \["42.1.XX.XX", "42.1. XX.XX", ... "42.1. XX.XX"\].
-   HostNames: the list of hostnames of all instances. The list is a formatted JSON array. Example: \["host1", "host2", ... "host3"\].
-   OrderId: the list of order IDs of all instances.
-   ZoneId: the ID of the zone where created instances reside.
-   RelatedOrderIds: the list of related order IDs of created ECS instances.

## Examples {#section_ygv_fr2_lfb .section}

``` {#codeblock_cpe_djk_cf3 .language-json}
{
  "ROSTemplateFormatVersion":"2015-09-01",
  "Resources":{
    "WebServer": {
      "Type": "ALIYUN::ECS::InstanceGroup",
      "Properties": {
        "ImageId":"m-25l0r****",
        "InstanceType": "ecs.t1.small",
        "SecurityGroupId": "sg-25zwc****",
        "ZoneId": "cn-beijing-b",
        "MaxAmount":1,
        "MinAmount":1,
        "Tags": [{
            "Key": "tiantt",
            "Value": "ros"
        },{
            "Key": "tiantt1",
            "Value": "ros1"
        }
        ]
      }
    }
  },
  "Outputs": {
    "InstanceIds": {
         "Value":{"get_attr": ["WebServer","InstanceIds"]}
    },
    "PublicIps": {
         "Value":{"get_attr": ["WebServer","PublicIps"]}
    }
  }
}
```

