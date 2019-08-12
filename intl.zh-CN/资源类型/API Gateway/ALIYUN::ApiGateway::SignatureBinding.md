# ALIYUN::ApiGateway::SignatureBinding {#concept_61483_zh .concept}

ALIYUN::ApiGateway::SignatureBinding 类型可用于绑定 API 与后端签名。

## 语法 {#section_sby_vb1_mfb .section}

``` {#codeblock_efu_1eq_p6u .language-json}
{
  "Type": "ALIYUN::ApiGateway::SignatureBinding",
  "Properties": {
    "ApiIds": List,
    "GroupId": String,
    "StageName": String,
    "SignatureId": String
  }
}
```

## 属性 {#section_o5r_ph9_76t .section}

|属性名称|类型|必须|允许更新|描述|
|ApiIds|list|是|是|指定要操作的 API 编号。支持输入多个，最多支持 100 个。|
|GroupId|string|是|是|指定要操作 API 所属分组 ID。|
|StageName|string|是|是|指定要操作 API 的环境。取值：TEST、PRE、RELEASE。|
|SignatureId|string|是|是|指定要操作的签名密钥 ID。|

## 返回值 {#section_y5a_2if_n88 .section}

**Fn::GetAtt**

无。

## 示例 {#section_sn1_1he_qhz .section}

``` {#codeblock_efu_1eq_p6u .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "ApiIds": {
      "Type": "String",
      "Description": "API ID"
    },
    "GroupId": {
      "Type": "String"
    },
  },
  "Resources": {
    "Signature": {
      "Type": "ALIYUN::ApiGateway::Signature",
      "Properties": {
        "SignatureName": "ros_test_11",
        "SignatureKey": "demo_test_key",
        "SignatureSecret": "demo_test_secret"
      }
    },
    "SignatureBinding": {
      "Type": "ALIYUN::ApiGateway::SignatureBinding",
      "Properties": {
        "GroupId": {
         "Ref": "GroupId"
        },
        "SignatureId": {
          "Ref": "Signature"
        },
        "ApiIds": [{
          "Ref": "ApiIds"
        }],
        "StageName": "PRE"
      }
    }
  }
}
```

