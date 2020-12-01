# Aliyun::Serverless::Log::Logstore

Aliyun::Serverless::Log::Logstore类型用于在日志项目下创建日志库。

## 语法

```
{
  "Type": "Aliyun::Serverless::Log::Logstore",
  "Properties": {
    "TTL": Integer,
    "ShardCount": Integer
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|TTL|Number|否|是|数据的保存时间。|取值范围： 1~3600。单位：天。

默认值：30。|
|ShardCount|Number|否|是|分区个数。|取值范围： 1~100。|

## 返回值

Fn::GetAtt

Name: 日志项目名称。

## 示例

`JSON`格式

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

`YAML`格式

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

