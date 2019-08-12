# ALIYUN::NAS::MountTarget {#concept_hr4_gkr_dhb .concept}

ALIYUN::NAS::MountTarget is used to create a mount point.

## Syntax {#section_opn_jkr_dhb .section}

```
{
  "Type": "ALIYUN::NAS::MountTarget",
  "Properties": {
    "Status": String,
    "VpcId": String,
    "FileSystemId": String,
    "VSwitchId": String,
    "NetworkType": String,
    "AccessGroupName": String
  }
}
```

## Properties {#section_igc_jwq_dhb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Status|String|No|Yes|The status of a file system.|Valid values: Active and Inactive.|
|VpcId|String|No|No|The ID of the VPC to which the file system belongs.|None|
|FileSystemId|String|Yes|No|The ID of the file system.|None|
|VSwitchId|String|No|No|The ID of the VSwitch in the VPC.|None|
|NetworkType|String|Yes|No|The network type.|Valid values: VPC and Classic.|
|AccessGroupName|String|Yes|Yes|The permission group name.|None|

## Response parameters {#section_utp_2wq_dhb .section}

**FN::GetAtt**

MountTargetDomain: the domain name of the mount point.

## Examples {#section_mn3_wwq_dhb .section}

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "MountTarget": {
      "Type": "ALIYUN::NAS::MountTarget",
      "Properties": {
        "Status": {
          "Ref": "Status"
        },
        "VpcId": {
          "Ref": "VpcId"
        },
        "FileSystemId": {
          "Ref": "FileSystemId"
        },
        "VSwitchId": {
          "Ref": "VSwitchId"
        },
        "NetworkType": {
          "Ref": "NetworkType"
        },
        "AccessGroupName": {
          "Ref": "AccessGroupName"
        }
      }
    }
  },
  "Parameters": {
    "Status": {
      "Type": "String",
      "Description": "Status, including Active and Inactive",
      "AllowedValues": ["Active", "Inactive"]
    },
    "VpcId": {
      "Type": "String",
      "Description": "VPC network ID"
    },
    "FileSystemId": {
      "Type": "String",
      "Description": "File system ID"
    },
    "VSwitchId": {
      "Type": "String",
      "Description": "VSwitch ID."
    },
    "NetworkType": {
      "Type": "String",
      "Description": "Network type, including Vpc and Classic networks.",
      "AllowedValues": ["Vpc", "Classic"]
    },
    "AccessGroupName": {
      "Type": "String",
      "Description": "Permission group name"
    }
  },
  "Outputs": {
    "MountTargetDomain": {
      "Description": "Mount point domain name",
      "Value": {
        "Fn::GetAtt": ["MountTarget", "MountTargetDomain"]
      }
    }
  }
}
```

