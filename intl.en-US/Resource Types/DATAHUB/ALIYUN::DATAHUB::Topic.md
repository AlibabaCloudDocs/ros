# ALIYUN::DATAHUB::Topic

ALIYUN::DATAHUB::Topic is used to create topics.

Alibaba Cloud allows you to create topics in the following regions:

-   China \(Hangzhou\)
-   China \(Shanghai\)
-   China \(Beijing\)
-   China \(Zhangjiakou-Beijing Winter Olympics\)
-   China \(Shenzhen\)
-   Singapore
-   Malaysia \(Kuala Lumpur\)
-   Germany \(Frankfurt\)
-   India \(Mumbai\)

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Comment|String|Yes|No|The description of the topic.|The description must be 3 to 1,024 characters in length.|
|RecordType|String|Yes|No|The type of the topic.|Valid values: -   TUPLE: structured data
-   BLOB: unstructured data |
|ProjectName|String|Yes|No|The name of the project.|None.|
|RecordSchema|String|No|No|The details of the schema.|You must specify this parameter when you create a topic of the TUPLE type. Do not specify this parameter when you create a topic of the BLOB type.|
|TopicName|String|Yes|No|The name of the topic.|The name must be 3 to 64 characters in length and can contain letters, digits, and underscores \(\_\). It is case-sensitive and must start with a letter.|
|ShardCount|Integer|No|No|The initial number of shards.|None.|
|Lifecycle|Integer|No|No|The lifecycle of data storage.|None.|

## Response parameters

Fn::GetAtt

-   ProjectName: the name of the project.
-   TopicName: the name of the topic.

## Examples

`JSON` format

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

`YAML` format

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

