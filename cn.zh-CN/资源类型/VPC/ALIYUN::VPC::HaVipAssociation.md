# ALIYUN::VPC::HaVipAssociation {#concept_mtg_rln_tgb .concept}

ALIYUN::VPC::HaVipAssociation类型用于将HaVip实例绑定到相同VPC相同VSwitch的ECS实例上。

**说明：** 

-   1个ECS实例只能同时绑定5个HaVip实例。
-   1个HaVip实例只能同时绑定2个ECS实例。

## 语法 {#section_ksl_112_lfb .section}

```language-json
{
  "Type": "ALIYUN::VPC::HaVipAssociation",
  "Properties": {
    "HaVipId":  String,
    "InstanceId":  String,
  }
}
```

## 属性 {#section_gjx_w1t_jgb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|HaVipId|String|是|否|要绑定的HaVip实例的ID。|无|
|InstanceId|String|是|否|要绑定的ECS实例的ID。|无|

## 返回值 {#section_zqt_33n_tgb .section}

**Fn::GetAtt**

无

## 示例 {#section_art_33n_tgb .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "HaVipAssociation": {
      "Type": "ALIYUN::VPC::HaVipAssociation",
      "Properties": {
        "HaVipId": "",
        "InstanceId": ""
      }
    }
  }
}
```

