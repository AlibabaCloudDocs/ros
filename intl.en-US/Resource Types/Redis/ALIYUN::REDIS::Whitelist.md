# ALIYUN::REDIS::Whitelist

ALIYUN::REDIS::Whitelist is used to configure an IP address whitelist for an ApsaraDB for Redis instance.

## Syntax

```
{
  "Type": "ALIYUN::REDIS::Whitelist",
  "Properties": {
    "InstanceId": String,
    "SecurityIpGroupName": String,
    "SecurityIpGroupAttribute": String,
    "SecurityIps": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|InstanceId|String|Yes|No|The globally unique ID of the ApsaraDB for Redis instance.|None|
|SecurityIpGroupName|String|No|No|The name of the whitelist. Default value: default.|None|
|SecurityIpGroupAttribute|String|No|No|The attribute value of the whitelist. This parameter is empty by default. The whitelist for which this parameter is set to hidden is not displayed in the console.|None|
|SecurityIps|String|Yes|Yes|The IP addresses in the IP address whitelist. Separate multiple IP addresses with commas \(,\). Supported formats are IP addresses such as 0.0.0.0/0 and 10.23.12.24, or CIDR blocks such as 10.23.12.24/24. /24 indicates the length of the IP address prefix. The IP address prefix can consist of 1 to 32 bits.|A maximum of 1,000 IP addresses can be added.|

## Response parameters

Fn::GetAtt

-   SecurityIpGroupName: the name of the whitelist.
-   SecurityIpGroupAttribute: the attribute value of the whitelist.
-   SecurityIps: the modified IP address whitelist.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "Whitelist": {
      "Type": "ALIYUN::REDIS::Whitelist",
      "Properties": {
        "InstanceId": {
          "Ref": "InstanceId"
        },
        "SecurityIpGroupName": {
          "Ref": "SecurityIpGroupName"
        },
        "SecurityIpGroupAttribute": {
          "Ref": "SecurityIpGroupAttribute"
        },
        "SecurityIps": {
          "Ref": "SecurityIps"
        }
      }
    }
  },
  "Parameters": {
    "InstanceId": {
      "Type": "String",
      "Description": "The globally unique ID of the ApsaraDB for Redis instance."
    },
    "SecurityIpGroupName": {
      "AllowedPattern": "[a-z][a-zA-Z0-9_]*[a-zA-Z0-9]",
      "MinLength": 2,
      "Type": "String",
      "Description": "The name of the whitelist.",
      "MaxLength": 32
    },
    "SecurityIpGroupAttribute": {
      "Type": "String",
      "Description": ""This parameter is empty by default. To distinguish attribute values, the whitelist for which this parameter is set to hidden is not displayed in the console."
    },
    "SecurityIps": {
      "Type": "String",
      "Description": "The IP addresses in the IP address whitelist."
    }
  },
  "Outputs": {
    "SecurityIpGroupName": {
      "Description": "The name of the whitelist.",
      "Value": {
        "Fn::GetAtt": [
          "Whitelist",
          "SecurityIpGroupName"
        ]
      }
    },
    "SecurityIpGroupAttribute": {
      "Description": "The attribute value of the whitelist.",
      "Value": {
        "Fn::GetAtt": [
          "Whitelist",
          "SecurityIpGroupAttribute"
        ]
      }
    },
    "SecurityIps": {
      "Description": "The modified IP address whitelist.",
      "Value": {
        "Fn::GetAtt": [
          "Whitelist",
          "SecurityIps"
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
  Whitelist:
    Type: ALIYUN::REDIS::Whitelist
    Properties:
      InstanceId:
        Ref: InstanceId
      SecurityIpGroupName:
        Ref: SecurityIpGroupName
      SecurityIpGroupAttribute:
        Ref: SecurityIpGroupAttribute
      SecurityIps:
        Ref: SecurityIps
Parameters:
  InstanceId:
    Type: String
    Description: The globally unique ID of the ApsaraDB for Redis instance.
  SecurityIpGroupName:
    AllowedPattern: "[a-z][a-zA-Z0-9_]*[a-zA-Z0-9]"
    MinLength: 2
    Type: String
    Description: The name of the whitelist.
    MaxLength: 32
  SecurityIpGroupAttribute:
    Type: String
    Description: This parameter is empty by default. To distinguish attribute values, the whitelist for which this parameter is set to hidden is not displayed in the console.
  SecurityIps:
    Type: String
    Description: The IP addresses in the IP address whitelist.
Outputs:
  SecurityIpGroupName:
    Description: The name of the whitelist.
    Value:
      Fn::GetAtt:
      - Whitelist
      - SecurityIpGroupName
  SecurityIpGroupAttribute:
    Description: The attribute value of the whitelist.
    Value:
      Fn::GetAtt:
      - Whitelist
      - SecurityIpGroupAttribute
  SecurityIps:
    Description: The modified IP address whitelist.
    Value:
      Fn::GetAtt:
      - Whitelist
      - SecurityIps
			
```

