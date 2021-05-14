# ALIYUN::VPC::NetworkAclAssociation

ALIYUN::VPC::NetworkAclAssociation类型用于绑定网络ACL到交换机。

## 语法

```
{
  "Type": "ALIYUN::VPC::NetworkAclAssociation",
  "Properties": {
    "NetworkAclId": String,
    "Resources": List
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|NetworkAclId|String|是|否|网络ACL的ID。|无|
|Resources|List|是|否|网络ACL关联的资源。|最多支持关联20个资源。更多信息，请参见[Resources属性](#section_ag8_qga_s8g)。 |

## Resources语法

```
"Resources": [
  {
    "ResourceId": String,
    "ResourceType": String
  }
]
```

## Resources属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ResourceId|String|是|否|资源ID。|无|
|ResourceType|String|否|否|资源类型。|取值：VSwitch，表示交换机。|

## 返回值

Fn::GetAtt

NetworkAclId：网络ACL的ID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "NetworkAclId": {
      "Type": "String",
      "Description": "The ID of the network ACL."
    },
    "Resources": {
      "Type": "Json",
      "Description": "The list of resources that need to be associated with network ACL.",
      "MinLength": 1,
      "MaxLength": 20
    }
  },
  "Resources": {
    "NetworkAclAssociation": {
      "Type": "ALIYUN::VPC::NetworkAclAssociation",
      "Properties": {
        "NetworkAclId": {
          "Ref": "NetworkAclId"
        },
        "Resources": {
          "Ref": "Resources"
        }
      }
    }
  },
  "Outputs": {
    "NetworkAclId": {
      "Description": "The ID of the network ACL.",
      "Value": {
        "Fn::GetAtt": [
          "NetworkAclAssociation",
          "NetworkAclId"
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
  NetworkAclId:
    Description: The ID of the network ACL.
    Type: String
  Resources:
    Description: The list of resources that need to be associated with network ACL.
    MaxLength: 20
    MinLength: 1
    Type: Json
Resources:
  NetworkAclAssociation:
    Properties:
      NetworkAclId:
        Ref: NetworkAclId
      Resources:
        Ref: Resources
    Type: ALIYUN::VPC::NetworkAclAssociation
Outputs:
  NetworkAclId:
    Description: The ID of the network ACL.
    Value:
      Fn::GetAtt:
      - NetworkAclAssociation
      - NetworkAclId
```

