# ALIYUN::SAG::ACL {#concept_263795 .concept}

ALIYUN::SAG::ACL is used to create an access control list \(ACL\).

## Syntax {#section_569_l30_cg6 .section}

``` {#codeblock_j43_p7l_iz8 .language-json}
{
  "Type": "ALIYUN::SAG::ACL",
  "Properties": {
    "Name": String
  }
}
```

## Properties {#section_ndm_cmd_5h4 .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Name|String|Yes|Yes|The name of the ACL to be created.| The name must be 2 to 128 characters in length and can contain letters, digits, periods \(.\), underscores \(\_\), and hyphens \(-\). It must start with a letter but cannot start with http:// or https://.

 |

## Response parameters {#section_xbp_zo3_o2q .section}

 **Fn::GetAtt** 

AclId: the ID of the ACL.

## Examples {#section_3po_0ko_tdl .section}

``` {#codeblock_0cl_g4z_kf5 .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "ACL": {
      "Type": "ALIYUN::SAG::ACL",
      "Properties": {
        "Name": {
          "Ref": "Name"
        }
      }
    }
  },
  "Parameters": {
    "Name": {
      "Type": "String",
      "Description": "ACL name.\nThe length is 2-128 characters. It must start with a letter. It can contain digits, periods (.), underscores (_) and hyphens (-), but cannot start with http:// or https://."
    }
  },
  "Outputs": {
    "AclId": {
      "Description": "ACL ID.",
      "Value": {
        "Fn::GetAtt": [
          "ACL",
          "AclId"
        ]
      }
    }
  }
}
```

