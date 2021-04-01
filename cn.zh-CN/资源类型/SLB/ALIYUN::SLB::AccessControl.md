# ALIYUN::SLB::AccessControl

ALIYUN::SLB::AccessControl用于创建访问控制策略组。

## 语法

```
{
  "Type": "ALIYUN::SLB::AccessControl",
  "Properties": {
    "AddressIPVersion": String,
    "AclName": String,
    "AclEntrys": List,
    "Tags": List
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|AddressIPVersion|String|否|否|IP版本。|取值：-   ipv4
-   ipv6 |
|AclName|String|是|是|访问控制策略组名称。|无|
|AclEntrys|List|否|否|访问控制策略组的信息列表。|最多支持50个信息列表。更多信息，请参见[AclEntrys属性](#section_wwl_vw2_2hb)。 |
|Tags|List|否|是|标签。|最多支持添加20个标签。更多信息，请参见[Tags属性](#section_nm7_b4o_vux)。 |

## AclEntrys语法

```
"AclEntrys": [
  {
    "comment": String,
    "entry": String
  }
]
```

## AclEntrys属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|comment|String|否|否|访问控制条目备注。|无|
|entry|String|是|否|IP地址或CIDR网段。|无|

## Tags语法

```
"Tags": [
  {
    "Key": String,
    "Value": String
  }
]  
```

## Tags属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Key|String|是|否|标签键。|长度为1~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或者`https://` 。|
|Value|String|否|否|标签值。|长度为0~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或者`https://` 。|

## 返回值

Fn::GetAtt

AclId：访问控制策略组ID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "AclEntrys": {
      "Type": "Json",
      "Description": "A list of acl entrys. Each entry can be IP addresses or CIDR blocks. Max length: 50.",
      "MaxLength": 50
    },
    "AddressIPVersion": {
      "Type": "String",
      "Description": "IP version. Could be \"ipv4\" or \"ipv6\".",
      "AllowedValues": [
        "ipv4",
        "ipv6"
      ]
    },
    "AclName": {
      "Type": "String",
      "Description": "The name of the access control list."
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to instance. Max support 20 tags to add during create instance. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
    }
  },
  "Resources": {
    "AccessControl": {
      "Type": "ALIYUN::SLB::AccessControl",
      "Properties": {
        "AclEntrys": {
          "Ref": "AclEntrys"
        },
        "AddressIPVersion": {
          "Ref": "AddressIPVersion"
        },
        "AclName": {
          "Ref": "AclName"
        },
        "Tags": {
          "Ref": "Tags"
        }
      }
    }
  },
  "Outputs": {
    "AclId": {
      "Description": "The ID of the access control list.",
      "Value": {
        "Fn::GetAtt": [
          "AccessControl",
          "AclId"
        ]
      }
    }
  }
}
```

`YAML`格式

```
ROSTemplateFormatVersion: '2015-09-01'
Parameters:
  AclEntrys:
    Description: 'A list of acl entrys. Each entry can be IP addresses or CIDR blocks.
      Max length: 50.'
    MaxLength: 50
    Type: Json
  AclName:
    Description: The name of the access control list.
    Type: String
  AddressIPVersion:
    AllowedValues:
    - ipv4
    - ipv6
    Description: IP version. Could be "ipv4" or "ipv6".
    Type: String
  Tags:
    Description: Tags to attach to instance. Max support 20 tags to add during create
      instance. Each tag with two properties Key and Value, and Key is required.
    MaxLength: 20
    Type: Json
Resources:
  AccessControl:
    Properties:
      AclEntrys:
        Ref: AclEntrys
      AclName:
        Ref: AclName
      AddressIPVersion:
        Ref: AddressIPVersion
      Tags:
        Ref: Tags
    Type: ALIYUN::SLB::AccessControl
Outputs:
  AclId:
    Description: The ID of the access control list.
    Value:
      Fn::GetAtt:
      - AccessControl
      - AclId
```

更多示例，请参见：[JSON示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/SLB/JSON/AccessControl.json)和[YAML示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/SLB/YAML/AccessControl.yml)。

