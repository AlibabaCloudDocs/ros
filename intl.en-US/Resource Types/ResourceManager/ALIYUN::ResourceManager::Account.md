# ALIYUN::ResourceManager::Account

ALIYUN::ResourceManager::Account is used to create a resource account as a member account.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|PayerAccountId|String|No|No|The ID of the settlement account.|If this parameter is left empty, the current account is used for settlement.|
|DisplayName|String|Yes|Yes|The name of the member account.|The name must be 2 to 50 characters in length and can contain letters, digits, underscores \(\_\), periods \(.\), and hyphens \(-\).The name must be unique in the current resource directory. |
|FolderId|String|No|Yes|The ID of the folder.|None|

## Response parameters

Fn::GetAtt

-   FolderId: the ID of the folder.
-   ResourceDirectoryId: the ID of the resource directory.
-   AccountId: the ID of the member account.
-   DisplayName: the name of the member account.
-   Type: the type of the member account. ResourceAccount indicates that a resource account is created as the member account.
-   JoinMethod: the method for the member account to join the resource directory. invited indicates that the member account is invited. created indicates that the member account is created.
-   ModifyTime: the time when the member account was modified.

## Examples

`JSON` format

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
    "ModifyTime": {
      "Description": "The modification time of the invitation",
      "Value": {
        "Fn::GetAtt": [
          "ResourceManagerAccount",
          "ModifyTime"
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

`YAML` format

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
  ModifyTime:
    Description: The modification time of the invitation
    Value:
      'Fn::GetAtt':
        - ResourceManagerAccount
        - ModifyTime
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

