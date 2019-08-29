# ALIYUN::KMS::Alias {#concept_12345_zh .concept}

ALIYUN::KMS::Alias类型用于给主密钥（CMK）创建一个别名。

## 语法 {#section_bnr_dxz_lfb .section}

``` {#codeblock_3ez_bta_9di .language-json}
{
  "Type": "ALIYUN::KMS::Alias",
  "Properties": {
    "KeyId": String,
    "AliasName": String
  }
}
```

## 属性 {#section_wjt_1ml_w2c .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|KeyId|String|是|否|Key的全局唯一标识符。|无。|
|AliasName|String|是|否|CMK 的别名，可以使用别名调用 Encrypt、GenerateDataKey、 DescribeKey。|前缀以外的字符长度：最小长度为 1 字符，最大长度为255 字符。 - 必须包含前缀 alias/。|

## 返回值 {#section_c33_eq8_wy0 .section}

**Fn::GetAtt**

-   无。

## 示例 {#section_zhq_syz_lfb .section}

``` {#codeblock_5g8_7lf_kwq .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "Alias": {
      "Type": "ALIYUN::KMS::Alias",
      "Properties": {
        "KeyId": {
          "Ref": "KeyId"
        },
        "AliasName": {
          "Ref": "AliasName"
        }
      }
    }
  },
  "Parameters": {
    "KeyId": {
      "Type": "String",
      "Description": "Globally unique identifier of the CMK."
    },
    "AliasName": {
      "MinLength": 1,
      "Type": "String",
      "Description": "- The display name of the key. You can use the alias to call APIs such as Encrypt, GenerateDataKey, and DescribeKey. - Not including the prefix, the minimum length of an alias is 1 and the maximum length is 255. - The prefix alias/ must be included.",
      "MaxLength": 255
    }
  },
  "Outputs": {}
}
```

