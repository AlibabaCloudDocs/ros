# ALIYUN::UIS::Uis {#concept_12345_zh .concept}

ALIYUN::UIS::Uis is used to create an UIS instance. After the instance is created, the tunneling protocol is specified and the password used to manage VPN databases is generated.

## Syntax {#section_bnr_dxz_lfb .section}

``` {#codeblock_zzr_ep3_fnv .language-json}
{
  "Type": "ALIYUN::UIS::Uis",
  "Properties": {
    "Description": String,
    "Name": String
  }
}
```

## Properties {#section_zzv_qc5_xpt .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Description|String|No|Yes|The description of the UIS instance to be created. The description must be 2 to 256 characters in length. It must start with a letter and cannot start with http:// or https://.|None|
|Name|String|No|Yes|The name of the UIS instance. The name must be 2 to 128 characters in length and can contain letters, digits, periods \(.\), underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with http:// or https://.|None|

## Response parameters {#section_9hm_267_txr .section}

**Fn::GetAtt**

-   SslClientCertUrl: the URL for SSL client certificate authentication.
-   ClientInfoDB: the client information database.
-   ClientInfoDBPassword: the password used to log on to the client information database.
-   UisId: the ID of the UIS instance.
-   ClientInfoDBAccount: the account used to log on to the client information database.

## Examples {#section_zhq_syz_lfb .section}

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
      "Description": "The description of the instance.\n The description must be 2 to 256 characters in length. It must start with a letter and cannot start with http:// or https://.",
      "MaxLength": 256
    },
    "Name": {
      "MinLength": 2,
      "Type": "String",
      "Description": "The name of the instance.\n The name must be 2 to 128 characters in length and can contain letters, digits, periods (.), underscores (_), and hyphens (-). It must start with a letter and cannot start with http:// or https://.",
      "MaxLength": 128
    }
  },
  "Outputs": {
    "ClientInfoDBPassword": {
      "Description": "The password used to log on to the client information database.",
      "Value": {
        "Fn::GetAtt": [
          "Uis",
          "ClientInfoDBPassword"
        ]
      }
    },
    "ClientInfoDB": {
      "Description": "The client information database.",
      "Value": {
        "Fn::GetAtt": [
          "Uis",
          "ClientInfoDB"
        ]
      }
    },
    "SslClientCertUrl": {
      "Description": "The URL for SSL client certificate authentication.",
      "Value": {
        "Fn::GetAtt": [
          "Uis",
          "SslClientCertUrl"
        ]
      }
    },
    "ClientInfoDBAccount": {
      "Description": "The account used to log on to the client information database.",
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

