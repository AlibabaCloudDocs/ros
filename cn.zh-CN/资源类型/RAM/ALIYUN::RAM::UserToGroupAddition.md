# ALIYUN::RAM::UserToGroupAddition {#concept_48373_zh .concept}

ALIYUN::RAM::UserToGroupAddition 类型用于把多个 RAM 用户加入 RAM 群组。

## 语法 {#section_wcz_hwz_lfb .section}

``` {#codeblock_9n2_gyw_0xz .language-json}
{
  "Type": "ALIYUN::RAM::UserToGroupAddition",
  "Properties": {
    "GroupName": String,
    "Users": List
  }
}
```

## 属性 {#section_b4z_3wz_lfb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|GroupName|String|是|否|指定群组名。|长度为 1-64 个字符，允许英文字母、数字，或连字符（-）。|
|Users|List|是|否|指定用户名。|无|

## 返回值 {#section_t3p_pwz_lfb .section}

**Fn::GetAtt**

无。

## 示例 {#section_nml_rwz_lfb .section}

``` {#codeblock_8rd_cay_f9d .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
    "Resources": {
      "RamUserToGroup": {
        "Type": "ALIYUN::RAM::UserToGroupAddition",
          "Properties": {
            "GroupName": "hope",
              "Users": ["hope"]
          }
      }
    },
    "Outputs": {
        "GroupName": {
            "Value": {"Fn::GetAtt": ["RamGroup", "GroupName"]}
        }
    }
}
```

