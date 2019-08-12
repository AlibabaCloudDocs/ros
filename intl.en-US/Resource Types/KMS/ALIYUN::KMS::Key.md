# ALIYUN::KMS::Key {#concept_12345_zh .concept}

ALIYUN::KMS::Key is used to create a Customer Master Key \(CMK\).

## Syntax {#section_bnr_dxz_lfb .section}

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

## Properties {#section_yie_0z3_y4l .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|KeyUsage|String|No|No|The intended use of the CMK to be created.|Default value: ENCRYPT/DECRYPT|
|Enable|Boolean|No|No|Specifies whether to enable the CMK.|Default value: true|
|PendingWindowInDays|Integer|No|No|The number of days to wait before deleting the CMK. During this period, the CMK is in the PendingDeletion state and the delete operation can be canceled.|Valid values: 7 to 30. Default value: 30.|
|Description|String|No|No|The description of the CMK.|The description can be up to 8,192 characters in length.|

## Response parameters {#section_y43_kr2_1pz .section}

**Fn::GetAtt**

-   KeyId: the globally unique identifier of the CMK.
-   Arn: the Alibaba Cloud Resource Name \(ARN\) of the CMK.

## Examples {#section_zhq_syz_lfb .section}

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
      "Description": "Specifies whether to enable the CMK. Default value: true.",
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
      "Description": "The number of days to wait before deleting the CMK. During this period, the CMK is in the PendingDeletion state and the delete operation can be canceled. Valid values: 7 to 30. Default value: 30.",
      "MaxValue": 30,
      "MinValue": 7
    },
    "Description": {
      "MinLength": 0,
      "Type": "String",
      "Description": "The description of the CMK. The description can be up to 8,192 characters in length.",
      "MaxLength": 8192
    }
  },
  "Outputs": {
    "KeyId": {
      "Description": "The globally unique identifier of the CMK.",
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

