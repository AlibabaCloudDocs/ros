# ALIYUN::ResourceManager::Handshake

ALIYUN::ResourceManager::Handshake类型用于创建邀请。

## 语法

```
{
  "Type": "ALIYUN::ResourceManager::Handshake",
  "Properties": {
    "Note": String,
    "TargetType": String,
    "TargetEntity": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Note|String|否|否|备注。|无|
|TargetType|String|是|否|被邀请账号类型。|取值：-   Account：账号ID。
-   Email：账号登录邮箱。 |
|TargetEntity|String|是|否|被邀请账号ID或登录邮箱。|无|

## 返回值

Fn::GetAtt

-   ResourceDirectoryId：资源目录ID。
-   HandshakeId：邀请ID。
-   Note：备注。
-   TargetType：被邀请账号类型。
-   TargetEntity：被邀请账号ID或登录邮箱。
-   MasterAccountName：企业管理账号名称。
-   MasterAccountId：企业管理账号ID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Note": {
      "Type": "String",
      "Description": "Remarks"
    },
    "TargetType": {
      "Type": "String",
      "Description": "Type of account being invited. Valid values: Account, Email"
    },
    "TargetEntity": {
      "Type": "String",
      "Description": "Invited account ID or login email"
    }
  },
  "Resources": {
    "ResourceManagerHandshake": {
      "Type": "ALIYUN::ResourceManager::Handshake",
      "Properties": {
        "Note": {
          "Ref": "Note"
        },
        "TargetType": {
          "Ref": "TargetType"
        },
        "TargetEntity": {
          "Ref": "TargetEntity"
        }
      }
    }
  },
  "Outputs": {
    "ResourceDirectoryId": {
      "Description": "Resource directory ID",
      "Value": {
        "Fn::GetAtt": [
          "ResourceManagerHandshake",
          "ResourceDirectoryId"
        ]
      }
    },
    "HandshakeId": {
      "Description": "This ID of Resource Manager handshake",
      "Value": {
        "Fn::GetAtt": [
          "ResourceManagerHandshake",
          "HandshakeId"
        ]
      }
    },
    "Note": {
      "Description": "Remarks",
      "Value": {
        "Fn::GetAtt": [
          "ResourceManagerHandshake",
          "Note"
        ]
      }
    },
    "MasterAccountName": {
      "Description": "The name of the main account of the resource directory",
      "Value": {
        "Fn::GetAtt": [
          "ResourceManagerHandshake",
          "MasterAccountName"
        ]
      }
    },
    "TargetType": {
      "Description": "Type of account being invited. Valid values: Account, Email",
      "Value": {
        "Fn::GetAtt": [
          "ResourceManagerHandshake",
          "TargetType"
        ]
      }
    },
    "MasterAccountId": {
      "Description": "Resource account master account ID",
      "Value": {
        "Fn::GetAtt": [
          "ResourceManagerHandshake",
          "MasterAccountId"
        ]
      }
    },
    "TargetEntity": {
      "Description": "Invited account ID or login email",
      "Value": {
        "Fn::GetAtt": [
          "ResourceManagerHandshake",
          "TargetEntity"
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
  Note:
    Type: String
    Description: Remarks
  TargetType:
    Type: String
    Description: 'Type of account being invited. Valid values: Account, Email'
  TargetEntity:
    Type: String
    Description: Invited account ID or login email
Resources:
  ResourceManagerHandshake:
    Type: 'ALIYUN::ResourceManager::Handshake'
    Properties:
      Note:
        Ref: Note
      TargetType:
        Ref: TargetType
      TargetEntity:
        Ref: TargetEntity
Outputs:
  ResourceDirectoryId:
    Description: Resource directory ID
    Value:
      'Fn::GetAtt':
        - ResourceManagerHandshake
        - ResourceDirectoryId
  HandshakeId:
    Description: This ID of Resource Manager handshake
    Value:
      'Fn::GetAtt':
        - ResourceManagerHandshake
        - HandshakeId
  Note:
    Description: Remarks
    Value:
      'Fn::GetAtt':
        - ResourceManagerHandshake
        - Note
  MasterAccountName:
    Description: The name of the main account of the resource directory
    Value:
      'Fn::GetAtt':
        - ResourceManagerHandshake
        - MasterAccountName
  TargetType:
    Description: 'Type of account being invited. Valid values: Account, Email'
    Value:
      'Fn::GetAtt':
        - ResourceManagerHandshake
        - TargetType
  MasterAccountId:
    Description: Resource account master account ID
    Value:
      'Fn::GetAtt':
        - ResourceManagerHandshake
        - MasterAccountId
  TargetEntity:
    Description: Invited account ID or login email
    Value:
      'Fn::GetAtt':
        - ResourceManagerHandshake
        - TargetEntity
```

