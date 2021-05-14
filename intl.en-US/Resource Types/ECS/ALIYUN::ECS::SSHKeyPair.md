# ALIYUN::ECS::SSHKeyPair

ALIYUN::ECS::SSHKeyPair is used to create an SSH key pair or import an existing SSH key pair to access an Elastic Compute Service \(ECS\) instance.

## Syntax

```
{
  "Type": "ALIYUN::ECS::SSHKeyPair",
  "Properties": {
    "ResourceGroupId": String,
    "KeyPairName": String,
    "PublicKeyBody": String,
    "Tags": List
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ResourceGroupId|String|No|No|The ID of the resource group to which the ECS instance belongs.|None|
|KeyPairName|String|Yes|No|The name of the key pair.|The name must be 2 to 128 characters in length and can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with `http://` or `https://`.|
|PublicKeyBody|String|No|No|The public key of the key pair.|This parameter is required only when you import an SSH key pair.|
|Tags|List|No|Yes|The tags of the key pair.|A maximum of 20 tags can be specified. For more information, see [Tags properties](#section_nqw_otp_iaq). |

## Tags syntax

```
"Tags": [
  {
    "Key": String,
    "Value": String
  }
]  
```

## Tags properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Key|String|Yes|No|The tag key.|The tag key must be 1 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|
|Value|String|No|No|The tag value.|The tag value must be 0 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|

## Response parameters

Fn::GetAtt

-   KeyPairFingerPrint: the fingerprint of the key pair. The fingerprint uses the message-digest algorithm 5 \(MD5\) based on the public key fingerprint format defined in RFC 4716.
-   PrivateKeyBody: the private key of the key pair. An unencrypted RSA private key must be encoded in the PKCS\#8 format by using PEM. The private key of a key pair can be obtained only when the key pair is first created. If you import an existing public key, no private key information is available.
-   KeyPairName: the name of the key pair.

## Examples

`JSON` format

```
{
"ROSTemplateFormatVersion": "2015-09-01",
  "Parameters":
{
    "KeyPairName": {
      "Type":
"String",
      "Description": "SSH key pair name.
It must be unique. [2, 128] characters.
All character sets are supported. Do not start with a special character, digit, http://, or https://. It can contain digits, \".\", \"_\", or \"-\"."
    },
    "ResourceGroupId": {
      "Type": "String",
      "Description": "Resource group id." },
    "Tags":
{
      "Type":
"Json",
      "Description": "Tags to attach to instance.
Max support 20 tags to add during create instance. Each tag with two properties Key and Value, and Key is required.",
"MaxLength": 20
    },
    "PublicKeyBody":
{
      "Type":
"String",
      "Description": "SSH Public key.
If PublicKeyBody is specified, existed public key body will be imported instead of creating new SSH key pair." }
  },
  "Resources":
{
    "SSHKeyPair": {
      "Type": "ALIYUN::ECS::SSHKeyPair",
      "Properties": {
        "KeyPairName":
{
          "Ref": "KeyPairName"
        },
        "ResourceGroupId":
{
          "Ref":
"ResourceGroupId"
        },
        "Tags": {
          "Ref":
"Tags"
        },
        "PublicKeyBody": {
          "Ref":
"PublicKeyBody"
        }
      }
    }
  },
  "Outputs": {
    "KeyPairFingerPrint": {
      "Description":
"The fingerprint of the key pair.
The public key fingerprint format defined in RFC4716:
MD5 message digest algorithm. Refer to http://tools.ietf.org/html/rfc4716.",
"Value": {
        "Fn::GetAtt":
[
          "SSHKeyPair",
          "KeyPairFingerPrint"
        ]
      }
    },
    "KeyPairName": {
      "Description":
"SSH Key pair name.", "Value":
{
        "Fn::GetAtt": [
          "SSHKeyPair",
          "KeyPairName"
        ]
      }
    },
    "PrivateKeyBody":
{
      "Description": "The private key of the key pair.
Content of the RSA private key in the PKCS#8 format of the unencrypted PEM encoding.
Refer to: https://www.openssl.org/docs/apps/pkcs8.html.User only can get the private key one time when and only when SSH key pair is created.", "Value":
{
        "Fn::GetAtt": [
          "SSHKeyPair",
          "PrivateKeyBody"
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
KeyPairName:
Description: SSH key pair name. It must be unique. [2, 128] characters. All character
      sets are supported.
Do not start with a special character, digit, http://, or
      https://. It can contain digits, ".", "_", or "-".
    Type:
String
  PublicKeyBody: Description:
SSH Public key. If PublicKeyBody is specified, existed public key
      body will be imported instead of creating new SSH key pair.
Type:
String
  ResourceGroupId: Description: Resource group id.
Type:
String
  Tags: Description:
Tags to attach to instance.
Max support 20 tags to add during create
      instance. Each tag with two properties Key and Value, and Key is required.
MaxLength: 20
    Type:
Json
Resources:
SSHKeyPair: Properties: KeyPairName:
Ref: KeyPairName
      PublicKeyBody:
Ref: PublicKeyBody
      ResourceGroupId:
Ref: ResourceGroupId
      Tags:
Ref:
Tags
    Type:
ALIYUN::ECS::SSHKeyPair
Outputs:
KeyPairFingerPrint:
Description: 'The fingerprint of the key pair.
The public key fingerprint format
      defined in RFC4716:
MD5 message digest algorithm. Refer to http://tools.ietf.org/html/rfc4716.'
Value:
Fn::GetAtt: - SSHKeyPair
      - KeyPairFingerPrint
  KeyPairName:
Description:
SSH Key pair name. Value:
Fn::GetAtt: - SSHKeyPair
      - KeyPairName
  PrivateKeyBody:
Description:
'The private key of the key pair.
Content of the RSA private key
      in the PKCS#8 format of the unencrypted PEM encoding. Refer to: https://www.openssl.org/docs/apps/pkcs8.html.User
      only can get the private key one time when and only when SSH key pair is created.' Value:
Fn::GetAtt: - SSHKeyPair
      - PrivateKeyBody  
```

For more examples, visit [Instance.json](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ECS/JSON/Instance.json) and [Instance.yml](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ECS/YAML/Instance.yml). In the examples, the ALIYUN::ECS::Instance, ALIYUN::ECS::SSHKeyPair, and ALIYUN::ECS::SSHKeyPairAttachment resource types are involved.

