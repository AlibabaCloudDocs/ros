# ALIYUN::ResourceManager::ResourceShare

ALIYUN::ResourceManager::ResourceShare类型用于创建共享单元。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ResourceShareName|String|是|是|共享单元名称。|长度为1~50个字符。可包含英文字母、数字、汉字、半角句号（.）、下划线（\_）和短划线（-）。|
|Targets|List|否|否|资源使用者。|资源共享的受益方，可以使用共享的资源，通常为资源目录内的成员账号UID。关于如何获取成员账号UID，请参见[查看成员详情]()。取值范围：1~5，即每次最多添加5个资源使用者。 |
|Resources|List|否|否|共享资源。|取值范围：1~5，即每次最多添加5个共享资源。更多信息，请参见[Resources属性](#section_uw7_zcp_7jb)。 |

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
|ResourceId|String|是|否|共享资源ID。|取值示例：`vsw-bp183p93qs667muql****`。|
|ResourceType|String|是|否|共享资源类型。|取值：VSwitch。|

## 返回值

Fn::GetAtt

ResourceShareId：共享单元ID。

## 示例

`JSON`格式

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

`YAML`格式

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

