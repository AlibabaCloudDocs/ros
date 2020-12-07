# ALIYUN::ROCKETMQ::Instance

ALIYUN::ROCKETMQ::Instance类型用于创建标准版实例。

## 语法

```
{
  "Type": "ALIYUN::ROCKETMQ::Instance",
  "Properties": {
    "Remark": String,
    "InstanceName": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Remark|String|否|是|备注|最大长度为128个字符。|
|InstanceName|String|是|是|实例名称|长度为3~64个字符，可包含英文字母、汉字、数字、短划线（-）和下划线（\_）。|

## 返回值

Fn::GetAtt

-   InstanceId：实例ID。
-   InstanceType：实例类型，1表示标准版。
-   HttpInternetEndpoint：HTTP公网接入点。
-   HttpInternetSecureEndpoint：HTTPS公网接入点。
-   TcpEndpoint：TCP协议接入点。
-   HttpInternalEndpoint：HTTP内网接入点。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "InstanceName": {
      "Type": "String",
      "Description": "The name of the instance, which contains 3 to 64 characters in Chinese or English.",
      "MinLength": 3,
      "MaxLength": 64
    },
    "Remark": {
      "Type": "String",
      "Description": "The remark of instance."
    }
  },
  "Resources": {
    "Instance": {
      "Type": "ALIYUN::ROCKETMQ::Instance",
      "Properties": {
        "InstanceName": {
          "Ref": "InstanceName"
        },
        "Remark": {
          "Ref": "Remark"
        }
      }
    }
  },
  "Outputs": {
    "HttpInternalEndpoint": {
      "Description": "The internal HTTP endpoint for the Message Queue for Apache RocketMQ instance.",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "HttpInternalEndpoint"
        ]
      }
    },
    "InstanceId": {
      "Description": "Instance ID created",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "InstanceId"
        ]
      }
    },
    "TcpEndpoint": {
      "Description": "The TCP endpoint for the Message Queue for Apache RocketMQ instance.",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "TcpEndpoint"
        ]
      }
    },
    "HttpInternetEndpoint": {
      "Description": "The Internet HTTP endpoint for the Message Queue for Apache RocketMQ instance.",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "HttpInternetEndpoint"
        ]
      }
    },
    "InstanceType": {
      "Description": "Instance Type",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "InstanceType"
        ]
      }
    },
    "HttpInternetSecureEndpoint": {
      "Description": "The Internet HTTPS endpoint for the Message Queue for Apache RocketMQ instance.",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "HttpInternetSecureEndpoint"
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
  InstanceName:
    Type: String
    Description: >-
      The name of the instance, which contains 3 to 64 characters in Chinese or
      English.
    MinLength: 3
    MaxLength: 64
  Remark:
    Type: String
    Description: The remark of instance.
Resources:
  Instance:
    Type: 'ALIYUN::ROCKETMQ::Instance'
    Properties:
      InstanceName:
        Ref: InstanceName
      Remark:
        Ref: Remark
Outputs:
  HttpInternalEndpoint:
    Description: >-
      The internal HTTP endpoint for the Message Queue for Apache RocketMQ
      instance.
    Value:
      'Fn::GetAtt':
        - Instance
        - HttpInternalEndpoint
  InstanceId:
    Description: Instance ID created
    Value:
      'Fn::GetAtt':
        - Instance
        - InstanceId
  TcpEndpoint:
    Description: The TCP endpoint for the Message Queue for Apache RocketMQ instance.
    Value:
      'Fn::GetAtt':
        - Instance
        - TcpEndpoint
  HttpInternetEndpoint:
    Description: >-
      The Internet HTTP endpoint for the Message Queue for Apache RocketMQ
      instance.
    Value:
      'Fn::GetAtt':
        - Instance
        - HttpInternetEndpoint
  InstanceType:
    Description: Instance Type
    Value:
      'Fn::GetAtt':
        - Instance
        - InstanceType
  HttpInternetSecureEndpoint:
    Description: >-
      The Internet HTTPS endpoint for the Message Queue for Apache RocketMQ
      instance.
    Value:
      'Fn::GetAtt':
        - Instance
        - HttpInternetSecureEndpoint
```

