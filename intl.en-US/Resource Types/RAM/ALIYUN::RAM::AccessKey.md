# ALIYUN::RAM::AccessKey

ALIYUN::RAM::AccessKey is used to obtain the AccessKey pair \(AccessKey ID and AccessKey secret\) of a specified user and its status.

## Syntax

```
{
  "Type": "ALIYUN::RAM::AccessKey ",
  "Properties": {
    "UserName": String
   }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|UserName|String|Yes|No|The name of the user.|None|

## Response parameters

Fn::GetAtt

-   AccessKeyId: the AccessKey ID.
-   AccessKeySecret: the AccessKey secret.
-   Status: the status of the AccessKey pair. It can be enabled or disabled.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "UserName": {
      "Type": "String",
      "Description": "Specifies the user name, containing up to 64 characters."
    }
  },
  "Resources": {
    "AccessKey": {
      "Type": "ALIYUN::RAM::AccessKey",
      "Properties": {
        "UserName": {
          "Ref": "UserName"
        }
      }
    }
  },
  "Outputs": {
    "Status": {
      "Description": "Status of access key.",
      "Value": {
        "Fn::GetAtt": [
          "AccessKey",
          "Status"
        ]
      }
    },
    "AccessKeyId": {
      "Description": "Id of access key.",
      "Value": {
        "Fn::GetAtt": [
          "AccessKey",
          "AccessKeyId"
        ]
      }
    },
    "AccessKeySecret": {
      "Description": "Secret of access key.",
      "Value": {
        "Fn::GetAtt": [
          "AccessKey",
          "AccessKeySecret"
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
  UserName:
    Type: String
    Description: 'Specifies the user name, containing up to 64 characters.'
Resources:
  AccessKey:
    Type: 'ALIYUN::RAM::AccessKey'
    Properties:
      UserName:
        Ref: UserName
Outputs:
  Status:
    Description: Status of access key.
    Value:
      'Fn::GetAtt':
        - AccessKey
        - Status
  AccessKeyId:
    Description: Id of access key.
    Value:
      'Fn::GetAtt':
        - AccessKey
        - AccessKeyId
  AccessKeySecret:
    Description: Secret of access key.
    Value:
      'Fn::GetAtt':
        - AccessKey
        - AccessKeySecret
```

