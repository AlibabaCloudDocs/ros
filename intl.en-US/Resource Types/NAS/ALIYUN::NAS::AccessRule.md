# ALIYUN::NAS::AccessRule {#concept_p54_tbr_dhb .concept}

ALIYUN::NAS::AccessRule is used to create a permission rule.

## Syntax {#section_grp_bdr_dhb .section}

```
{
  "Type": "ALIYUN::NAS::AccessRule",
  "Properties": {
    "Priority": Integer,
    "UserAccessType": String,
    "AccessGroupName": String,
    "SourceCidrIp": String,
    "RWAccessType": String
  }
}
```

## Properties {#section_igc_jwq_dhb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Priority|Integer|No|Yes|The user access priority.|Valid values: 1 to 100. Default value: 1.|
|UserAccessType|String|No|Yes|The user access type.|Valid values: no\_squash, root\_squash, and all\_squash. Default value: no\_squash.|
|AccessGroupName|String|Yes|No|The name of the permission group.|None|
|SourceCidrIp|String|Yes|Yes|The authorized IP address or CIDR block.|None|
|RWAccessType|String|No|Yes|The read/write permission type.|Valid values: RDWR and RDONLY. Default value: RDWR.|

## Response parameters {#section_utp_2wq_dhb .section}

**FN::GetAtt**

AccessRuleId: the ID of the permission rule.

## Examples {#section_mn3_wwq_dhb .section}

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "AccessRule": {
      "Type": "ALIYUN::NAS::AccessRule",
      "Properties": {
        "Priority": {
          "Ref": "Priority"
        },
        "RWAccessType ":{
          "Ref": "RWAccessType"
        },
        "UserAccessType": {
          "Ref": "UserAccessType"
        },
        "SourceCidrIp": {
          "Ref": "SourceCidrIp"
        },
        "AccessGroupName": {
          "Ref": "AccessGroupName"
        }
      }
    }
  },
  "Parameters": {
    "Priority": {
      "Default": 1,
      "Type": "Number",
      "Description": "Priority level. Range: 1-100. Default value: 1",
      "MaxValue": 100,
      "MinValue": 1
    },
    "RWAccessType": {
      "Default": "RDWR",
      "Type": "String",
      "Description": "Read-write permission type: RDWR (default), RDONLY",
      "AllowedValues": ["RDWR", "RDONLY"]
    },
    "UserAccessType": {
      "Default": "no_squash",
      "Type": "String",
      "Description": "User permission type: no_squash (default), root_squash, all_squash",
      "AllowedValues": ["no_squash", "root_squash", "all_squash"]
    },
    "SourceCidrIp": {
      "Type": "String",
      "Description": "Address or address segment"
    },
    "AccessGroupName": {
      "Type": "String",
      "Description": "Permission group name"
    }
  },
  "Outputs": {
    "AccessRuleId": {
      "Description": "Rule serial number",
      "Value": {
        "Fn::GetAtt": ["AccessRule", "AccessRuleId"]
      }
    }
  }
}
```

