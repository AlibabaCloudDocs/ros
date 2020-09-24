# ALIYUN::RAM::AccessKey

ALIYUN::RAM::AccessKey类型用于获取指定用户的AccessKey ID、AccessKey Secret以及AccessKey的状态。

## 语法

```
{
  "Type": "ALIYUN::RAM::AccessKey ",
  "Properties": {
    "UserName": String
   }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|UserName|String|是|否|用户名|无|

## 返回值

Fn::GetAtt

-   AccessKeyId：AccessKey ID。
-   AccessKeySecret：AccessKey密钥。
-   Status：AccessKey状态，禁用或者开启。

## 示例

`JSON`格式

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

`YAML`格式

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

