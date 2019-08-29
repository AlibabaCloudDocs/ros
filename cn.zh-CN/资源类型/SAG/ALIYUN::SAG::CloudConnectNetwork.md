# ALIYUN::SAG::CloudConnectNetwork {#concept_qq1_f4h_hhb .concept}

ALIYUN::SAG::CloudConnectNetwork类型用于创建云连接网。云连接网是由阿里云分布式接入网关组成的设备接入矩阵。您可以将云连接网绑定到云企业网，实现线下接入矩阵和云上中心矩阵全连接。

## 语法 {#section_mjp_jj1_mfb .section}

```language-json
{
  "Type": "ALIYUN::SAG::CloudConnectNetwork",
  "Properties": {
    "Description": String,
    "IsDefault": Boolean,
    "Name": String
  }
}
```

## 属性 {#section_jkd_1j4_fhb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Description|String|否|是| 云连接网的描述。

 长度为2-256个字符，必须以字母或中文开头，但不能以`http://` 或 `https://`开头。

 |无。|
|IsDefault|Boolean|否|否|是否由系统创建。默认值：false。|无。|
|Name|String|否|是| 云连接网的名称。

 长度为2-128个字符，必须以字母或中文开头，可包含数字，点号（.），下划线（\_）和短横线（-），但不能以`http://` 或 `https://`开头。

 |无。|

## 返回值 {#section_pkd_1j4_fhb .section}

**Fn::GetAtt**

CcnId：云连接网ID。

## 示例 {#section_qkd_1j4_fhb .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "CloudConnectNetwork": {
      "Type": "ALIYUN::SAG::CloudConnectNetwork",
      "Properties": {
        "Description": {
          "Ref": "Description"
        },
        "IsDefault": {
          "Ref": "IsDefault"
        },
        "Name": {
          "Ref": "Name"
        }
      }
    }
  },
  "Parameters": {
    "Description": {
      "Type": "String",
      "Description": "The description of the CCN instance.\nThe description can contain 2 to 256 characters. The description cannot start with http:// or https://."
    },
    "IsDefault": {
      "Default": false,
      "Type": "Boolean",
      "Description": "Whether is created by system",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "Name": {
      "Type": "String",
      "Description": "The name of the CCN instance.\nThe name can contain 2 to 128 characters including a-z, A-Z, 0-9, chinese, underlines, and hyphens. The name must start with an English letter, but cannot start with http:// or https://."
    }
  },
  "Outputs": {
    "CcnId": {
      "Description": "The ID of the CCN instance.",
      "Value": {
        "Fn::GetAtt": [
          "CloudConnectNetwork",
          "CcnId"
        ]
      }
    }
  }
}
```

