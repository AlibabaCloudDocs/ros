# ALIYUN::ResourceManager::ResourceDirectory

ALIYUN::ResourceManager::ResourceDirectory类型用于开通资源目录。开通资源目录后，系统会为您创建一个Root资源夹，并将当前账号设置为企业管理账号。该企业管理账号具有管理资源目录的所有权限。

## 语法

```
{
  "Type": "ALIYUN::ResourceManager::ResourceDirectory",
  "Properties": {}
}
```

## 属性

无

## 返回值

Fn::GetAtt

-   ResourceDirectoryId：资源目录ID。
-   MasterAccountName：企业管理账号名称。
-   CreateTime：资源目录开通时间。
-   RootFolderId：Root资源夹ID。
-   MasterAccountId：企业管理账号ID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "ResourceManagerResourceDirectory": {
      "Type": "ALIYUN::ResourceManager::ResourceDirectory",
      "Properties": {}
    }
  },
  "Outputs": {
    "ResourceDirectoryId": {
      "Description": "The ID of the resource directory",
      "Value": {
        "Fn::GetAtt": [
          "ResourceManagerResourceDirectory",
          "ResourceDirectoryId"
        ]
      }
    },
    "MasterAccountName": {
      "Description": "The name of the master account",
      "Value": {
        "Fn::GetAtt": [
          "ResourceManagerResourceDirectory",
          "MasterAccountName"
        ]
      }
    },
    "CreateTime": {
      "Description": "The time when the resource directory was created",
      "Value": {
        "Fn::GetAtt": [
          "ResourceManagerResourceDirectory",
          "CreateTime"
        ]
      }
    },
    "RootFolderId": {
      "Description": "The ID of the root folder",
      "Value": {
        "Fn::GetAtt": [
          "ResourceManagerResourceDirectory",
          "RootFolderId"
        ]
      }
    },
    "MasterAccountId": {
      "Description": "The ID of the master account",
      "Value": {
        "Fn::GetAtt": [
          "ResourceManagerResourceDirectory",
          "MasterAccountId"
        ]
      }
    }
  }
}
```

`YAML`格式

```
ROSTemplateFormatVersion: '2015-09-01'
Resources:
  ResourceManagerResourceDirectory:
    Type: 'ALIYUN::ResourceManager::ResourceDirectory'
    Properties: {}
Outputs:
  ResourceDirectoryId:
    Description: The ID of the resource directory
    Value:
      'Fn::GetAtt':
        - ResourceManagerResourceDirectory
        - ResourceDirectoryId
  MasterAccountName:
    Description: The name of the master account
    Value:
      'Fn::GetAtt':
        - ResourceManagerResourceDirectory
        - MasterAccountName
  CreateTime:
    Description: The time when the resource directory was created
    Value:
      'Fn::GetAtt':
        - ResourceManagerResourceDirectory
        - CreateTime
  RootFolderId:
    Description: The ID of the root folder
    Value:
      'Fn::GetAtt':
        - ResourceManagerResourceDirectory
        - RootFolderId
  MasterAccountId:
    Description: The ID of the master account
    Value:
      'Fn::GetAtt':
        - ResourceManagerResourceDirectory
        - MasterAccountId
```

