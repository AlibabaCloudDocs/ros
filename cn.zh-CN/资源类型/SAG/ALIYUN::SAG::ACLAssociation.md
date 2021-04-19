# ALIYUN::SAG::ACLAssociation

ALIYUN::SAG::ACLAssociation类型用于绑定访问控制与智能接入网关实例。

## 语法

```
{
  "Type": "ALIYUN::SAG::ACLAssociation",
  "Properties": {
    "SmartAGId": String,
    "AclId": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|SmartAGId|String|是|否|需要绑定访问控制的智能网关实例ID。|无|
|AclId|String|是|否|访问控制ID。|无|

## 返回值

Fn::GetAtt

无

## 示例

`JSON`格式

```
{
    "ROSTemplateFormatVersion": "2015-09-01",
    "Parameters": {
    "AclId": {
      "Type": "String",
      "Description": "Access control ID."
    },
    "SmartAGId": {
      "Type": "String",
      "Description": "An intelligent gateway instance that needs to bind access control."
    }
  },
  "Resources": {
    "ACLAssociation": {
      "Type": "ALIYUN::SAG::ACLAssociation",
      "Properties": {
        "AclId": {
          "Ref": "AclId"
        },
        "SmartAGId": {
          "Ref": "SmartAGId"
        }
      }
    }
  },
  "Outputs": {}
}
```

`YAML`格式

```
ROSTemplateFormatVersion: '2015-09-01'
Parameters:
  AclId:
    Type: String
    Description: Access control ID.
  SmartAGId:
    Type: String
    Description: An intelligent gateway instance that needs to bind access control.
Resources:
  ACLAssociation:
    Type: 'ALIYUN::SAG::ACLAssociation'
    Properties:
      AclId:
        Ref: AclId
      SmartAGId:
        Ref: SmartAGId
Outputs: {}
```

