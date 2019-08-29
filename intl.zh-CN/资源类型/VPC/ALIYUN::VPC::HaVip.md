# ALIYUN::VPC::HaVip {#concept_kg5_h3n_tgb .concept}

ALIYUN::VPC::HaVip类型用于申请 HaVip。

**说明：** 每个VPC下只能同时拥有最多5个HaVip实例。

## 语法 {#section_ksl_112_lfb .section}

```language-json
{
  "Type": "ALIYUN::VPC::HaVip",
  "Properties": {
    "VSwitchId":  String,
    "IpAddress":  String,
    "Description": String
  }
}
```

## 属性 {#section_gjx_w1t_jgb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|VSwitchId|String|是|否|指定HaVip位于哪个虚拟交换机下。|否|
|IpAddress|String|否|否| HaVip的IP地址。

 不填写该地址，则随机指定当前交换机下的一个地址。

 |否|
|Description|String|否|否| 自定义描述信息。

 2到256个英文或中文字符，不能以 http:// 或 https:// 开头。不填为空。

 |否|

## 返回值 {#section_zqt_33n_tgb .section}

**Fn::GetAtt**

-   HaVipId：分配的HaVip的 ID。

## 示例 {#section_art_33n_tgb .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "HaVip": {
      "Type": "ALIYUN::VPC::HaVip",
      "Properties": {
        "VSwitchId": "vsw-abe5qu9utjer7gg87e2lh",
        "IpAddress": "192.168.1.100"
      }
    }
  },
  "Outputs": {
    "HaVipId": {
      "Value" : {"Fn::GetAtt": ["HaVip", "HaVipId"]}
    }
  }
}
```

