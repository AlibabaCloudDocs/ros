# ALIYUN::WAF::AclRule

ALIYUN::WAF::AclRule is used to add an ACL rule for a specified domain name.

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

|Parameter|Type|Required|Editable|Description|Constraint|
|---------|----|--------|--------|-----------|----------|
|Rules|String|Yes|Not supported|The detailed information about the HTTP-based ACL rule, in JSON string format.|None|
|InstanceId|String|Yes|Not supported|Web Application Firewall instance ID.|None|
|Domain|String|Yes|Not supported|The domain name.|None|
|Region|String|No|Released|The region of the Web Application Firewall instance.|Valid values: -   cn: Mainland China \(default\)
-   cn-hongkong: China \(Hong Kong\) and other regions outside China |
|RuleId|Integer|Erased|Released|The ID of the access control list rule.|None|

## Return value

Fn::GetAtt

None.

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
    -cn
    -cn-hongkong
  RuleId:
    Type: Number
    Description: Precise access control rule ID
            
```

