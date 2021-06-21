# ALIYUN::WAF::AclRule

ALIYUN::WAF::AclRule is used to add an HTTP access control list \(ACL\) rule for a specified domain name.

## Syntax

```
{
  "Type": "ALIYUN::WAF::AclRule",
  "Properties": {
    "Rules": String,
    "InstanceId": String,
    "Domain": String,
    "Region": String,
    "RuleId": Integer
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Rules|String|Yes|No|The detailed information of the HTTP ACL rule in the JSON format.|None|
|InstanceId|String|Yes|No|The ID of the Web Application Firewall \(WAF\) instance.|None|
|Domain|String|Yes|No|The domain name.|None|
|Region|String|No|No|The region where the WAF instance resides.|Default value: cn. Valid values: -   cn: mainland China
-   cn-hongkong: the China \(Hong Kong\) region and regions outside China |
|RuleId|Integer|No|No|The ID of the HTTP ACL rule.|None|

## Response parameters

Fn::GetAtt

None

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "AclRule": {
      "Type": "ALIYUN::WAF::AclRule",
      "Properties": {
        "Rules": {
          "Ref": "Rules"
        },
        "InstanceId": {
          "Ref": "InstanceId"
        },
        "Domain": {
          "Ref": "Domain"
        },
        "Region": {
          "Ref": "Region"
        },
        "RuleId": {
          "Ref": "RuleId"
        }
      }
    }
  },
  "Parameters": {
    "Rules": {
      "Type": "String",
      "Description": "Detailed information of precise access control rules, expressed in JSON format strings."
    },
    "InstanceId": {
      "Type": "String",
      "Description": "WAF instance ID. Description Interface You can view your current WAF instance ID by calling DescribePayInfo."
    },
    "Domain": {
      "Type": "String",
      "Description": "Domain name."
    },
    "Region": {
      "Type": "String",
      "Description": "The region where the WAF instance is located.
       Default value: cn.Valid 
       values: 
       cn: mainland China
       cn-hongkong: Hong Kong (China) and outside China"
      "AllowedValues": [
        "cn",
        "cn-hongkong"
      ]
    },
    "RuleId": {
      "Type": "Number",
      "Description": "Precise access control rule ID"
    }
  }
}
```

`YAML` format

```
ROSTemplateFormatVersion: '2015-09-01'
Resources:
  AclRule:
    Type: ALIYUN::WAF::AclRule
    Properties:
      Rules:
        Ref: Rules
      InstanceId:
        Ref: InstanceId
      Domain:
        Ref: Domain
      Region:
        Ref: Region
      RuleId:
        Ref: RuleId
Parameters:
  Rules:
    Type: String
    Description: Detailed information of precise access control rules, expressed in
      JSON format strings.
  InstanceId:
    Type: String
    Description: WAF instance ID. Description Interface You can view your current
      WAF instance ID by calling DescribePayInfo.
  Domain:
    Type: String
    Description: Domain name.
  Region:
    Type: String
    Description: 'The region where the WAF instance is located.
       Default value: cn.Valid 
       values: 
       cn: mainland China
       cn-hongkong: Hong Kong (China) and outside China'
    AllowedValues:
    - cn
    - cn-hongkong
  RuleId:
    Type: Number
    Description: Precise access control rule ID
            
```

