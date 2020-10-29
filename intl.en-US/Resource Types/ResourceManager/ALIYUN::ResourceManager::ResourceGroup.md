# ALIYUN::ResourceManager::ResourceGroup

ALIYUN::ResourceManager::ResourceGroup is used to create a resource group.

## Syntax

```
{
  "Type": "ALIYUN::ResourceManager::ResourceGroup",
  "Properties": {
    "DisplayName": String,
    "Name": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|DisplayName|String|Yes|Yes|The display name of the resource group.|The name must be 1 to 30 characters in length and can contain letters, digits, and hyphens \(-\).|
|Name|String|Yes|No|The unique identifier \(UID\) of the resource group.|The UID must be 3 to 12 characters in length and can contain letters, digits, and hyphens \(-\). It must start with a letter.|

## Response parameters

Fn::GetAtt

-   RegionStatuses: the statuses of the resource group in all regions.
-   AccountId: the ID of the Alibaba Cloud account to which the resource group belongs.
-   DisplayName: the display name of the resource group.
-   Id: the ID of the resource group.
-   CreateDate: the time when the resource group was created.
-   Name: the UID of the resource group.

## Examples

`JSON` format

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
    "CreateDate": {
      "Description": "The time when the resource group was created",
      "Value": {
        "Fn::GetAtt": [
          "ResourceManagerResourceGroup",
          "CreateDate"
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

`YAML` format

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
  CreateDate:
    Description: The time when the resource group was created
    Value:
      'Fn::GetAtt':
        - ResourceManagerResourceGroup
        - CreateDate
  Name:
    Description: The unique identifier of the resource group
    Value:
      'Fn::GetAtt':
        - ResourceManagerResourceGroup
        - Name
```

