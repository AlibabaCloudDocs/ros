# ALIYUN::ECS::InstanceClone {#concept_48279_zh .concept}

ALIYUN::ECS::InstanceClone类型用于克隆一个 ECS 实例。

## 语法 {#section_ysq_lmk_w3y .section}

``` {#codeblock_0j6_ilj_tew .language-json}
{
  "Type": "ALIYUN::ECS::InstanceClone",
  "Properties": {
    "DeletionProtection": Boolean,
    "DiskMappings": List,
    "LoadBalancerIdToAttach": String,
    "Description": String,
    "BackendServerWeight": Integer,
    "Tags": List,
    "SecurityGroupId": String,
    "RamRoleName": String,
    "ImageId": String,
    "ResourceGroupId": String,
    "SpotPriceLimit": String,
    "InstanceChargeType": String,
    "SourceInstanceId": String,
    "Period": Number,
    "SpotStrategy": String,
    "Password": String,
    "InstanceName": String,
    "InternetMaxBandwidthIn": Integer,
    "ZoneId": String,
    "KeyPairName": String
  }
}
```

## 属性 {#section_nbg_ck2_lfb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ResourceGroupId|String|否|否|实例所在的资源组ID。|无。|
|SourceInstanceId|String|是|否|待克隆的源 ECS 实例的 ID。|克隆实例规格、镜像、带宽收费方式、带宽限制、网络类型等所有实例数据和设置。如果源 ECS 实例加入多个安全组，新实例会加入源实例的第一个安全组。|
|BackendServerWeight|Integer|否|否|ECS 实例在负载均衡器实例中的权重。|取值范围：\[0, 100\]，默认值是 100。|
|LoadBalancerIdToAttach|String|否|否|ECS 实例待加入的负载均衡实例的 ID。|无|
|Description|String|否|否|描述信息。|最长 256 个字符。|
|ImageId|String|否|是|用于启动 ECS 实例的镜像 ID，包括公共镜像、自定义镜像和云市场镜像，请参见 [ECS 公共镜像列表](https://ros.console.aliyun.com/#/product/cn-hangzhou/list/imageList)。| 在编辑模板时，仅需指定镜像的类型，或类型和版本，ROS 会自动选择适配的公共镜像 ID。

 可以用星号通配符 （\\\*） 指代镜像 ID 的某一部分。

 以阿里云提供的全部 Ubuntu 公共镜像为例，在为 ECS 实例指定公共镜像 ID 时，可以按照如下方式：

 指定：ubuntu

 最终会匹配：ubuntu16\_0402\_64\_20G\_alibase\_20170818.vhd

 指定：ubuntu\_14

 最终会匹配：ubuntu\_14\_0405\_64\_20G\_alibase\_20170824.vhd

 指定：ubuntu\*14\*32

 最终会匹配：ubuntu\_14\_0405\_32\_40G\_alibase\_20170711.vhd

 指定：ubuntu\_16\_0402\_32

 最终会匹配：ubuntu\_16\_0402\_32\_40G\_alibase\_20170711.vhd

 |
|SecurityGroupId|String|否|否|新建实例所属安全组。|无|
|InstanceName|String|否|否|实例名称。|最长 128 个字符，可包含英文、中文、数字、下划线（\_）、点（.）、连字符（-）。|
|Password|String|否|否|ECS 实例登录密码。| 长度为 \[8, 30\]。

 必须同时包含大写或小写字母、数字和特殊字符。

 特殊字符包括以下：\( \) ' ~ ! @ \# $ % ^ & \* - + = | \{ \} \[ \] : ; ‘ < \> , . ? /。

 如果指定该参数，必须使用 HTTPS 协议调用 API，以免密码泄露。

 |
|DiskMappings|List|否|否|需要挂载的磁盘。|最多支持 16块磁盘。|
|Tags|List|否|否|用户自定义标签。|最多支持 20个标签，格式: \[\{"Key":"tagKey","Value":"tagValue"\}、\{"Key":"tagKey2","Value":"tagValue2"\}\]。|
|ZoneId|String|否|否|可用区 ID。|无|
|InstanceChargeType|String|否|否|实例的付费方式。| 可选值：Prepiad、Postpaid。

 默认值：Postpaid。如果指定为 Prepaid，必须确保余额充足，否则创建失败。

 |
|Period|Number|否|否|若 \`InstanceChargeType\` 为 Prepaid，必须设置此参数；若 \`InstanceChargeType\` 为 Postpaid，忽略此参数。|可选值：1-9、12、24、36，单位：月。|
|KeyPairName|String|否|否|ECS 实例绑定的密钥对名称。| Windows 系统保留默认值为空。

 在 Linux 系统中，如果指定该参数，Password 的内容仍旧会被设置到实例中，但是密码登录方式会默认被禁止，采用密钥对验证登录。

 |
|RamRoleName|String|否|否|实例RAM 角色名称。可以调用ListRoles查询。请参见[CreateRole](https://www.alibabacloud.com/help/doc-detail/28710.htm)和 [ListRoles](https://www.alibabacloud.com/help/doc-detail/28713.htm)|无|
|SpotPriceLimit|String|否|否|设置实例的每小时最高价格。|支持最多 3 位小数，参数 SpotStrategy取值为 SpotWithPriceLimit 时该参数生效。|
|SpotStrategy|String|否|否|按量付费实例的竞价策略。|参数 InstanceChargeType取值为 PostPaid 时生效。取值范围： NoSpot：正常按量付费实例。

 SpotWithPriceLimit：设置上限价格的竞价实例。

 SpotAsPriceGo：系统自动出价，最高不超过按量付费价格。

 默认值：NoSpot。

 |
|InternetMaxBandwidthIn|Integer|否|否|公网入带宽最大值，单位为Mbit/s。|取值范围：\[1,200\]。|
|DeletionProtection|Boolean|否|否|实例释放保护属性，指定是否支持通过控制台或 API（DeleteInstance）释放实例。|可用值：true、false。|

## DiskMappings 语法 {#section_zy1_0s5_vsf .section}

``` {#codeblock_p8c_f6m_3bd .language-json}
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

## DiskMappings 属性 {#section_y8y_lnw_k29 .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Size|String|是|否|数据盘大小，单位：GB。|无|
|Category|String|否|否|数据盘类型。| 可选值：cloud、cloud\_efficiency、cloud\_ssd、ephemeral\_ssd。

 默认值：cloud。

 |
|DiskName|String|否|否|数据盘名称。|最长 128 个字符，可包含英文、中文、数字、下划线（\_）、点（.）、连字符（-）。|
|Description|String|否|否|描述信息。|取值范围：\[2, 256\]，默认值为空。|
|Device|String|否|否|指定数据盘的设备名称。|如不指定，则默认由系统按顺序分配，即从/dev/xvdb到/dev/xvdz。|
|SnapshotId|String|否|否|创建数据盘使用的快照。|无|

## Tags 语法 {#section_lh3_atr_hq8 .section}

``` {#codeblock_6q6_9cs_32r .language-json}
"Tags": [
  {
    "Value": String,
    "Key": String
  }
]
```

## Tags 属性 {#section_yna_hli_1bd .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Key|String|是|否|标签键 ，不允许为空字符串。最多支持 64 个字符，不能以 aliyun 和 acs: 开头，不能包含 http:// 或者 https:// 。|无|
|Value|String|否|否|标签值 ，可以为空字符串。最多支持 128 个字符，不能以 aliyun 和 acs: 开头，不能包含 http:// 或者 https:// 。|无|

## 返回值 {#section_wy1_jm2_lfb .section}

**Fn::GetAtt**

-   InstanceId：实例 ID。由系统生成，实例的全局唯一标识。
-   PrivateIp：VPC 类型实例的私网 IP。 当NetworkType为 VPC 时，该参数生效。
-   InnerIp：Classic 类型实例的私网 IP。 当 NetworkType为 Classic 时，该参数生效。
-   PublicIp：Classic 类型实例的公网 IP 列表。 当NetworkType 为 Classic 时，该参数生效。
-   ZoneId：可用区 ID。
-   HostName：实例的主机名称。

## 示例 {#section_vwc_jm2_lfb .section}

``` {#codeblock_ehn_79m_xpe .language-json}
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

