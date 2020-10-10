# ALIYUN::DATAHUB::Topic

ALIYUN::DATAHUB::Topic类型用于创建Topic。

阿里云支持在以下地域创建Topic：

-   中国（杭州）
-   中国（上海）
-   中国（北京）
-   中国（张家口）
-   中国（深圳）
-   新加坡
-   马来西亚（吉隆坡）
-   德国（法兰克福）
-   印度（孟买）

## 语法

```
{
  "Type": "ALIYUN::DATAHUB::Topic",
  "Properties": {
    "Comment": String,
    "RecordType": String,
    "ProjectName": String,
    "RecordSchema": String,
    "TopicName": String,
    "ShardCount": Integer,
    "Lifecycle": Integer
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Comment|String|是|否|描述信息|长度为3~1024个字符。|
|RecordType|String|是|否|类型|取值： -   TUPLE：结构化数据
-   BLOB：非结构化数据 |
|ProjectName|String|是|否|项目名称|无|
|RecordSchema|String|否|否|Schema详情|创建TUPLE类型Topic时指定该参数，创建BLOB类型时不指定。|
|TopicName|String|是|否|Topic名称|长度为3~64个字符，以英文字母开头，可包含数字、英文字母（区分大小写）和下划线（\_）。|
|ShardCount|Integer|否|否|初始Shard数目|无|
|Lifecycle|Integer|否|否|数据存储生命周期|无|

## 返回值

Fn::GetAtt

-   ProjectName：项目名称。
-   TopicName：Topic名称。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "Topic": {
      "Type": "ALIYUN::DATAHUB::Topic",
      "Properties": {
        "Comment": {
          "Ref": "Comment"
        },
        "RecordType": {
          "Ref": "RecordType"
        },
        "ProjectName": {
          "Ref": "ProjectName"
        },
        "RecordSchema": {
          "Ref": "RecordSchema"
        },
        "Lifecycle": {
          "Ref": "Lifecycle"
        },
        "ShardCount": {
          "Ref": "ShardCount"
        },
        "TopicName": {
          "Ref": "TopicName"
        }
      }
    }
  },
  "Parameters": {
    "Comment": {
      "Type": "String",
      "Description": "The comment of topic."
    },
    "RecordType": {
      "Type": "String",
      "Description": "Record type. TUPLE: structured data, BLOB: unstructured data.",
      "AllowedValues": [
        "TUPLE",
        "BLOB"
      ]
    },
    "ProjectName": {
      "MinLength": 3,
      "Type": "String",
      "Description": "The name of the project. Length [3, 32]. Beginning with characters, only characters, numbers and _ are allowed.",
      "MaxLength": 32
    },
    "RecordSchema": {
      "Type": "String",
      "Description": "When creating a TUPLE type topic, you need to specify the schema, but the BLOB type does not pass this parameter."
    },
    "Lifecycle": {
      "Default": 3,
      "Type": "Number",
      "Description": "Data storage life cycle.",
      "MinValue": 1
    },
    "ShardCount": {
      "Default": 1,
      "Type": "Number",
      "Description": "Initial shard number.",
      "MinValue": 1
    },
    "TopicName": {
      "MinLength": 3,
      "Type": "String",
      "Description": "The name of the topic. Length [3, 64]. Beginning with characters, only characters, numbers and _ are allowed.",
      "MaxLength": 64
    }
  },
  "Outputs": {
    "ProjectName": {
      "Description": "Project name",
      "Value": {
        "Fn::GetAtt": [
          "Topic",
          "ProjectName"
        ]
      }
    },
    "TopicName": {
      "Description": "Topic name",
      "Value": {
        "Fn::GetAtt": [
          "Topic",
          "TopicName"
        ]
      }
    }
  }
}
```

`YAML`格式

```
ROSTemplateFormatVersion: '2015-09-01'
Resources:
  Topic:
    Type: 'ALIYUN::DATAHUB::Topic'
    Properties:
      Comment:
        Ref: Comment
      RecordType:
        Ref: RecordType
      ProjectName:
        Ref: ProjectName
      RecordSchema:
        Ref: RecordSchema
      Lifecycle:
        Ref: Lifecycle
      ShardCount:
        Ref: ShardCount
      TopicName:
        Ref: TopicName
Parameters:
  Comment:
    Type: String
    Description: The comment of topic.
  RecordType:
    Type: String
    Description: 'Record type. TUPLE: structured data, BLOB: unstructured data.'
    AllowedValues:
      - TUPLE
      - BLOB
  ProjectName:
    MinLength: 3
    Type: String
    Description: >-
      The name of the project. Length [3, 32]. Beginning with characters, only
      characters, numbers and _ are allowed.
    MaxLength: 32
  RecordSchema:
    Type: String
    Description: >-
      When creating a TUPLE type topic, you need to specify the schema, but the
      BLOB type does not pass this parameter.
  Lifecycle:
    Default: 3
    Type: Number
    Description: Data storage life cycle.
    MinValue: 1
  ShardCount:
    Default: 1
    Type: Number
    Description: Initial shard number.
    MinValue: 1
  TopicName:
    MinLength: 3
    Type: String
    Description: >-
      The name of the topic. Length [3, 64]. Beginning with characters, only
      characters, numbers and _ are allowed.
    MaxLength: 64
Outputs:
  ProjectName:
    Description: Project name
    Value:
      'Fn::GetAtt':
        - Topic
        - ProjectName
  TopicName:
    Description: Topic name
    Value:
      'Fn::GetAtt':
        - Topic
        - TopicName
```

