# ALIYUN::ApiGateway::Signature {#concept_61482_zh .concept}

ALIYUN::ApiGateway::Signature 类型可用于创建后端签名。

## 语法 {#section_wl5_4b1_mfb .section}

``` {#codeblock_efu_1eq_p6u .language-json}
{
  "Type": "ALIYUN::ApiGateway::Signature",
  "Properties": {
    "SignatureSecret": String,
    "SignatureName": String,
    "SignatureKey": String
  }
}
```

## 属性 {#section_u9l_kts_pf7 .section}

|属性名称|类型|必须|允许更新|描述|
|SignatureSecret|string|是|是|设置签名的 Secret 值。支持英文字母、数字、英文格式的下划线、及特殊字符（@、\#、!、\*），且必须以英文字母开头，长度为 6~30 个字符。|
|SignatureName|string|是|否|签名显示名称。支持汉字、英文字母、数字、英文格式的下划线，必须以英文字母或汉字开头，长度为 4~50 个字符。|
|SignatureKey|string|是|是|设置签名的 Key 值。支持英文字母、数字、英文格式的下划线，必须以英文字母开头，长度为 6~20 个字符。|

## 返回值 {#section_s7h_l1u_fye .section}

**Fn::GetAtt**

SignatureId: 后端签名 ID。

## 示例 {#section_evw_at8_z2a .section}

``` {#codeblock_efu_1eq_p6u .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "Signature": {
      "Type": "ALIYUN::ApiGateway::Signature",
      "Properties": {
        "SignatureName": "demo_test",
        "SignatureKey": "demo_test_key",
        "SignatureSecret": "demo_test_secret"
      }
    }
  }
}
```

