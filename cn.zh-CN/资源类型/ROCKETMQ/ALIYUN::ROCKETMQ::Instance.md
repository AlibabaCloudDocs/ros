# ALIYUN::ROCKETMQ::Instance

ALIYUN::ROCKETMQ::Instance类型用于创建标准版实例。

## 语法

```
{
  "Type": "ALIYUN::ROCKETMQ::Instance",
  "Properties": {
    "Remark": String,
    "InstanceName": String,
    "Tags": List
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Remark|String|否|是|备注。|最大长度为128个字符。|
|InstanceName|String|是|是|实例名称。|长度为3~64个字符，可包含英文字母、汉字、数字、短划线（-）和下划线（\_）。|
|Tags|List|否|是|标签。|最多支持添加20个标签。更多信息，请参见[Tags属性](#section_gor_asi_f84)。 |

## Tags语法

```
"Tags": [
  {
    "Key": String,
    "Value": String
  }
]  
```

## Tags属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Key|String|是|否|标签键。|长度为1~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或者`https://` 。|
|Value|String|否|否|标签值。|长度为0~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或者`https://` 。|

## 返回值

Fn::GetAtt

-   InstanceId：实例ID。
-   InstanceType：实例类型，1表示标准版。
-   HttpInternetEndpoint：HTTP公网接入点。
-   HttpInternetSecureEndpoint：HTTPS公网接入点。
-   TcpEndpoint：TCP协议接入点。
-   HttpInternalEndpoint：HTTP内网接入点。
-   InstanceName：实例名称。

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
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to instance. Max support 20 tags to add during create instance. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
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
        "Tags": {
          "Ref": "Tags"
        },
        "Remark": {
          "Ref": "Remark"
        }
      }
    }
  },
  "Outputs": {
    "InstanceName": {
      "Description": "Instance name",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "InstanceName"
        ]
      }
    },
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
    Description: The name of the instance, which contains 3 to 64 characters in Chinese
      or English.
    MaxLength: 64
    MinLength: 3
    Type: String
  Remark:
    Description: The remark of instance.
    Type: String
  Tags:
    Description: Tags to attach to instance. Max support 20 tags to add during create
      instance. Each tag with two properties Key and Value, and Key is required.
    MaxLength: 20
    Type: Json
Resources:
  Instance:
    Properties:
      InstanceName:
        Ref: InstanceName
      Remark:
        Ref: Remark
      Tags:
        Ref: Tags
    Type: ALIYUN::ROCKETMQ::Instance
Outputs:
  HttpInternalEndpoint:
    Description: The internal HTTP endpoint for the Message Queue for Apache RocketMQ
      instance.
    Value:
      Fn::GetAtt:
      - Instance
      - HttpInternalEndpoint
  HttpInternetEndpoint:
    Description: The Internet HTTP endpoint for the Message Queue for Apache RocketMQ
      instance.
    Value:
      Fn::GetAtt:
      - Instance
      - HttpInternetEndpoint
  HttpInternetSecureEndpoint:
    Description: The Internet HTTPS endpoint for the Message Queue for Apache RocketMQ
      instance.
    Value:
      Fn::GetAtt:
      - Instance
      - HttpInternetSecureEndpoint
  InstanceId:
    Description: Instance ID created
    Value:
      Fn::GetAtt:
      - Instance
      - InstanceId
  InstanceName:
    Description: Instance name
    Value:
      Fn::GetAtt:
      - Instance
      - InstanceName
  InstanceType:
    Description: Instance Type
    Value:
      Fn::GetAtt:
      - Instance
      - InstanceType
  TcpEndpoint:
    Description: The TCP endpoint for the Message Queue for Apache RocketMQ instance.
    Value:
      Fn::GetAtt:
      - Instance
      - TcpEndpoint
```

更多示例，请参见创建标准版实例、创建客户端Group ID和创建Topic的组合示例：[JSON示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ROCKETMQ/JSON/ROCKETMQ.json)和[YAML示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ROCKETMQ/YAML/ROCKETMQ.yml)。

