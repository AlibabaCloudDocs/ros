# ALIYUN::ECS::InstanceGroupClone {#concept_48289_zh .concept}

ALIYUN::ECS::InstanceGroupClone is used to clone an ECS instance group.

## Syntax {#section_zvw_gt2_lfb .section}

```language-json
{
  "Type": "ALIYUN::ECS::InstanceGroupClone",
  "Properties": {
    "SourceInstanceId": String,
    "MaxAmount": Integer,
    "MinAmount": Integer,
    "BackendServerWeight": Integer,
    "LoadBalancerIdToAttach": String,
    "SecurityGroupId": String,
    "ImageId": String,
    "InstanceName": String,
    "Description": String,
    "Password": String,
    "ZoneId": String,
    "InternetMaxBandwidthOut": Integer,
    "AutoReleaseTime": String,
    "DiskMappings": List,
    "Tags": List,
    "KeyPairName": String，
    "RamRoleName": String,
    "SpotPriceLimit": String,
    "SpotStrategy": String，
    "DeletionProtection": Boolean
  }
}
```

## Properties {#section_et2_ft2_lfb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|SourceInstanceId|String|Yes|No|The ID of the ECS instance to be cloned.|The clone operation clones the specified instance, including its instance type, image, bandwidth billing method, bandwidth limit, and network type. If the source ECS instance belongs to multiple security groups, the cloned instance is added only to the first of these security groups.|
|MaxAmount|Integer|Yes|Yes|The maximum number of ECS instances to be created.|Valid values: 1 to 100. The MaxAmount parameter must be set to a value greater than or equal to the value of MinAmount.|
|MinAmount|String|Yes|Yes|The minimum number of ECS instances to be created.|Valid values: 1 to 100. The MinAmount parameter must be set to a value less than or equal to the value of MaxAmount.|
|BackendServerWeight|Integer|No|No|The weight assigned to an ECS instance by the Server Load Balancer \(SLB\) instance.|Valid values: 0 to 100. Default value: 100.|
|LoadBalancerIdToAttach|String|No|No|The ID of the SLB instance to which an ECS instance is to be attached.|None|
|Description|String|No|No|The description of an ECS instance.|The description must be 1 to 256 characters in length.|
|ImageId|String|No|Yes|The ID of the image used to start an ECS instance. You can use public images, custom images, and Alibaba Cloud Marketplace images.|For more information, see [Public images for ECS instances](https://ros.console.aliyun.com/#/product/cn-hangzhou/list/imageList). You can specify part of a public image, without having to provide the complete information. When editing a template used to deploy an ECS instance, you can specify the image type and version or only the image type. ROS automatically selects an appropriate public image ID. You can use the wildcard character \(\*\) to represent part of an image ID. Take all Ubuntu public images provided by Alibaba Cloud as an example:

ubuntu\_14\_0405\_32\_40G\_alibase\_20170711.vhd

ubuntu\_14\_0405\_64\_20G\_alibase\_20170824.vhd

ubuntu\_16\_0402\_32\_40G\_alibase\_20170711.vhd

ubuntu\_16\_0402\_64\_20G\_alibase\_20170818.vhd

You can use one of the following methods to specify the public image ID for the ECS instance:

If you enter ubuntu,

the system matches it with the following ID: ubuntu16\_0402\_64\_20G\_alibase\_20170818.vhd

If you enter ubuntu\_14,

the system matches it with the following ID: ubuntu\_14\_0405\_64\_20G\_alibase\_20170824.vhd

If you enter ubuntu1432,

the system matches it with the following ID: ubuntu\_14\_0405\_32\_40G\_alibase\_20170711.vhd

If you enter ubuntu\_16\_0402\_32,

the system matches it with the following ID: ubuntu\_16\_0402\_32\_40G\_alibase\_20170711.vhd

 |
|InternetMaxBandwidthOut|Integer|No|No|The maximum outbound bandwidth to the Internet. Unit: Mbit/s.|Valid values in PayByBandwidth mode: 0 to 200. Default value: 0. Valid values in PayByTraffic mode: 1 to 200. You must specify this parameter if you choose to use the PayByTraffic mode.|
|SecurityGroupId|String|No|No|The ID of the security group to which a created instance belongs.|None|
|InstanceName|String|No|No|The name of an instance.|The name must be 1 to 128 characters in length and can contain letters, digits, underscores \(\_\), periods \(.\), and hyphens \(-\).|
|Password|String|No|No|The password used to log on to an ECS instance.|The password must be 8 to 30 characters in length. It must contain letters, digits, and special characters. The following special characters are allowed: parentheses \(\(\)\), apostrophes \('\), tildes \(~\), exclamation points \(!\), at signs \(@\), number signs \(\#\), dollar signs \($\), percent signs \(%\), caret signs \(^\), ampersands \(&\), asterisks \(\*\), minus signs \(-\), plus signs \(+\), equal signs \(=\), vertical bars \(|\), braces \(\{ \}\), brackets \(\[ \]\), colons \(:\), semicolons \(;\), angle brackets \(< \>\), commas \(,\), periods \(.\), question marks \(?\), and forward slashes \(/\). If you specify the Password parameter in the API request, use HTTPS to secure the API and protect your password.|
|DiskMappings|List|No|No|The list of disks to be attached to an ECS instance.|A maximum of four disks can be attached.|
|Tags|List|No|No|The custom tags.|A maximum of four tags are supported. The format is \[\{"Key":"tagKey","Value":"tagValue"\}, \{"Key":"tagKey2","Value":"tagValue2"\}\].|
|ZoneId|String|No|No|The ID of the zone where an ECS instance resides.|None|
|KeyPairName|String|No|No|The name of the key pair that is used to connect to an ECS instance. For Windows-based instances, this parameter is inapplicable and is empty by default. For Linux-based instances, the Password parameter still takes effect if this parameter is specified. However, logon by password is disabled, and the KeyPairName value is used.|None|
|RamRoleName|String|No|No|The RAM role name of an instance.|You can call the ListRoles operation to query the role name. For more information, see [CreateRole](https://partners-intl.aliyun.com/help/doc-detail/28710.htm) and [ListRoles](https://partners-intl.aliyun.com/help/doc-detail/28713.htm).|
|SpotPriceLimit|String|No|No|The maximum hourly price of an instance.|Three decimal places are allowed at most. This parameter is applicable only when SpotStrategy is set to SpotWithPriceLimit.|
|SpotStrategy|String|No|No|The spot strategy for a Pay-As-You-Go instance.|This parameter is applicable only when InstanceChargeType is set to PostPaid. Valid values:

NoSpot: indicates a regular Pay-As-You-Go instance.

SpotWithPriceLimit: indicates a Pay-As-You-Go instance with the maximum hourly price.

SpotAsPriceGo: indicates that the system automatically offers a spot hourly price for an instance based on the supply-demand statistics. The spot price is limited to the cost of resources you actually use.

Default value: NoSpot.

 |
|SystemDiskDiskName|String|No|Yes|The name of a system disk. The name must be 2 to 128 characters in length and can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). It must start with a letter but cannot start with http:// or https://. This parameter is empty by default.|None|
|PeriodUnit|String|No|Yes|The unit of the billing cycle.When the PeriodUnit parameter is set to Week:

-   Valid values for the Period parameter: 1, 2, 3, and 4.
-   Valid values for the AutoRenewPeriod parameter: 1, 2, and 3.

When the PeriodUnit parameter is set to Month:-   Valid values for the Period parameter: 1, 2, 3, 4, 5, 6, 7, 8, 9, 12, 24, 36, 48, and 60.
-   Valid values for the AutoRenewPeriod parameter: 1, 2, 3, 6, and 12.

| Valid values: Week and Month.

 Default value: Month.

 |
|AutoRenewPeriod|Number|No|Yes|The period your subscription is automatically extended by after an instance expires. This parameter is required when AutoRenew is set to True.| Valid values: 1, 2, 3, 6, and 12.

 Default value: 1.

 |
|AutoRenew|String|No|Yes|Indicates whether to enable automatic renewal for an instance. Default value: False. This parameter is applicable only when InstanceChargeType is set to PrePaid.|Valid values:-   True: indicates that automatic renewal is enabled for an instance.
-   False: indicates that automatic renewal is disabled for an instance.

|
|EniMappings|List|No|Yes|The elastic network interfaces \(ENIs\) attached to instances.|Only one ENI can be attached to an instance.|
|AutoReleaseTime|String|No|No|The time scheduled for an instance to be automatically released. It uses UTC and complies with the [ISO8601](https://partners-intl.aliyun.com/help/doc-detail/25696.htm) standard. The format is yyyy-MM-ddTHH:mm:ssZ.-   If the value of seconds \(ss\) is not 00, it is automatically set to the start time of the current minute \(mm\).
-   The minimum release time must be at least 30 minutes after the current time.
-   The maximum release time must be within 3 years from the current time.

 If you do not set AutoReleaseTime, automatic release is disabled for the ECS instance.|None|
|SystemDiskCategory|String|No|Yes|The type of the system disk.|Valid values:-   cloud: indicates a basic disk.
-   cloud\_efficiency: indicates an ultra disk.
-   cloud\_ssd: indicates an SSD.
-   ephemeral\_ssd: indicates a local SSD.
-   cloud\_essd: indicates an ESSD. You can only purchase the beta version of ESSD in selected zones because the product is not officially released. For more information, see [FAQs about ESSDs](https://partners-intl.aliyun.com/help/faq-detail/64950.htm#AvailableRegion).

Default value for [Retired instance types](https://www.alibabacloud.com/help/faq-detail/55263.htm) that are not I/O-optimized: cloud. Default value for other instances: cloud\_efficiency.|
|LaunchTemplateName|String|No|Yes|The name of the launch template for an instance.|None|
|LaunchTemplateVersion|String|No|Yes|The version of the launch template. If you do not specify a version, the default version is used.|None|
|InternetMaxBandwidthIn|Integer|No|No|The maximum inbound bandwidth from the Internet. Unit: Mbit/s.| Valid values: 1 to 200.

 Default value: 200.

 |
|LaunchTemplateId|String|No|Yes|The ID of the launch template.|None|
|SystemDiskDescription|String|No|Yes|The description of the system disk. The description must be 2 to 256 characters in length. It cannot start with http:// or https://. This parameter is empty by default.|None|
|DeletionProtection|Boolean|No|No|The release protection property of an instance. It indicates whether you can use the ECS console or call the DeleteInstance operation to release the instance.|Valid values: true and false.|

## DiskMappings syntax { .section}

```language-json
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

## DiskMappings properties { .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Size|String|Yes|No|The size of a data disk. Unit: GB.|None|
|Category|String|No|No|The type of the data disk.|Valid values: cloud, cloud\_efficiency, cloud\_ssd, and ephemeral\_ssd.|
|DiskName|String|No|No|The name of the data disk.|The name must be 1 to 128 characters in length and can contain letters, digits, underscores \(\_\), periods \(.\), and hyphens \(-\).|
|Description|String|No|No|The description of the data disk.|The description must be 2 to 256 characters in length. This parameter is empty by default.|
|Device|String|No|No|The device name of the data disk to be attached to an ECS instance.|For example, /dev/xvd\[a-z\].|
|SnapshotId|String|No|No|The ID of the snapshot used to create the data disk.|None|

## Tags syntax { .section}

```language-json
"Tags": [
  {
    "Value": String,
    "Key": String
  }
]
```

## Tags properties { .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Key|String|Yes|No|None|None|
|Value|String|No|No|None|None|

## Response parameters { .section}

**Fn::GetAtt**

-   InstanceIds: the IDs of instances in an instance group. An ID is a system-generated globally unique identifier \(GUID\) for each instance.
-   PrivateIps: the list of private IP addresses of instances in a VPC. This parameter is applicable only when the NetworkType parameter is set to VPC. The list is a formatted JSON array, containing up to 100 IP addresses that are separated by commas \(,\). For example, \["172.16. XX.XX", "172.16. XX.XX", … "172.16. XX.XX"\].
-   InnerIps: the list of private IP addresses of instances in a classic network. This parameter is applicable only when the NetworkType parameter is set to Classic. The list is a formatted JSON array, containing up to 100 IP addresses that are separated by commas \(,\). For example, \["10.1. XX.XX", "10.1. XX.XX", … "10.1. XX.XX"\].
-   PublicIps: the list of public IP addresses of instances in a classic network. This parameter is applicable only when the NetworkType parameter is set is Classic. The list is a formatted JSON array, containing up to 100 IP addresses that are separated by commas \(,\). For example, \["42.1. XX.XX", "42.1. XX.XX", … "42.1. XX.XX"\].
-   ZoneId: the ID of the zone where an instance resides.
-   HostNames: the list of hostnames of all instances. The list is a formatted JSON array. For example, \["host1", "host2", … "host3"\].

## Examples { .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "WebServer": {
      "Type": "ALIYUN::ECS::InstanceGroupClone",
      "Properties": {
        "SourceInstanceId": "i-25zsk****",
        "ImageId": "m-25l0r****",
        "SecurityGroupId": "sg-25zwc****",
        "ZoneId": "cn-beijing-b",
        "MaxAmount": 1,
        "MinAmount": 1
      }
    }
  },
  "Outputs": {
    "InstanceIds": {
      "Value": {"get_attr": ["WebServer","InstanceIds"]}
    },
    "PublicIps": {
      "Value": {"get_attr": ["WebServer","PublicIps"]}
    }
  }
}
```

