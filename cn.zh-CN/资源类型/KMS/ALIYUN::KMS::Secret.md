# ALIYUN::KMS::Secret

ALIYUN::KMS::Secret类型用于创建凭据，并存入凭据的初始版本。

## 语法

```
{
  "Type": "ALIYUN::KMS::Secret",
  "Properties": {
    "VersionId": String,
    "SecretName": String,
    "Description": String,
    "SecretDataType": String,
    "SecretData": String,
    "VersionStages": List,
    "EncryptionKeyId": String,
    "RecoveryWindowInDays": Integer,
    "ForceDeleteWithoutRecovery": Boolean
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|VersionId|String|是|是|初始版本的版本号。|凭据对象内版本号唯一。|
|SecretName|String|是|否|凭据名称。|无|
|Description|String|否|是|凭据的描述信息。|无|
|SecretDataType|String|否|否|凭据值类型。|取值：-   text
-   binary |
|SecretData|String|是|是|新创建凭据的凭据值。凭据管家将其加密后，存入初始版本中。|无|
|VersionStages|List|否|是|版本的状态标记。|默认标记：ACSCurrent。最多指定7个标记。 |
|EncryptionKeyId|String|否|否|用于加密保护凭据值的KMS主密钥的标识符。|如果不指定，则凭据管家使用系统创建的密钥来加密保护凭据数据。**说明：** KMS主密钥必须是对称密钥。 |
|RecoveryWindowInDays|Integer|否|是|按照可恢复的方式删除凭据，且指定可恢复的窗口。|默认值：30。单位：天。 |
|ForceDeleteWithoutRecovery|Boolean|否|是|是否强制删除凭据，且不允许恢复。|取值范围：-   true
-   false（默认值） |

## 返回值

Fn::GetAtt

-   SecretName：凭据名称。
-   Arn：阿里云资源名称。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "VersionId": {
      "Type": "String",
      "Description": "The version number of the initial version. Version numbers are unique in each secret\nobject."
    },
    "SecretName": {
      "Type": "String",
      "Description": "The name of the secret."
    },
    "Description": {
      "Type": "String",
      "Description": "The description of the secret."
    },
    "SecretDataType": {
      "Type": "String",
      "Description": "The type of the secret value. Valid values:\ntext (default value)\nbinary",
      "AllowedValues": [
        "text",
        "binary"
      ]
    },
    "SecretData": {
      "Type": "String",
      "Description": "The value of the secret that you want to create. Secrets Manager encrypts the secret\nvalue and stores it in the initial version."
    },
    "VersionStages": {
      "Type": "Json",
      "Description": "The stage labels that mark the secret version. ACSCurrent will be marked as DefaultIf you do not specify it, Secrets Manager marks it with \"ACSCurrent\".",
      "MinLength": 1,
      "MaxLength": 7
    },
    "EncryptionKeyId": {
      "Type": "String",
      "Description": "The ID of the KMS CMK that is used to encrypt the secret value.\nIf you do not specify this parameter, Secrets Manager automatically creates an encryption\nkey to encrypt the secret.\nNote The KMS CMK must be a symmetric key."
    },
    "RecoveryWindowInDays": {
      "Type": "Number",
      "Description": "Specifies the recovery period of the secret if you do not forcibly delete it. Default value: 30",
      "Default": 30
    },
    "ForceDeleteWithoutRecovery": {
      "Type": "Boolean",
      "Description": "Specifies whether to forcibly delete the secret. If this parameter is set to true, the secret cannot be recovered. Valid values:\ntrue\nfalse (default value)",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ],
      "Default": false
    }
  },
  "Resources": {
    "Secret": {
      "Type": "ALIYUN::KMS::Secret",
      "Properties": {
        "VersionId": {
          "Ref": "VersionId"
        },
        "SecretName": {
          "Ref": "SecretName"
        },
        "Description": {
          "Ref": "Description"
        },
        "SecretDataType": {
          "Ref": "SecretDataType"
        },
        "SecretData": {
          "Ref": "SecretData"
        },
        "VersionStages": {
          "Ref": "VersionStages"
        },
        "EncryptionKeyId": {
          "Ref": "EncryptionKeyId"
        },
        "RecoveryWindowInDays": {
          "Ref": "RecoveryWindowInDays"
        },
        "ForceDeleteWithoutRecovery": {
          "Ref": "ForceDeleteWithoutRecovery"
        }
      }
    }
  },
  "Outputs": {
    "SecretName": {
      "Description": "The name of the secret.",
      "Value": {
        "Fn::GetAtt": [
          "Secret",
          "SecretName"
        ]
      }
    },
    "Arn": {
      "Description": "The Alibaba Cloud Resource Name (ARN).",
      "Value": {
        "Fn::GetAtt": [
          "Secret",
          "Arn"
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
  VersionId:
    Type: String
    Description: >-
      The version number of the initial version. Version numbers are unique in
      each secret

      object.
  SecretName:
    Type: String
    Description: The name of the secret.
  Description:
    Type: String
    Description: The description of the secret.
  SecretDataType:
    Type: String
    Description: |-
      The type of the secret value. Valid values:
      text (default value)
      binary
    AllowedValues:
      - text
      - binary
  SecretData:
    Type: String
    Description: >-
      The value of the secret that you want to create. Secrets Manager encrypts
      the secret

      value and stores it in the initial version.
  VersionStages:
    Type: Json
    Description: >-
      The stage labels that mark the secret version. ACSCurrent will be marked
      as DefaultIf you do not specify it, Secrets Manager marks it with
      "ACSCurrent".
    MinLength: 1
    MaxLength: 7
  EncryptionKeyId:
    Type: String
    Description: >-
      The ID of the KMS CMK that is used to encrypt the secret value.

      If you do not specify this parameter, Secrets Manager automatically
      creates an encryption

      key to encrypt the secret.

      Note The KMS CMK must be a symmetric key.
  RecoveryWindowInDays:
    Type: Number
    Description: >-
      Specifies the recovery period of the secret if you do not forcibly delete
      it. Default value: 30
    Default: 30
  ForceDeleteWithoutRecovery:
    Type: Boolean
    Description: >-
      Specifies whether to forcibly delete the secret. If this parameter is set
      to true, the secret cannot be recovered. Valid values:

      true

      false (default value)
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
    Default: false
Resources:
  Secret:
    Type: 'ALIYUN::KMS::Secret'
    Properties:
      VersionId:
        Ref: VersionId
      SecretName:
        Ref: SecretName
      Description:
        Ref: Description
      SecretDataType:
        Ref: SecretDataType
      SecretData:
        Ref: SecretData
      VersionStages:
        Ref: VersionStages
      EncryptionKeyId:
        Ref: EncryptionKeyId
      RecoveryWindowInDays:
        Ref: RecoveryWindowInDays
      ForceDeleteWithoutRecovery:
        Ref: ForceDeleteWithoutRecovery
Outputs:
  SecretName:
    Description: The name of the secret.
    Value:
      'Fn::GetAtt':
        - Secret
        - SecretName
  Arn:
    Description: The Alibaba Cloud Resource Name (ARN).
    Value:
      'Fn::GetAtt':
        - Secret
        - Arn
```

