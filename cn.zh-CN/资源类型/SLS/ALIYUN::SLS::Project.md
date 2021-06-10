# ALIYUN::SLS::Project

ALIYUN::SLS::Project类型用于创建一个日志项目。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Name|String|是|否|日志项目的名称。|长度为3~36个字符。必须以小写英文字母或数字开头和结尾。可包含小写英文字母、数字和短划线（-）。|
|Description|String|否|否|日志项目的描述。|长度不超过64个字符。不支持特殊字符`<>'\"`。|
|Tags|List|否|否|标签。|最多支持20个标签。更多信息，请参见[Tags属性](#section_n16_q4m_ulw)。 |

## Tags语法

```
"Tags": [
  {
    "Key": String,
    "Value": String
  }
]  
```

## Tags属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Key|String|是|否|标签键。|长度为1~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或`https://` 。|
|Value|String|否|否|标签值。|长度为0~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或`https://` 。|

## 返回值

Fn::GetAtt

Name: 日志项目名称。

## 示例

`JSON`格式

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

`YAML`格式

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

更多示例，请参见[JSON示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/SLS/JSON/SLS.json)和[YAML示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/SLS/YAML/SLS.yml)。示例可实现以下功能：

-   创建日志项目
-   在日志项目下创建日志库
-   为指定的Logstore创建索引
-   配置采集数据时的Logtail参数
-   创建日志服务机器组
-   将日志服务的日志配置应用于机器组
-   创建日志配置
-   将查询结果保存为快速查询
-   创建告警

