# ALIYUN::ACM::Namespace

ALIYUN::ACM::Namespace类型用于创建命名空间。

## 语法

```
{
  "Type": "ALIYUN::ACM::Namespace",
  "Properties": {
    "Name": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Name|String|是|是|命名空间名称|无|

## 返回值

Fn::GetAtt

-   NamespaceId：命名空间ID。
-   Endpoint：命名空间Endpoint。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "Namespace": {
      "Type": "ALIYUN::ACM::Namespace",
      "Properties": {
        "Name": {
          "Ref": "Name"
        }
      }
    }
  },
  "Parameters": {
    "Name": {
      "Type": "String",
      "Description": "Namespace name"
    }
  },
  "Outputs": {
    "Endpoint": {
      "Description": "Endpoint",
      "Value": {
        "Fn::GetAtt": [
          "Namespace",
          "Endpoint"
        ]
      }
    },
    "NamespaceId": {
      "Description": "ID namespace",
      "Value": {
        "Fn::GetAtt": [
          "Namespace",
          "NamespaceId"
        ]
      }
    }
  }
}
```

`YAML`格式

```
ROSTemplateFormatVersion: '2015-09-01'
Resources:
  Namespace:
    Type: 'ALIYUN::ACM::Namespace'
    Properties:
      Name:
        Ref: Name
Parameters:
  Name:
    Type: String
    Description: Namespace name
Outputs:
  Endpoint:
    Description: Endpoint
    Value:
      'Fn::GetAtt':
        - Namespace
        - Endpoint
  NamespaceId:
    Description: ID namespace
    Value:
      'Fn::GetAtt':
        - Namespace
        - NamespaceId
```

