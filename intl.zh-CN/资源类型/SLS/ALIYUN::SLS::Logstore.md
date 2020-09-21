# ALIYUN::SLS::Logstore

ALIYUN::SLS::Logstore类型用于在日志项目下创建日志库。

## 语法

```
{
  "Type": "ALIYUN::SLS::Logstore",
  "Properties": {
    "ProjectName": String,
    "ShardCount": Integer,
    "AutoSplit": Boolean,
    "MaxSplitShard": Integer,
    "LogstoreName": String,
    "AppendMeta": Boolean,
    "TTL": Integer,
    "EnableTracking": Boolean,
    "PreserveStorage": Boolean
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ProjectName|String|是|否|要创建的日志库所属日志项目的名字。|-   长度为3~36个字符。
-   支持小写字母、数字、连字符（-）、下划线（\_）。
-   必须以小写字母或数字开头和结尾。 |
|ShardCount|Integer|否|是|分区个数。|取值范围：1~100。

 默认值：2。

 单位：个。 |
|MaxSplitShard|Integer|否|是|自动分裂时，分裂出最大的分区个数 。|取值范围：1~64。 当autoSplit为true时，必须指定该参数。 |
|LogstoreName|String|是|否|日志库的名称。|在一个日志项目中，日志库的名称必须具有唯一性。 -   长度为3~36个字符。
-   支持小写字母、数字、连字符（-）、下划线（\_）。
-   必须以小写字母或数字开头和结尾。 |
|AutoSplit|Boolean|否|是|是否自动分裂分区。|取值范围： -   true
-   false

 默认值：false。 |
|TTL|Integer|否|是|数据的保存时间。|取值范围：1~3600。 默认值：30。

 单位：天。 |
|EnableTracking|Boolean|否|是|是否开启WebTracking采集信息。|支持采集各种浏览器以及iOS/Android APP的信息。

 取值范围： -   true
-   false

 默认值：false。 |
|PreserveStorage|Boolean|否|是|是否永久保存日志。|取值范围： -   true
-   false

 默认值：false。

 如果取值为true，则TTL的设置不生效。 |
|AppendMeta|Boolean|否|是|接收日志后，自动添加客户端外网IP和日志到达时间。|取值范围： -   true
-   false

 默认值：false。 |

## 返回值

Fn::GetAtt

LogstoreName：日志库名称。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "Logstore": {
      "Type": "ALIYUN::SLS::Logstore",
      "Properties": {
        "ProjectName": {
          "Ref": "ProjectName"
        },
        "TTL": {
          "Ref": "TTL"
        },
        "AutoSplit": {
          "Ref": "AutoSplit"
        },
        "MaxSplitShard": {
          "Ref": "MaxSplitShard"
        },
        "LogstoreName": {
          "Ref": "LogstoreName"
        },
        "AppendMeta": {
          "Ref": "AppendMeta"
        },
        "ShardCount": {
          "Ref": "ShardCount"
        },
        "EnableTracking": {
          "Ref": "EnableTracking"
        },
        "PreserveStorage": {
          "Ref": "PreserveStorage"
        }
      }
    }
  },
  "Parameters": {
    "ProjectName": {
      "MinLength": 3,
      "Type": "String",
      "Description": "Project name: 1. Only supports lowercase letters, numbers, hyphens (-) and underscores (_). 2. Must start and end with lowercase letters and numbers. 3. The name length is 3-63 characters.",
      "MaxLength": 63
    },
    "TTL": {
      "Default": 30,
      "Type": "Number",
      "Description": "The lifecycle of log in the logstore in days. Allowed Values: 1-3600, default to 30.",
      "MaxValue": 3600,
      "MinValue": 1
    },
    "AutoSplit": {
      "Default": false,
      "Type": "Boolean",
      "Description": "Whether to automatically split the shard. Default to false.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "MaxSplitShard": {
      "Type": "Number",
      "Description": "The maximum number of shards when splitting automatically. Must be specified if AutoSplit is set to true. Allowed Values: 1-64.",
      "MaxValue": 64,
      "MinValue": 1
    },
    "LogstoreName": {
      "MinLength": 3,
      "Type": "String",
      "Description": "Logstore name: 1. Only supports lowercase letters, numbers, hyphens (-) and underscores (_). 2. Must start and end with lowercase letters and numbers. 3. The name length is 3-63 characters.",
      "MaxLength": 63
    },
    "AppendMeta": {
      "Default": false,
      "Type": "Boolean",
      "Description": "Whether to add client external network IP and log arrival time after receiving the log. Default to false.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "ShardCount": {
      "Default": 2,
      "Type": "Number",
      "Description": "The number of Shards. Allowed Values: 1-100, default to 2.",
      "MaxValue": 100,
      "MinValue": 1
    },
    "EnableTracking": {
      "Default": false,
      "Type": "Boolean",
      "Description": "Whether to enable WebTracking, which supports fast capture of various browsers and iOS/Android/APP access information. Default to false.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "PreserveStorage": {
      "Default": false,
      "Type": "Boolean",
      "Description": "Whether to keep the log permanently. If set to true, TTL will be ignored. Default to false.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    }
  }
}
```

`YAML`格式

```
ROSTemplateFormatVersion: '2015-09-01'
Resources:
  Logstore:
    Type: ALIYUN::SLS::Logstore
    Properties:
      ProjectName:
        Ref: ProjectName
      TTL:
        Ref: TTL
      AutoSplit:
        Ref: AutoSplit
      MaxSplitShard:
        Ref: MaxSplitShard
      LogstoreName:
        Ref: LogstoreName
      AppendMeta:
        Ref: AppendMeta
      ShardCount:
        Ref: ShardCount
      EnableTracking:
        Ref: EnableTracking
      PreserveStorage:
        Ref: PreserveStorage
Parameters:
  ProjectName:
    MinLength: 3
    Type: String
    Description: Project name: 1. Only supports lowercase letters, numbers, hyphens
      (-) and underscores (_). 2. Must start and end with lowercase letters and numbers. 3.
      The name length is 3-63 characters.
    MaxLength: 63
  TTL:
    Default: 30
    Type: Number
    Description: 'The lifecycle of log in the logstore in days. Allowed Values: 1-3600,
      default to 30.'
    MaxValue: 3600
    MinValue: 1
  AutoSplit:
    Default: false
    Type: Boolean
    Description: Whether to automatically split the shard.Default to false.
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
  MaxSplitShard:
    Type: Number
    Description: 'The maximum number of shards when splitting automatically. Must
      be specified if AutoSplit is set to true. Allowed Values: 1-64.'
    MaxValue: 64
    MinValue: 1
  LogstoreName:
    MinLength: 3
    Type: String
    Description: Logstore name: 1. Only supports lowercase letters, numbers, hyphens
      (-) and underscores (_). 2. Must start and end with lowercase letters and numbers. 3. 
      The name length is 3-63 characters.
    MaxLength: 63
  AppendMeta:
    Default: false
    Type: Boolean
    Description: Whether to add client external network IP and log arrival time after
      receiving the log. Default to false.
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
  ShardCount:
    Default: 2
    Type: Number
    Description: 'The number of Shards. Allowed Values: 1-100, default to 2.'
    MaxValue: 100
    MinValue: 1
  EnableTracking:
    Default: false
    Type: Boolean
    Description: Whether to enable WebTracking, which supports fast capture of various
      browsers and iOS/Android/APP access information. Default to false.
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
  PreserveStorage:
    Default: false
    Type: Boolean
    Description: Whether to keep the log permanently. If set to true, TTL will be ignored. Default
      to false.
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
			
```

