# Aliyun::Serverless::Log::Logstore

Aliyun::Serverless::Log::Logstore is used to create a Logstore in a Log Service project.

## Syntax

```
{
  "Type": "Aliyun::Serverless::Log::Logstore",
  "Properties": {
    "TTL": Integer,
    "ShardCount": Integer
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|TTL|Number|No|Yes|The time to live \(TTL\) of log data.|Valid values: 1 to 3600.Unit: days.

Default value: 30.|
|ShardCount|Number|No|Yes|The number of the shards.|Valid values: 1 to 100.|

## Response parameters

Fn::GetAtt

Name: the name of the project.

## Examples

`JSON` format

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Transform": "Aliyun::Serverless-2018-04-03",
  "Parameters": {
    "TTL": {
      "Type": "Number",
      "Default": 10
    },
    "ShardCount": {
      "Type": "Number",
      "Default": 1
    }
  },
  "Resources": {
    "SlsProject": {
      "Type": "Aliyun::Serverless::Log",
      "Properties": {
        "Description": "just test log"
      },
      "SlsLogstore": {
        "Type": "Aliyun::Serverless::Log::Logstore",
        "Properties": {
          "TTL": {
            "Ref": "TTL"
          },
          "ShardCount": {
            "Ref": "ShardCount"
          }
        }
      }
    }
  },
  "Outputs": {
    "LogstoreName": {
      "Value": {
        "Fn::GetAtt": [
          "SlsProjectSlsLogstore",
          "LogstoreName"
        ]
      }
    }
  }
}
```

`YAML` format

```
ROSTemplateFormatVersion: '2015-09-01'
Transform: 'Aliyun::Serverless-2018-04-03'
Parameters:
  TTL:
    Type: Number
    Default: 10
  ShardCount:
    Type: Number
    Default: 1
Resources:
  SlsProject:
    Type: 'Aliyun::Serverless::Log'
    Properties:
      Description: just test log
    SlsLogstore:
      Type: 'Aliyun::Serverless::Log::Logstore'
      Properties:
        TTL:
          Ref: TTL
        ShardCount:
          Ref: ShardCount
Outputs:
  LogstoreName:
    Value:
      'Fn::GetAtt':
        - SlsProjectSlsLogstore
        - LogstoreName
```

