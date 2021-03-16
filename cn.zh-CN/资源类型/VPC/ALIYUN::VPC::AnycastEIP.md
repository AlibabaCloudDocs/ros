# ALIYUN::VPC::AnycastEIP

ALIYUN::VPC::AnycastEIP类型用于创建任播弹性公网IP（Anycast EIP）实例。

## 语法

```
{
  "Type": "ALIYUN::VPC::AnycastEIP",
  "Properties": {
    "Description": String,
    "ServiceLocation": String,
    "InstanceChargeType": String,
    "InternetChargeType": String,
    "Name": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Description|String|否|是|Anycast EIP实例描述。|无|
|ServiceLocation|String|否|否|Anycast EIP实例接入地域。|取值：international，表示中国内地以外的地域。|
|InstanceChargeType|String|否|否|Anycast EIP实例付费类型。|取值：PostPaid，表示后付费。|
|InternetChargeType|String|否|否|Anycast EIP实例访问公网计费方式。|取值：PayByTraffic，表示按流量计费。|
|Name|String|否|是|Anycast EIP实例名称。|长度为2~128个字符，以英文字母或汉字开头，可包含英文字母、汉字、数字、下划线（\_）和短划线（-）。|

## 返回值

Fn::GetAtt

-   AnycastId：Anycast EIP实例ID。
-   IpAddress：Anycast EIP IP地址。
-   OrderId：订单ID。
-   Name：Anycast EIP实例名称。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Description": {
      "Type": "String",
      "Description": "Anycast EIP instance description"
    },
    "ServiceLocation": {
      "Type": "String",
      "Description": "Anycast EIP instance access area",
      "AllowedValues": [
        "international"
      ],
      "Default": "international"
    },
    "InstanceChargeType": {
      "Type": "String",
      "Description": "Anycast EIP instance charge type",
      "AllowedValues": [
        "PostPaid"
      ]
    },
    "InternetChargeType": {
      "Type": "String",
      "Description": "Anycast EIP instance access public network billing method",
      "AllowedValues": [
        "PayByTraffic"
      ]
    },
    "Name": {
      "Type": "String",
      "Description": "Anycast EIP instance name"
    }
  },
  "Resources": {
    "AnycastEip": {
      "Type": "ALIYUN::VPC::AnycastEIP",
      "Properties": {
        "Description": {
          "Ref": "Description"
        },
        "ServiceLocation": {
          "Ref": "ServiceLocation"
        },
        "InstanceChargeType": {
          "Ref": "InstanceChargeType"
        },
        "InternetChargeType": {
          "Ref": "InternetChargeType"
        },
        "Name": {
          "Ref": "Name"
        }
      }
    }
  },
  "Outputs": {
    "AnycastId": {
      "Description": "Anycast EIP instance ID",
      "Value": {
        "Fn::GetAtt": [
          "AnycastEip",
          "AnycastId"
        ]
      }
    },
    "IpAddress": {
      "Description": "Anycase IP address",
      "Value": {
        "Fn::GetAtt": [
          "AnycastEip",
          "IpAddress"
        ]
      }
    },
    "OrderId": {
      "Description": "Order ID",
      "Value": {
        "Fn::GetAtt": [
          "AnycastEip",
          "OrderId"
        ]
      }
    },
    "Name": {
      "Description": "Anycast EIP instance name",
      "Value": {
        "Fn::GetAtt": [
          "AnycastEip",
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
Parameters:
  Description:
    Description: Anycast EIP instance description
    Type: String
  InstanceChargeType:
    AllowedValues:
    - PostPaid
    Description: Anycast EIP instance charge type
    Type: String
  InternetChargeType:
    AllowedValues:
    - PayByTraffic
    Description: Anycast EIP instance access public network billing method
    Type: String
  Name:
    Description: Anycast EIP instance name
    Type: String
  ServiceLocation:
    AllowedValues:
    - international
    Default: international
    Description: Anycast EIP instance access area
    Type: String
Resources:
  AnycastEip:
    Properties:
      Description:
        Ref: Description
      InstanceChargeType:
        Ref: InstanceChargeType
      InternetChargeType:
        Ref: InternetChargeType
      Name:
        Ref: Name
      ServiceLocation:
        Ref: ServiceLocation
    Type: ALIYUN::VPC::AnycastEIP
Outputs:
  AnycastId:
    Description: Anycast EIP instance ID
    Value:
      Fn::GetAtt:
      - AnycastEip
      - AnycastId
  IpAddress:
    Description: Anycase IP address
    Value:
      Fn::GetAtt:
      - AnycastEip
      - IpAddress
  Name:
    Description: Anycast EIP instance name
    Value:
      Fn::GetAtt:
      - AnycastEip
      - Name
  OrderId:
    Description: Order ID
    Value:
      Fn::GetAtt:
      - AnycastEip
      - OrderId
```

