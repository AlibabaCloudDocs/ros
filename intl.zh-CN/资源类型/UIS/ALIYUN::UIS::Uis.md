# ALIYUN::UIS::Uis {#concept_12345_zh .concept}

ALIYUN::UIS::Uis类型创建一个实例。实例创建后会指定隧道协议并生成VPN数据库的管理口令。

## 语法 {#section_bnr_dxz_lfb .section}

``` {#codeblock_zzr_ep3_fnv .language-json}
{
  "Type": "ALIYUN::UIS::Uis",
  "Properties": {
    "Description": String,
    "Name": String
  }
}
```

## 属性 {#section_zzv_qc5_xpt .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Description|String|否|是|实例的描述信息。长度为 2-256个字符，必须以字母或中文开头，但不能以http://或https://开头。|无。|
|Name|String|否|是|实例的名称。长度为 2-128个字符，必须以字母或中文开头，可包含数字，点号（.），下划线（\_）和短横线（-）。但不能以http:// 或https://开头。|无。|

## 返回值 {#section_9hm_267_txr .section}

**Fn::GetAtt**

-   SslClientCertUrl: ssl客户端证书url。
-   ClientInfoDB: 客户端数据库信息。
-   ClientInfoDBPassword: 客户端数据库密码信息。
-   UisId: 实例的ID。
-   ClientInfoDBAccount: 客户端数据库账号信息。

## 示例 {#section_zhq_syz_lfb .section}

``` {#codeblock_33x_fcs_hsp .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "Uis": {
      "Type": "ALIYUN::UIS::Uis",
      "Properties": {
        "Description": {
          "Ref": "Description"
        },
        "Name": {
          "Ref": "Name"
        }
      }
    }
  },
  "Parameters": {
    "Description": {
      "MinLength": 2,
      "Type": "String",
      "Description": "Description of the instance.\nThe length is 2-256 characters and must start with a letter or Chinese, but cannot start with http:// or https://.",
      "MaxLength": 256
    },
    "Name": {
      "MinLength": 2,
      "Type": "String",
      "Description": "The name of the instance.\nThe length is 2-128 characters and must start with a letter or Chinese. It can contain numbers, periods (.), underscores (_), and dashes (-). But it can't start with http:// or https://.",
      "MaxLength": 128
    }
  },
  "Outputs": {
    "ClientInfoDBPassword": {
      "Description": "The client info DB password.",
      "Value": {
        "Fn::GetAtt": [
          "Uis",
          "ClientInfoDBPassword"
        ]
      }
    },
    "ClientInfoDB": {
      "Description": "The client info DB.",
      "Value": {
        "Fn::GetAtt": [
          "Uis",
          "ClientInfoDB"
        ]
      }
    },
    "SslClientCertUrl": {
      "Description": "The ssl client cert url.",
      "Value": {
        "Fn::GetAtt": [
          "Uis",
          "SslClientCertUrl"
        ]
      }
    },
    "ClientInfoDBAccount": {
      "Description": "The client info DB account.",
      "Value": {
        "Fn::GetAtt": [
          "Uis",
          "ClientInfoDBAccount"
        ]
      }
    },
    "UisId": {
      "Description": "The ID of the instance.",
      "Value": {
        "Fn::GetAtt": [
          "Uis",
          "UisId"
        ]
      }
    }
  }
}
```

