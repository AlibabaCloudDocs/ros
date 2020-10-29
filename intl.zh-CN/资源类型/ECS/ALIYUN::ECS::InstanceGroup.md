# ALIYUN::ECS::InstanceGroup

ALIYUN::ECS::InstanceGroup类型用于创建一组相同配置的ECS实例。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ResourceGroupId|String|否|是|实例所在的企业资源组ID。|无|
|HpcClusterId|String|否|是|实例所属的HPC集群ID。|无|
|MaxAmount|Integer|是|是|一次性创建ECS实例的个数。|取值范围：1~100。|
|Description|String|否|是|描述信息。|最长256个字符。|
|InstanceType|String|是|是|ECS实例规格。|详情请参见[实例规格族](/intl.zh-CN/实例/实例规格族.md)。|
|ImageId|String|是|是|用于启动ECS实例的镜像ID，包括公共镜像、自定义镜像和云市场镜像。|支持通过模糊的方式指定公共镜像ID，而不需要指定一个完整的公共镜像ID。例如： -   指定Ubuntu，最终会匹配ubuntu\_16\_0402\_64\_20G\_alibase\_20170818.vhd。
-   指定ubuntu1432，最终会匹配ubuntu\_14\_0405\_32\_40G\_alibase\_20170711.vhd。

详情请参见[请求参数](/intl.zh-CN/API参考/实例/RunInstances.md)。|
|SecurityGroupId|String|否|否|指定创建实例所属安全组。|不支持同时指定SecurityGroupId和SecurityGroupIds。|
|SecurityGroupIds|List|否|否|将实例同时加入多个安全组，实例能够加入安全组配额请参见[安全组](/intl.zh-CN/产品简介/使用限制.md)。|不支持同时指定SecurityGroupId和SecurityGroupIds。|
|InstanceName|String|否|否|实例名称。|最长为128个字符。可包含英文字母、汉字、数字、下划线（\_）、英文句点（.）和短划线（-）。 通过`name_prefix[begin_number,bits]name_suffix`格式为各个ECS实例指定不同的实例名，详情请参见[请求参数](/intl.zh-CN/API参考/实例/RunInstances.md)

。|
|Password|String|否|是|ECS实例登录密码。|长度为8~30个字符。必须同时包含大写英文字母、小写英文字母、数字和特殊字符其中三项，支持的特殊字符如下：```
：( ) ` ~ ! @ # $ % ^ & * - + = | { } [ ] : ; ‘ < > , . ? /
```

如果指定Password参数，请使用HTTPS协议调用API，以免发生密码泄露。|
|PasswordInherit|Boolean|否|否|是否使用镜像预设的密码。|取值：-   true：使用。
-   false：不使用。

**说明：** 使用该参数时，Password参数必须为空，同时您需要确保使用的镜像已经设置了密码。 |
|HostName|String|否|否|主机名。|长度最少2个字符。英文句点（.）和短划线（-）不能作为hostname的首尾字符，且不能连续使用。详情请参见[请求参数](/intl.zh-CN/API参考/实例/RunInstances.md)。|
|AllocatePublicIP|Boolean|否|否|是否创建公网IP。|如果InternetMaxBandwidthOut为0，则不会分配公网IP。 取值：

-   true（默认值）
-   false |
|AutoReleaseTime|String|否|否|ECS实例自动释放的时间。|时间格式必须遵守ISO8601规范，例如`"yyyy-MM-ddTHH:mm:ssZ"`。释放时间不能超过三年。|
|PrivateIpAddress|String|否|否|实例私网IP地址。|专有网络类型ECS实例设置私网IP地址时，必须从虚拟交换机的空闲网段中选择。 **说明：** 如果设置PrivateIpAddress，MaxAmount取值只能为1。 |
|DiskMappings|List|否|是|为ECS实例创建的数据盘。|最多创建16块数据盘。 修改该参数，不会影响已创建的实例，新创建的实例会使用修改后的值。

详情请参见[DiskMappings属性](#section_39d_e40_xo6)。 |
|InternetChargeType|String|否|否|公网访问带宽计费方式。|取值： -   PayByBandwidth：按固定带宽计费。
-   PayByTraffic（默认值）：按流量计费。 |
|InternetMaxBandwidthIn|Integer|否|否|公网最大入网带宽。|取值范围：1~100。

单位：Mbps。

默认值：100。 |
|InternetMaxBandwidthOut|Integer|否|否|公网出带宽最大值。|取值范围：0~100。

单位：Mbps。

默认值：0。 |
|IoOptimized|String|否|否|是否创建I/O优化实例。|取值： -   none：非 I/O 优化。
-   optimized（默认值）：I/O 优化。 |
|SystemDiskCategory|String|否|是|系统盘类型。|取值： -   cloud：普通云盘。
-   cloud\_efficiency：高效云盘。
-   cloud\_ssd：SSD云盘。
-   cloud\_essd：ESSD云盘。
-   ephemeral\_ssd：本地SSD盘。 |
|SystemDiskDescription|String|否|是|系统盘描述信息。|无|
|SystemDiskDiskName|String|否|是|系统盘名称。|无|
|SystemDiskSize|Number|否|是|系统盘大小。|取值范围：40~500。 单位：GB。

如果使用自定义镜像创建系统盘，需要保证系统盘大于自定义镜像大小。 |
|Tags|List|否|是|用户自定义标签。|最多支持20个标签，格式：`[{"Key":"tagKey","Value":"tagValue"},{"Key":"tagKey2","Value":"tagValue2"}]`。 详情请参见[Tags属性](#section_668_3ad_arl)。 |
|UserData|String|否|是|创建ECS实例时传递的用户数据。|内容需要限制在16KB以内。无需用Base64转码，特殊字符需要使用转义符。|
|ZoneId|String|否|否|可用区ID。|无|
|VpcId|String|否|否|虚拟专有网络ID。|无|
|VSwitchId|String|否|否|交换机ID。|无|
|KeyPairName|String|否|是|ECS实例绑定的密钥对名称。|如果是Windows ECS实例，则忽略该参数。默认为空。

如果已填写KeyPairName，Password的内容仍会被设置到实例中，但是Linux系统中的密码登录方式会被禁止。|
|RamRoleName|String|否|是|实例RAM角色名称。|您可以调用ListRoles查询实例RAM角色名称，详情请参见[CreateRole](/intl.zh-CN/API参考（RAM）/角色管理接口/CreateRole.md)和[ListRoles](/intl.zh-CN/API参考（RAM）/角色管理接口/ListRoles.md)。|
|SpotPriceLimit|String|否|否|实例的每小时最高价格。|最大支持3位小数。当SpotStrategy为SpotWithPriceLimit时，该参数生效。|
|SpotStrategy|String|否|否|后付费实例的竞价策略。|当InstanceChargeType为PostPaid时，该参数生效。取值： -   NoSpot（默认值）：正常按量付费实例。
-   SpotWithPriceLimit：设置上限价格的竞价实例。
-   SpotAsPriceGo：系统自动出价，最高按量付费价格。 |
|DedicatedHostId|String|否|否|专有宿主机ID。|无|
|LaunchTemplateName|String|否|是|启动模板名称。|无|
|PeriodUnit|String|否|是|购买资源的时长周期。|取值： -   Week
-   Month（默认值） |
|AutoRenewPeriod|Number|否|是|每次自动续费的时长。|当AutoRenew为True时，此参数为必填参数。 取值：

-   1（默认值）
-   2
-   3
-   6
-   12 |
|AutoRenew|String|否|是|是否自动续费。|当InstanceChargeType为PrePaid时，该参数生效。取值： -   True：自动续费。
-   False（默认值）：不自动续费。 |
|InstanceChargeType|String|否|是|实例的付费方式。|取值： -   PrePaid：预付费，包年包月。

**说明：** 当取值为PrePaid时，您必须确认自己的账号支持余额支付/信用支付，否则将返回InvalidPayMethod错误消息提示。

-   PostPaid（默认值）：按量付费。 |
|EniMappings|List|否|是|附加到实例的弹性网卡。|附加到实例的弹性网卡个数最多为1个。 详情请参见[EniMappings属性](#section_qf5_2mx_o68)。 |
|LaunchTemplateId|String|否|是|启动模板ID。|无|
|LaunchTemplateVersion|String|否|是|启动模板的版本。|如果没有指定版本，则使用默认版本。|
|Period|Number|否|是|购买资源的时长。|当InstanceChargeType为PrePaid时，该参数生效且为必选参数。一旦指定了DedicatedHostId，则取值不能超过专有宿主机的订阅时长。 -   当PeriodUnit为Week时，Period取值：1~4。
-   当PeriodUnit为Month时，Period取值：1~9、12、24、36、48、60。 |
|NetworkType|String|否|否|ECS实例网络类型。|取值： -   vpc
-   classic（默认值） |
|DeletionProtection|Boolean|否|否|实例释放保护属性，指定是否支持通过控制台或[DeleteInstance](/intl.zh-CN/API参考/实例/DeleteInstance.md)接口释放实例。|取值： -   true
-   false |
|DeploymentSetId|String|否|是|部署集ID。|无|
|Ipv6AddressCount|Integer|否|是|为弹性网卡指定随机生成的IPv6地址数量。|不能同时指定Ipv6Addresses和Ipv6AddressCount。|
|Ipv6Addresses|List|否|是|为弹性网卡指定一个或多个IPv6地址。|最多指定一个IPv6地址。属性的更改不影响现有实例。不能同时指定Ipv6Addresses和Ipv6AddressCount。|
|SystemDiskAutoSnapshotPolicyId|String|否|是|系统盘自动快照策略ID。|无|
|SystemDiskPerformanceLevel|String|否|否|创建ESSD云盘作为系统盘使用时，设置云盘的性能等级。|取值： -   PL1（默认值）：单盘最高随机读写IOPS为5万。
-   PL2：单盘最高随机读写IOPS为10万。
-   PL3：单盘最高随机读写IOPS为100万。

关于如何选择ESSD性能等级，请参见[ESSD云盘](/intl.zh-CN/块存储/块存储介绍/ESSD云盘.md)。|

## DiskMappings语法

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

## DiskMappings属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Size|String|是|否|数据盘大小。|单位：GB。|
|Category|String|否|否|数据盘的类型。|取值： -   cloud
-   cloud\_efficiency
-   cloud\_ssd
-   cloud\_essd
-   ephemeral\_ssd

对于I/O优化实例，默认值为cloud\_efficiency。对于非I/O优化实例，默认值为cloud。|
|DiskName|String|否|否|数据盘的名称。|长度为2~128个字符。必须以英文字母或汉字开头，不能以`http://`或`https://`开头。可包含英文字母、汉字、数字、下划线（\_）、半角冒号（:）和短划线（-）。|
|Description|String|否|否|数据盘的描述。|长度为2~256个字符。不能以`http://`或`https://`开头。|
|Device|String|否|否|数据盘在ECS中的名称。|**说明：** 该参数即将停止使用，为提高兼容性，请尽量使用其他参数。 |
|SnapshotId|String|否|否|快照ID。|无|
|Encrypted|String|否|否|数据盘是否加密。|取值： -   true
-   false（默认值） |
|KMSKeyId|String|否|否|数据盘对应的KMS密钥ID。|无|
|AutoSnapshotPolicyId|String|否|否|自动快照策略ID。|无|
|PerformanceLevel|String|否|否|创建ESSD云盘作为数据盘使用时，设置云盘的性能等级。|取值： -   PL1（默认值）：单盘最高随机读写IOPS为5万。
-   PL2：单盘最高随机读写IOPS为10万。
-   PL3：单盘最高随机读写IOPS为100万。

关于如何选择ESSD性能等级，请参见[ESSD云盘](/intl.zh-CN/块存储/块存储介绍/ESSD云盘.md)。|

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
|Key|String|是|否|标签键|长度为1~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或`https://` 。|
|Value|String|否|否|标签值|长度为0~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或`https://` 。|

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
|SecurityGroupId|String|是|是|安全组ID。|所属的安全组ID必须是同一个专有网络下的安全组。|
|VSwitchId|String|是|否|交换机ID。|无|
|Description|String|否|是|弹性网卡的描述信息。|长度为2~256个字符，不能以`http://`或`https://`开头。|
|NetworkInterfaceName|String|否|是|弹性网卡名称。|长度为2~128个字符。必须以英文字母或汉字开头，不能以`http://`或`https://`开头。可包含英文字母、汉字、数字、半角冒号（:）、下划线（\_）和短划线（-）。|
|PrimaryIpAddress|String|否|否|弹性网卡的主私有IP地址。|指定的IP必须是在所属交换机的地址段内的空闲地址。如果不指定IP，则默认随机分配该交换机中的空闲地址。|

## 返回值

Fn::GetAtt

-   InstanceIds：实例ID，访问实例的唯一标识。由系统生成，全局唯一。
-   PrivateIps：VPC类型实例的私网IP列表。当NetworkType为VPC时，此参数生效。例如：一个带有格式的JSON Array：`["172.16.XX.XX", "172.16.XX.XX", … "172.16.XX.XX"]`，最多100个IP，用英文逗号（,）隔开。
-   InnerIps：Classic类型实例的私网IP列表。当NetworkType为Classic时，此参数生效。例如：一个带有格式的JSON Array：`["10.1.XX.XX", "10.1.XX.XX", … "10.1.XX.XX"]`，最多100个IP，用英文逗号（,）隔开。
-   PublicIps：Classic类型实例的公网IP列表。当NetworkType为Classic时，此参数生效。例如：一个带有格式的JSON Array：`["42.1.XX.XX", "42.1.XX.XX", … "42.1.XX.XX"]`，最多100个IP，用英文逗号（,）隔开。
-   HostNames：所有实例的主机名称列表。
-   OrderId：实例的订单ID列表。
-   ZoneIds：可用区ID。

## 示例

`JSON`格式

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
      "Description": "Instance network type. Support 'vpc' and 'classic', for compatible reason, default is 'classic'. If vswitch id and vpc id is specified, the property will be forced to be set to 'vpc'  ",
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
        "LaunchTemplateVersion": {
          "Ref": "LaunchTemplateVersion"
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

`YAML`格式

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
      InstanceName:
        Ref: InstanceName
      DeploymentSetId:
        Ref: DeploymentSetId
      InternetMaxBandwidthOut:
        Ref: InternetMaxBandwidthOut
      VpcId:
        Ref: VpcId
      LaunchTemplateVersion:
        Ref: LaunchTemplateVersion
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

