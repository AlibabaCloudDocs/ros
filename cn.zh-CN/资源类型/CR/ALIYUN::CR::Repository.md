# ALIYUN::CR::Repository

ALIYUN::CR::Repository类型用于创建一个新的镜像仓库。

## 语法

```
{
  "Type": "ALIYUN::CR::Repository",
  "Properties": {
    "RepoNamespace": String,
    "Summary": String,
    "RepoType": String,
    "Detail": String,
    "RepoName": String,
    "RepoSource": Map
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|RepoNamespace|String|是|否|镜像仓库命名空间。|无|
|Summary|String|是|是|镜像仓库摘要。|长度为1~100个字符。|
|RepoType|String|是|是|镜像仓库类型。|取值：-   PUBLIC：公有仓库。支持匿名下载。
-   PRIVATE：私有仓库。必须登录下载。 |
|Detail|String|否|是|镜像仓库详细描述。|支持MarkDown格式，长度不超过2000个字符。|
|RepoName|String|是|否|镜像仓库名称。|长度为2~64个字符，可包含小写英文字母、数字、半角句号（.）、短划线（-）和下划线（\_）。|
|RepoSource|Map|否|否|镜像仓库绑定的源代码仓库及构建设置。|更多信息，请参见[RepoSource属性](#section_o7r_vke_vmg)。|

## RepoSource语法

```
"RepoSource": {
  "SourceRepoNamespace": String,
  "SourceRepoName": String,
  "IsOversea": Boolean,
  "IsDisableCache": Boolean,
  "SourceRepoType": String,
  "IsAutoBuild": Boolean
}
```

## RepoSource属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|SourceRepoNamespace|String|是|否|源代码仓库命名空间。|无|
|SourceRepoName|String|是|否|源代码仓库名称。|无|
|IsOversea|Boolean|是|否|是否启用海外构建。|取值：-   true
-   false |
|IsDisableCache|Boolean|是|否|是否在构建时禁用Cache。|取值：-   true
-   false |
|SourceRepoType|String|是|否|源代码仓库类型。|取值：-   PUBLIC：公有仓库。
-   PRIVATE：私有仓库。 |
|IsAutoBuild|Boolean|是|否|是否开启自动构建。|取值：-   true
-   false |

## 返回值

Fn::GetAtt

RepoId：镜像仓库ID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "RepoNamespace": {
      "Type": "String",
      "Description": "the namespace the repo belongs to",
      "MinLength": 2,
      "MaxLength": 30
    },
    "RepoType": {
      "Type": "String",
      "Description": "repository visibility, public or private",
      "AllowedValues": [
        "PUBLIC",
        "PRIVATE"
      ]
    },
    "RepoName": {
      "Type": "String",
      "Description": "the name of the repo",
      "MinLength": 1,
      "MaxLength": 64
    },
    "Summary": {
      "Type": "String",
      "Description": "description or something alike",
      "MinLength": 1,
      "MaxLength": 100
    },
    "Detail": {
      "Type": "String",
      "Description": "detailed configuration in markdown format",
      "MaxLength": 2000
    },
    "RepoSource": {
      "Type": "Json",
      "Description": "Code Source message. "
    }
  },
  "Resources": {
    "Repository": {
      "Type": "ALIYUN::CR::Repository",
      "Properties": {
        "RepoNamespace": {
          "Ref": "RepoNamespace"
        },
        "RepoType": {
          "Ref": "RepoType"
        },
        "RepoName": {
          "Ref": "RepoName"
        },
        "Summary": {
          "Ref": "Summary"
        },
        "Detail": {
          "Ref": "Detail"
        },
        "RepoSource": {
          "Ref": "RepoSource"
        }
      }
    }
  },
  "Outputs": {
    "RepoId": {
      "Description": "The repo id",
      "Value": {
        "Fn::GetAtt": [
          "Repository",
          "RepoId"
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
  Detail:
    Description: detailed configuration in markdown format
    MaxLength: 2000
    Type: String
  RepoName:
    Description: the name of the repo
    MaxLength: 64
    MinLength: 1
    Type: String
  RepoNamespace:
    Description: the namespace the repo belongs to
    MaxLength: 30
    MinLength: 2
    Type: String
  RepoSource:
    Description: 'Code Source message. '
    Type: Json
  RepoType:
    AllowedValues:
    - PUBLIC
    - PRIVATE
    Description: repository visibility, public or private
    Type: String
  Summary:
    Description: description or something alike
    MaxLength: 100
    MinLength: 1
    Type: String
Resources:
  Repository:
    Properties:
      Detail:
        Ref: Detail
      RepoName:
        Ref: RepoName
      RepoNamespace:
        Ref: RepoNamespace
      RepoSource:
        Ref: RepoSource
      RepoType:
        Ref: RepoType
      Summary:
        Ref: Summary
    Type: ALIYUN::CR::Repository
Outputs:
  RepoId:
    Description: The repo id
    Value:
      Fn::GetAtt:
      - Repository
      - RepoId
```

更多示例，请参见：[JSON示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/CR/JSON/Repository.json)和[YAML示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/CR/YAML/Repository.yml)。

