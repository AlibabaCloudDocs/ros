# ALIYUN::ApiGateway::LogConfig

ALIYUN::ApiGateway::LogConfig类型用于创建日志配置。

## 语法

```
{
  "Type": "ALIYUN::ApiGateway::LogConfig",
  "Properties": {
    "SlsLogStore": String,
    "SlsProject": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|SlsProject|String|是|是|日志项目。|无|
|SlsLogStore|String|是|是|日志项目下的日志库。|无|

## 返回值

Fn::GetAtt

-   SlsProject：日志项目名称。
-   SlsLogStore：日志库名称。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "SlsLogStore": {
      "Type": "String",
      "Description": "Logstore name of SLS",
      "MinLength": 3,
      "MaxLength": 63
    },
    "SlsProject": {
      "Type": "String",
      "Description": "Project name of SLS",
      "MinLength": 3,
      "MaxLength": 63
    }
  },
  "Resources": {
    "LogConfig": {
      "Type": "ALIYUN::ApiGateway::LogConfig",
      "Properties": {
        "SlsLogStore": {
          "Ref": "SlsLogStore"
        },
        "SlsProject": {
          "Ref": "SlsProject"
        }
      }
    }
  },
  "Outputs": {
    "SlsLogStore": {
      "Description": "Logstore name of SLS",
      "Value": {
        "Fn::GetAtt": [
          "LogConfig",
          "SlsLogStore"
        ]
      }
    },
    "SlsProject": {
      "Description": "Project name of SLS",
      "Value": {
        "Fn::GetAtt": [
          "LogConfig",
          "SlsProject"
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
  SlsLogStore:
    Type: String
    Description: Logstore name of SLS
    MinLength: 3
    MaxLength: 63
  SlsProject:
    Type: String
    Description: Project name of SLS
    MinLength: 3
    MaxLength: 63
Resources:
  LogConfig:
    Type: 'ALIYUN::ApiGateway::LogConfig'
    Properties:
      SlsLogStore:
        Ref: SlsLogStore
      SlsProject:
        Ref: SlsProject
Outputs:
  SlsLogStore:
    Description: Logstore name of SLS
    Value:
      'Fn::GetAtt':
        - LogConfig
        - SlsLogStore
  SlsProject:
    Description: Project name of SLS
    Value:
      'Fn::GetAtt':
        - LogConfig
        - SlsProject
```

