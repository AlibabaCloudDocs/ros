# ALIYUN::ResourceManager::ResourceGroup

ALIYUN::ResourceManager::ResourceGroup类型用于创建资源组。

## 语法

```
{
  "Type": "ALIYUN::ResourceManager::ResourceGroup",
  "Properties": {
    "DisplayName": String,
    "Name": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|DisplayName|String|是|是|资源组显示名称。|长度为1~30个字符，可包含汉字、英文字母、数字和短划线（-）。|
|Name|String|是|否|资源组唯一标识。|长度为3~12个字符，必须以英文字母开头。可包含英文字母、数字和短划线（-）。|

## 返回值

Fn::GetAtt

-   RegionStatuses：各个地域的资源组状态。
-   AccountId：资源组所属的阿里云账号ID。
-   DisplayName：资源组显示名称。
-   Id：资源组ID。
-   Name：资源组唯一标识。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "DisplayName": {
      "Type": "String",
      "Description": "The display name of the resource group"
    },
    "Name": {
      "Type": "String",
      "Description": "The unique identifier of the resource group"
    }
  },
  "Resources": {
    "ResourceManagerResourceGroup": {
      "Type": "ALIYUN::ResourceManager::ResourceGroup",
      "Properties": {
        "DisplayName": {
          "Ref": "DisplayName"
        },
        "Name": {
          "Ref": "Name"
        }
      }
    }
  },
  "Outputs": {
    "RegionStatuses": {
      "Description": "The status of the resource group in all regions",
      "Value": {
        "Fn::GetAtt": [
          "ResourceManagerResourceGroup",
          "RegionStatuses"
        ]
      }
    },
    "AccountId": {
      "Description": "The ID of the Alibaba Cloud account to which the resource group belongs",
      "Value": {
        "Fn::GetAtt": [
          "ResourceManagerResourceGroup",
          "AccountId"
        ]
      }
    },
    "DisplayName": {
      "Description": "The display name of the resource group",
      "Value": {
        "Fn::GetAtt": [
          "ResourceManagerResourceGroup",
          "DisplayName"
        ]
      }
    },
    "Id": {
      "Description": "The ID of the resource group",
      "Value": {
        "Fn::GetAtt": [
          "ResourceManagerResourceGroup",
          "Id"
        ]
      }
    },
    "Name": {
      "Description": "The unique identifier of the resource group",
      "Value": {
        "Fn::GetAtt": [
          "ResourceManagerResourceGroup",
          "Name"
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
  DisplayName:
    Type: String
    Description: The display name of the resource group
  Name:
    Type: String
    Description: The unique identifier of the resource group
Resources:
  ResourceManagerResourceGroup:
    Type: 'ALIYUN::ResourceManager::ResourceGroup'
    Properties:
      DisplayName:
        Ref: DisplayName
      Name:
        Ref: Name
Outputs:
  RegionStatuses:
    Description: The status of the resource group in all regions
    Value:
      'Fn::GetAtt':
        - ResourceManagerResourceGroup
        - RegionStatuses
  AccountId:
    Description: The ID of the Alibaba Cloud account to which the resource group belongs
    Value:
      'Fn::GetAtt':
        - ResourceManagerResourceGroup
        - AccountId
  DisplayName:
    Description: The display name of the resource group
    Value:
      'Fn::GetAtt':
        - ResourceManagerResourceGroup
        - DisplayName
  Id:
    Description: The ID of the resource group
    Value:
      'Fn::GetAtt':
        - ResourceManagerResourceGroup
        - Id
  Name:
    Description: The unique identifier of the resource group
    Value:
      'Fn::GetAtt':
        - ResourceManagerResourceGroup
        - Name
```

