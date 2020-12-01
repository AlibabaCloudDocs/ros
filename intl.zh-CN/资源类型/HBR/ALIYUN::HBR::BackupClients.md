# ALIYUN::HBR::BackupClients

ALIYUN::HBR::BackupClients类型用于为ECS实例安装备份客户端。

## 语法

```
{
  "Type": "ALIYUN::HBR::BackupClients",
  "Properties": {
    "InstanceIds": List
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|InstanceIds|List|是|否|安装ECS备份客户端的实例ID。|最多支持为20个ECS实例安装备份客户端。|

## 返回值

Fn::GetAtt

-   InstanceIds：ECS实例ID。
-   ClientIds：备份客户端ID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "InstanceIds": {
      "Type": "Json",
      "Description": "ID list of instances to install backup client",
      "MinLength": 1,
      "MaxLength": 20
    }
  },
  "Resources": {
    "BackupClients": {
      "Type": "ALIYUN::HBR::BackupClients",
      "Properties": {
        "InstanceIds": {
          "Ref": "InstanceIds"
        }
      }
    }
  },
  "Outputs": {
    "InstanceIds": {
      "Description": "ID list of instances to install backup client",
      "Value": {
        "Fn::GetAtt": [
          "BackupClients",
          "InstanceIds"
        ]
      }
    },
    "ClientIds": {
      "Description": "ID list of clients installed in instances",
      "Value": {
        "Fn::GetAtt": [
          "BackupClients",
          "ClientIds"
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
  InstanceIds:
    Type: Json
    Description: ID list of instances to install backup client
    MinLength: 1
    MaxLength: 20
Resources:
  BackupClients:
    Type: 'ALIYUN::HBR::BackupClients'
    Properties:
      InstanceIds:
        Ref: InstanceIds
Outputs:
  InstanceIds:
    Description: ID list of instances to install backup client
    Value:
      'Fn::GetAtt':
        - BackupClients
        - InstanceIds
  ClientIds:
    Description: ID list of clients installed in instances
    Value:
      'Fn::GetAtt':
        - BackupClients
        - ClientIds
```

