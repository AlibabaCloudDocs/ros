# ALIYUN::ECS::InstanceClone {#concept_48279_zh .concept}

ALIYUN::ECS::InstanceClone is used to clone an ECS instance.

## Syntax {#section_c7m_w5j_7j1 .section}

``` {#codeblock_xir_uvn_n12 .language-json}
{
  "Type": "ALIYUN::ECS::InstanceClone",
  "Properties": {
    "SourceInstanceId": String,
    "BackendServerWeight": Integer,
    "LoadBalancerIdToAttach": String,
    "SecurityGroupId": String,
    "ImageId": String,
    "InstanceName": String,
    "Description": String,
    "Password": String,
    "ZoneId": String,
    "DiskMappings": List,
    "Tags": List,
    "KeyPairName": String,
    "RamRoleName": String,
    "SpotPriceLimit": String,
    "SpotStrategy": String,
    "DeletionProtection": Boolean
  }
}
```

## Properties {#section_nbg_ck2_lfb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|SourceInstanceId|String|Yes|No|The ID of the ECS instance to be cloned.|The clone operation clones the specified instance, including its instance type, image, bandwidth billing method, bandwidth limit, and network type. If the source ECS instance belongs to multiple security groups, the cloned instance is added only to the first of these security groups.|
|BackendServerWeight|Integer|No|No|The weight of the ECS instance in the Server Load Balancer \(SLB\) instance.|Valid values: 0 to 100. Default value: 100.|
|LoadBalancerIdToAttach|String|No|No|The ID of the SLB instance to which the ECS instance is attached.|None|
|Description|String|No|No|The description of the ECS instance.|The description must be 1 to 256 characters in length.|
|ImageId|String|No|Yes|The ID of the image used to start the ECS instance. You can use public images, custom images, and Alibaba Cloud Marketplace images. For more information, see [Public images for ECS instances](https://ros.console.aliyun.com/#/product/cn-hangzhou/list/imageList).| When editing a template, you can specify the image type and version or only the image type. ROS automatically selects an appropriate public image ID.

 You can use the wildcard character \(\*\) to represent part of an image ID.

 Take all Ubuntu public images provided by Alibaba Cloud as an example. You can use one of the following methods to specify the public image ID for the ECS instance:

 If you enter ubuntu,

 the system matches it with the following ID: ubuntu16\_0402\_64\_20G\_alibase\_20170818.vhd

 If you enter ubuntu\_14,

 the system matches it with the following ID: ubuntu\_14\_0405\_64\_20G\_alibase\_20170824.vhd

 If you enter ubuntu\*14\*32,

 the system matches it with the following ID: ubuntu\_14\_0405\_32\_40G\_alibase\_20170711.vhd

 If you enter ubuntu\_16\_0402\_32,

 the system matches it with the following ID: ubuntu\_16\_0402\_32\_40G\_alibase\_20170711.vhd

 |
|SecurityGroupId|String|No|No|The ID of the security group to which the created instance belongs.|None|
|InstanceName|String|No|No|The name of the instance.|The name must be 1 to 128 characters in length and can contain letters, digits, underscores \(\_\), periods \(.\), and hyphens \(-\).|
|Password|String|No|No|The password used to log on to the ECS instance.| The password must be 8 to 30 characters in length.

 It must contain letters, digits, and special characters.

 The following special characters are allowed: parentheses \(\(\)\), apostrophes \('\), tildes \(~\), exclamation points \(!\), at signs \(@\), number signs \(\#\), dollar signs \($\), percent signs \(%\), caret signs \(^\), ampersands \(&\), asterisks \(\*\), minus signs \(-\), plus signs \(+\), equal signs \(=\), vertical bars \(|\), braces \(\{ \}\), brackets \(\[ \]\), colons \(:\), semicolons \(;\), angle brackets \(< \>\), commas \(,\), periods \(.\), question marks \(?\), and forward slashes \(/\).

 If you specify the Password parameter in the API request, use HTTPS to secure the API and protect your password.

 |
|DiskMappings|List|No|No|The list of disks to be attached to the ECS instance.|A maximum of four disks can be attached.|
|Tags|List|No|No|The custom tags.|A maximum of four tags are supported. The format is \[\{"Key":"tagKey","Value":"tagValue"\}, \{"Key":"tagKey2","Value":"tagValue2"\}\].|
|ZoneId|String|No|No|The ID of the zone where the ECS instance resides.|None|
|InstanceChargeType|String|No|No|The billing method of the instance.| Valid values: PrePaid and PostPaid.

 Default value: PostPaid. If you set this parameter to PrePaid, make sure you have sufficient balance in your account. Otherwise, the instance fails to be created.

 |
|Period|Number|No|No|The subscription period of the instance. This parameter must be set when InstanceChargeType is set to PrePaid. This parameter is inapplicable when InstanceChargeType is set to PostPaid.|Valid values: 1, 2, 3, 4, 5, 6, 7, 8, 9, 12, 24, and 36. Unit: month.|
|KeyPairName|String|No|No|The name of the key pair that is used to connect to the ECS instance.| For Windows-based instances, this parameter is empty by default.

 For Linux-based instances, the Password parameter still takes effect if this parameter is specified. However, logon by password is disabled, and the KeyPairName value is used.

 |
|RamRoleName|String|No|No|The RAM role name of the instance. You can call the ListRoles operation to query the role name. For more information, see [CreateRole](https://partners-intl.aliyun.com/help/doc-detail/28710.htm) and [ListRoles](https://partners-intl.aliyun.com/help/doc-detail/28713.htm).|None|
|SpotPriceLimit|String|No|No|The maximum hourly price of the instance.|This parameter is applicable only when SpotStrategy is set to SpotWithPriceLimit. Three decimal places are allowed at most.|
|SpotStrategy|String|No|No|The spot strategy for a Pay-As-You-Go instance.|This parameter is applicable only when InstanceChargeType is set to PostPaid. Valid values: NoSpot: indicates a regular Pay-As-You-Go instance.

 SpotWithPriceLimit: indicates a Pay-As-You-Go instance with the maximum hourly price.

 SpotAsPriceGo: indicates that the system automatically offers a spot hourly price for an instance based on the supply-demand statistics. The spot price is limited to the cost of resources you actually use.

 Default value: NoSpot.

 |
|InternetMaxBandwidthIn|Integer|No|No|The maximum inbound bandwidth from the Internet. Unit: Mbit/s.|Valid values: 1 to 200.|
|DeletionProtection|Boolean|No|No|The release protection property of the instance. It indicates whether you can use the ECS console or call the DeleteInstance operation to release the instance.|Valid values: true and false.|

## DiskMappings syntax {#section_mue_aaz_zoc .section}

``` {#codeblock_ikm_l2d_9ac .language-json}
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

## DiskMappings properties {#section_qes_5x9_def .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Size|String|Yes|No|The size of a data disk. Unit: GB.|None|
|Category|String|No|No|The type of the data disk.| Valid values: cloud, cloud\_efficiency, cloud\_ssd, and ephemeral\_ssd.

 Default value: cloud.

 |
|DiskName|String|No|No|The name of the data disk.|The name must be 1 to 128 characters in length and can contain letters, digits, underscores \(\_\), periods \(.\), and hyphens \(-\).|
|Description|String|No|No|The description of the data disk.|The description must be 2 to 256 characters in length. This parameter is empty by default.|
|Device|String|No|No|The device name of the data disk.|If you do not set this parameter, the system allocates a device name in alphabetical order from /dev/xvdb to /dev/xvdz.|
|SnapshotId|String|No|No|The ID of the snapshot used to create the data disk.|None|

## Tags syntax {#section_6a4_lbj_r7j .section}

``` {#codeblock_d8s_6p7_brb .language-json}
"Tags": [
  {
    "Value": String,
    "Key": String
  }
]
```

## Tags properties {#section_9v1_wi4_dnw .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Key|String|Yes|No|The key of a tag. Once you use this parameter, it cannot be a null string. It can be up to 64 characters in length. It cannot begin with "aliyun", "acs:", "http://", or "https://".|None|
|Value|String|No|No|The value of a tag. Once you use this parameter, it can be a null string. It can be up to 128 characters in length. It cannot begin with "aliyun", "acs:", "http://", or "https://".|None|

## Response parameters {#section_wy1_jm2_lfb .section}

**Fn::GetAtt**

-   InstanceId: the ID of an instance in a VPC. It is a globally unique identifier \(GUID\) generated by the system for the instance.
-   PrivateIp: the private IP address of an instance in a VPC. This parameter is applicable only when the `NetworkType` parameter is set to VPC.
-   InnerIp: the private IP address of an instance in a classic network. This parameter is applicable only when the `NetworkType` parameter is set to Classic.
-   PublicIp: the list of public IP addresses of instances in a classic network. This parameter is applicable only when the `NetworkType` parameter is set to Classic.
-   ZoneId: the ID of the zone where the instance resides.
-   HostName: the hostname of the instance.

## Examples {#section_vwc_jm2_lfb .section}

``` {#codeblock_ytl_p4v_uw0 .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "WebServer": {
      "Type": "ALIYUN::ECS::InstanceClone",
      "Properties": {
        "SourceInstanceId": "i-25zsk****",
        "SecurityGroupId": "sg-25zwc****",
        "ZoneId": "cn-beijing-b",
        "DiskMappings": [
            {"Size": 10, "Category": "cloud"},
            {"Size": 10, "Category": "cloud", "SnapshotId": "s-25wsw****"}
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

