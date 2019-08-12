# ALIYUN::SLB::AccessControl {#concept_yd3_rw2_2hb .concept}

ALIYUN::SLB::AccessControl is used to create an access control list \(ACL\).

## Syntax {#section_ey2_ycz_lfb .section}

```language-json
{
  "Type": "ALIYUN::SLB::AccessControl",
  "Properties": {
    "AddressIPVersion": String,
    "AclName": String,
    "AclEntrys": List
  }
}
```

## Properties {#section_n13_22z_lfb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|AddressIPVersion|String|No|No|The IP version.|Valid values: ipv4 and ipv6.|
|AclName|String|Yes|Yes|The name of the ACL.|None|
|AclEntrys|List|No|No|The list of ACL entries.|A list can contain a maximum of 50 ACL entries.|

## AclEntrys syntax {#section_vwl_vw2_2hb .section}

```
"AclEntrys": [
  {
    "Comment": String,
    "Entry": String
  }
]
```

## AclEntrys properties {#section_wwl_vw2_2hb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Comment|String|No|No|The comment on an ACL entry.|None|
|Entry|String|Yes|No|The authorized IP addresses or CIDR blocks.|None|

## Response parameters {#section_wfc_q2z_lfb .section}

**Fn::GetAtt**

AclId: the ID of the ACL.

## Examples {#section_lcd_s2z_lfb .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "AccessControl": {
      "Type": "ALIYUN::SLB::AccessControl",
      "Properties": {
        "AddressIPVersion": {
          "Ref": "AddressIPVersion"
        },
        "AclName": {
          "Ref": "AclName"
        },
        "AclEntrys": {
          "Fn::Split": [",", {
            "Ref": "AclEntrys"
          }, {
            "Ref": "AclEntrys"
          }]
        }
      }
    }
  },
  "Parameters": {
    "AddressIPVersion": {
      "Type": "String",
      "Description": "IP version. Could be \"ipv4\" or \"ipv6\".",
      "AllowedValues": ["ipv4", "ipv6"]
    },
    "AclName": {
      "Type": "String",
      "Description": "The name of the access control list."
    },
    "AclEntrys": {
      "Type": "CommaDelimitedList",
      "Description": "A list of acl entrys. Each entry can be IP addresses or CIDR blocks. Max length: 50.",
      "MaxLength": 50
    }
  },
  "Outputs": {
    "AclId": {
      "Description": "The ID of the access control list.",
      "value": {
        "Fn::GetAtt": ["AccessControl", "AclId"]
      }
    }
  }
}
```

