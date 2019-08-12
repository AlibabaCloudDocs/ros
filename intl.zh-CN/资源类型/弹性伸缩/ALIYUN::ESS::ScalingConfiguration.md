# ALIYUN::ESS::ScalingConfiguration {#concept_51203_zh .concept}

ALIYUN::ESS::ScalingConfiguration 类型可用于创建伸缩配置。

## 语法 {#section_k4p_5d1_mfb .section}

```language-json
{
  "Type": "ALIYUN::ESS::ScalingConfiguration",
  "Properties": {
    "DiskMappings": List,
    "InternetMaxBandwidthIn": Integer,
    "InstanceId": String,
    "SecurityGroupId": String,
    "SystemDiskCategory": String,
    "SystemDiskSize": Integer,
    "ImageId": String,
    "InternetMaxBandwidthOut": Integer,
    "IoOptimized": String,
    "ScalingGroupId": String,
    "InternetChargeType": String,
    "InstanceType": String,
    "ScalingConfigurationName": String,
    "InstanceTypes": List,
    "KeyPairName": String,
    "UserData": String,
    "RamRoleName": String
  }
}

```

## 属性 {#section_zvc_wd1_mfb .section}

|属性名称|类型|是否必需|允许更新|描述|约束|
|----|--|----|----|--|--|
|ScalingGroupId|string|是|否|伸缩配置所属的伸缩组 ID|无|
|DiskMappings|list|否|否|指定需要挂载的磁盘|最多支持 4 块磁盘。|
|InternetChargeType|string|否|否|公网访问带宽计费方式|可选值: PayByBandwidth（按固定带宽计费）、PayByTraffic（按流量计费）。默认值：PayByTraffic（按流量计费）。|
|InternetMaxBandwidthIn|integer|否|否|公网最大入网带宽 单位：Mbps|数值范围：\[1, 100\]。默认值：100。|
|InternetMaxBandwidthOut|integer|否|否|公网最大出网带宽单位：Mbps|按固定带宽计费时取值范围：\[0, 200\]，默认值为 0。按流量计费时取值范围：\[1, 200\], 必须指定。|
|InstanceId|string|否|否|创建伸缩配置依据的 ECS 实例|无|
|SystemDiskCategory|string|否|否|指定系统盘类型|可选值: \_cloud、cloud\_efficiency、cloud\_ssd、和 ephemeral\_ssd。|
|ImageId|string|否|否|用于启动 ECS 实例的镜像 ID，包括公共镜像、自定义镜像和云市场镜像。|见[ECS 公共镜像列表](https://ros.console.aliyun.com/#/product/cn-hangzhou/list/imageList)。|
|InstanceType|string|否|否|ECS实例规格|见[ECS实例规格列表](https://www.alibabacloud.com/help/doc-detail/25378.htm)。|
|SecurityGroupId|string|否|否|指定创建实例所属的安全组|无|
|IoOptimized|string|否|否|指定是否创建IO优化实例|可选值：none（非 I/O 优化）和 optimized（I/O 优化）。默认：none。|
|ScalingConfigurationName|string|否|否|伸缩配置的显示名称|长度为 2-40 个英文或中文字符，以数字、大小字母或中文开头，可包含字母、汉字、数字、下划线\_（\_）、连字符（-）、和点号（.）。同一用户账号，同一地域，同一伸缩组内，名称不能重复。如果没有指定该参数，默认值为 ScalingConfigurationId。|
|KeyPairName|string|否|否|给 ECS 实例绑定的密钥对名称|如果是 Windows ECS 实例，则忽略该参数。默认为空。如果填写了 KeyPairName，Password 的内容仍旧会被设置到实例中，但是在 Linux 系统中的密码登录方式会被初始化成禁止。|
|RamRoleName|string|否|否|实例 RAM 角色名称|您可以使用 RAM API ListRoles查询实例 RAM 角色名称。参考相关 API [CreateRole](https://www.alibabacloud.com/help/doc-detail/28710.htm)和 [ListRoles](https://www.alibabacloud.com/help/doc-detail/28713.htm)。|
|SystemDiskSize|string|否|是|系统盘大小|取值范围: 40 GB ~ 500 GB。如果使用自定义镜像创建系统盘，需要保证系统盘大于自定义镜像大小。|
|UserData|string|否|否|创建 ECS 实例时传递的用户数据|内容需要限制在16KB以内，不需要Base64，特殊字符需要使用 "\\" 转义。|
|InstanceTypes|list|否|否|指定的供弹性伸缩选择的多个 ECS 实例规格|最多可以指定 10 个 ECS 实例规格。如果指定了 InstanceType，将忽略 InstanceType 的值。|

## DiskMappings语法 {#section_cvf_221_mfb .section}

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

## DiskMappings 属性 { .section}

|属性名称|类型|是否必需|允许更新|描述|约束|
|----|--|----|----|--|--|
|Size|string|是|否|数据盘大小单位：GB|无|
|Category|string|否|否|数据盘的类型|可选值：cloud、cloud\_efficiency、cloud\_ssd、和 ephemeral\_ssdDefault。|
|DiskName|string|否|否|数据盘的名称|最长128个字符，可包含英文、中文、数字、下划线\_（\_）、连字符（-）、和点号（.）。|
|Description|string|否|否|描述信息|取值范围：\[2,256\]。 默认值是空。|
|Device|string|否|否|数据盘在 ECS 实例中的设备名称|例如：/dev/xvd\[a-z\]。|
|SnapshotId|string|否|否|用于创建数据盘的 SnapshotId|无|

## 返回值 {#section_bsn_k21_mfb .section}

**Fn::GetAtt**

ScalingConfigurationId：伸缩配置的 ID。由系统生成，全局唯一。

## 示例 {#section_ozp_n21_mfb .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "ScalingConfiguration": {
      "Type": "ALIYUN::ESS::ScalingConfiguration",
      "Properties": {
        "ImageId": "ubuntu1404_64_20G_aliaegis_20150325.vhd",
        "InstanceType": "ecs.t1.small",
        "InstanceId": "i-25xhhcqbu",
        "InternetChargeType": "PayByTraffic",
        "InternetMaxBandwidthIn": 1,
        "InternetMaxBandwidthOut": 20,
        "SystemDisk_Category": "cloud",
        "ScalingGroupId": "bwhtvpcBcKYac9fe3vd0kv7E",
        "SecurityGroupId": "sg-25zwc3se0",
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

