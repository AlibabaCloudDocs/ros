# ALIYUN::KMS::Key {#concept_12345_zh .concept}

ALIYUN::KMS::Key类型用于创建一个主密钥。

## 语法 {#section_bnr_dxz_lfb .section}

``` {#codeblock_gm8_i3y_zh1 .language-json}
{
  "Type": "ALIYUN::KMS::Key",
  "Properties": {
    "KeyUsage": String,
    "Enable": Boolean,
    "PendingWindowInDays": Integer,
    "Description": String
  }
}
```

## 属性 {#section_yie_0z3_y4l .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|KeyUsage|String|否|否|密钥的用途。|默认值：ENCRYPT/DECRYPT。|
|Enable|Boolean|否|否|将Key设置为启用或禁用状态。|默认值：true。|
|PendingWindowInDays|Integer|否|否|密钥预删除周期。在这段时间内，您可以撤销删除处于待删除状态的密钥；预删除时间过后无法撤销删除。|有效值：最小值为 7，最大值为 30。默认值：30。|
|Description|String|否|否|密钥的描述。 |长度必须在 0 到 8192 个字符之间。|

## 返回值 {#section_y43_kr2_1pz .section}

**Fn::GetAtt**

-   KeyId: 密钥的全局唯一标识符。
-   Arn: 当前密钥的阿里云资源名称。

## 示例 {#section_zhq_syz_lfb .section}

``` {#codeblock_u87_uaf_njk .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "Key": {
      "Type": "ALIYUN::KMS::Key",
      "Properties": {
        "KeyUsage": {
          "Ref": "KeyUsage"
        },
        "Enable": {
          "Ref": "Enable"
        },
        "PendingWindowInDays": {
          "Ref": "PendingWindowInDays"
        },
        "Description": {
          "Ref": "Description"
        }
      }
    }
  },
  "Parameters": {
    "KeyUsage": {
      "Default": "ENCRYPT/DECRYPT",
      "Type": "String",
      "Description": "The intended use of the CMK. Default value: ENCRYPT/DECRYPT."
    },
    "Enable": {
      "Default": true,
      "Type": "Boolean",
      "Description": "Specifies whether the key is enabled. Defaults to true.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "PendingWindowInDays": {
      "Default": 30,
      "Type": "Number",
      "Description": "The waiting period, specified in number of days. During this period, you can cancel the CMK in PendingDeletion status. After the waiting period expires, you cannot cancel the deletion. The value must be between 7 and 30. Default value is 30.",
      "MaxValue": 30,
      "MinValue": 7
    },
    "Description": {
      "MinLength": 0,
      "Type": "String",
      "Description": "The description of the CMK. Length constraints: Minimum length of 0 characters. Maximum length of 8192 characters.",
      "MaxLength": 8192
    }
  },
  "Outputs": {
    "KeyId": {
      "Description": "The globally unique identifier for the CMK.",
      "Value": {
        "Fn::GetAtt": [
          "Key",
          "KeyId"
        ]
      }
    }
  }
}
```

