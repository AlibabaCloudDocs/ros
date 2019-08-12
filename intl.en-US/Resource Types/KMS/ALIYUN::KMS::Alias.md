# ALIYUN::KMS::Alias {#concept_12345_zh .concept}

ALIYUN::KMS::Alias is used to create an alias for a Customer Master Key \(CMK\).

## Syntax {#section_bnr_dxz_lfb .section}

``` {#codeblock_3ez_bta_9di .language-json}
{
  "Type": "ALIYUN::KMS::Alias",
  "Properties": {
    "KeyId": String,
    "AliasName": String
  }
}
```

## Properties {#section_wjt_1ml_w2c .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|KeyId|String|Yes|No|The globally unique identifier of the CMK.|None|
|AliasName|String|Yes|No|The alias to give to the CMK. This alias can be used to call the Encrypt, GenerateDataKey, and DescribeKey operations.|Excluding the prefix, an alias must be 1 to 255 characters in length. The prefix alias/ must be included.|

## Response parameters {#section_c33_eq8_wy0 .section}

**Fn::GetAtt**

-   None

## Examples {#section_zhq_syz_lfb .section}

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
      "Description": "The globally unique identifier of the CMK."
    },
    "AliasName": {
      "MinLength": 1,
      "Type": "String",
      "Description": "- The display name of the key. You can use the alias to call APIs such as Encrypt, GenerateDataKey, and DescribeKey. Excluding the prefix, an alias must be 1 to 255 characters in length. The prefix alias/ must be included.",
      "MaxLength": 255
    }
  },
  "Outputs": {}
}
```

