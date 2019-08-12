# ALIYUN::SAG::CloudConnectNetwork {#concept_qq1_f4h_hhb .concept}

ALIYUN::SAG::CloudConnectNetwork is used to create a Cloud Connect Network \(CCN\) instance. CNN is a device access matrix composed of Alibaba Cloud distributed Smart Access Gateways \(SAGs\). You can add multiple SAGs to a CCN instance and then attach the CCN instance to a Cloud Enterprise Network \(CEN\) instance. In this way, you can connect your local branches to Alibaba Cloud.

## Syntax {#section_mjp_jj1_mfb .section}

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

## Properties {#section_jkd_1j4_fhb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Description|String|No|Yes| The description of the CCN instance.

 The description must be 2 to 256 characters in length. It must start with a letter but cannot start with `http://` or `https://`.

 |None|
|IsDefault|Boolean|No|No|Indicates whether the CCN instance is created by the system. Default value: false.|None|
|Name|String|No|Yes| The name of the CCN instance.

 The name must be 2 to 128 characters in length and can contain letters, digits, periods \(.\), underscores \(\_\), and hyphens \(-\). It must start with a letter but cannot start with `http://` or `https://`.

 |None|

## Response parameters {#section_pkd_1j4_fhb .section}

**Fn::GetAtt**

CcnId: the ID of the CCN instance.

## Examples {#section_qkd_1j4_fhb .section}

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
      "Description": "Whether the CCN instance is created by the system",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "Name": {
      "Type": "String",
      "Description": "The name of the CCN instance.\n The name must be 2 to 128 characters in length and can contain letters, digits, periods (.), underscores (_), and hyphens (-).  It must start with a letter but cannot start with http:// or https://."
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

