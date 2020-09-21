# ALIYUN::SLS::Logstore

ALIYUN::SLS::Logstore is used to create a Logstore in a Log Service project.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ProjectName|String|Yes|No|The name of the Log Service project.|-   The name must be 3 to 36 characters in length.
-   It can contain lowercase letters, digits, hyphens \(-\), and underscores \(\_\).
-   It must start and end with a lowercase letter or digit. |
|ShardCount|Integer|No|Yes|The number of shards.|Valid values: 1 to 100.

 Default value: 2.

  |
|MaxSplitShard|Integer|No|Yes|The maximum number of shards during automatic splitting.|Valid values: 1 to 64. This parameter is required when the AutoSplit parameter is set to true. |
|LogstoreName|String|Yes|No|The name of the Logstore.|The name must be unique in a project. -   The name must be 3 to 36 characters in length.
-   It can contain lowercase letters, digits, hyphens \(-\), and underscores \(\_\).
-   It must start and end with a lowercase letter or digit. |
|AutoSplit|Boolean|No|Yes|Specifies whether to automatically split shards.|Valid values: -   true
-   false

 Default value: false. |
|TTL|Integer|No|Yes|The data retention period.|Valid values: 1 to 3600. Default value: 30.

 Unit: days. |
|EnableTracking|Boolean|No|Yes|Specifies whether to enable WebTracking.|WebTracking can collect access information about web browsers, iOS applications, and Android applications.

 Valid values: -   true
-   false

 Default value: false. |
|PreserveStorage|Boolean|No|Yes|Specifies whether to permanently preserve logs.|Valid values: -   true
-   false

 Default value: false.

 If this parameter is set to true, the TTL parameter does not take effect. |
|AppendMeta|Boolean|No|Yes|Specifies whether to add the public IP address of the client and the log arrival time after the log is received.|Valid values: -   true
-   false

 Default value: false. |

## Response parameters

Fn::GetAtt

LogstoreName: the name of the Logstore.

## Examples

`JSON` format

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

`YAML` format

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

