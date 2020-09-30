# ALIYUN::KMS::Key

ALIYUN::KMS::Key is used to create a customer master key \(CMK\).

## Syntax

```
{
  "Type": "ALIYUN::KMS::Key",
  "Properties": {
    "KeyUsage": String,
    "Enable": Boolean,
    "PendingWindowInDays": Integer,
    "Description": String,
    "KeySpec": String,
    "EnableAutomaticRotation": Boolean,
    "RotationInterval": String,
    "ProtectionLevel": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|KeyUsage|String|No|No|The intended use of the CMK.|Valid values: -   ENCRYPT/DECRYPT: The CMK encrypts or decrypts data.
-   SIGN/VERIFY: The CMK generates or verifies a digital signature. |
|Enable|Boolean|No|Yes|Specifies whether to enable the CMK.|Default value: true. Valid values: -   true
-   false |
|PendingWindowInDays|Integer|No|No|The number of days to wait before the CMK is deleted. During this period, the CMK is in the PendingDeletion state and the delete operation can be canceled.|Valid values: 7 to 30. Default value: 30.

Unit: days. |
|Description|String|No|Yes|The description of the CMK.|The description can be up to 8,192 characters in length.|
|KeySpec|String|No|No|The type of the CMK.|Valid values: -   Aliyun\_AES\_256
-   Aliyun\_SM4
-   RSA\_2048
-   EC\_P256
-   EC\_P256K
-   EC\_SM2

**Note:** If the CMK is created in Managed HSM in a region within mainland China, the default value is Aliyun\_SM4. In other cases, the default value is Aliyun\_AES\_256. |
|EnableAutomaticRotation|Boolean|No|Yes|Specifies whether to enable automatic key rotation.|Default value: false. Valid values: -   true
-   false |
|RotationInterval|String|No|Yes|The period of automatic key rotation. Example: `365d`.|It must be in the `integer[unit]` format.````Valid values for the `unit`:

-   d: days
-   h: hours
-   m: minutes
-   s: seconds

For example, both 7d and 604800s represent a seven-day period.The period can range from 7 to 730 days. |
|ProtectionLevel|String|No|No|The protection level of the CMK.|Default value: SOFTWARE. Valid values: -   SOFTWARE
-   HSM |

## Response parameters

Fn::GetAtt

KeyId: the globally unique identifier of the CMK.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "ProtectionLevel": {
      "Type": "String",
      "Description": "The protection level of the CMK to create. Valid value: SOFTWARE and HSM. When this parameter is set to HSM:\nIf the Origin parameter is set to Aliyun_KMS, the CMK is created in Managed HSM.\nIf the Origin parameter is set to EXTERNAL, you can import external keys to Managed HSM."
    },
    "Description": {
      "Type": "String",
      "Description": "The description of the CMK. Length constraints: Minimum length of 0 characters. Maximum length of 8192 characters.",
      "MinLength": 0,
      "MaxLength": 8192
    },
    "RotationInterval": {
      "Type": "String",
      "Description": "The time period for automatic rotation. The format is integer[unit], where integer represents the length of time and unit represents the time unit. The legal unit units are: d (day), h (hour), m (minute), s (second). 7d or 604800s both represent a 7-day cycle. Value: 7~730 days."
    },
    "EnableAutomaticRotation": {
      "Type": "Boolean",
      "Description": "Whether to enable automatic key rotation. Valid value: true/false (default)",
      "AllowedValues": [
        true,
        false
      ]
    },
    "PendingWindowInDays": {
      "Type": "Number",
      "Description": "The waiting period, specified in number of days. During this period, you can cancel the CMK in PendingDeletion status. After the waiting period expires, you cannot cancel the deletion. The value must be between 7 and 30. Default value is 30.",
      "MinValue": 7,
      "MaxValue": 30,
      "Default": 30
    },
    "KeySpec": {
      "Type": "String",
      "Description": "Key type. Valid value: Aliyun_AES_256/Aliyun_SM4/RSA_2048/EC_P256/EC_P256K/EC_SM2"
    },
    "Enable": {
      "Type": "Boolean",
      "Description": "Specifies whether the key is enabled. Defaults to true.",
      "AllowedValues": [
        true,
        false
      ],
      "Default": true
    },
    "KeyUsage": {
      "Type": "String",
      "Description": "The intended use of the CMK. Default value: ENCRYPT/DECRYPT.",
      "Default": "ENCRYPT/DECRYPT"
    }
  },
  "Resources": {
    "Key": {
      "Type": "ALIYUN::KMS::Key",
      "Properties": {
        "ProtectionLevel": {
          "Ref": "ProtectionLevel"
        },
        "Description": {
          "Ref": "Description"
        },
        "RotationInterval": {
          "Ref": "RotationInterval"
        },
        "EnableAutomaticRotation": {
          "Ref": "EnableAutomaticRotation"
        },
        "PendingWindowInDays": {
          "Ref": "PendingWindowInDays"
        },
        "KeySpec": {
          "Ref": "KeySpec"
        },
        "Enable": {
          "Ref": "Enable"
        },
        "KeyUsage": {
          "Ref": "KeyUsage"
        }
      }
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

`YAML` format

```
ROSTemplateFormatVersion: '2015-09-01'
Parameters:
  ProtectionLevel:
    Type: String
    Description: >-
      The protection level of the CMK to create. Valid value: SOFTWARE and HSM.
      When this parameter is set to HSM:

      If the Origin parameter is set to Aliyun_KMS, the CMK is created in
      Managed HSM.

      If the Origin parameter is set to EXTERNAL, you can import external keys
      to Managed HSM.
  Description:
    Type: String
    Description: >-
      The description of the CMK. Length constraints: Minimum length of 0
      characters. Maximum length of 8192 characters.
    MinLength: 0
    MaxLength: 8192
  RotationInterval:
    Type: String
    Description: >-
      The time period for automatic rotation. The format is integer[unit], where
      integer represents the length of time and unit represents the time unit.
      The legal unit units are: d (day), h (hour), m (minute), s (second). 7d or
      604800s both represent a 7-day cycle. Value: 7~730 days.
  EnableAutomaticRotation:
    Type: Boolean
    Description: >-
      Whether to enable automatic key rotation. Valid value: true/false
      (default)
    AllowedValues:
      - true
      - false
  PendingWindowInDays:
    Type: Number
    Description: >-
      The waiting period, specified in number of days. During this period, you
      can cancel the CMK in PendingDeletion status. After the waiting period
      expires, you cannot cancel the deletion. The value must be between 7 and
      30. Default value is 30.
    MinValue: 7
    MaxValue: 30
    Default: 30
  KeySpec:
    Type: String
    Description: >-
      Key type. Valid value:
      Aliyun_AES_256/Aliyun_SM4/RSA_2048/EC_P256/EC_P256K/EC_SM2
  Enable:
    Type: Boolean
    Description: Specifies whether the key is enabled. Defaults to true.
    AllowedValues:
      - true
      - false
    Default: true
  KeyUsage:
    Type: String
    Description: 'The intended use of the CMK. Default value: ENCRYPT/DECRYPT.'
    Default: ENCRYPT/DECRYPT
Resources:
  Key:
    Type: 'ALIYUN::KMS::Key'
    Properties:
      ProtectionLevel:
        Ref: ProtectionLevel
      Description:
        Ref: Description
      RotationInterval:
        Ref: RotationInterval
      EnableAutomaticRotation:
        Ref: EnableAutomaticRotation
      PendingWindowInDays:
        Ref: PendingWindowInDays
      KeySpec:
        Ref: KeySpec
      Enable:
        Ref: Enable
      KeyUsage:
        Ref: KeyUsage
Outputs:
  KeyId:
    Description: The globally unique identifier for the CMK.
    Value:
      'Fn::GetAtt':
        - Key
        - KeyId
```

