# ALIYUN::NAS::AccessGroup {#concept_q3d_xvq_dhb .concept}

ALIYUN::NAS::AccessGroup用于创建权限组。

## 语法 { .section}

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

## 属性 {#section_igc_jwq_dhb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|AccessGroupType|String|是|否|权限组类型。|可用值：Vpc、Classic。|
|AccessGroupName|String|是|否|权限组名称。|以大、小写、数字、中横线开头，最少3个字符，最多64个字符。|
|Description|String|否|是|权限组描述，默认和名称相同。|无。|

## 返回值 {#section_utp_2wq_dhb .section}

**Fn::GetAtt**

AccessGroupName：权限组名称。

## 示例 {#section_mn3_wwq_dhb .section}

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

