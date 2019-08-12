# ALIYUN::RAM::AttachPolicyToRole {#concept_mqv_kbb_rgb .concept}

ALIYUN::RAM::AttachPolicyToRole类型用于为指定角色附加授权。

## 语法 {#section_wcz_hwz_lfb .section}

``` {#codeblock_3qd_z9h_wz6 .language-json}
{
  "Type": "ALIYUN::RAM::AttachPolicyToRole",
  "Properties": {
    "PolicyName": String,
    "PolicyType": String,
    "RoleName": String
  }
}
```

## 属性 {#section_b4z_3wz_lfb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|PolicyName|String|是|否|指定权限策略名称。|无|
|PolicyType|String|是|否|指定权限的类型。|取值`System`或`Custom。`|
|RoleName|String|是|否|指定角色名，例如：dev。|无|

## 返回值 {#section_y5a_2if_n88 .section}

**Fn::GetAtt**

无。

## 示例 {#section_nml_rwz_lfb .section}

``` {#codeblock_td1_ml1_muo .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "AttachPolicyToRole": {
      "Type": "ALIYUN::RAM::AttachPolicyToRole",
      "Properties": {
        "PolicyName": "OSS-Administrator",
        "PolicyType": "Custom",
        "RoleName": "OSSAdminRole"
      }
    }
  }
}
```

