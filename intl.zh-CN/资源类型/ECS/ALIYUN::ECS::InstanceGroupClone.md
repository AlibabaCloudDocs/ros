# ALIYUN::ECS::InstanceGroupClone

ALIYUN::ECS::InstanceGroupClone类型用于克隆一组ECS实例。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ResourceGroupId|String|否|否|实例所在的企业资源组ID。|无|
|HpcClusterId|String|否|是|实例所属的EHPC集群ID。|无|
|SourceInstanceId|String|是|否|需要克隆的ECS实例ID。|克隆实例规格、镜像、带宽收费方式、带宽限制、网络类型等。如果源ECS实例加入多个安全组，新的安全组会加入源实例的第一个安全组。|
|MaxAmount|Integer|是|是|一次性创建ECS实例的个数。|取值范围：1~100。|
|BackendServerWeight|Integer|否|否|ECS实例在负载均衡器实例中权重。|取值范围：0~100。 默认值：100。 |
|LoadBalancerIdToAttach|String|否|否|ECS实例将加入到的负载均衡实例的ID。|无|
|Description|String|否|是|描述信息。|最长256个字符。|
|ImageId|String|否|是|用于启动ECS实例的镜像ID，包括公共镜像、自定义镜像和云市场镜像。|支持通过模糊的方式指定公共镜像ID，无需指定一个完整的公共镜像ID。例如： -   指定ubuntu，最终会匹配ubuntu16\_0402\_64\_20G\_alibase\_20170818.vhd。
-   指定ubuntu\_14，最终会匹配ubuntu\_14\_0405\_64\_20G\_alibase\_20170824.vhd。
-   指定ubuntu\*14\*32，最终会匹配ubuntu\_14\_0405\_32\_40G\_alibase\_20170711.vhd。
-   指定ubuntu\_16\_0402\_32，最终会匹配ubuntu\_16\_0402\_32\_40G\_alibase\_20170711.vhd。 |
|InternetMaxBandwidthOut|Integer|否|否|公网最大出网带宽。|单位：Mbps。 -   按固定带宽计费时，取值范围：0~200。
-   按流量计费时，取值范围：1~200。 |
|SecurityGroupId|String|否|否|实例加入的安全组。|不支持同时指定SecurityGroupId和SecurityGroupIds。|
|SecurityGroupIds|List|否|否|将实例同时加入多个安全组，实例能够加入安全组配额请参见[安全组](/intl.zh-CN/产品简介/使用限制.md)。|不支持同时指定SecurityGroupId和SecurityGroupIds。|
|InstanceName|String|否|否|实例名称。|最长为128个字符。可包含英文字母、汉字、数字、下划线（\_）、英文句点（.）和短划线。|
|Password|String|否|是|ECS实例登录密码。|长度为8~30个字符。必须同时包含英文字母、数字和特殊字符，支持以下特殊字符： ```
( ) ‘ ~ ! @ # $ % ^ & * - + = | { } [ ] : ; ‘ < > , . ? / -
```

 如果指定此参数，请使用HTTPS协议调用API，以避免密码泄露。|
|DiskMappings|List|否|是|需要挂载的磁盘。|最多支持16块磁盘。 详情请参见[DiskMappings属性](#section_1an_6zh_or9)。 |
|Period|Number|否|是|付费周期。|取值：1、2、3、4、5、6、7、8、9、12、24、36。 单位：月。

 当InstanceChargeType取值为PrePaid时，此参数为必选参数；当 InstanceChargeType取值为PostPaid时，此参数为可选参数。|
|Tags|List|否|是|用户自定义标签。|最多支持20个标签，格式：`[{"Key": "tagKey", "Value": "tagValue"},{"Key": "tagKey2", "Value": "tagValue2"}]`。 详情请参见[Tags属性](#section_4pe_ycf_0op)。 |
|ZoneId|String|否|否|可用区ID。|无|
|KeyPairName|String|否|是|ECS实例绑定的密钥对名称。|如果是Windows ECS实例，则忽略该参数。如果已填写KeyPairName，Password的内容仍会被设置到实例中，但是Linux系统中的密码登录方式会被禁止。|
|RamRoleName|String|否|是|实例RAM角色名称。|您可以调用ListRoles查询实例RAM角色名称，详情请参见[CreateRole](/intl.zh-CN/API参考（RAM）/角色管理接口/CreateRole.md)和[ListRoles](/intl.zh-CN/API参考（RAM）/角色管理接口/ListRoles.md)。|
|SpotPriceLimit|String|否|否|实例的每小时最高价格。|最大支持3位小数。当SpotStrategy为SpotWithPriceLimit时，该参数生效。|
|SpotStrategy|String|否|否|后付费实例的竞价策略。|当InstanceChargeType取值为PostPaid时，此参数为必选参数。 取值：

-   NoSpot（默认值）：正常按量付费实例。
-   SpotWithPriceLimit：上限价格的竞价实例。
-   SpotAsPriceGo：系统自动出价，最高不超过按量付费价格。 |
|SystemDiskDiskName|String|否|是|系统盘名称。|-   长度为2~128个字符。
-   必须以英文字母或汉字开头，不能以`http://`或`https://`开头。
-   可包含数字、半角冒号（:）、下划线（\_）和短划线（-）。 |
|PeriodUnit|String|否|是|购买资源的时长。|取值： -   Week

PeriodUnit取值为Week时，Period取值为1、2、3、4，AutoRenewPeriod取值为1、2、3。

-   Month（默认值）

PeriodUnit取值为Month时，Period取值为1、2、3、4、5、6、7、8、9、12、24、36、48、60，AutoRenewPeriod取值为1、2、3、6、12。 |
|AutoRenewPeriod|Number|否|是|每次自动续费的时长。|当AutoRenew为true时，该参数为必填参数。 取值：1、2、3、6、12。

 默认值：1 。|
|AutoRenew|String|否|是|是否要自动续费。|取值： -   True：自动续费
-   False（默认值）：不自动续费

 当InstanceChargeType取值PrePaid时，此参数为必选参数。|
|EniMappings|List|否|是|附加到实例的弹性网卡。|附加到实例的弹性网卡个数最多为1个。 详情请参见[EniMappings属性](#section_4pe_ycf_0rp)。 |
|AutoReleaseTime|String|否|否|ECS实例自动释放的时间。|时间格式必须遵守ISO8601规范，例如：`yyyy-MM-ddTHH:mm:ssZ`。释放时间不能超过三年。|
|SystemDiskCategory|String|否|是|系统盘类型。|取值： -   cloud
-   cloud\_efficiency
-   cloud\_ssd
-   cloud\_essd |
|LaunchTemplateName|String|否|是|启动模板的名称。|无|
|LaunchTemplateVersion|String|否|是|启动模板的版本。|如果没有指定版本，则使用默认版本。|
|InternetMaxBandwidthIn|Integer|否|否|公网最大入网带宽。|单位：Mbps。 取值范围：1~100。

 默认值：100。|
|LaunchTemplateId|String|否|是|启动模板ID。|无|
|SystemDiskDescription|String|否|是|系统盘描述信息。|无|
|DeletionProtection|Boolean|否|否|实例释放保护属性，指定是否支持通过控制台或[DeleteInstance](/intl.zh-CN/API参考/实例/DeleteInstance.md)接口释放实例。|取值： -   true
-   false |
|DeploymentSetId|String|否|是|部署集ID。|无|
|Ipv6AddressCount|Integer|否|是|为弹性网卡指定随机生成的IPv6地址数量。|不能同时指定Ipv6Addresses和Ipv6AddressCount。|
|Ipv6Addresses|List|否|是|为弹性网卡指定的一个或多个IPv6地址。|列表最大长度为1。属性的更改不影响现有实例。不能同时指定Ipv6Addresses和Ipv6AddressCount。|
|SystemDiskAutoSnapshotPolicyId|String|否|是|系统盘自动快照策略ID。|无|

## DiskMappings语法

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

## DiskMappings属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Size|String|是|否|数据盘大小。|单位：GB。|
|Category|String|否|否|数据盘的类型。|取值： -   cloud（默认值）：普通云盘。
-   cloud\_ssd：SSD云盘。
-   cloud\_essd：ESSD云盘。
-   cloud\_efficiency：高效云盘。 |
|DiskName|String|否|否|数据盘的名称。|最长128个字符。可包含英文字母、汉字、数字、下划线（\_）、英文句点（.）和短划线（-）。|
|Description|String|否|否|数据盘的描述。|长度为2~256个字符。不能以`http://`或`https://`开头。|
|Device|String|否|否|数据盘在ECS中的名称。|例如：`/dev/xvd[a-z]`。|
|SnapshotId|String|否|否|快照ID。|无|
|Encrypted|String|否|否|数据盘是否加密。|取值： -   true
-   false（默认值） |
|KMSKeyId|String|否|否|数据盘对应的KMS密钥ID。|无|
|AutoSnapshotPolicyId|String|否|否|自动快照策略ID。|无|
|PerformanceLevel|String|否|否|创建ESSD云盘作为系统盘使用时，设置云盘的性能等级。|-   PL1（默认）：单盘最高随机读写IOPS为5万。
-   PL2：单盘最高随机读写IOPS为10万。
-   PL3：单盘最高随机读写IOPS为100万。

 关于如何选择ESSD性能等级，请参见[ESSD云盘](/intl.zh-CN/块存储/块存储介绍/ESSD云盘.md)。|

## EniMappings语法

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

## EniMappings属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|SecurityGroupId|String|是|是|弹性网卡所属的安全组ID。|无|
|VSwitchId|String|是|否|弹性网卡所属的虚拟交换机ID。|无|
|Description|String|否|是|弹性网卡的描述。|长度为2~256个字符。不能以`http://`或`https://`开头。|
|NetworkInterfaceName|String|否|是|弹性网卡名称。|无|
|PrimaryIpAddress|String|否|否|弹性网卡的主IP地址。|无|

## Tags语法

```
"Tags": [
  {
    "Value": String,
    "Key": String
  }
]
```

## Tags属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Key|String|是|否|标签键。|长度为1~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或`https://`。|
|Value|String|否|否|标签值。|长度为0~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或`https://`。|

## 返回值

Fn::GetAtt

-   InstanceIds：实例ID，是访问实例的唯一标识。由系统生成，全局唯一。
-   PrivateIps：VPC类型实例的私网IP列表。当NetworkType为VPC时，此参数生效。例如：一个带有格式的JSON Array: \[“172.16.XX.XX”, “172.16.XX.XX”, … “172.16.XX.XX”\]，最多100个IP，用半角逗号（,）隔开。
-   InnerIps：Classic类型实例的私网IP列表。当NetworkType为Classic时，此参数生效。例如：一个带有格式的JSON Array: \[“10.1.XX.XX”, “10.1.XX.XX”, … “10.1.XX.XX”\]，最多100个IP，用半角逗号（,）隔开。
-   PublicIps：Classic类型实例的公网IP列表。当NetworkType为Classic时，此参数生效。例如：一个带有格式的JSON Array: \[“42.1.XX.XX”, “42.1.XX.XX”, … “42.1.XX.XX”\]，最多100个IP，用半角逗号（,）隔开。
-   HostNames：所有实例的主机名称列表。
-   OrderId：实例的订单ID列表。
-   ZoneIds：可用区ID。

## 示例

`JSON`格式

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
      "Description": "Disk mappings to attach to instance. Max support 16 disks.\nIf the image contains a data disk, you can specify other parameters of the data disk via the same value of parameter \"Device\". If parameter \"Category\" is not specified, it will be cloud_efficiency instead of \"Category\" of data disk in the image.Old instances will not be changed.",
      "MaxLength": 16
    },
    "ResourceGroupId": {
      "Type": "String",
      "Description": "Resource group id."
    },
    "SystemDiskDescription": {
      "Type": "String",
      "Description": "Description of created system disk.Old instances will not be changed."
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
      "Description": "Name of created system disk.Old instances will not be changed."
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
    "BackendServerWeight": {
      "Type": "Number",
      "Description": "The weight of backend server of load balancer. From 0 to 100, 0 means offline. Default is 100.",
      "MinValue": 0,
      "MaxValue": 100,
      "Default": 100
    },
    "KeyPairName": {
      "Type": "String",
      "Description": "SSH key pair name.Old instances will not be changed."
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
      "Description": "Unit of prepaid time period, it could be Week/Month. Default value is Month.Old instances will not be changed.",
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

`YAML`格式

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
      "Category" of data disk in the image.Old instances will not be changed.
    MaxLength: 16
  ResourceGroupId:
    Type: String
    Description: Resource group id.
  SystemDiskDescription:
    Type: String
    Description: Description of created system disk.Old instances will not be changed.
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
    Description: Name of created system disk.Old instances will not be changed.
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
    Description: SSH key pair name.Old instances will not be changed.
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
      Month.Old instances will not be changed.
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

