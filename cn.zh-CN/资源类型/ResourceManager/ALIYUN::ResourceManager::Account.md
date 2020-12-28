# ALIYUN::ResourceManager::Account

ALIYUN::ResourceManager::Account类型用于创建资源账号类型的成员。

## 语法

```
{
  "Type": "ALIYUN::ResourceManager::Account",
  "Properties": {
    "PayerAccountId": String,
    "DisplayName": String,
    "FolderId": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|PayerAccountId|String|否|否|结算账号ID。|取值为空表示采用当前账号结算。|
|DisplayName|String|是|是|成员名称。|长度为2~50个字符，可包含汉字、英文字母、数字、下划线（\_）、英文句点（.）和短划线（-）。成员名称在资源目录内必须唯一。 |
|FolderId|String|否|是|资源夹ID。|无|

## 返回值

Fn::GetAtt

-   FolderId：资源夹ID。
-   ResourceDirectoryId：资源目录ID。
-   AccountId：账号ID。
-   DisplayName：成员名称。
-   Type：成员类型。ResourceAccount表示资源账号。
-   JoinMethod：成员加入方式。invited表示邀请，created表示创建。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "PayerAccountId": {
      "Type": "String",
      "Description": ""
    },
    "DisplayName": {
      "Type": "String",
      "Description": "Member name"
    },
    "FolderId": {
      "Type": "String",
      "Description": "The ID of the parent folder"
    }
  },
  "Resources": {
    "ResourceManagerAccount": {
      "Type": "ALIYUN::ResourceManager::Account",
      "Properties": {
        "PayerAccountId": {
          "Ref": "PayerAccountId"
        },
        "DisplayName": {
          "Ref": "DisplayName"
        },
        "FolderId": {
          "Ref": "FolderId"
        }
      }
    }
  },
  "Outputs": {
    "JoinMethod": {
      "Description": "Ways for members to join the resource directory. Valid values: invited, created",
      "Value": {
        "Fn::GetAtt": [
          "ResourceManagerAccount",
          "JoinMethod"
        ]
      }
    },
    "ResourceDirectoryId": {
      "Description": "Resource directory ID",
      "Value": {
        "Fn::GetAtt": [
          "ResourceManagerAccount",
          "ResourceDirectoryId"
        ]
      }
    },
    "Type": {
      "Description": "Member type. The value of ResourceAccount indicates the resource account",
      "Value": {
        "Fn::GetAtt": [
          "ResourceManagerAccount",
          "Type"
        ]
      }
    },
    "AccountId": {
      "Description": "This ID of Resource Manager Account",
      "Value": {
        "Fn::GetAtt": [
          "ResourceManagerAccount",
          "AccountId"
        ]
      }
    },
    "DisplayName": {
      "Description": "Member name",
      "Value": {
        "Fn::GetAtt": [
          "ResourceManagerAccount",
          "DisplayName"
        ]
      }
    },
    "FolderId": {
      "Description": "The ID of the parent folder",
      "Value": {
        "Fn::GetAtt": [
          "ResourceManagerAccount",
          "FolderId"
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
  PayerAccountId:
    Type: String
    Description: ''
  DisplayName:
    Type: String
    Description: Member name
  FolderId:
    Type: String
    Description: The ID of the parent folder
Resources:
  ResourceManagerAccount:
    Type: 'ALIYUN::ResourceManager::Account'
    Properties:
      PayerAccountId:
        Ref: PayerAccountId
      DisplayName:
        Ref: DisplayName
      FolderId:
        Ref: FolderId
Outputs:
  JoinMethod:
    Description: >-
      Ways for members to join the resource directory. Valid values: invited,
      created
    Value:
      'Fn::GetAtt':
        - ResourceManagerAccount
        - JoinMethod
  ResourceDirectoryId:
    Description: Resource directory ID
    Value:
      'Fn::GetAtt':
        - ResourceManagerAccount
        - ResourceDirectoryId
  Type:
    Description: Member type. The value of ResourceAccount indicates the resource account
    Value:
      'Fn::GetAtt':
        - ResourceManagerAccount
        - Type
  AccountId:
    Description: This ID of Resource Manager Account
    Value:
      'Fn::GetAtt':
        - ResourceManagerAccount
        - AccountId
  DisplayName:
    Description: Member name
    Value:
      'Fn::GetAtt':
        - ResourceManagerAccount
        - DisplayName
  FolderId:
    Description: The ID of the parent folder
    Value:
      'Fn::GetAtt':
        - ResourceManagerAccount
        - FolderId
```

