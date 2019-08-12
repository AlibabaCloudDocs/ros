# ALIYUN::ECS::InstanceGroupClone {#concept_48289_zh .concept}

ALIYUN::ECS::InstanceGroupClone 类型可用于克隆生产一组 ECS 实例。

## 语法 {#section_zvw_gt2_lfb .section}

``` {#codeblock_sgi_ga3_5u4 .language-json}
{
  "Type": "ALIYUN::ECS::InstanceGroupClone",
  "Properties": {
    "BackendServerWeight": Integer,
    "DiskMappings": List,
    "LaunchTemplateName": String,
    "SpotPriceLimit": String,
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
    "SecurityGroupId": String,
    "RamRoleName": String,
    "HpcClusterId": String,
    "SystemDiskDescription": String
  }
}
```

## 属性 {#section_et2_ft2_lfb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ResourceGroupId|String|否|否|实例所在的企业资源组ID。|无。|
|HpcClusterId|String|否|是|实例所属的EHPC集群ID。|无。|
|SourceInstanceId|String|是|否|指定需要克隆的 ECS 实例 ID。|将会克隆实例规格、镜像、带宽收费方式、带宽限制、网络类型等等。如果源 ECS 实例加入多个安全组，新的安全组会加入源实例的第一个安全组。|
|MaxAmount|Integer|是|是|指定最多创建多少个 ECS 实例。|取值范围：\[1-100\]，必须大于等于 MinAmount。|
|MinAmount|String|是|是|指定至少创建多少个 ECS 实例。|取值范围：\[1-100\]，必须小于等于 MaxAmount。|
|BackendServerWeight|Integer|否|否|指定 ECS 实例在负载均衡器实例中权重。|取值范围：\[0-100\]，默认值是 100。|
|LoadBalancerIdToAttach|String|否|否|指定 ECS 实例将加入到哪个负载均衡实例 ID。|无|
|Description|String|否|否|描述信息。|最长 256 个字符。|
|ImageId|String|否|是|用于启动 ECS 实例的镜像 ID，包括公共镜像、自定义镜像和云市场镜像。|[ECS 公共镜像列表](https://ros.console.aliyun.com/#/product/cn-hangzhou/list/imageList)。支持通过模糊的方式指定公共镜像 ID，而不需要指定一个完整的公共镜像 ID。部署 ECS 实例时，只需在编辑模板中指定镜像的类型和版本或者只指定镜像类型，ROS会选择自动适配符合的公共镜像 ID。在模糊镜像 ID 中，可以用通配符（\\\*）指代镜像 ID 的某一部分。 以所有阿里云提供的Ubuntu的公共镜像为例：

 ubuntu\_14\_0405\_32\_40G\_alibase\_20170711.vhd

 ubuntu\_14\_0405\_64\_20G\_alibase\_20170824.vhd

 ubuntu\_16\_0402\_32\_40G\_alibase\_20170711.vhd

 ubuntu\_16\_0402\_64\_20G\_alibase\_20170818.vhd

 在给ECS 指定公共镜像Id的时候，可以按照如下方式：

 指定：ubuntu

 最终会匹配：ubuntu\_16\_0402\_64\_20G\_alibase\_20170818.vhd

 指定：ubuntu\_14

 最终会匹配：ubuntu\_14\_0405\_64\_20G\_alibase\_20170824.vhd

 指定：ubuntu1432

 最终会匹配：ubuntu\_14\_0405\_32\_40G\_alibase\_20170711.vhd

 指定：ubuntu\_16\_0402\_32

 最终会匹配：ubuntu\_16\_0402\_32\_40G\_alibase\_20170711.vhd

 |
|InternetMaxBandwidthOut|Integer|否|否|公网最大出网带宽，单位 Mbps。|按固定带宽计费时取值范围：\[0, 200\]，默认值为 0；按流量计费时取值范围：\[1, 200\]，必须指定。|
|SecurityGroupId|String|否|否|指定创建实例所属安全组。|无|
|InstanceName|String|否|否|实例名称。|最长 128 个字符，可包含英文、中文、数字、下划线\_（\_）、点号（.）、和连字符（-）。|
|Password|String|否|否|ECS 实例登录密码。|实例的密码。8-30 个字符，必须同时包含三项（大、小写字母，数字和特殊符号）。支持以下特殊字符：\( \) \` ~ ! @ \# $ % ^ & \* - + = | \{ \} \[ \] : ; ‘ < \> , . ? /。如果传入 Password 参数，请务必使用 HTTPS 协议调用 API 以避免可能发生的密码泄露。|
|DiskMappings|List|否|否|指定需要挂载的磁盘。|最多支持 16 块磁盘。|
|Tags|List|否|否|用户自定义标签。|最多支持 20 个标签，格式如: \[\{"Key":"tagKey","Value":"tagValue"\},\{"Key":"tagKey2","Value":"tagValue2"\}\]。|
|ZoneId|String|否|否|可用区 ID。|无|
|KeyPairName|String|否|否|给 ECS 实例绑定的密钥对名称。如果是 Windows ECS 实例，则忽略该参数。默认为空。如果填写了 KeyPairName，Password 的内容仍旧会被设置到实例中，但是 Linux 中的密码登录方式会被初始化成禁止。|无|
|RamRoleName|String|否|否|实例 RAM 角色名称。|您可以使用 RAM API ListRoles查询实例RAM角色名称。请参见相关 API 文档[CreateRole](https://www.alibabacloud.com/help/doc-detail/28710.htm) 和 [ListRoles](https://www.alibabacloud.com/help/doc-detail/28713.htm)|
|SpotPriceLimit|String|否|否|设置实例的每小时最高价格。|支持最大 3 位小数。参数 SpotStrategy 取值为 SpotWithPriceLimit 时生效。|
|SpotStrategy|String|否|否|后付费实例的竞价策略。|当参数 InstanceChargeType取值为 PostPaid 时为生效。 取值范围：

 NoSpot：正常按量付费实例。

 SpotWithPriceLimit：设置上限价格的竞价实例.

 SpotAsPriceGo：系统自动出价，最高按量付费价格。

 默认值：NoSpot。

 |
|SystemDiskDiskName|String|否|是|系统盘名称。长度为 \[2, 128\] 个英文或中文字符。必须以大小字母或中文开头，不能以 http:// 和 https:// 开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。默认值：空。|无|
|PeriodUnit|String|否|是|购买资源的时长。 PeriodUnit 为 Week 时：

 -   Period 取值 \{“1”, “2”, “3”, “4”\}
-   AutoRenewPeriod 取值 \{“1”, “2”, “3”\}

 PeriodUnit 为 Month 时： -   Period 取值 \{ “1”, “2”, “3”, “4”, “5”, “6”, “7”, “8”, “9”, “12”, “24”, “36”,”48”,”60”\}
-   AutoRenewPeriod 取值 \{“1”, “2”, “3”, “6”, “12”\}

 | 可选值：Week | Month。

 默认值：Month。

 |
|AutoRenewPeriod|Number|否|是|每次自动续费的时长，当参数AutoRenew取值True时为必填。| 可用值：1，2，3，6，12。

 默认值：1 。

 |
|AutoRenew|String|否|是|是否要自动续费。当参数 InstanceChargeType 取值 PrePaid 时才生效。|取值范围： -   True：自动续费。
-   False（默认）：不自动续费。

 |
|EniMappings|List|否|是|附加到实例的弹性网卡。|最多1个。|
|AutoReleaseTime|String|否|否|自动释放时间。按照[ISO8601](https://www.alibabacloud.com/help/doc-detail/25696.htm)标准表示，并需要使用 UTC 时间。格式为：yyyy-MM-ddTHH:mm:ssZ。 -   如果秒（ss）取值不是 00，则自动取为当前分钟（mm）开始时。
-   最短释放时间为当前时间半小时之后。
-   最长释放时间不能超过当前时间三年。

 如果不传入参数 AutoReleaseTime，表示自动释放功能已取消，ECS 实例不再自动释放。|无。|
|SystemDiskCategory|String|否|是|系统盘的磁盘种类。|取值范围： -   cloud：普通云盘
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD 云盘
-   ephemeral\_ssd：本地 SSD 盘
-   cloud\_essd：ESSD 云盘。目前 ESSD 云盘正在火热公测中，仅部分地域下的可用区可以选购。更多详情，请参阅 [ESSD 云盘 FAQ](https://www.alibabacloud.com/help/faq-detail/64950.htm#AvailableRegion)。

 [已停售的实例规格](https://www.alibabacloud.com/help/faq-detail/55263.htm)且非 I/O 优化实例默认值：cloud，否则，默认值：cloud\_efficiency|
|LaunchTemplateName|String|否|是|启动模板名称。|无|
|LaunchTemplateVersion|String|否|是|启动模板的版本。如果没有指定版本，则使用默认版本。|无。|
|InternetMaxBandwidthIn|Integer|否|否|公网入带宽最大值，单位为Mbit/s。| 取值范围：1-200。

 默认值：200。

 |
|LaunchTemplateId|String|否|是|启动模板ID。|无|
|SystemDiskDescription|String|否|是|系统盘描述。长度为 \[2, 256\] 个英文或中文字符，不能以 http:// 和 https:// 开头。默认值：空。|无|
|DeletionProtection|Boolean|否|否|实例释放保护属性，指定是否支持通过控制台或 API（DeleteInstance）释放实例。|可用值：true、false。|
|DeploymentSetId|String|否|是|部署集 ID。|无。|

## DiskMappings 语法 {#section_f5t_blf_5dz .section}

``` {#codeblock_aou_514_bip .language-json}
"DiskMappings": [
  {
    "Category": String,
    "DiskName": String,
    "Description": String,
    "Encrypted": String,
    "KMSKeyId": String,
    "Device": String,
    "SnapshotId": String,
    "Size": String
  }
]
```

## DiskMappings 属性 {#section_l54_pls_j27 .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Encrypted|String|否|否|Whether the data disk is encrypted or not. Options: true: Encrypted. false: Not encrypted. Default value: false.|可用值: true, false|
|KMSKeyId|String|否|否|The KMS key ID for the data disk.|无。|
|Size|String|是|否|数据盘大小，单位：GB。|无|
|Category|String|否|否|数据盘的类型。|允许的可选值：cloud、cloud\_efficiency、cloud\_ssd、ephemeral\_ssdDefault。|
|DiskName|String|否|否|数据盘的名称。|最长 128 个字符，可包含英文、中文、数字、下划线\_（\_）、点号（.）、和连字符（-）。|
|Description|String|否|否|描述信息。|取值范围：\[2,256\]，默认值是空。|
|Device|String|否|否|指定数据盘的在 ECS 服务器中的设备名称。|例如：/dev/xvd\[a-z\]。|
|SnapshotId|String|否|否|通过 SnapshotId 创建数据盘。|无|

## EniMappings 语法 {#section_ouq_juy_gie .section}

``` {#codeblock_2yy_14n_cxf .language-json}
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

## EniMappings 属性 {#section_4pe_ycf_0rp .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|SecurityGroupId|String|是|是|弹性网卡所属的安全组ID。|无。|
|VSwitchId|String|是|否|弹性网卡所属的虚拟交换机ID。|无 。|
|Description|String|否|是|弹性网卡的描述。长度为2~256个英文或中文字符，不能以 http:// 和 https:// 开头。|无。|
|NetworkInterfaceName|String|否|是|弹性网卡名称。|无。|
|PrimaryIpAddress|String|否|否|弹性网卡的主IP地址。|无 。|

## Tags 语法 {#section_ouq_juy_fie .section}

``` {#codeblock_2yy_14n_cxf .language-json}
"Tags": [
  {
    "Value": String,
    "Key": String
  }
]
```

## Tags 属性 {#section_4pe_ycf_0op .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Key|String|是|否|无|无|
|Value|String|否|否|无|无|

## 返回值 {#section_876_zs6_y42 .section}

**Fn::GetAtt**

-   InstanceIds：实例 ID。由系统生成，全局唯一。是访问实例的唯一标识。
-   PrivateIps：VPC 类型实例的私网 IP 列表。当 NetworkType 为 VPC 时，这个参数生效。一个带有格式的 Json Array: \[“172.16.XX.XX”, ”172.16.XX.XX”, … “172.16.XX.XX”\]。最多 100 个 IP，用半角逗号字符隔开。
-   InnerIps：Classic 类型实例的私网 IP 列表。当 NetworkType 为 Classic 时，这个参数生效。一个带有格式的 Json Array: \[“10.1.XX.XX”, ”10.1.XX.XX”, … “10.1.XX.XX”\]。最多 100 个 IP，用半角逗号字符隔开。
-   PublicIps：Classic 类型实例的公网 IP 列表。当 NetworkType 为 Classic 时，这个参数生效。一个带有格式的 Json Array: \[“42.1.XX.XX”, ”42.1.XX.XX”, … “42.1.XX.XX”\]。最多 100 个 IP，用半角逗号字符隔开。
-   HostNames：所有实例的主机名称列表。一个带有格式的 Json Array: \[“host1”, “host2”,… “host3”\]。
-   OrderId: 实例的订单ID列表。
-   ZoneIds: 可用区 ID。

## 示例 {#section_p5r_uhf_bro .section}

``` {#codeblock_8u9_h1f_1fo .language-json}
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

