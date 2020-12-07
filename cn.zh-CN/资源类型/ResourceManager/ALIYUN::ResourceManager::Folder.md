# ALIYUN::ResourceManager::Folder

ALIYUN::ResourceManager::Folder类型用于创建资源夹。

## 语法

```
{
  "Type": "ALIYUN::ResourceManager::Folder",
  "Properties": {
    "FolderName": String,
    "ParentFolderId": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|FolderName|String|是|是|资源夹名称。|长度为1~24个字符，可包含汉字、英文字母、数字、下划线（\_）、英文句点（.）和短划线（-）。|
|ParentFolderId|String|否|否|父资源夹ID。|无|

## 返回值

Fn::GetAtt

-   FolderId：资源夹ID。
-   FolderName：资源夹名称。
-   ParentFolderId：父资源夹ID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "FolderName": {
      "Type": "String",
      "Description": "The name of the folder"
    },
    "ParentFolderId": {
      "Type": "String",
      "Description": "The ID of the parent folder. If not set, the system default value will be used"
    }
  },
  "Resources": {
    "ResourceManagerFolder": {
      "Type": "ALIYUN::ResourceManager::Folder",
      "Properties": {
        "FolderName": {
          "Ref": "FolderName"
        },
        "ParentFolderId": {
          "Ref": "ParentFolderId"
        }
      }
    }
  },
  "Outputs": {
    "FolderId": {
      "Description": "The ID of the folder",
      "Value": {
        "Fn::GetAtt": [
          "ResourceManagerFolder",
          "FolderId"
        ]
      }
    },
    "FolderName": {
      "Description": "The name of the folder",
      "Value": {
        "Fn::GetAtt": [
          "ResourceManagerFolder",
          "FolderName"
        ]
      }
    },
    "ParentFolderId": {
      "Description": "The ID of the parent folder. If not set, the system default value will be used",
      "Value": {
        "Fn::GetAtt": [
          "ResourceManagerFolder",
          "ParentFolderId"
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
  FolderName:
    Type: String
    Description: The name of the folder
  ParentFolderId:
    Type: String
    Description: >-
      The ID of the parent folder. If not set, the system default value will be
      used
Resources:
  ResourceManagerFolder:
    Type: 'ALIYUN::ResourceManager::Folder'
    Properties:
      FolderName:
        Ref: FolderName
      ParentFolderId:
        Ref: ParentFolderId
Outputs:
  FolderId:
    Description: The ID of the folder
    Value:
      'Fn::GetAtt':
        - ResourceManagerFolder
        - FolderId
  FolderName:
    Description: The name of the folder
    Value:
      'Fn::GetAtt':
        - ResourceManagerFolder
        - FolderName
  ParentFolderId:
    Description: >-
      The ID of the parent folder. If not set, the system default value will be
      used
    Value:
      'Fn::GetAtt':
        - ResourceManagerFolder
        - ParentFolderId
```

