# Aliyun::Serverless::Log

Aliyun::Serverless::Log类型用于创建日志项目。

## 语法

```
{
  "Type": "Aliyun::Serverless::Log",
  "Properties": {
    "Description": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Description|String|是|否|日志项目描述。|长度为0~64个字符。不支持特殊字符`'<>"\`。|

## 返回值

Fn::GetAtt

Name: 日志项目名称。

## 示例

`JSON`格式

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Transform": "Aliyun::Serverless-2018-04-03",
  "Resources": {
    "MySlsProject": {
      "Type": "Aliyun::Serverless::Log",
      "Properties": {
        "Description": "Test log"
      }
    }
  },
  "Outputs": {
    "Name": {
      "Value": {
        "Fn::GetAtt": [
          "MySlsProject",
          "Name"
        ]
      }
    }
  }
}
```

`YAML`格式

```
ROSTemplateFormatVersion: '2015-09-01'
Transform: 'Aliyun::Serverless-2018-04-03'
Resources:
  MySlsProject:
    Type: 'Aliyun::Serverless::Log'
    Properties:
      Description: Test log
Outputs:
  Name:
    Value:
      'Fn::GetAtt':
        - MySlsProject
        - Name
```

