# ALIYUN::WAF::LogServiceEnable

ALIYUN::WAF::LogServiceEnable is used to enable the log collection feature for a specific domain name.

## Syntax

```
{
  "Type": "ALIYUN::WAF::LogServiceEnable",
  "Properties": {
    "InstanceId": String,
    "Domain": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|InstanceId|String|Yes|No|The ID of the Web Application Firewall \(WAF\) instance.|You can call the [DescribeInstanceInfo](/intl.en-US/API Reference/Instance information/DescribeInstanceInfo.md) operation to query the ID of a WAF instance.|
|Domain|String|Yes|No|The domain name that is added to WAF.|None|

## Response parameters

Fn::GetAtt

-   InstanceId: the ID of the WAF instance.
-   Domain: the domain name that is added to WAF.

## Examples

`JSON` format

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

`YAML` format

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

