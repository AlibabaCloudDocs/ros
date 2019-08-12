# ALIYUN::ECS::JoinSecurityGroup {#concept_48917_zh .concept}

ALIYUN::ECS::JoinSecurityGroup 类型用于把一个或多个 ECS 实例加入指定的安全组。

## 语法 {#section_n51_g52_lfb .section}

``` {#codeblock_efu_1eq_p6u .language-json}
{
  "Type": "ALIYUN::ECS::JoinSecurityGroup",
  "Properties": {
    "InstanceId": String,
    "InstanceIdList": List,
    "SecurityGroupId": String
  }
}
```

## 属性 {#section_8xy_723_z2u .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|SecurityGroupId|String|是|否|安全组 ID|无|
|InstanceId|String|否|否|指定需要加入安全组的 ECS 实例 ID|无|
|InstanceIdList|List|否|是|指定需要加入安全组的多个 ECS 实例 ID|无|

## 返回值 {#section_lad_vxs_5j1 .section}

## Fn::GetAtt {#section_tlt_udi_9zx .section}

无。

## 示例 {#section_dhd_2et_ick .section}

``` {#codeblock_efu_1eq_p6u .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "SG": {
      "Type": "ALIYUN::ECS::JoinSecurityGroup",
      "Properties": {
        "SecurityGroupId": "sg-****",
        "InstanceIdList": [
          "i-01****",
          "i-02****"
        ]
      }
    }
  }
}
```

