# ALIYUN::ARMS::RetcodeApp

ALIYUN::ARMS::RetcodeApp is used to create an Application Real-Time Monitoring Service \(ARMS\) browser monitoring job.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|RetcodeAppType|String|Yes|No|The type of the application for which you want to create the browser monitoring job.|Valid values: -   web
-   weex
-   mini\_dd
-   mini\_alipay
-   mini\_wx
-   mini\_common |
|RegionId|String|Yes|No|The ID of the region.|Valid values: -   cn-hangzhou
-   ap-southeast-1 |
|RetcodeAppName|String|Yes|No|The name of the application for which you want to create the browser monitoring job.|None|

## Response parameters

Fn::GetAtt

-   Pid: the pid of the application.
-   AppId: the ID of the application.

## Examples

`JSON` format

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

`YAML` format

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

