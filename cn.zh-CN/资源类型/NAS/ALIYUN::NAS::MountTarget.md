# ALIYUN::NAS::MountTarget {#concept_hr4_gkr_dhb .concept}

ALIYUN::NAS::MountTarget类型用于创建挂载点。

## 语法 {#section_opn_jkr_dhb .section}

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

## 属性 {#section_igc_jwq_dhb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Status|String|否|是|状态。|可用值：Active 、Inactive。|
|VpcId|String|否|否|VPC 网络 ID。|无。|
|FileSystemId|String|是|否|文件系统 ID。|无。|
|VSwitchId|String|否|否|交换机 ID。|无。|
|NetworkType|String|是|否|网络类型。|可用值：Vpc、Classic。|
|AccessGroupName|String|是|是|权限组名称。|无。|

## 返回值 {#section_utp_2wq_dhb .section}

**Fn::GetAtt**

MountTargetDomain：挂载点域名。

## 示例 {#section_mn3_wwq_dhb .section}

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

