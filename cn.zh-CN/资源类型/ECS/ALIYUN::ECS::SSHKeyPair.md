# ALIYUN::ECS::SSHKeyPair {#concept_54422_zh .concept}

ALIYUN::ECS::SSHKeyPair 类型用于创建全新或导入已有的 SSH 密钥。

## 语法 {#section_ohs_jcf_lfb .section}

``` {#codeblock_efu_1eq_p6u .language-json}
{
  "Type": "ALIYUN::ECS::SSHKeyPair",
  "Properties": {
    "ResourceGroupId": String,
    "KeyPairName": String,
    "PublicKeyBody": String
  }
}
```

## 属性 {#section_2fs_2yc_v4x .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ResourceGroupId|String|否|否|实例所在的资源组ID。|无。|
|KeyPairName|String|是|否|SSH 密钥对的全局唯一名称。|名称可包括 \[2, 128\] 字符，必须以大小字母或中文开头，可包含字母、汉字、数字、点号（.）、下划线（\_）、和连字符（-）。不能以 http:// 和 https:// 开头。|
|PublicKeyBody|String|否|否|指定要导入的 SSH 公钥。|无|

## 返回值 {#section_ynf_0o1_9cl .section}

**Fn::GetAtt**

-   KeyPairFingerPrint：密钥对的指纹。根据RFC4716定义的公钥指纹格式，采用MD5信息摘要算法。
-   PrivateKeyBody：密钥对的私钥。未加密的 PEM 编码 PKCS\#8 格式的 RSA 私钥内容。只有在第一次创建完成后有唯一的机会获取密钥对的私钥。如果是导入已有公钥，则不会有私钥信息。
-   KeyPairName：全局唯一的 SSH 密钥对名称。

## 示例 {#section_hn4_j0r_oje .section}

``` {#codeblock_efu_1eq_p6u .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "SSHKeyPair": {
      "Type": "ALIYUN::ECS::SSHKeyPair",
      "Properties": {
        "KeyPairName": "ssh_key_pair_v1"
      }
    }
  },
  "Outputs": {
    "KeyPairName": {
      "Value": {
        "Fn::GetAtt": [
          "SSHKeyPair",
          "KeyPairName"
        ]
      }
    },
    "PrivateKeyBody": {
      "Value": {
        "Fn::GetAtt": [
          "SSHKeyPair",
          "PrivateKeyBody"
        ]
      }
    },
    "KeyPairFingerPrint": {
      "Value": {
        "Fn::GetAtt": [
          "SSHKeyPair",
          "KeyPairFingerPrint"
        ]
      }
    }
  }
}
```

