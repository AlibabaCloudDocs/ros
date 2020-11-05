# ALIYUN::SLS::Savedsearch

ALIYUN::SLS::Savedsearch类型用于将查询结果保存为快速查询。

## 语法

```
{
  "Type": "ALIYUN::SLS::Savedsearch",
  "Properties": {
    "Project": String,
    "Detail": Map
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Project|String|是|否|日志项目名称|无|
|Detail|Map|是|是|查询详情|更多信息，请参见[Detail属性](#section_q8b_7zx_l47)。|

## Detail语法

```
"Detail": {
  "SearchQuery": String,
  "Logstore": String,
  "DisplayName": String,
  "SavedsearchName": String,
  "Topic": String
}
```

## Detail属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|SearchQuery|String|是|是|查询语句|无|
|Logstore|String|是|是|日志库|无|
|DisplayName|String|否|是|快速查询名称|长度为1~63个字符。|
|SavedsearchName|String|是|否|保存的查询名称|无|
|Topic|String|是|是|日志主题|无|

## 返回值

Fn::GetAtt

SavedsearchName：保存的查询名称

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Project": {
      "Type": "String",
      "Description": "Project name"
    },
    "Detail": {
      "Type": "Json",
      "Description": ""
    }
  },
  "Resources": {
    "SavedSearch": {
      "Type": "ALIYUN::SLS::Savedsearch",
      "Properties": {
        "Project": {
          "Ref": "Project"
        },
        "Detail": {
          "Ref": "Detail"
        }
      }
    }
  },
  "Outputs": {
    "SavedsearchName": {
      "Description": "Savedsearch name.",
      "Value": {
        "Fn::GetAtt": [
          "SavedSearch",
          "SavedsearchName"
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
  Project:
    Type: String
    Description: Project name
  Detail:
    Type: Json
    Description: ''
Resources:
  SavedSearch:
    Type: 'ALIYUN::SLS::Savedsearch'
    Properties:
      Project:
        Ref: Project
      Detail:
        Ref: Detail
Outputs:
  SavedsearchName:
    Description: Savedsearch name.
    Value:
      'Fn::GetAtt':
        - SavedSearch
        - SavedsearchName
```

