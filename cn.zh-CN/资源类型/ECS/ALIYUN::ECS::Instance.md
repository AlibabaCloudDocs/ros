# ALIYUN::ECS::Instance {#concept_51198_zh .concept}

ALIYUN::ECS::Instance类型用于创建 ECS 实例。

## 语法 {#section_ljn_3d2_lfb .section}

``` {#codeblock_zfi_624_1ju .language-json}
{
  "Type": "ALIYUN::ECS::Instance",
  "Properties": {
    "DedicatedHostId": String,
    "Period": Number,
    "AutoRenew": String,
    "RamRoleName": String,
    "IoOptimized": String,
    "InternetChargeType": String,
    "PrivateIpAddress": String,
    "KeyPairName": String,
    "SystemDiskDiskName": String,
    "PeriodUnit": String,
    "Description": String,
    "Tags": List,
    "HostName": String,
    "AutoRenewPeriod": Number,
    "ImageId": String,
    "ResourceGroupId": String,
    "InstanceChargeType": String,
    "VSwitchId": String,
    "Password": String,
    "InstanceType": String,
    "SystemDiskCategory": String,
    "UserData": String,
    "SystemDiskSize": Number,
    "ZoneId": String,
    "InternetMaxBandwidthOut": Integer,
    "VpcId": String,
    "SpotStrategy": String,
    "InstanceName": String,
    "InternetMaxBandwidthIn": Integer,
    "DeletionProtection": Boolean,
    "DeploymentSetId": String,
    "SecurityGroupId": String,
    "SpotPriceLimit": String,
    "HpcClusterId": String,
    "AllocatePublicIP": Boolean,
    "SystemDiskDescription": String,
    "DiskMappings": List
  }
}
```

## 属性 {#section_atw_kd2_lfb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ResourceGroupId|String|否|否|实例所在的资源组 ID。|无。|
|ImageId|String|是|是|ECS 实例的镜像 ID，包括公共镜像、自定义镜像和云市场镜像。| 在编辑模板时，只需要指定镜像类型或者镜像类型和版本，ROS 就会自动选择适配的公共镜像 ID。

 可以用星号通配符 （\*） 指代镜像 ID 的某一部分。

 以所有阿里云提供的 Ubuntu 的公共镜像为例，在给 ECS 实例指定公共镜像 ID 时，规则如下：

-   指定 ubuntu，最终会匹配 ubuntu16\_0402\_64\_20G\_alibase\_20170818.vhd。
-   指定 ubuntu\_14，最终会匹配 ubuntu\_14\_0405\_64\_20G\_alibase\_20170824.vhd。
-   指定 ubuntu\*14\*32，最终会匹配 ubuntu\_14\_0405\_32\_40G\_alibase\_20170711.vhd。
-   指定 ubuntu\_16\_0402\_32，最终会匹配 ubuntu\_16\_0402\_32\_40G\_alibase\_20170711.vhd。

 |
|InstanceType|String|是|否|ECS 实例规格。详情请参见 [ECS实例规格](https://help.aliyun.com/document_detail/25378.html)。|无。|
|SecurityGroupId|String|是|否|新建实例所属安全组。|无。|
|Description|String|否|否|描述信息。|最长 256 个字符。|
|InstanceName|String|否|否|实例名称。|最长 128 个字符，可包含英文、中文、数字、下划线（\_）、点（.）、连字符（-）。|
|Password|String|否|否|ECS 实例登录密码。| 字符长度为 \[8, 30\]。

 必须同时包含三项大、小写字母，数字和特殊符号。

 支持以下特殊字符：\( \) ‘ ~ ! @ \# $ % ^ & \* - + = | \{ \} \[ \] : ; ‘ < \> , . ? / - 。如果指定该参数，请务必使用 HTTPS 协议调用 API， 以避免密码泄露。

 |
|HostName|String|否|否|云服务器的主机名。| 最少 2 个字符。

 点（.）和连字符（-）不能作为 hostname 的首尾字符，且不能连续使用。

 Windows 平台支持最长 15 个字符，支持字母（不限制大小写）、数字和连字符（-）；不支持点号（.）；不能全是数字。

 其它（Linux 等）平台支持最长 30 个字符，支持多个点号（.），点之间为一段；每段可以由大小写字母、数字和连字符（-）组成。

 |
|AllocatePublicIP|Boolean|否|否|指定是否创建公网 IP。如果 InternetMaxBandwidthOut 设置为 0，不会分配公网 IP。|默认值： True。|
|PrivateIpAddress|String|否|否|在 VPC 网络环境下，指定内网 IP。IP 地址不能与 VPC 网络下的其它实例重复。|无。|
|InternetChargeType|String|否|否|访问公网计费方式。| 可选值: PayByBandwidth（按固定带宽计费）、PayByTraffic（按流量计费）。

 默认值： PayByTraffic（按流量付费）。

 |
|InternetMaxBandwidthIn|Integer|否|否|公网最大入网带宽，单位：Mbps。|取值范围：\[1, 100\]，默认值：100。|
|InternetMaxBandwidthOut|Integer|否|否|公网最大出网带宽，单位：Mbps。| 按固定带宽计费时取值范围：\[0, 200\]，默认值为 0。

 按流量计费时取值范围：\[1, 200\]，必须指定数值。

 |
|IoOptimized|String|否|否|指定是否创建 I/O 优化实例。|可选值：none（非 I/O 优化）、optimized（I/O 优化），默认值：none。|
|DiskMappings|List|否|否|指定需要挂载的磁盘。|最多支持 16 块磁盘。|
|SystemDiskCategory|String|否|否|指定系统盘类型。|可选值：cloud、cloud\_efficiency、cloud\_ssd、 ephemeral\_ssd。|
|SystemDiskDescription|String|否|否|系统盘描述信息。|无。|
|SystemDiskDiskName|String|否|否|系统盘名称。|无。|
|SystemDiskSize|Number|否|是|系统盘大小。单位：GB。| 取值范围：\[40, 500\]。

 如果使用自定义镜像创建系统盘，需要保证系统盘大于自定义镜像大小。

 |
|Tags|List|否|否|用户自定义标签。|最多支持 20 个标签，格式: \[\{“Key”:”tagKey”,”Value”:”tagValue”\},\{“Key”:”tagKey2”,”Value”:”tagValue2”\}\]。|
|UserData|String|否|否|创建 ECS 实例时传递的用户数据。|内容需要限制在 16KB 以内，不需要 Base64，特殊字符需要使用 "\\" 转义。|
|ZoneId|String|否|否|可用区 ID。|无。|
|HpcClusterId|String|否|否|实例所属的HPC集群ID。|无。|
|VpcId|String|否|否|VPC ID。|无。|
|VSwitchId|String|否|否|VSwitch ID。|无。|
|InstanceChargeType|String|否|否|指定创建按量付费或是预付费 ECS 实例。| 可选值：Prepiad（预付费）、Postpaid（按量付费）。

 默认值：Postpaid。如果指定 Prepaid，必须确保余额充足，否则会导致实例创建失败。

 |
|Period|Number|否|否|当 InstanceChargeType 指定为 Prepaid，必需指定付费周期；当 InstanceChargeType 指定为 Postpaid，忽略该值。|可选值：1-9、12、24、36，单位：月。|
|KeyPairName|String|否|否|ECS 实例绑定的密钥对名称。| Windows 系统保留默认值为空。

 在 Linux 系统中，如果指定该参数，Password 的内容仍旧会被设置到实例中，但是密码登录方式会默认被禁止，采用密钥对验证登录。

 |
|RamRoleName|String|否|否|实例 RAM 角色名称。可以调用 ListRoles 查询。详情请参见[CreateRole](https://help.aliyun.com/document_detail/28710.html)和 [ListRoles](https://help.aliyun.com/document_detail/28713.html)|无。|
|SpotPriceLimit|String|否|否|设置实例的每小时最高价格。|支持最多 3 位小数，参数 SpotStrategy 取值为 SpotWithPriceLimit 时该参数生效。|
|SpotStrategy|String|否|否|按量付费实例的竞价策略。|参数 InstanceChargeType 取值为 PostPaid 时生效。取值范围： NoSpot：正常按量付费实例。

 SpotWithPriceLimit：设置上限价格的竞价实例。

 SpotAsPriceGo：系统自动出价，最高不超过按量付费价格。

 默认值：NoSpot。

 |
|DedicatedHostId|String|否|否| 是否在专有宿主机上创建 ECS 实例。您可以通过 [DescribeDedicatedHosts](https://help.aliyun.com/document_detail/94572.html) 查询专有宿主机 ID 列表。

 由于专有宿主机不支持创建抢占式实例，指定 DedicatedHostId 参数后，会自动忽略请求中的 SpotStrategy 和 SpotPriceLimit 设置。

 |无。|
|PeriodUnit|String|否|否|购买资源的时长。 PeriodUnit 为 Week 时：

 -   Period 取值 \{“1”, “2”, “3”, “4”\}
-   AutoRenewPeriod 取值 \{“1”, “2”, “3”\}

 PeriodUnit 为 Month 时： -   Period 取值 \{ “1”, “2”, “3”, “4”, “5”, “6”, “7”, “8”, “9”, “12”, “24”, “36”,”48”,”60”\}
-   AutoRenewPeriod 取值 \{“1”, “2”, “3”, “6”, “12”\}

 默认值：Month|可选值：Week | Month。默认值：Month。|
|AutoRenewPeriod|Number|否|否|每次自动续费的时长，当参数AutoRenew 取值 True 时为必填。|取值范围：1 | 2 | 3 | 6 |12。|
|AutoRenew|String|否|否|是否要自动续费。当参数 InstanceChargeType 取值 PrePaid 时才生效。|取值范围： -   True：自动续费。
-   False（默认）：不自动续费。

 |
|DeletionProtection|Boolean|否|否|实例释放保护属性，指定是否支持通过控制台或 API（DeleteInstance）释放实例。|可用值：True、False。|
|DeploymentSetId|String|否|是|部署集 ID。|无。|

## DiskMappings 语法 {#section_3b8_74v_45b .section}

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

## DiskMappings 属性 {#section_8il_fs8_t3z .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Size|String|是|否|数据盘大小，单位：GB。|无|
|Category|String|否|否|数据盘的类型。| 可选值：cloud、cloud\_efficiency、cloud\_ssd、ephemeral\_ssd。

 默认值：cloud。

 |
|DiskName|String|否|否|数据盘的名称。|最长 128 个字符，可包含英文、中文、数字、下划线（\_）、点（.）、连字符（-）。|
|Description|String|否|否|描述信息。|取值范围：\[2,256\]，默认值为空。|
|Device|String|否|否|指定数据盘的设备名称。|如不指定，则默认由系统按顺序分配，即从/dev/xvdb到/dev/xvdz。|
|SnapshotId|String|否|否|创建数据盘使用的快照。|无|

## Tags 语法 {#section_gff_lrv_g26 .section}

``` {#codeblock_4cc_u4e_0rm .language-json}
"Tags": [
  {
    "Value": String,
    "Key": String
  }
]
```

## Tags 属性 {#section_fes_3kc_798 .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Key|String|是|否|无。|无。|
|Value|String|否|否|无。|无。|

## 返回值 {#section_dx4_222_lfb .section}

**Fn::GetAtt**

-   InstanceId：实例 ID。由系统生成，实例的全局唯一标识。
-   PrivateIp：VPC 类型实例的私网 IP。当NetworkType为 VPC 时，该参数生效。
-   InnerIp：Classic 类型实例的私网 IP。当NetworkType为 Classic 时，该参数生效。
-   PublicIp：Classic 类型实例的公网 IP 列表。当 NetworkType为 Classic 时，该参数生效。
-   ZoneId：可用区 ID。
-   HostName：实例的主机名称。

## 示例 {#section_z3v_222_lfb .section}

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

