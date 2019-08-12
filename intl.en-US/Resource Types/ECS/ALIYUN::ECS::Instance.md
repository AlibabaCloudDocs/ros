# ALIYUN::ECS::Instance {#concept_51198_zh .concept}

ALIYUN::ECS::Instance is used to create an ECS instance.

## Syntax {#section_ljn_3d2_lfb .section}

``` {#codeblock_zfi_624_1ju .language-json}
{
  "Type": "ALIYUN::ECS::Instance",
  "Properties": {
    "DiskMappings": List,
    "IoOptimized": String,
    "InternetChargeType": String,
    "PrivateIpAddress": String,
    "SystemDiskDiskName": String,
    "VpcId": String,
    "Description": String,
    "Tags": List,
    "HostName": String,
    "ImageId": String,
    "InstanceChargeType": String,
    "VSwitchId": String,
    "Password": String,
    "InstanceType": String,
    "SystemDiskCategory": String,
    "SystemDiskSize": Number,
    "ZoneId": String,
    "InternetMaxBandwidthOut": Integer,
    "InstanceName": String,
    "InternetMaxBandwidthIn": Integer,
    "UserData": String,
    "SecurityGroupId": String,
    "Period": Number,
    "AllocatePublicIP": Boolean,
    "SystemDiskDescription": String,
    "KeyPairName": String,
    "RamRoleName": String,
    "SpotPriceLimit": String,
    "SpotStrategy": String,
    "DeletionProtection": Boolean,
    "DeploymentSetId": String
  }
}
			
```

## Properties {#section_atw_kd2_lfb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|ImageId|String|Yes|Yes|The ID of the image used to start the ECS instance. You can use a public image, custom image, or Alibaba Cloud Marketplace image.| When editing a template, you can specify either the image type and version or only the image type. ROS automatically selects an appropriate public image ID.

 You can use the wildcard character \(\*\) to represent part of an image ID.

 Take the Ubuntu public images provided by Alibaba Cloud as an example. You can use one of the following methods to specify the public image ID for the ECS instance:

 If you enter ubuntu,

 the system matches it with the following ID: ubuntu16\_0402\_64\_20G\_alibase\_20170818.vhd

 If you enter ubuntu\_14,

 the system matches it with the following ID: ubuntu\_14\_0405\_64\_20G\_alibase\_20170824.vhd

 If you enter ubuntu\*14\*32,

 the system matches it with the following ID: ubuntu\_14\_0405\_32\_40G\_alibase\_20170711.vhd

 If you enter ubuntu\_16\_0402\_32,

 the system matches it with the following ID: ubuntu\_16\_0402\_32\_40G\_alibase\_20170711.vhd

 |
|InstanceType|String|Yes|No|The type of the ECS instance. For more information, see [Instance type families](https://partners-intl.aliyun.com/help/doc-detail/25378.htm).|None|
|SecurityGroupId|String|Yes|No|The ID of the security group to which the created instance will belong.|None|
|Description|String|No|No|The description of the ECS instance.|The description can be up to 256 characters in length.|
|InstanceName|String|No|No|The name of the ECS instance.|The name can be up to 128 characters in length and can contain letters, digits, underscores \(\_\), periods \(.\), and hyphens \(-\).|
|Password|String|No|No|The password used to log on to the ECS instance.| The password must be 8 to 30 characters in length.

 It must contain letters, digits, and special characters.

 The following special characters are allowed: \( \) ' ~ ! @ \# $ % ^ & \* - + = | \{ \} \[ \] : ; ‘ < \> , . ? / - If you specify the Password parameter in the API request, use HTTPS to secure the API and protect your password.

 |
|HostName|String|No|No|The hostname of the ECS instance.| The hostname must be at least 2 characters in length.

 It cannot start or end with a period \(.\) or a hyphen \(-\). It cannot contain consecutive periods \(.\) or hyphens \(-\).

 For Windows-based instances, the hostname must be 2 to 15 characters in length and can contain letters, digits, and hyphens \(-\). It cannot contain periods \(.\) and cannot be composed of only digits.

 For Linux-based instances, the hostname must be 2 to 30 characters in length and can contain letters, digits, hyphens \(-\), and periods \(.\). You can use periods \(.\) to separate a name into multiple segments.

 |
|AllocatePublicIP|Boolean|No|No|Specifies whether the system allocates a public IP address to the instance. If InternetMaxBandwidthOut is set to 0, no public IP addresses will be allocated.|Default value: true|
|PrivateIpAddress|String|No|No|The private IP address of an instance in a VPC. The specified IP address must not be used by other instances in the VPC.|None|
|InternetChargeType|String|No|No|The billing method for Internet traffic.| Valid values: PayByBandwidth and PayByTraffic

 Default value: PayByTraffic

 |
|InternetMaxBandwidthIn|Integer|No|No|The maximum inbound bandwidth from the Internet. Unit: Mbit/s.|Valid values: 1 to 100. Default value: 100.|
|InternetMaxBandwidthOut|Integer|No|No|The maximum outbound bandwidth to the Internet. Unit: Mbit/s.| Valid values in PayByBandwidth mode: 0 to 200. Default value: 0.

 Valid values in PayByTraffic mode: 1 to 200. If you choose to use the PayByTraffic mode, you must specify this parameter.

 |
|IoOptimized|String|No|No|Specifies whether the created instance is I/O optimized.|Valid values: none \(non-I/O optimized\) and optimized \(I/O optimized\). Default value: none.|
|DiskMappings|List|No|No|The data disks to be attached to the ECS instance.|A maximum of 16 data disks can be attached.|
|SystemDiskCategory|String|No|No|The type of the ECS instance system disk.|Valid values: cloud, cloud\_efficiency, cloud\_ssd, and ephemeral\_ssd|
|SystemDiskDescription|String|No|No|The description of the ECS instance system disk.|None|
|SystemDiskDiskName|String|No|No|The name of the ECS instance system disk.|None|
|SystemDiskSize|Number|No|Yes|The size of the ECS instance system disk. Unit: GB.| Valid values: 40 to 500.

 If a custom image is used to create a system disk, make sure that the size of the system disk is greater than that of the custom image.

 |
|Tags|List|No|No|The custom tags of the ECS instance.|A maximum of 20 tags can be specified in the \[\{"Key":"tagKey","Value":"tagValue"\}, \{"Key":"tagKey2","Value":"tagValue2"\}\] format.|
|UserData|String|No|No|The user data you provide when you create the ECS instance.|The user data can be up to 16 KB in size. You must convert the data into Base64-encoded strings. If the data contains special characters, add a backslash \(\\\) immediately before each special character.|
|ZoneId|String|No|No|The ID of the zone where the ECS instance resides.|None|
|VpcId|String|No|No|The ID of the VPC to which the ECS instance will belong.|None|
|VSwitchId|String|No|No|The ID of the VSwitch for the ECS instance.|None|
|InstanceChargeType|String|No|No|The billing method of the ECS instance.| Valid values: PrePaid and PostPaid

 Default value: PostPaid. If you set this parameter to PrePaid, make sure you have sufficient balance in your account. Otherwise, the instance will fail to be created.

 |
|Period|Number|No|No|The subscription period of the ECS instance. This parameter must be set when the InstanceChargeType parameter is set to PrePaid. This parameter is ignored when the InstanceChargeType parameter is set to PostPaid.|Valid values: 1, 2, 3, 4, 5, 6, 7, 8, 9, 12, 24, and 36. Unit: months.|
|KeyPairName|String|No|No|The name of the key pair that is used to connect to the ECS instance.| For Windows-based instances, this parameter is empty by default.

 For Linux-based ECS instances, the Password parameter will still take effect if the KeyPairName parameter is specified. However, logon by password is disabled, and the KeyPairName value is used.

 |
|RamRoleName|String|No|No|The RAM role name of the instance. You can call the ListRoles API to query the role name. For more information, see [CreateRole](https://partners-intl.aliyun.com/help/doc-detail/28710.htm) and [ListRoles](https://partners-intl.aliyun.com/help/doc-detail/28713.htm).|None|
|SpotPriceLimit|String|No|No|The maximum hourly price of the instance.|This parameter is only valid when the `SpotStrategy` parameter is set to SpotWithPriceLimit. A maximum of three decimal places can be specified.|
|SpotStrategy|String|No|No|The spot strategy for a pay-as-you-go instance.|This parameter is only valid when the `InstanceChargeType` parameter is set to PostPaid. Valid values: NoSpot: specifies a regular pay-as-you-go instance.

 SpotWithPriceLimit: specifies a pay-as-you-go instance with a maximum hourly price.

 SpotAsPriceGo: specifies a pay-as-you-go instance priced at the market price at the time of purchase.

 Default value: NoSpot

 |
|DedicatedHostId|String|No|No| The ID of the dedicated host \(DDH\) for the ECS instance. You can use the API to query the list of DDH IDs.

 After you set the DedicatedHostId parameter, the system automatically ignores the SpotStrategy and SpotPriceLimit settings in the request. This is because you cannot create preemptible instances on DDHs.

 |None|
|PeriodUnit|String|No|No|The unit of billing cycle for the ECS instance. When the PeriodUnit parameter is set to Week:

 -   Valid values for the Period parameter: 1, 2, 3, and 4
-   Valid values for the AutoRenewPeriod parameter: 1, 2, and 3

 When the PeriodUnit parameter is set to Month: -   Valid values for the Period parameter: 1, 2, 3, 4, 5, 6, 7, 8, 9, 12, 24, 36, 48, and 60
-   Valid values for the AutoRenewPeriod parameter: 1, 2, 3, 6, and 12

 Default value: Month|Valid values: Week and Month. Default value: Month.|
|AutoRenewPeriod|Number|No|No|The automatic subscription renewal period for the ECS instance. This parameter is required when AutoRenew is set to True. Valid values: 1, 2, 3, 6, and 12.|Valid values: 1, 2, 3, 6, and 12|
|AutoRenew|String|No|No|Specifies whether to enable automatic renewal for the ECS instance. Default value: False. This parameter is only valid when InstanceChargeType is set to PrePaid.|Valid values: -   True: specifies to enable automatic renewal for the instance.
-   False: specifies to disable automatic renewal for the instance.

 |
|DeletionProtection|Boolean|No|No|The release protection property of the instance. It specifies whether the instance can be released from the ECS console or through the DeleteInstance API.|Valid values: true and false|
|DeploymentSetId|String|No|Yes|The ID of the deployment set used to create the ECS instance.|None|

## DiskMappings syntax {#section_3b8_74v_45b .section}

``` {#codeblock_0yd_jyo_omg .language-json}
"DiskMappings": [
  {
    "Category": String,
    "DiskName": String,
    "Description": String,
    "Device": String,
    "SnapshotId": String,
    "Size": String
  }
]
```

## DiskMappings properties {#section_8il_fs8_t3z .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Size|String|Yes|No|The size of a data disk. Unit: GB.|None|
|Category|String|No|No|The type of a data disk.| Valid values: cloud, cloud\_efficiency, cloud\_ssd, and ephemeral\_ssd

 Default value: cloud

 |
|DiskName|String|No|No|The name of a data disk.|The name can be up to 128 characters in length and can contain letters, digits, underscores \(\_\), periods \(.\), and hyphens \(-\).|
|Description|String|No|No|The description of a data disk.|The description must be 2 to 256 characters in length. Default value: null.|
|Device|String|No|No|The device name of a data disk to be attached to the instance.|If you do not set this parameter, the system allocates a device name in alphabetical order from /dev/xvdb to /dev/xvdz.|
|SnapshotId|String|No|No|The ID of the snapshot used to create a data disk.|None|

## Tags syntax {#section_gff_lrv_g26 .section}

``` {#codeblock_4cc_u4e_0rm .language-json}
"Tags": [
  {
    "Value": String,
    "Key": String
  }
]
```

## Tags properties {#section_fes_3kc_798 .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Key|String|Yes|No|None|None|
|Value|String|No|No|None|None|

## Response parameters {#section_dx4_222_lfb .section}

**Fn::GetAtt**

-   InstanceId: the ID of the instance. The instance ID is a globally unique identifier \(GUID\) generated by the system for the instance.
-   PrivateIp: the private IP address of the VPC-connected instance. This parameter is only valid when the `NetworkType` parameter is set to VPC.
-   InnerIp: the private IP address of the classic network-connected instance. This parameter is only valid when the `NetworkType` parameter is set to Classic.
-   PublicIp: the list of public IP addresses of the classic network-connected instance. This parameter is only valid when the `NetworkType` parameter is set to Classic.
-   ZoneId: the ID of the zone where the instance resides.
-   HostName: the hostname of the instance.

## Examples {#section_z3v_222_lfb .section}

``` {#codeblock_11v_7g5_g53 .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "WebServer": {
      "Type": "ALIYUN::ECS::Instance",
      "Properties": {
        "ImageId": "m-25l0rc****",
        "InstanceType": "ecs.t1.small",
        "SecurityGroupId": "sg-25zwc****",
        "ZoneId": "cn-beijing-b",
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
    "InstanceId": {
         "Value": {"get_attr": ["WebServer","InstanceId"]}
    },
    "PublicIp": {
         "Value": {"get_attr": ["WebServer","PublicIp"]}
    }
  }
}
```

