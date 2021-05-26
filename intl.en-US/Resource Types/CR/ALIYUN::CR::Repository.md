# ALIYUN::CR::Repository

ALIYUN::CR::Repository is used to create an image repository.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|RepoNamespace|String|Yes|No|The namespace to which the image repository belongs.|None|
|Summary|String|Yes|Yes|The summary of the image repository.|The summary must be 1 to 100 characters in length.|
|RepoType|String|Yes|Yes|The type of the image repository.|Valid values:-   PUBLIC: Public image repositories support anonymous downloads.
-   PRIVATE: Private image repositories require logon to download. |
|Detail|String|No|Yes|The description of the image repository.|The Markdown syntax is supported. The description can be up to 2,000 characters in length.|
|RepoName|String|Yes|No|The name of the image repository.|The name must be 2 to 64 characters in length and can contain lowercase letters, digits, periods \(.\), hyphens \(-\), and underscores \(\_\).|
|RepoSource|Map|No|No|The source code repository and image build settings of the image repository.|For more information, see [RepoSource properties](#section_o7r_vke_vmg).|

## RepoSource syntax

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

## RepoSource properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|SourceRepoNamespace|String|Yes|No|The namespace to which the source code repository belongs.|None|
|SourceRepoName|String|Yes|No|The name of the source code repository.|None|
|IsOversea|Boolean|Yes|No|Specifies whether to enable image build in machines that are located in regions outside China.|Valid values:-   true
-   false |
|IsDisableCache|Boolean|Yes|No|Specifies whether to disable cache for image build.|Valid values:-   true
-   false |
|SourceRepoType|String|Yes|No|The type of source code repository.|Valid values:-   PUBLIC
-   PRIVATE |
|IsAutoBuild|Boolean|Yes|No|Specifies whether to enable automatic image build.|Valid values:-   true
-   false |

## Response parameters

Fn::GetAtt

RepoId: the ID of the image repository.

## Examples

`JSON` format

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

`YAML` format

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

For more examples, visit [Repository.json](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/CR/JSON/Repository.json) and [Repository.yml](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/CR/YAML/Repository.yml).

