# ALIYUN::CR::Repository

ALIYUN::CR::Repository类型用于创建一个新的仓库。

## 语法

```
{
  "Type": "ALIYUN::CR::Repository",
  "Properties": {
    "RepoNamespace": String,
    "Summary": String,
    "RepoType": String,
    "Detail": String,
    "RepoName": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|RepoNamespace|String|是|否|命名空间|无|
|Summary|String|是|是|摘要|长度为1~100个字符。|
|RepoType|String|是|是|公有仓库支持匿名下载，私有仓库必须登录下载。|取值： -   PUBLIC
-   PRIVATE |
|Detail|String|否|是|描述详情|支持MarkDown格式，长度不超过2000个字符。|
|RepoName|String|是|否|仓库名称|长度为2~64个字符，可包含小写英文字符、数字、英文句点（.）、短划线（-）和下划线（\_）。|

## 返回值

Fn::GetAtt

RepoId：仓库ID。

## 示例

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "Repository": {
      "Type": "ALIYUN::CR::Repository",
      "Properties": {
        "RepoType": {
          "Ref": "RepoType"
        },
        "RepoNamespace": {
          "Ref": "RepoNamespace"
        },
        "Detail": {
          "Ref": "Detail"
        },
        "RepoName": {
          "Ref": "RepoName"
        },
        "Summary": {
          "Ref": "Summary"
        }
      }
    }
  },
  "Parameters": {
    "RepoType": {
      "Type": "String",
      "Description": "repository visibility, public or private",
      "AllowedValues": [
        "PUBLIC",
        "PRIVATE"
      ]
    },
    "RepoNamespace": {
      "MinLength": 2,
      "Type": "String",
      "Description": "the namespace the repo belongs to",
      "MaxLength": 30
    },
    "Detail": {
      "Type": "String",
      "Description": "detailed configuration in markdown format",
      "MaxLength": 2000
    },
    "RepoName": {
      "MinLength": 1,
      "Type": "String",
      "Description": "the name of the repo",
      "MaxLength": 64
    },
    "Summary": {
      "MinLength": 1,
      "Type": "String",
      "Description": "description or something alike",
      "MaxLength": 100
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

