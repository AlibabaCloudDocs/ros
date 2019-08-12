# ALIYUN::CEN::CenInstance {#concept_xj1_ymh_hhb .concept}

ALIYUN::CEN::CenInstance is used to create a CEN instance.

## Syntax {#section_xyg_tn2_lfb .section}

```language-json
{
  "Type": "ALIYUN::CEN::CenInstance",
  "Properties": {
    "Description": String,
    "Name": String
  }
}
```

## Properties {#section_cgd_53n_4fb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Description|String|No|Yes| The description of the CEN instance.

 The description must be 2 to 256 characters in length. It must start with a letter but cannot start with `http://` or `https://`.

 |None|
|Name|String|No|Yes| The name of the CEN instance.

 The name must be 2 to 128 characters in length and can contain letters, digits, periods \(.\), underscores \(\_\), and hyphens \(-\). It must start with a letter but cannot start with `http://` or `https://`.

 |None|

## Response parameters {#section_fsg_t4n_4fb .section}

**Fn::GetAtt**

CenId: The ID of the created CEN instance.

## Examples {#section_klp_54n_4fb .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "CenInstance": {
      "Type": "ALIYUN::CEN::CenInstance",
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
      "Type": "String",
      "Description": "The description of the CEN instance.\n The description must be 2 to 256 characters in length and can contain letters, digits, underscores (_), and hyphens (-).  It must start with a letter but cannot start with http:// or https://."
    },
    "Name": {
      "Type": "String",
      "Description": "The name of the CEN instance.\n The name must be 2 to 128 characters in length and can contain letters, digits, underscores (_), and hyphens (-).  It must start with a letter but cannot start with http:// or https://."
    }
  },
  "Outputs": {
    "CenId": {
      "Description": "The ID of the request.",
      "Value": {
        "Fn::GetAtt": [
          "CenInstance",
          "CenId"
        ]
      }
    }
  }
}
```

