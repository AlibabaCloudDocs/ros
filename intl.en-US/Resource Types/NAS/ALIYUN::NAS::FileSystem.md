# ALIYUN::NAS::FileSystem {#concept_nr2_vgr_dhb .concept}

ALIYUN::NAS::FileSystem is used to create a new file system.

## Syntax {#section_grp_bdr_dhb .section}

```
{
  "Type": "ALIYUN::NAS::FileSystem",
  "Properties": {
    "ProtocolType": String,
    "StorageType": String,
    "Description": String
  }
}
```

## Properties {#section_igc_jwq_dhb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|ProtocolType|String|Yes|No|The protocol type used for the file system.|Valid values: NFS and SMB.|
|StorageType|String|Yes|No|The type of file system to use.|Valid values: Performance and Capacity.|
|Description|String|No|Yes|The description of the file system. Space characters are not allowed.|None|

## Response parameters {#section_utp_2wq_dhb .section}

**FN::GetAtt**

FileSystemId: the ID of the created file system.

## Examples {#section_mn3_wwq_dhb .section}

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "FileSystem": {
      "Type": "ALIYUN::NAS::FileSystem",
      "Properties": {
        "ProtocolType": {
          "Ref": "ProtocolType"
        },
        "StorageType": {
          "Ref": "StorageType"
        },
        "Description": {
          "Ref": "Description"
        }
      }
    }
  },
  "Parameters": {
    "ProtocolType": {
      "Type": "String",
      "Description": "Type of protocol used. Currently includes the NFS type and the SMB type",
      "AllowedValues": ["NFS", "SMB"]
    },
    "StorageType": {
      "Type": "String",
      "Description": "The file system type. Currently includes the Performance type and the Capacity type",
      "AllowedValues": ["Performance", "Capacity"]
    },
    "Description": {
      "Type": "String",
      "Description": "File system description (space characters are not allowed)"
    }
  },
  "Outputs": {
    "FileSystemId": {
      "Description": "ID of the file system created",
      "Value": {
        "Fn::GetAtt": ["FileSystem", "FileSystemId"]
      }
    }
  }
}
```

