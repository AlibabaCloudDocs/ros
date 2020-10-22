# ALIYUN::ARMS::RetcodeApp

ALIYUN::ARMS::RetcodeApp类型用于创建前端监控任务。

## 语法

```
{
  "Type": "ALIYUN::ARMS::RetcodeApp",
  "Properties": {
    "RetcodeAppType": String,
    "RegionId": String,
    "RetcodeAppName": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|RetcodeAppType|String|是|否|前端监控应用类型|取值： -   web
-   weex
-   mini\_dd
-   mini\_alipay
-   mini\_wx
-   mini\_common |
|RegionId|String|是|否|地域ID|取值： -   cn-hangzhou
-   ap-southeast-1 |
|RetcodeAppName|String|是|否|前端监控应用名称|无|

## 返回值

Fn::GetAtt

-   Pid：PID。
-   AppId：应用ID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "RetcodeApp": {
      "Type": "ALIYUN::ARMS::RetcodeApp",
      "Properties": {
        "RetcodeAppType": {
          "Ref": "RetcodeAppType"
        },
        "RegionId": {
          "Ref": "RegionId"
        },
        "RetcodeAppName": {
          "Ref": "RetcodeAppName"
        }
      }
    }
  },
  "Parameters": {
    "RetcodeAppType": {
      "Type": "String",
      "Description": "The type of the application for which you want to create the browser monitoring job. Allowed values: web, weex, mini_dd, mini_alipay, mini_wx, mini_common."
    },
    "RegionId": {
      "Default": "cn-hangzhou",
      "Type": "String",
      "Description": "Region ID. Allowed values: cn-hangzhou, ap-southeast-1. Default to cn-hangzhou.",
      "AllowedValues": [
        "cn-hangzhou",
        "ap-southeast-1"
      ]
    },
    "RetcodeAppName": {
      "Type": "String",
      "Description": "The name of the application for which you want to create the browser monitoring job."
    }
  },
  "Outputs": {
    "Pid": {
      "Description": "The PID.",
      "Value": {
        "Fn::GetAtt": [
          "RetcodeApp",
          "Pid"
        ]
      }
    },
    "AppId": {
      "Description": "The ID of the application for which you created the browser monitoring job.",
      "Value": {
        "Fn::GetAtt": [
          "RetcodeApp",
          "AppId"
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
  RetcodeApp:
    Type: 'ALIYUN::ARMS::RetcodeApp'
    Properties:
      RetcodeAppType:
        Ref: RetcodeAppType
      RegionId:
        Ref: RegionId
      RetcodeAppName:
        Ref: RetcodeAppName
Parameters:
  RetcodeAppType:
    Type: String
    Description: >-
      The type of the application for which you want to create the browser
      monitoring job. Allowed values: web, weex, mini_dd, mini_alipay, mini_wx,
      mini_common.
  RegionId:
    Default: cn-hangzhou
    Type: String
    Description: >-
      Region ID. Allowed values: cn-hangzhou, ap-southeast-1. Default to
      cn-hangzhou.
    AllowedValues:
      - cn-hangzhou
      - ap-southeast-1
  RetcodeAppName:
    Type: String
    Description: >-
      The name of the application for which you want to create the browser
      monitoring job.
Outputs:
  Pid:
    Description: The PID.
    Value:
      'Fn::GetAtt':
        - RetcodeApp
        - Pid
  AppId:
    Description: >-
      The ID of the application for which you created the browser monitoring
      job.
    Value:
      'Fn::GetAtt':
        - RetcodeApp
        - AppId
```

