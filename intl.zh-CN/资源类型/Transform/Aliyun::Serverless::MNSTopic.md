# Aliyun::Serverless::MNSTopic

Aliyun::Serverless::MNSTopic类型用于创建主题。

## 语法

```
{
  "Type": "Aliyun::Serverless::MNSTopic",
  "Properties": {
    "LoggingEnabled": Boolean,
    "MaximumMessageSize": Integer
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|MaximumMessageSize|Integer|否|是|发送到该主题的消息体最大长度。|取值范围：1024（1KB）~65,536（64KB）。

单位：Byte。

默认值：65,536（64KB）。 |
|LoggingEnabled|Boolean|否|是|是否启用日志管理功能。|取值： -   true：启用。
-   false（默认值）：停用。 |

## 返回值

Fn::GetAtt

-   TopicUrl：所创建的主题的URL。
-   TopicName：主题名称。
-   ARN.WithSlash：主题的ARN。

## 示例

`JSON`格式

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Transform": "Aliyun::Serverless-2018-04-03",
  "Resources": {
    "MnsTopic": {
      "Type": "Aliyun::Serverless::MNSTopic",
      "Properties": {
        "MaximumMessageSize": 2048,
        "LoggingEnabled": false
      }
    }
  },
  "Outputs": {
    "TopicUrl": {
      "Value": {
        "Fn::GetAtt": [
          "MnsTopic",
          "TopicUrl"
        ]
      }
    },
    "TopicName": {
      "Value": {
        "Fn::GetAtt": [
          "MnsTopic",
          "TopicName"
        ]
      }
    },
    "ARN.WithSlash": {
      "Value": {
        "Fn::GetAtt": [
          "MnsTopic",
          "ARN.WithSlash"
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
  MnsTopic:
    Type: 'Aliyun::Serverless::MNSTopic'
    Properties:
      MaximumMessageSize: 2048
      LoggingEnabled: false
Outputs:
  TopicUrl:
    Value:
      'Fn::GetAtt':
        - MnsTopic
        - TopicUrl
  TopicName:
    Value:
      'Fn::GetAtt':
        - MnsTopic
        - TopicName
  ARN.WithSlash:
    Value:
      'Fn::GetAtt':
        - MnsTopic
        - ARN.WithSlash
```

