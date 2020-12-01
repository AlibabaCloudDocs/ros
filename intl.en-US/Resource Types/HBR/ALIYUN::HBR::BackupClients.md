# ALIYUN::HBR::BackupClients

ALIYUN::HBR::BackupClients is used to install one or more backup clients on ECS instances.

## Syntax

```
{
  "Type": "ALIYUN::HBR::BackupClients",
  "Properties": {
    "InstanceIds": List
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|InstanceIds|List|Yes|No|The IDs of one or more ECS instances on which to install a backup client.|You can install backup clients on a maximum of 20 ECS instances|

## Response parameters

Fn::GetAtt

-   InstanceIds: the IDs of one or more ECS instances on which backup clients are installed.
-   ClientIds: one or more backup client IDs.

## Examples

`JSON` format

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

`YAML` format

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

