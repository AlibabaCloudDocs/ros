# ALIYUN::SLS::Index

ALIYUN::SLS::Index类型用于为指定的日志库创建索引。

## 语法

```
{
  "Type": "ALIYUN::SLS::Index",
  "Properties": {
    "ProjectName": String,
    "FullTextIndex": Map,
    "LogstoreName": String,
    "KeyIndices": List,
    "LogReduce": Boolean
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ProjectName|String|是|否|日志项目名称。|长度为3~36个字符。必须以小写字母或数字开头和结尾，可包含小写字母、数字、短划线（-）和下划线（\_）。|
|FullTextIndex|Map|是|是|全文索引配置。|详情请参见[FullTextIndex属性](#section_i6q_ofb_6dk)。|
|LogstoreName|String|是|否|日志库名称。|无|
|KeyIndices|List|否|是|字段索引配置。|全文索引和字段索引至少配置一个。 详情请参见[属性](#section_1zx_gy0_w02)。 |
|LogReduce|Boolean|否|是|是否启用日志分割。|取值： -   true
-   false（默认值） |

## FullTextIndex语法

```
"FullTextIndex": {
  "CaseSensitive": Boolean,
  "Delimiter": String,
  "IncludeChinese": Boolean,
  "Enable": Boolean
}
```

## FullTextIndex属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Enable|Boolean|是|是|是否启用全文索引。|取值： -   true（默认值）
-   false |
|CaseSensitive|Boolean|否|是|是否区分大小写。|取值： -   true
-   false（默认值） |
|Delimiter|String|否|是|分词符。|支持以下特殊字符：```
,'";=()[]{}?@&<>/:\n\t\r
``` |
|IncludeChinese|Boolean|否|是|是否包含中文。|取值： -   true
-   false（默认值） |

## KeyIndices语法

```
"KeyIndices": [
  {
    "Name": String,
    "EnableAnalytics": Boolean,
    "Delimiter": String,
    "CaseSensitive": Boolean,
    "JsonKeyIndices": List,
    "Alias": String,
    "IncludeChinese": String,
    "Type": String
  }
]
```

## KeyIndices属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Name|String|是|是|字段名。|可以使用嵌套名，以英文句点（.）分隔，例如：k1.k2.k3。|
|EnableAnalytics|Boolean|否|是|该字段是否开启统计。|取值： -   true（默认值）
-   false |
|Delimiter|String|否|是|分词符。|支持以下特殊字符：```
,'";=()[]{}?@&<>/:\n\t\r
``` |
|CaseSensitive|Boolean|否|是|是否区分大小写。|取值： -   true
-   false（默认值）

只有当Type参数取值为text或json时该参数生效。|
|JsonKeyIndices|List|否|是|JSON索引配置。格式：`[{"key1": "value1", "key2": "value2", ...}]`。|支持的key为：Name、Alias、Type和EnableAnalytics。 详情请参见[JsonKeyIndices属性](#section_y1e_mtq_3xd)。 |
|Alias|String|否|是|字段别名。|无|
|IncludeChinese|Boolean|否|是|是否包含中文。|取值： -   true
-   false（默认值）

只有当Type参数取值为text时该参数生效。|
|Type|String|是|是|字段类型。|取值： -   text（默认值）
-   long
-   double
-   json |

## JsonKeyIndices语法

```
"JsonKeyIndices": [
  {
    "Type": String,
    "Alias": String,
    "EnableAnalytics": Boolean,
    "Name": String
  }
]  
```

## JsonKeyIndices属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Name|String|是|是|字段名。|无|
|EnableAnalytics|Boolean|否|是|是否支持查询分析。|取值： -   true
-   false |
|Alias|String|否|是|字段别名。|无|
|Type|String|是|是|字段类型。|无|

## 返回值

Fn::GetAtt

无。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "Index": {
      "Type": "ALIYUN::SLS::Index",
      "Properties": {
        "ProjectName": {
          "Ref": "ProjectName"
        },
        "FullTextIndex": {
          "Ref": "FullTextIndex"
        },
        "LogstoreName": {
          "Ref": "LogstoreName"
        },
        "KeyIndices": {
          "Ref": "KeyIndices"
        },
        "LogReduce": {
          "Ref": "LogReduce"
        }
      }
    }
  },
  "Parameters": {
    "ProjectName": {
      "Type": "String",
      "Description": "Project name:1. Only supports lowercase letters, numbers, hyphens (-) and underscores (_).2. Must start and end with lowercase letters and numbers.3. The name length is 3-63 characters.",
      "MinLength": 3,
      "MaxLength": 63
    },
    "FullTextIndex": {
      "Type": "Map",
      "Description": "Full-text indexing configuration.Full-text indexing and key indexing must have at least one enabled."
    },
    "LogstoreName": {
      "Type": "String",
      "Description": "Logstore name:1. Only supports lowercase letters, numbers, hyphens (-) and underscores (_).2. Must start and end with lowercase letters and numbers.3. The name length is 3-63 characters.",
      "MinLength": 3,
      "MaxLength": 63
    },
    "KeyIndices": {
      "Type": "List",
      "Description": "Key index configurations.Full-text indexing and key indexing must have at least one enabled."
    },
    "LogReduce": {
      "Default": false,
      "Type": "Boolean",
      "Description": "Whether to enable log reduce. Default to false.",
      "AllowedValues": [
        true,
        false
      ]
    }
  }
}
```

`YAML`格式

```
ROSTemplateFormatVersion: '2015-09-01'
Resources:
  Index:
    Type: ALIYUN::SLS::Index
    Properties:
      ProjectName:
        Ref: ProjectName
      FullTextIndex:
        Ref: FullTextIndex
      LogstoreName:
        Ref: LogstoreName
      KeyIndices:
        Ref: KeyIndices
      LogReduce:
        Ref: LogReduce
Parameters:
  ProjectName:
    MinLength: 3
    MaxLength: 63
    Type: String
    Description: Project name:1. Only supports lowercase letters, numbers, hyphens
      (-) and underscores (_).2. Must start and end with lowercase letters and numbers.3.
      The name length is 3-63 characters.
  FullTextIndex:
    Type: Map
    Description: Full-text indexing configuration.Full-text indexing and key indexing
      must have at least one enabled.
  LogstoreName:
    MinLength: 3
    MaxLength: 63
    Type: String
    Description: Logstore name:1. Only supports lowercase letters, numbers, hyphens
      (-) and underscores (_).2. Must start and end with lowercase letters and numbers.3.
      The name length is 3-63 characters.
  KeyIndices:
    Type: List
    Description: Key index configurations.Full-text indexing and key indexing must
      have at least one enabled.
  LogReduce:
    Default: false
    Type: Boolean
    Description: Whether to enable log reduce. Default to false.
    AllowedValues:
    - true
    - false
            
```

