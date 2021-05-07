# ALIYUN::WAF::AclRule

ALIYUN::WAF::AclRule类型用于为指定域名添加精准访问控制规则。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Rules|String|是|否|精准访问控制规则详细信息，采用JSON格式的字符串表述。|无|
|InstanceId|String|是|否|Web应用防火墙实例ID。|无|
|Domain|String|是|否|域名名称。|无|
|Region|String|否|否|Web应用防火墙实例所在的地域。|取值： -   cn：中国内地（默认值）
-   cn-hongkong：中国香港及海外地区 |
|RuleId|Integer|否|否|精准访问控制规则ID。|无|

## 返回值

Fn::GetAtt

无。

## 示例

`JSON`格式

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

`YAML`格式

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

