# ALIYUN::ECS::SSHKeyPair

ALIYUN::ECS::SSHKeyPair类型用于创建SSH密钥对或导入已有的SSH密钥对。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ResourceGroupId|String|否|否|实例所在的资源组ID。|无|
|KeyPairName|String|是|否|密钥对的名称。|长度为2~128个字符。必须以字母或汉字开头，不能以`http://`和`https://`开头。可包含英文字母、汉字、数字、半角冒号（:）、下划线（\_）和短划线（-）。|
|PublicKeyBody|String|否|否|密钥对的公钥内容。|仅在导入密钥对时需要指定该参数。|
|Tags|List|否|是|标签。|最多支持添加20个标签。更多信息，请参见[Tags属性](#section_nqw_otp_iaq)。 |

## Tags语法

```
"Tags": [
  {
    "Key": String,
    "Value": String
  }
]  
```

## Tags属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Key|String|是|否|标签键。|长度为1~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或者`https://` 。|
|Value|String|否|否|标签值。|长度为0~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或者`https://` 。|

## 返回值

Fn::GetAtt

-   KeyPairFingerPrint：密钥对的指纹。根据RFC4716定义的公钥指纹格式，采用MD5信息摘要算法。
-   PrivateKeyBody：密钥对的私钥。未加密的PEM编码PKCS\#8格式的RSA私钥内容。只有在第一次创建完成后有唯一的机会获取密钥对的私钥。如果是导入已有公钥，则不会有私钥信息。
-   KeyPairName：密钥对名称。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "KeyPairName": {
      "Type": "String",
      "Description": "SSH key pair name. It must be unique. [2, 128] characters. All character sets are supported. Do not start with a special character, digit, http://, or https://. It can contain digits, \".\", \"_\", or \"-\"."
    },
    "ResourceGroupId": {
      "Type": "String",
      "Description": "Resource group id."
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to instance. Max support 20 tags to add during create instance. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
    },
    "PublicKeyBody": {
      "Type": "String",
      "Description": "SSH Public key. If PublicKeyBody is specified, existed public key body will be imported instead of creating new SSH key pair."
    }
  },
  "Resources": {
    "SSHKeyPair": {
      "Type": "ALIYUN::ECS::SSHKeyPair",
      "Properties": {
        "KeyPairName": {
          "Ref": "KeyPairName"
        },
        "ResourceGroupId": {
          "Ref": "ResourceGroupId"
        },
        "Tags": {
          "Ref": "Tags"
        },
        "PublicKeyBody": {
          "Ref": "PublicKeyBody"
        }
      }
    }
  },
  "Outputs": {
    "KeyPairFingerPrint": {
      "Description": "The fingerprint of the key pair. The public key fingerprint format defined in RFC4716: MD5 message digest algorithm. Refer to http://tools.ietf.org/html/rfc4716.",
      "Value": {
        "Fn::GetAtt": [
          "SSHKeyPair",
          "KeyPairFingerPrint"
        ]
      }
    },
    "KeyPairName": {
      "Description": "SSH Key pair name.",
      "Value": {
        "Fn::GetAtt": [
          "SSHKeyPair",
          "KeyPairName"
        ]
      }
    },
    "PrivateKeyBody": {
      "Description": "The private key of the key pair. Content of the RSA private key in the PKCS#8 format of the unencrypted PEM encoding. Refer to: https://www.openssl.org/docs/apps/pkcs8.html.User only can get the private key one time when and only when SSH key pair is created.",
      "Value": {
        "Fn::GetAtt": [
          "SSHKeyPair",
          "PrivateKeyBody"
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
  KeyPairName:
    Description: SSH key pair name. It must be unique. [2, 128] characters. All character
      sets are supported. Do not start with a special character, digit, http://, or
      https://. It can contain digits, ".", "_", or "-".
    Type: String
  PublicKeyBody:
    Description: SSH Public key. If PublicKeyBody is specified, existed public key
      body will be imported instead of creating new SSH key pair.
    Type: String
  ResourceGroupId:
    Description: Resource group id.
    Type: String
  Tags:
    Description: Tags to attach to instance. Max support 20 tags to add during create
      instance. Each tag with two properties Key and Value, and Key is required.
    MaxLength: 20
    Type: Json
Resources:
  SSHKeyPair:
    Properties:
      KeyPairName:
        Ref: KeyPairName
      PublicKeyBody:
        Ref: PublicKeyBody
      ResourceGroupId:
        Ref: ResourceGroupId
      Tags:
        Ref: Tags
    Type: ALIYUN::ECS::SSHKeyPair
Outputs:
  KeyPairFingerPrint:
    Description: 'The fingerprint of the key pair. The public key fingerprint format
      defined in RFC4716: MD5 message digest algorithm. Refer to http://tools.ietf.org/html/rfc4716.'
    Value:
      Fn::GetAtt:
      - SSHKeyPair
      - KeyPairFingerPrint
  KeyPairName:
    Description: SSH Key pair name.
    Value:
      Fn::GetAtt:
      - SSHKeyPair
      - KeyPairName
  PrivateKeyBody:
    Description: 'The private key of the key pair. Content of the RSA private key
      in the PKCS#8 format of the unencrypted PEM encoding. Refer to: https://www.openssl.org/docs/apps/pkcs8.html.User
      only can get the private key one time when and only when SSH key pair is created.'
    Value:
      Fn::GetAtt:
      - SSHKeyPair
      - PrivateKeyBody
```

更多示例，请参见创建单个ECS实例、创建SSH密钥对和绑定SSH密钥和ECS实例的组合示例：[JSON示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ECS/JSON/Instance.json)和[YAML示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ECS/YAML/Instance.yml)。

