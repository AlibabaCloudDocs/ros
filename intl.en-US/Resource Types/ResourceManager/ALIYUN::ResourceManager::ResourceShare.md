# ALIYUN::ResourceManager::ResourceShare

ALIYUN::ResourceManager::ResourceShare is used to create a resource share.

## Syntax

```
{
  "Type": "ALIYUN::ResourceManager::ResourceShare",
  "Properties": {
    "ResourceShareName": String,
    "Targets": List,
    "Resources": List
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ResourceShareName|String|Yes|Yes|The name of the resource share.|The name must be 1 to 50 characters in length and can contain letters, digits, periods \(.\), underscores \(\_\), and hyphens \(-\).|
|Targets|List|No|No|The list of shared targets.|A shared target shares the resources of resource owners. You can share your resources only with the member accounts in your resource directory. A shared target is indicated by its account ID. For more information about how to obtain the ID, see [View the detailed information of a member account](). One to five shared targets can be specified at a time. |
|Resources|List|No|No|The list of shared resources.|One to five shared resources can be specified at a time. For more information, see [Resources properties](#section_uw7_zcp_7jb). |

## Resources syntax

```
"Resources": [
  {
    "ResourceId": String,
    "ResourceType": String
  }
]
```

## Resources properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ResourceId|String|Yes|No|The ID of the shared resource.|Sample value: `vsw-bp183p93qs667muql****`.|
|ResourceType|String|Yes|No|The type of the shared resource.|Set the value to VSwitch.|

## Response parameters

Fn::GetAtt

ResourceShareId: the ID of the resource share.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "ResourceShareName": {
      "Type": "String",
      "Description": "The name of the resource share.\nThe name must be 1 to 50 characters in length.\nIt can contain letters, digits, periods (.), underscores (_), and hyphens (-).",
      "AllowedPattern": "[-a-zA-Z0-9_\\.]{1,50}"
    },
    "Targets": {
      "Type": "Json",
      "Description": "The shared target.\nA shared target shares the resources of resource owners. You can share your resources\nonly with the member accounts in your resource directory. A shared target is indicated\nby its account ID. For more information about how to obtain the ID, see View the basic information of a member account.",
      "MaxLength": 5
    },
    "Resources": {
      "Type": "Json",
      "Description": "",
      "MaxLength": 5
    }
  },
  "Resources": {
    "ResourceShare": {
      "Type": "ALIYUN::ResourceManager::ResourceShare",
      "Properties": {
        "ResourceShareName": {
          "Ref": "ResourceShareName"
        },
        "Targets": {
          "Ref": "Targets"
        },
        "Resources": {
          "Ref": "Resources"
        }
      }
    }
  },
  "Outputs": {
    "ResourceShareId": {
      "Description": "The ID of the resource share.",
      "Value": {
        "Fn::GetAtt": [
          "ResourceShare",
          "ResourceShareId"
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
  ResourceShareName:
    AllowedPattern: '[-a-zA-Z0-9_\.]{1,50}'
    Description: 'The name of the resource share.

      The name must be 1 to 50 characters in length.

      It can contain letters, digits, periods (.), underscores (_), and hyphens (-).'
    Type: String
  Resources:
    Description: ''
    MaxLength: 5
    Type: Json
  Targets:
    Description: 'The shared target.

      A shared target shares the resources of resource owners. You can share your
      resources

      only with the member accounts in your resource directory. A shared target is
      indicated

      by its account ID. For more information about how to obtain the ID, see View
      the basic information of a member account.'
    MaxLength: 5
    Type: Json
Resources:
  ResourceShare:
    Properties:
      ResourceShareName:
        Ref: ResourceShareName
      Resources:
        Ref: Resources
      Targets:
        Ref: Targets
    Type: ALIYUN::ResourceManager::ResourceShare
Outputs:
  ResourceShareId:
    Description: The ID of the resource share.
    Value:
      Fn::GetAtt:
      - ResourceShare
      - ResourceShareId
```

