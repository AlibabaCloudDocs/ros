# ALIYUN::SLS::Project

ALIYUN::SLS::Project is used to create a Log Service project.

## Syntax

```
{
  "Type": "ALIYUN::SLS::Project",
  "Properties": {
    "Name": String,
    "Description": String,
    "Tags": List
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Name|String|Yes|No|The name of the project.|The name must be 3 to 36 characters in length and can contain lowercase letters, digits, and hyphens \(-\). It must start and end with a lowercase letter or digit.|
|Description|String|No|No|The description of the project.|The description can be up to 64 characters in length and cannot contain the following special characters: `< > ' \ "`.|
|Tags|List|No|No|The list of one or more tags of the project.|A maximum of 20 tags can be specified. For more information, see [Tags properties](#section_n16_q4m_ulw). |

## Tags syntax

```
"Tags": [
  {
    "Key": String,
    "Value": String
  }
]  
```

## Tags properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Key|String|Yes|No|The key of the tag.|The tag key must be 1 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|
|Value|String|No|No|The value of the tag.|The tag value must be 0 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|

## Response parameters

Fn::GetAtt

Name: The name of the Log Service project.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Description": {
      "Type": "String",
      "Description": "Project description: <>'\"\\ is not supported, up to 64 characters.",
      "MaxLength": 64
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to project. Max support 20 tags to add during create project. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
    },
    "Name": {
      "Type": "String",
      "Description": "Project name:\n1. Only supports lowercase letters, numbers, hyphens (-) and underscores (_).\n2. Must start and end with lowercase letters and numbers.\n3. The name length is 3-63 characters.",
      "AllowedPattern": "^[a-zA-Z0-9_-]+$",
      "MinLength": 3,
      "MaxLength": 63
    }
  },
  "Resources": {
    "Project": {
      "Type": "ALIYUN::SLS::Project",
      "Properties": {
        "Description": {
          "Ref": "Description"
        },
        "Tags": {
          "Ref": "Tags"
        },
        "Name": {
          "Ref": "Name"
        }
      }
    }
  },
  "Outputs": {
    "Name": {
      "Description": "Project name.",
      "Value": {
        "Fn::GetAtt": [
          "Project",
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
  Description:
    Type: String
    Description: 'Project description: <>''"\ is not supported, up to 64 characters.'
    MaxLength: 64
  Tags:
    Type: Json
    Description: >-
      Tags to attach to project. Max support 20 tags to add during create
      project. Each tag with two properties Key and Value, and Key is required.
    MaxLength: 20
  Name:
    Type: String
    Description: >-
      Project name:

      1. Only supports lowercase letters, numbers, hyphens (-) and underscores
      (_).

      2. Must start and end with lowercase letters and numbers.

      3. The name length is 3-63 characters.
    AllowedPattern: '^[a-zA-Z0-9_-]+$'
    MinLength: 3
    MaxLength: 63
Resources:
  Project:
    Type: 'ALIYUN::SLS::Project'
    Properties:
      Description:
        Ref: Description
      Tags:
        Ref: Tags
      Name:
        Ref: Name
Outputs:
  Name:
    Description: Project name.
    Value:
      'Fn::GetAtt':
        - Project
        - Name
```

To view more examples, visit [SLS.json](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/SLS/JSON/SLS.json) and [SLS.yml](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/SLS/YAML/SLS.yml). The following resource types are involved in these examples:

-   ALIYUN::SLS::Project
-   ALIYUN::SLS::Logstore
-   ALIYUN::SLS::Index
-   ALIYUN::SLS::LogtailConfig
-   ALIYUN::SLS::MachineGroup
-   ALIYUN::SLS::ApplyConfigToMachineGroup
-   ALIYUN::ApiGateway::LogConfig
-   ALIYUN::SLS::Savedsearch
-   ALIYUN::SLS::Alert

