# ALIYUN::WAF::LogServiceEnable

ALIYUN::WAF::LogServiceEnable类型用于开启指定域名配置的日志采集功能。

## 语法

```
{
  "Type": "ALIYUN::WAF::LogServiceEnable",
  "Properties": {
    "InstanceId": String,
    "Domain": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|InstanceId|String|是|否|Web应用防火墙（WAF）实例ID。|您可以调用[DescribeInstanceInfo](/intl.zh-CN/API参考/实例信息/DescribeInstanceInfo.md)查询WAF实例ID。|
|Domain|String|是|否|已添加的域名名称。|无|

## 返回值

Fn::GetAtt

-   InstanceId：WAF实例ID。
-   Domain：已添加的域名名称。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "InstanceId": {
      "Type": "String",
      "Description": "The ID of the WAF instance.\nYou can call the DescribeInstanceInfo operation to query the ID of the WAF instance."
    },
    "Domain": {
      "Type": "String",
      "Description": "The domain name that is added to WAF."
    }
  },
  "Resources": {
    "LogServiceEnable": {
      "Type": "ALIYUN::WAF::LogServiceEnable",
      "Properties": {
        "InstanceId": {
          "Ref": "InstanceId"
        },
        "Domain": {
          "Ref": "Domain"
        }
      }
    }
  },
  "Outputs": {
    "InstanceId": {
      "Description": "The ID of the WAF instance.\nYou can call the DescribeInstanceInfo operation to query the ID of the WAF instance.",
      "Value": {
        "Fn::GetAtt": [
          "LogServiceEnable",
          "InstanceId"
        ]
      }
    },
    "Domain": {
      "Description": "The domain name that is added to WAF.",
      "Value": {
        "Fn::GetAtt": [
          "LogServiceEnable",
          "Domain"
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
  Domain:
    Description: The domain name that is added to WAF.
    Type: String
  InstanceId:
    Description: 'The ID of the WAF instance.

      You can call the DescribeInstanceInfo operation to query the ID of the WAF instance.'
    Type: String
Resources:
  LogServiceEnable:
    Properties:
      Domain:
        Ref: Domain
      InstanceId:
        Ref: InstanceId
    Type: ALIYUN::WAF::LogServiceEnable
Outputs:
  Domain:
    Description: The domain name that is added to WAF.
    Value:
      Fn::GetAtt:
      - LogServiceEnable
      - Domain
  InstanceId:
    Description: 'The ID of the WAF instance.

      You can call the DescribeInstanceInfo operation to query the ID of the WAF instance.'
    Value:
      Fn::GetAtt:
      - LogServiceEnable
      - InstanceId
```

