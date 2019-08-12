# ALIYUN::NAS::AccessGroup {#concept_q3d_xvq_dhb .concept}

ALIYUN::NAS::AccessGroup is used to create a permission group.

## Syntax { .section}

```
{
  "Type": "ALIYUN::NAS::AccessGroup",
  "Properties": {
    "AccessGroupType": String,
    "AccessGroupName": String,
    "Description": String
  }
}
```

## Properties {#section_igc_jwq_dhb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|AccessGroupType|String|Yes|No|The type of the permission group.|Valid values: VPC and Classic.|
|AccessGroupName|String|Yes|No|The name of the permission group.|The name must be 3 to 64 characters in length. It must start with a letter, digit, or hyphen \(-\).|
|Description|String|No|Yes|The description of the permission group. The description is the same as the permission group name by default.|None|

## Response parameters {#section_utp_2wq_dhb .section}

**FN::GetAtt**

AccessGroupName: the name of the permission group.

## Examples {#section_mn3_wwq_dhb .section}

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "AccessGroup": {
      "Type": "ALIYUN::NAS::AccessGroup",
      "Properties": {
        "AccessGroupType": {
          "Ref": "AccessGroupType"
        },
        "AccessGroupName": {
          "Ref": "AccessGroupName"
        },
        "Description": {
          "Ref": "Description"
        }
      }
    }
  },
  "Parameters": {
    "AccessGroupType": {
      "Type": "String",
      "Description": "Permission group type, including the Vpc and Classic types",
      "AllowedValues": ["Vpc", "Classic"]
    },
    "AccessGroupName": {
      "AllowedPattern": "^[a-zA-Z0-9-]{3,64}$",
      "Type": "String",
      "Description": "Permission group name"
    },
    "Description": {
      "Type": "String",
      "Description": "Permission group description. It is the same as the permission group name by default."
    }
  },
  "Outputs": {
    "AccessGroupName": {
      "Description": "Permission group name",
      "Value": {
        "Fn::GetAtt": ["AccessGroup", "AccessGroupName"]
      }
    }
  }
}
```

