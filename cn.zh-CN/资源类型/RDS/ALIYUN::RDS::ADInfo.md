# ALIYUN::RDS::ADInfo

ALIYUN::RDS::ADInfo类型用于配置AD域服务。

## 语法

```
{
  "Type": "ALIYUN::RDS::ADInfo",
  "Properties": {
    "ADServerIpAddress": String,
    "ADDNS": String,
    "DBInstanceId": String,
    "ADPassword": String,
    "ADAccountName": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ADServerIpAddress|String|是|否|AD服务器所在IP地址。|必须与RDS处于同一专有网络。|
|ADDNS|String|是|否|域名。|无|
|DBInstanceId|String|是|否|RDS实例ID。|无|
|ADPassword|String|是|否|域密码。|无|
|ADAccountName|String|是|否|域账号。|无|

## 返回值

Fn::GetAtt

-   ADDNS：域名。
-   DBInstanceId：RDS实例ID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "ADServerIpAddress": {
      "Type": "String",
      "Description": "The IP address of the AD server, it must be in the same VPC as the RDS."
    },
    "ADDNS": {
      "Type": "String",
      "Description": "Active directory domain name."
    },
    "DBInstanceId": {
      "Type": "String",
      "Description": "The ID of the instance."
    },
    "ADPassword": {
      "Type": "String",
      "Description": "Domain password. "
    },
    "ADAccountName": {
      "Type": "String",
      "Description": "Domain account name. "
    }
  },
  "Resources": {
    "AdInfo": {
      "Type": "ALIYUN::RDS::ADInfo",
      "Properties": {
        "ADServerIpAddress": {
          "Ref": "ADServerIpAddress"
        },
        "ADDNS": {
          "Ref": "ADDNS"
        },
        "DBInstanceId": {
          "Ref": "DBInstanceId"
        },
        "ADPassword": {
          "Ref": "ADPassword"
        },
        "ADAccountName": {
          "Ref": "ADAccountName"
        }
      }
    }
  },
  "Outputs": {
    "ADDNS": {
      "Description": "Active directory domain name.",
      "Value": {
        "Fn::GetAtt": [
          "AdInfo",
          "ADDNS"
        ]
      }
    },
    "DBInstanceId": {
      "Description": "The ID of the instance.",
      "Value": {
        "Fn::GetAtt": [
          "AdInfo",
          "DBInstanceId"
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
  ADServerIpAddress:
    Type: String
    Description: 'The IP address of the AD server, it must be in the same VPC as the RDS.'
  ADDNS:
    Type: String
    Description: Active directory domain name.
  DBInstanceId:
    Type: String
    Description: The ID of the instance.
  ADPassword:
    Type: String
    Description: 'Domain password. '
  ADAccountName:
    Type: String
    Description: 'Domain account name. '
Resources:
  AdInfo:
    Type: 'ALIYUN::RDS::ADInfo'
    Properties:
      ADServerIpAddress:
        Ref: ADServerIpAddress
      ADDNS:
        Ref: ADDNS
      DBInstanceId:
        Ref: DBInstanceId
      ADPassword:
        Ref: ADPassword
      ADAccountName:
        Ref: ADAccountName
Outputs:
  ADDNS:
    Description: Active directory domain name.
    Value:
      'Fn::GetAtt':
        - AdInfo
        - ADDNS
  DBInstanceId:
    Description: The ID of the instance.
    Value:
      'Fn::GetAtt':
        - AdInfo
        - DBInstanceId
```

