# ALIYUN::ECS::InstanceGroup {#concept_48278_zh .concept}

ALIYUN::ECS::InstanceGroup 类型可用于创建一组 ECS 实例。

## 语法 {#section_xyg_tn2_lfb .section}

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

## 属性 {#section_pzg_wn2_lfb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ResourceGroupId|String|否|是|实例所在的企业资源组ID。|无。|
|HpcClusterId|String|否|是|实例所属的HPC集群ID。|无。|
|MaxAmount|Integer|是|是|一次最多创建多少个 ECS 实例。|取 1-100 之间的任意值，必须大于等于 MinAmount。|
|MinAmount|String|是|是|一次至少创建多少个 ECS 实例。|取 1-100 之间的任意值，必须小于等于 MaxAmount。|
|Description|String|否|否|描述信息。|最长 256 个字符。|
|InstanceType|String|是|否|ECS 实例规格。|请参见 [ECS实例规格](https://www.alibabacloud.com/help/doc-detail/25378.htm)。|
|ImageId|String|是|是|用于启动 ECS 实例的镜像 ID，包括公共镜像、自定义镜像和云市场镜像。|[ECS 公共镜像列表](https://ros.console.aliyun.com/#/product/cn-hangzhou/list/imageList)。支持通过模糊的方式指定公共镜像 ID，而不需要指定一个完整的公共镜像 ID。 部署 ECS 的时候，如果只对镜像类型和版本有要求，只需要在编辑模板时，指定镜像的类型和版本或者只指定镜像类型，ROS 会选择自动适配符合的公共镜像 ID。在模糊镜像 ID 中，可以用通配符 （\\\*）指代镜像 ID 的某一部分。 以所有阿里云提供的 Ubuntu 的公共镜像为例：

 ubuntu\_14\_0405\_32\_40G\_alibase\_20170711.vhd

 ubuntu\_14\_0405\_64\_20G\_alibase\_20170824.vhd

 ubuntu\_16\_0402\_32\_40G\_alibase\_20170711.vhd

 ubuntu\_16\_0402\_64\_20G\_alibase\_20170818.vhd

 在给ECS 指定公共镜像 ID 的时候，可以按照如下方式：

 指定：ubuntu

 最终会匹配：ubuntu\_16\_0402\_64\_20G\_alibase\_20170818.vhd

 指定：ubuntu\_14

 最终会匹配：ubuntu\_14\_0405\_64\_20G\_alibase\_20170824.vhd

 指定：ubuntu1432

 最终会匹配：ubuntu\_14\_0405\_32\_40G\_alibase\_20170711.vhd 指定：ubuntu\_16\_0402\_32

 最终会匹配：ubuntu\_16\_0402\_32\_40G\_alibase\_20170711.vhd|
|SecurityGroupId|String|否|否|指定创建实例所属安全组。|无|
|InstanceName|String|否|否|实例名称。|最长 128 个字符，可包含英文、中文、数字、下划线（\_）、点号（.）、和连字符（-）。 通过 name\_prefix\[begin\_number,bits\]name\_suffix 格式给各个 ECS 实例指定不同的实例名。 name\_prefix 为实例名称的前缀，必须要指定。\[begin\_number,bits\] 指定各个实例名称的相区别的部分。begin\_number 指定实例名称的开始数字；bits 指定每个数字在实例名中的所占位数。name\_suffix 指定实例名的后缀（可选）。 \[begin\_number,bits\]需要满足以下规则：

 整个字段中不能有空格。

 bits 必须属于 \[1, 6\]。

 begin\_number 必须属于 \[0, 999999\]。

 如果只指定 begin\_number, 则bits 会默认取值 6。

 如果只指定 \[\] 或者 \[,\], 则begin\_number 从 0 开始取值，bits 会默认取值 6。

 如果指定的 begin\_number 位数大于 bits 所指定的。如：\[123456,1\] 中 bits 虽被指定为 1，但是 begin\_number 为 123456，则 bits 实际会取值为 6。

 |
|Password|String|否|否|ECS 实例登录密码。|实例的密码。8-30 个字符，必须同时包含三项（大、小写字母，数字和特殊符号）。支持以下特殊字符：\( \) \` ~ ! @ \# $ % ^ & \* - + = | \{ \} \[ \] : ; ‘ < \> , . ? /。如果传入 Password 参数，请务必使用 HTTPS 协议调用 API 以避免可能发生的密码泄露。|
|HostName|String|否|否|主机名。| 表示云服务器的主机名，最少 2 字符，点号（.）和连字符（-）不能作为 hostname 的首尾字符，且不能连续使用。

 Windows 平台中，HostName 最长为 15 字符，允许由字母（不限制大小写）、数字和连字符（-）组成；不支持点号（.）；不能全是数字。

 其他（Linux 等）平台中，HostName 最长为 30 字符，允许使用多个点号（.）。点号之间为一段，每段允许由字母（不限制大小写）、数字和连字符（-）组成。

 通过 name\_prefix\[begin\_number,bits\]name\_suffix 格式给各个 ECS 指定不同的主机名。

 name\_prefix 为主机名称的前缀，必须要指定。

 \[begin\_number,bits\] 指定各个主机名称的变化的部分，begin\_number 指定主机名称的开始数字，bits 指定每个数字在主机名中的所占位数。

 name\_suffix 指定主机名的后缀，可选。

 \[begin\_number,bits\]需要满足以下规则： 整个字段中不能有空格。

 bits 必须属于 \[1, 6\] 。

 begin\_number 必须属于 \[0, 999999\] 。

 如果只指定 begin\_number, 则bits 会默认取值 6。

 如果只指定 \[\] 或者 \[,\], 则begin\_number 从 0 开始取值，bits 会默认取值 6 。

 如果指定的 begin\_number 位数大于 bits 所指定的。如：\[123456,1\] 中 bits 虽被指定为 1，但是 begin\_number 为 123456，则 bits 实际会取值为 6。

 |
|AllocatePublicIP|Boolean|否|否|指定是否创建公网 IP。如果 InternetMaxBandwidthOut 设置为 0，不会分配公网 IP。|默认为 true。|
|AutoReleaseTime|String|否|否|ECS 实例自动释放的时间。|时间格式必须遵守 ISO8601 规范，如 “yyyy-MM-ddTHH:mm:ssZ” ，释放时间不能超过三年。|
|PrivateIpAddress|String|否|否|在 VPC 网络环境下，指定内网 IP，且 IP 地址不能与 VPC 网络下的其他实例重复。|无|
|DiskMappings|List|否|否|为 ECS 实例创建数据盘。|无|
|InternetChargeType|String|否|否|公网访问带宽计费方式。| 可选值：PayByBandwidth（按固定带宽计费）、PayByTraffic（按流量计费）。

 默认值： PayByTraffic （按流量付费）。

 |
|InternetMaxBandwidthIn|Integer|否|否|公网最大入网带宽，单位 Mbps。|数值范围：\[1, 100\]，默认值：100。|
|InternetMaxBandwidthOut|Integer|否|否|公网最大出网带宽，单位 Mbps。|按固定带宽计费时取值范围：\[0, 200\]，默认值为 0；按流量计费时取值范围：\[1, 200\]，必须指定。|
|IoOptimized|String|否|否|指定是否创建 I/O 优化实例。| 可选值：none（非 I/O 优化）、optimized（I/O 优化）。

 默认值：none。

 |
|SystemDiskCategory|String|否|否|指定系统盘类型。|可选值: cloud、cloud\_efficiency、cloud\_ssd、ephemeral\_ssd。|
|SystemDiskDescription|String|否|否|系统盘描述信息。|无|
|SystemDiskDiskName|String|否|否|系统盘名称。|无|
|SystemDiskSize|Number|否|是|系统盘大小。|取值范围: 40 GB ~ 500 GB。如果使用自定义镜像创建系统盘，需要保证系统盘大于自定义镜像大小。|
|Tags|List|否|否|用户自定义标签。|最多支持 20 个标签，格式如：\[\{“Key”:”tagKey”,”Value”:”tagValue”\},\{“Key”:”tagKey2”,”Value”:”tagValue2”\}\]。|
|UserData|String|否|否|创建 ECS 实例时传递的用户数据。|内容需要限制在16KB以内，不需要Base64，特殊字符需要使用 "\\" 转义。|
|ZoneId|String|否|否|可用区 ID。|无|
|VpcId|String|否|否|VPC ID。|无|
|VSwitchId|String|否|否|VSwitch ID。|无|
|KeyPairName|String|否|否|给 ECS 实例绑定的密钥对名称。如果是 Windows ECS 实例，则忽略该参数。默认为空。如果填写了 KeyPairName，Password 的内容仍旧会被设置到实例中，但是 Linux 系统中的密码登录方式会被禁止。|无|
|RamRoleName|String|否|否|实例 RAM 角色名称。|您可以使用 RAM API ListRoles查询实例RAM角色名称。请参见相关 API 文档[CreateRole](https://www.alibabacloud.com/help/doc-detail/28710.htm) 和 [ListRoles](https://www.alibabacloud.com/help/doc-detail/28713.htm)|
|SpotPriceLimit|String|否|否|设置实例的每小时最高价格。|支持最大 3 位小数，参数 SpotStrategy取值为 SpotWithPriceLimit 时生效。|
|SpotStrategy|String|否|否|后付费实例的竞价策略。|当参数 InstanceChargeType取值为 PostPaid 时为生效。 取值范围：

 NoSpot：正常按量付费实例。

 SpotWithPriceLimit：设置上限价格的竞价实例。

 SpotAsPriceGo：系统自动出价，最高按量付费价格。

 默认值：NoSpot。

 |
|DedicatedHostId|String|否|否|专有宿主机 ID。|无|
|LaunchTemplateName|String|否|否|启动模板名称。|无|
|PeriodUnit|String|否|否|购买资源的时长周期。 PeriodUnit 为 Week时：

 -   Period 取值 \{“1”, “2”, “3”, “4”\}
-   AutoRenewPeriod 取值 \{“1”, “2”, “3”\}

 PeriodUnit 为 Month 时： -   Period 取值 \{ “1”, “2”, “3”, “4”, “5”, “6”, “7”, “8”, “9”, “12”, “24”, “36”,”48”,”60”\}
-   AutoRenewPeriod 取值 \{“1”, “2”, “3”, “6”, “12”\}

 | 可选值：Week | Month

 默认值：Month。

 |
|AutoRenewPeriod|Number|否|是|每次自动续费的时长，当参数AutoRenew取值True时为必填。| 可用值：1，2，3，6，12。

 默认值：1 。

 |
|AutoRenew|String|否|是|是否要自动续费。当参数 InstanceChargeType 取值 PrePaid 时才生效。|取值范围： -   True：自动续费。
-   False（默认）：不自动续费。

 |
|InstanceChargeType|String|否|是|实例的付费方式。|取值范围： -   PrePaid：预付费，包年包月。选择该类付费方式时，您必须确认自己的账号支持余额支付/信用支付，否则将返回 `InvalidPayMethod` 的错误提示。
-   PostPaid（默认）：按量付费。

 |
|EniMappings|List|否|是|附加到实例的弹性网卡。|最多1个。|
|LaunchTemplateId|String|否|是|启动模板ID。|无|
|LaunchTemplateVersion|String|否|是|启动模板的版本。如果没有指定版本，则使用默认版本。|无。|
|Period|Number|否|是|购买资源的时长，单位为：月。当参数 InstanceChargeType 取值为 PrePaid 时才生效且为必选值。一旦指定了 DedicatedHostId，则取值范围不能超过专有宿主机的订阅时长。|取值范围： -   `PeriodUnit=Week`时，Period取值：\{“1”, “2”, “3”, “4”\}
-   `PeriodUnit=Month`时，Period取值：\{ “1”, “2”, “3”, “4”, “5”, “6”, “7”, “8”, “9”, “12”, “24”, “36”,”48”,”60”\}

 |
|NetworkType|String|否|否|ECS 实例网络类型。| 可用值：vpc | classic。

 默认值：classic。

 |
|DeletionProtection|Boolean|否|否|实例释放保护属性，指定是否支持通过控制台或 API（DeleteInstance）释放实例。|可用值：true、false。|
|DeploymentSetId|String|否|是|部署集 ID。|无。|

## DiskMappings 语法 {#section_tjh_kal_k6c .section}

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

## DiskMappings 属性 {#section_39d_e40_xo6 .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Size|String|是|否|数据盘大小，单位：GB。|无|
|Category|String|否|否|数据盘的类型。|可选值：cloud、cloud\_efficiency、cloud\_ssd、ephemeral\_ssdDefault。|
|DiskName|String|否|否|数据盘的名称。|最长 128 个字符，可包含英文、中文、数字、下划线\_（\_）、点号（.）、和连字符（-） 。|
|Description|String|否|否|数据盘的描述。|长度为 2~256 个英文或中文字符，不能以 http:// 和 https:// 开头。|
|Device|String|否|否|指定数据盘在 ECS 中的名称。|例如：/dev/xvd\[a-z\]。|
|SnapshotId|String|否|否|通过 SnapshotId 创建数据盘。|无|
|Encrypted|String|否|否|数据盘是否加密。|默认值：false。|
|KMSKeyId|String|否|否|数据盘对应的KMS密钥ID。|无|

## Tags 语法 {#section_yw8_jqs_gx1 .section}

``` {#codeblock_ha2_frx_24k .language-json}
"Tags": [
  {
    "Value": String,
    "Key": String
  }
]
```

## Tags 属性 {#section_qf5_2mx_o68 .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Key|String|是|否|无。|无。|
|Value|String|否|否|无。|无。|

## 返回值 {#section_ijt_fr2_lfb .section}

**Fn::GetAtt**

-   InstanceIds：实例 ID。由系统生成，全局唯一。是访问实例的唯一标识。
-   PrivateIps：VPC 类型实例的私网 IP 列表。当 NetworkType 为 VPC 时，这个参数生效。一个带有格式的 Json Array: \[“172.16.XX.XX”, “172.16.XX.XX”, … “172.16.XX.XX”\]，最多 100 个 IP，用半角逗号字符隔开。
-   InnerIps：Classic 类型实例的私网 IP 列表。当 NetworkType 为 Classic 时，这个参数生效。一个带有格式的 Json Array: \[“10.1.XX.XX”, “10.1.XX.XX”, … “10.1.XX.XX”\]，最多 100 个 IP，用半角逗号字符隔开。
-   PublicIps：Classic 类型实例的公网 IP 列表。当 NetworkType 为 Classic 时，这个参数生效。一个带有格式的 Json Array: \[“42.1.XX.XX”, “42.1.XX.XX”, … “42.1.XX.XX”\]，最多 100 个 IP，用半角逗号字符隔开。
-   HostNames：所有实例的主机名称列表。一个带有格式的 Json Array: \[“host1”, “host2”, … “host3”\]。
-   OrderId: 实例的订单id列表。
-   ZoneIds: 可用区 ID。
-   RelatedOrderIds: 已创建ecs实例的相关订单id列表。

## 示例 {#section_ygv_fr2_lfb .section}

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

