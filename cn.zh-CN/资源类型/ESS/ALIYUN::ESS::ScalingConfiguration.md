# ALIYUN::ESS::ScalingConfiguration {#concept_51203_zh .concept}

ALIYUN::ESS::ScalingConfiguration 类型可用于创建伸缩配置。

## 语法 {#section_k4p_5d1_mfb .section}

``` {#codeblock_j79_nqv_ah7 .language-json}
{
  "Type": "ALIYUN::ESS::ScalingConfiguration",
  "Properties": {
    "PasswordInherit": Boolean,
    "DiskMappings": List,
    "RamRoleName": String,
    "IoOptimized": String,
    "InternetChargeType": String,
    "KeyPairName": String,
    "InstanceId": String,
    "InstanceTypes": List,
    "ImageId": String,
    "ResourceGroupId": String,
    "SpotStrategy": String,
    "InstanceType": String,
    "SystemDiskCategory": String,
    "SystemDiskSize": Integer,
    "InternetMaxBandwidthOut": Integer,
    "InstanceName": String,
    "InternetMaxBandwidthIn": Integer,
    "ScalingConfigurationName": String,
    "UserData": String,
    "DeploymentSetId": String,
    "SecurityGroupId": String,
    "SpotPriceLimit": Number,
    "HpcClusterId": String,
    "ScalingGroupId": String,
    "SpotPriceLimitForInstanceType": Map,
    "TagList": List
  }
}
```

## 属性 {#section_zvc_wd1_mfb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ResourceGroupId|String|否|是|实例所在的资源组ID。|无。|
|DeploymentSetId|String|否|否|部署集 ID。|无。|
|HpcClusterId|String|否|否|实例所属的EHPC集群ID。|无。|
|ScalingGroupId|String|是|否|伸缩配置所属的伸缩组 ID 。|无|
|DiskMappings|List|否|否|指定需要挂载的磁盘。|最多支持 16 块磁盘。|
|InternetChargeType|String|否|否|公网访问带宽计费方式。| 可选值: PayByBandwidth（按固定带宽计费）、PayByTraffic（按流量计费）。

 默认值：PayByTraffic（按流量计费）。

 |
|InternetMaxBandwidthIn|Integer|否|否|公网最大入网带宽。单位：Mbps。| 数值范围：\[1, 100\]。

 默认值：100。

 |
|InternetMaxBandwidthOut|Integer|否|否|公网最大出网带宽。单位：Mbps。| 按固定带宽计费时取值范围：\[0, 200\]，默认值为 0。

 按流量计费时取值范围：\[1, 200\], 必须指定。

 |
|InstanceId|String|否|否|创建伸缩配置依据的 ECS 实例 。|无|
|SystemDiskCategory|String|否|否|指定系统盘类型。|可选值: \_cloud、cloud\_efficiency、cloud\_ssd和 ephemeral\_ssd。|
|ImageId|String|否|否|用于启动 ECS 实例的镜像 ID，包括公共镜像、自定义镜像和云市场镜像。|请参见[ECS 公共镜像列表](https://ros.console.aliyun.com/#/product/cn-hangzhou/list/imageList)。|
|InstanceType|String|否|否|ECS实例规格 。|请参见 [ECS实例规格](https://www.alibabacloud.com/help/doc-detail/25378.htm)。|
|SecurityGroupId|String|否|否|指定创建实例所属的安全组。|无|
|IoOptimized|String|否|否|指定是否创建IO优化实例。| 可选值：none（非 I/O 优化）和 optimized（I/O 优化）。

 默认：none。

 |
|ScalingConfigurationName|String|否|否|伸缩配置的显示名称。|长度为 2-40 个英文或中文字符，以数字、大小字母或中文开头，可包含字母、汉字、数字、下划线（\_）、连字符（-）和点号（.）。同一用户账号，同一地域，同一伸缩组内，名称不能重复。如果没有指定该参数，默认值为 ScalingConfigurationId。|
|KeyPairName|String|否|否|给 ECS 实例绑定的密钥对名称 。|如果是 Windows ECS 实例，则忽略该参数。默认为空。如果填写了 KeyPairName，Password 的内容仍旧会被设置到实例中，但是在 Linux 系统中的密码登录方式会被初始化成禁止。|
|RamRoleName|String|否|否|实例 RAM 角色名称。|您可以使用 RAM API ListRoles查询。请参见[CreateRole](https://www.alibabacloud.com/help/doc-detail/28710.htm)和 [ListRoles](https://www.alibabacloud.com/help/doc-detail/28713.htm)|
|SystemDiskSize|Integer|否|是|系统盘大小。|取值范围: 40 GB ~ 500 GB。如果使用自定义镜像创建系统盘，需要保证系统盘大于自定义镜像大小。|
|UserData|String|否|否|创建 ECS 实例时传递的用户数据。|内容需要限制在16KB以内，不需要Base64，特殊字符需要使用 "\\" 转义。|
|InstanceTypes|List|否|否|指定的供弹性伸缩选择的多个 ECS 实例规格。|最多可以指定 10 个 ECS 实例规格。如果指定了 InstanceType，将忽略 InstanceType 的值。|
|PasswordInherit|Boolean|否|是|是否使用镜像预设的密码。使用该参数时，您需要所用镜像已经预设了密码。|无|
|TagList|List|否|是|实例标签。标签以键值对方式传入，最多可以使用 20组标签。Key 和 Value 的使用要求如下： -   Key 最多支持 64 个字符，不支持以 aliyun、http:// 和 https:// 开头。一旦使用标签，Key 不允许为空字符串。
-   Value 最多支持 128 个字符，不支持以 aliyun、http:// 和 https:// 开头。Value 可以为空字符串。

 |无|
|SpotStrategy|String|否|是|后付费实例的抢占策略。取值范围： -   NoSpot：正常按量付费实例
-   SpotWithPriceLimit：设置上限价格的抢占式实例
-   SpotAsPriceGo：系统自动出价，跟随当前市场实际价格

 默认值：NoSpot。

 |可用值：NoSpot | SpotWithPriceLimit | SpotAsPriceGo。|
|InstanceName|String|否|是|基于当前伸缩配置创建出来的实例的名称。|无|
|SpotPriceLimit|Number|否|是|抢占式实例对应的出价，其中 N 的取值范围：1-10。SpotStrategy 取值为 SpotWithPriceLimit时生效。支持最多3位小数，所有实例类型的默认值，可以被SpotPriceLimitForInstanceType覆盖。|无|
|SpotPriceLimitForInstanceType|Map|否|是|抢占式实例的实例规格，其中 N 的取值范围：1-10。SpotStrategy 取值为 SpotWithPriceLimit时生效。如\{"key1":"value1"，"key2":"value2"，…“key5":"value5"\}。 Key ecs实例类型，Value 支持最多3位小数。

 |无|

## DiskMappings语法 {#section_cvf_221_mfb .section}

``` {#codeblock_nw4_z1f_v4c .language-json}
"DiskMappings": [
  {
    "Category": String,
    "Device": String,
    "SnapshotId": String,
    "Size": String,
    "Encrypted": String,
    "KMSKeyId": String,
    "Description": String,
    "DiskName": String
  }
]
```

## DiskMappings 属性 {#section_ej4_e8i_zho .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Size|String|是|否|数据盘大小。单位：GB|无|
|Category|String|否|否|数据盘的类型。|可选值：cloud、cloud\_efficiency、cloud\_ssd和 ephemeral\_ssd。|
|DiskName|String|否|否|数据盘的名称 。|长度为 2~128 个英文或中文字符。必须以大小字母或中文开头，不能以 http:// 和 https:// 开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。 默认值：空。

 |
|Description|String|否|否|数据盘的描述。|长度为 2~256 个英文或中文字符，不能以 http:// 和 https:// 开头。|
|Device|String|否|否|数据盘挂载点。|例如：/dev/xvd\[a-z\]。|
|SnapshotId|String|否|否|用于创建数据盘的 SnapshotId。|无|
|Encrypted|String|否|否|数据盘是否加密。|默认值：false。|
|KMSKeyId|String|否|否|数据盘对应的KMS密钥ID。|无|

## TagList语法 {#section_y5m_jod_yzj .section}

``` {#codeblock_7ys_9p9_3qd .language-json}
"TagList": [
  {
    "Value": String,
    "Key": String
  }
]
```

## TagList属性 {#section_46t_1x3_9fy .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Key|String|是|否|无|无|
|Value|String|是|否|无|无|

## 返回值 {#section_bsn_k21_mfb .section}

**Fn::GetAtt**

ScalingConfigurationId：伸缩配置的 ID。由系统生成，全局唯一。

## 示例 {#section_ozp_n21_mfb .section}

``` {#codeblock_oz9_nxq_8is .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "ScalingConfiguration": {
      "Type": "ALIYUN::ESS::ScalingConfiguration",
      "Properties": {
        "ImageId": "ubuntu1404_64_20G_aliaegis_20150325.vhd",
        "InstanceType": "ecs.t1.small",
        "InstanceId": "i-25xhh****",
        "InternetChargeType": "PayByTraffic",
        "InternetMaxBandwidthIn": 1,
        "InternetMaxBandwidthOut": 20,
        "SystemDisk_Category": "cloud",
        "ScalingGroupId": "bwhtvpcBcKYac9fe3vd0****",
        "SecurityGroupId": "sg-25zwc****",
        "DiskMappings": [
          {
            "Size": 10
          },
          {
            "Category": "cloud",
            "Size": 10
          }
        ]
      }
    }
  },
  "Outputs": {
    "ScalingConfiguration": {
      "Value": {"get_attr": ["ScalingConfigurationId"]}
    }
  }
}
```

