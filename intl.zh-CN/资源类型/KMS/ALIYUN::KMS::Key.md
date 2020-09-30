# ALIYUN::KMS::Key

ALIYUN::KMS::Key类型用于创建一个主密钥。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|KeyUsage|String|否|否|密钥的用途。|取值： -   ENCRYPT/DECRYPT：数据加密和解密。
-   SIGN/VERIFY：产生和验证数字签名。 |
|Enable|Boolean|否|是|将密钥设置为启用或禁用状态。|取值： -   true（默认值）：启用。
-   false：禁用。 |
|PendingWindowInDays|Integer|否|否|密钥预删除周期。在这段时间内，您可以撤销删除处于待删除状态的密钥；预删除时间过后无法撤销删除。|取值范围：7~30。 默认值：30。

单位：天。 |
|Description|String|否|是|密钥的描述。|长度为0~8192个字符。|
|KeySpec|String|否|否|密钥的类型。|取值： -   Aliyun\_AES\_256
-   Aliyun\_SM4
-   RSA\_2048
-   EC\_P256
-   EC\_P256K
-   EC\_SM2

**说明：** 在中国内地使用托管密码机创建的密钥，默认为Aliyun\_SM4类型，其余情况下默认为Aliyun\_AES\_256。 |
|EnableAutomaticRotation|Boolean|否|是|是否开启自动密钥轮转。|取值： -   true
-   false（默认值） |
|RotationInterval|String|否|是|自动轮转的时间周期。例如：`365d`。|格式为`integer[unit]`，其中`integer`表示时间长度，`unit`表示时间单位。合法的`unit`单位取值如下：

-   d：天
-   h：小时
-   m：分钟
-   s：秒

7d或者604800s均表示7天的周期。取值范围：7~730天。 |
|ProtectionLevel|String|否|否|密钥的保护级别。|取值： -   SOFTWARE（默认值）
-   HSM |

## 返回值

Fn::GetAtt

KeyId：密钥的全局唯一标识符。

## 示例

`JSON`格式

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

`YAML`格式

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

