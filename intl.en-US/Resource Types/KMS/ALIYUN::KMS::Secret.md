# ALIYUN::KMS::Secret

ALIYUN::KMS::Secret is used to create a Key Management Service \(KMS\) secret and keep the initial version of the secret.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|VersionId|String|Yes|Yes|The version number of the initial version.|Version numbers are unique in each secret object.|
|SecretName|String|Yes|No|The name of the secret.|None|
|Description|String|No|Yes|The description of the secret.|None|
|SecretDataType|String|No|No|The type of the secret value.|Valid values:-   text
-   binary |
|SecretData|String|Yes|Yes|The value of the secret that you want to create. Secrets Manager encrypts the secret value and stores it in the initial version.|None|
|VersionStages|List|No|Yes|The stage labels that mark the secret version.|Default value: ACSCurrent.You can specify up to seven labels for each secret version. |
|EncryptionKeyId|String|No|No|The ID of the KMS customer master key \(CMK\) that is used to encrypt the secret value.|If you do not specify this parameter, Secrets Manager automatically creates an encryption key to encrypt the secret.**Note:** The KMS CMK must be a symmetric key. |
|RecoveryWindowInDays|Integer|No|Yes|Specifies the recovery period of the secret if you do not forcibly delete it.|Default value: 30.Unit: days. |
|ForceDeleteWithoutRecovery|Boolean|No|Yes|Specifies whether to forcibly delete the secret. If this parameter is set to true, the secret cannot be recovered.|Valid values:-   true
-   false |

## Response parameters

Fn::GetAtt

-   SecretName: the secret name.
-   Arn: the Alibaba Cloud Resource Name \(ARN\) of the secret.

## Examples

`JSON` format

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

`YAML` format

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

