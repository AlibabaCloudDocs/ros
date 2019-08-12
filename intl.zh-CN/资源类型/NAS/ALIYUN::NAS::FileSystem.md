# ALIYUN::NAS::FileSystem {#concept_nr2_vgr_dhb .concept}

ALIYUN::NAS::FileSystem 用于创建新的文件系统。

## 语法 {#section_grp_bdr_dhb .section}

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

## 属性 {#section_igc_jwq_dhb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ProtocolType|String|是|否|使用的协议类型。|可用值：NFS、SMB。|
|StorageType|String|是|否|文件系统类别，目前包含 Performance（性能型）、Capacity（容量型）。|可用值：Performance、Capacity。|
|Description|String|否|是|文件系统描述（不可用空格符）。|无。|

## 返回值 {#section_utp_2wq_dhb .section}

**Fn::GetAtt**

FileSystemId：文件系统 ID。

## 示例 {#section_mn3_wwq_dhb .section}

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

