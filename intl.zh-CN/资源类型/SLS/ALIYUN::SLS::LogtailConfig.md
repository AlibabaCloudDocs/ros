# ALIYUN::SLS::LogtailConfig

ALIYUN::SLS::LogtailConfig类型用于配置采集数据时的Logtail参数。

## 语法

```
{
  "Type": "ALIYUN::SLS::LogtailConfig",
  "Properties": {
    "ProjectName": String,
    "LogtailConfigName": String,
    "LogstoreName": String,
    "RawConfigData": Map,
    "CloneFrom": Map
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ProjectName|String|是|否|日志项目名称。|无|
|LogtailConfigName|String|是|否|Logtail配置名称。|同一项目下配置名称必须唯一。长度为2~128个字符。必须以小写英文字母或者数字开头和结尾。可包含小写英文字母、数字、短划线（-）和下划线（\_）。 |
|LogstoreName|String|是|否|日志库名称。|无|
|RawConfigData|Map|否|是|原始配置数据。|格式与SLS API [GetConfig](/intl.zh-CN/开发指南/API 参考/Logtail配置相关接口/GetConfig.md)的响应相同。如果同时指定CloneFrom和RawConfigData，LogtailConfig的数据将会和RawConfigData合并，RawConfigData中的configName、outputType和outputDetail会被忽略。

取值示例：`{"configName": "test-logtail-config", "createTime": 1574843554, "inputDetail": {"acceptNoEnoughKeys": false, "adjustTimezone": false, "advanced": { "force_multiconfig": false }, "autoExtend": true, "delayAlarmBytes": 0, "delaySkipBytes": 0, "discardNonUtf8": false, "discardUnmatch": false, "dockerExcludeEnv": {}, "dockerExcludeLabel": {}, "dockerFile": false, "dockerIncludeEnv": {}, "dockerIncludeLabel": {}, "enableRawLog": false, "enableTag": false, "fileEncoding": "utf8", "filePattern": "test.log*", "filterKey": [], "filterRegex": [], "key": [ "time", "logger", "level", "request_id", "user_id", "region_id", "content" ], "localStorage": true, "logPath": "/var/log/test", "logTimezone": "", "logType": "delimiter_log", "maxDepth": 100, "maxSendRate": -1, "mergeType": "topic", "preserve": true, "preserveDepth": 1, "priority": 0, "quote": "\u0001", "sendRateExpire": 0, "sensitive_keys": [], "separator": ",,,", "shardHashKey": [], "tailExisted": false, "timeFormat": "", "timeKey": "", "topicFormat": "none" }, "inputType": "file", "lastModifyTime": 1574843554, "logSample": "2019-11-27 10:48:23,160,,,MAIN,,,INFO,,,98DCC51D-BE5D-49C7-B3FD-37B2BAEFB296,,,123456789,,,cn-hangzhou,,,this is a simple test.", "outputDetail": { "endpoint": "cn-hangzhou-intranet.log.aliyuncs.com", "logstoreName": "test-logstore", "region": "cn-hangzhou"}, "outputType": "LogService"}`。 |
|CloneFrom|Map|否|是|克隆其他日志项目的LogtailConfig。|CloneFrom和LogtailConfig必须指定一个。更多信息，请参见[CloneFrom属性](#section_g99_de7_6lc)。 |

## CloneFrom语法

```
"CloneFrom": {
  "ProjectName": String,
  "LogtailConfigName": String
}
```

## CloneFrom属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ProjectName|String|是|是|日志项目名称。|无|
|LogtailConfigName|String|是|是|Logtail配置名称。|无|

## 返回值

Fn::GetAtt

-   Endpoint：Endpoint地址。
-   AppliedMachineGroups：日志采集配置的机器列表。
-   LogtailConfigName：Logtail配置名称。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "LogtailConfig": {
      "Type": "ALIYUN::SLS::LogtailConfig",
      "Properties": {
        "ProjectName": {
          "Ref": "ProjectName"
        },
        "LogtailConfigName": {
          "Ref": "LogtailConfigName"
        },
        "LogstoreName": {
          "Ref": "LogstoreName"
        },
        "RawConfigData": {
          "Ref": "RawConfigData"
        },
        "CloneFrom": {
          "Ref": "CloneFrom"
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
    "LogtailConfigName": {
      "MinLength": 3,
      "Type": "String",
      "Description": "Logtail config name: 1. Only supports lowercase letters, numbers, hyphens (-) and underscores (_). 2. Must start and end with lowercase letters and numbers. 3. The name length is 3-63 characters.",
      "MaxLength": 63
    },
    "LogstoreName": {
      "MinLength": 3,
      "Type": "String",
      "Description": "Logstore name: 1. Only supports lowercase letters, numbers, hyphens (-) and underscores (_). 2. Must start and end with lowercase letters and numbers. 3. The name length is 3-63 characters.",
      "MaxLength": 63
    },
    "RawConfigData": {
      "Type": "Json",
      "Description": "The format is the same as the response of SLS API GetConfig. Either CloneFrom or RawConfigData must be specified. If CloneFrom and RawConfigData are both specified, logtail config data will be merged from both with RawConfigData first. configName, outputType, outputDetail in data will be ignored.For example:\n{\"configName\": \"test-logtail-config\",\"createTime\": 1574843554,\"inputDetail\": { \"acceptNoEnoughKeys\": false, \"adjustTimezone\": false, \"advanced\": {   \"force_multiconfig\": false }, \"autoExtend\": true, \"delayAlarmBytes\": 0, \"delaySkipBytes\": 0, \"discardNonUtf8\": false, \"discardUnmatch\": false, \"dockerExcludeEnv\": {}, \"dockerExcludeLabel\": {}, \"dockerFile\": false, \"dockerIncludeEnv\": {}, \"dockerIncludeLabel\": {}, \"enableRawLog\": false, \"enableTag\": false, \"fileEncoding\": \"utf8\", \"filePattern\": \"test.log*\", \"filterKey\": [], \"filterRegex\": [], \"key\": [   \"time\",   \"logger\",   \"level\",   \"request_id\",   \"user_id\",   \"region_id\",   \"content\" ], \"localStorage\": true, \"logPath\": \"/var/log/test\", \"logTimezone\": \"\", \"logType\": \"delimiter_log\", \"maxDepth\": 100, \"maxSendRate\": -1, \"mergeType\": \"topic\", \"preserve\": true, \"preserveDepth\": 1, \"priority\": 0, \"quote\": \"\\u0001\", \"sendRateExpire\": 0, \"sensitive_keys\": [], \"separator\": \",,,\", \"shardHashKey\": [], \"tailExisted\": false, \"timeFormat\": \"\", \"timeKey\": \"\", \"topicFormat\": \"none\"}, \"inputType\": \"file\", \"lastModifyTime\": 1574843554, \"logSample\": \"2019-11-27 10:48:23,160,,,MAIN,,,INFO,,,98DCC51D-BE5D-49C7-B3FD-37B2BAEFB296,,,123456789,,,cn-hangzhou,,,this is a simple test.\", \"outputDetail\": {\"endpoint\": \"cn-hangzhou-intranet.log.aliyuncs.com\", \"logstoreName\": \"test-logstore\",\"region\": \"cn-hangzhou\"}, \"outputType\": \"LogService\"}"
    },
    "CloneFrom": {
      "Type": "Json",
      "Description": "Clone logtail config data from existing logtail config. Either CloneFrom or RawConfigData must be specified. If CloneFrom and RawConfigData are both specified, logtail config data will be merged from both with RawConfigData first."
    }
  },
  "Outputs": {
    "LogtailConfigName": {
      "Description": "Logtail config name.",
      "Value": {
        "Fn::GetAtt": [
          "LogtailConfig",
          "LogtailConfigName"
        ]
      }
    },
    "Endpoint": {
      "Description": "Endpoint address.",
      "Value": {
        "Fn::GetAtt": [
          "LogtailConfig",
          "Endpoint"
        ]
      }
    },
    "AppliedMachineGroups": {
      "Description": "Applied machine groups.",
      "Value": {
        "Fn::GetAtt": [
          "LogtailConfig",
          "AppliedMachineGroups"
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
  LogtailConfig:
    Type: ALIYUN::SLS::LogtailConfig
    Properties:
      ProjectName:
        Ref: ProjectName
      LogtailConfigName:
        Ref: LogtailConfigName
      LogstoreName:
        Ref: LogstoreName
      RawConfigData:
        Ref: RawConfigData
      CloneFrom:
        Ref: CloneFrom
Parameters:
  ProjectName:
    MinLength: 3
    Type: String
    Description: 'Project name: 1. Only supports lowercase letters, numbers, hyphens
      (-) and underscores (_). 2. Must start and end with lowercase letters and numbers.
      3. The name length is 3-63 characters.'
    MaxLength: 63
  LogtailConfigName:
    MinLength: 3
    Type: String
    Description: 'Logtail config name: 1. Only supports lowercase letters, numbers,
      hyphens (-) and underscores (_). 2. Must start and end with lowercase letters
      and numbers. 3. The name length is 3-63 characters.'
    MaxLength: 63
  LogstoreName:
    MinLength: 3
    Type: String
    Description: 'Logstore name: 1. Only supports lowercase letters, numbers, hyphens
      (-) and underscores (_). 2. Must start and end with lowercase letters and numbers.
      3. The name length is 3-63 characters.'
    MaxLength: 63
  RawConfigData:
    Type: Json
    Description: |-
      The format is the same as the response of SLS API GetConfig. Either CloneFrom or RawConfigData must be specified. If CloneFrom and RawConfigData are both specified, logtail config data will be merged from both with RawConfigData first. configName, outputType, outputDetail in data will be ignored.For example:
      {"configName": "test-logtail-config","createTime": 1574843554,"inputDetail": { "acceptNoEnoughKeys": false, "adjustTimezone": false, "advanced": {   "force_multiconfig": false }, "autoExtend": true, "delayAlarmBytes": 0, "delaySkipBytes": 0, "discardNonUtf8": false, "discardUnmatch": false, "dockerExcludeEnv": {}, "dockerExcludeLabel": {}, "dockerFile": false, "dockerIncludeEnv": {}, "dockerIncludeLabel": {}, "enableRawLog": false, "enableTag": false, "fileEncoding": "utf8", "filePattern": "test.log*", "filterKey": [], "filterRegex": [], "key": [   "time",   "logger",   "level",   "request_id",   "user_id",   "region_id",   "content" ], "localStorage": true, "logPath": "/var/log/test", "logTimezone": "", "logType": "delimiter_log", "maxDepth": 100, "maxSendRate": -1, "mergeType": "topic", "preserve": true, "preserveDepth": 1, "priority": 0, "quote": "\u0001", "sendRateExpire": 0, "sensitive_keys": [], "separator": ",,,", "shardHashKey": [], "tailExisted": false, "timeFormat": "", "timeKey": "", "topicFormat": "none"}, "inputType": "file", "lastModifyTime": 1574843554, "logSample": "2019-11-27 10:48:23,160,,,MAIN,,,INFO,,,98DCC51D-BE5D-49C7-B3FD-37B2BAEFB296,,,123456789,,,cn-hangzhou,,,this is a simple test.", "outputDetail": {"endpoint": "cn-hangzhou-intranet.log.aliyuncs.com", "logstoreName": "test-logstore","region": "cn-hangzhou"}, "outputType": "LogService"}
  CloneFrom:
    Type: Json
    Description: Clone logtail config data from existing logtail config. Either CloneFrom
      or RawConfigData must be specified. If CloneFrom and RawConfigData are both
      specified, logtail config data will be merged from both with RawConfigData first.
Outputs:
  Endpoint:
    Description: Endpoint address.
    Value:
      Fn::GetAtt:
      - LogtailConfig
      - Endpoint
  AppliedMachineGroups:
    Description: Applied machine groups.
    Value:
      Fn::GetAtt:
      - LogtailConfig
      - AppliedMachineGroups
  LogtailConfigName:
    Description: Logtail config name.
    Value:
      Fn::GetAtt:
      - LogtailConfig
      - LogtailConfigName
```

更多示例，请参见创建日志项目、在日志项目下创建日志库、为指定的Logstore创建索引、配置采集数据时的Logtail参数、创建日志服务机器组、将日志服务的日志配置应用于机器组、创建日志配置、将查询结果保存为快速查询和创建告警的组合示例：[JSON示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/SLS/JSON/SLS.json)和[YAML示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/SLS/YAML/SLS.yml)。

