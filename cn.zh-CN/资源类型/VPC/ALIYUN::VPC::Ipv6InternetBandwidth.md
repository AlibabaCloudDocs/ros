# ALIYUN::VPC::Ipv6InternetBandwidth

ALIYUN::VPC::Ipv6InternetBandwidth类型用于为IPv6地址购买公网带宽。

## 语法

```
{
  "Type": "ALIYUN::VPC::Ipv6InternetBandwidth",
  "Properties": {
    "Bandwidth": Integer,
    "Ipv6AddressId": String,
    "Ipv6GatewayId": String,
    "InternetChargeType": String,
    "Tags": List
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Bandwidth|Integer|是|是|IPv6地址的公网带宽。|取值范围：-   InternetChargeType取值为PayByBandwidth时：1~5000。
-   InternetChargeType取值为PayByTraffic时，IPv6地址的公网带宽取值范围同时受到IPv6网关规格的制约：
    -   Small（默认免费版）：1~500。
    -   Medium（企业版）：1~1000。
    -   Large（企业增强版）：1~2000。

单位：Mbps。 |
|Ipv6AddressId|String|是|否|IPv6地址的实例ID。|无|
|Ipv6GatewayId|String|是|否|IPv6网关的ID。|无|
|InternetChargeType|String|否|否|IPv6公网带宽的计费方式。|取值： -   PayByTraffic：按使用流量计费。
-   PayByBandwidth（默认值）：按带宽计费。 |
|Tags|List|否|是|标签。|最多支持添加20个标签。更多信息，请参见[Tags属性](#section_3qi_zd5_v6i)。 |

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

InternetBandwidthId：公网带宽ID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Bandwidth": {
      "Type": "Number",
      "Description": "Public IPv6 address of bandwidth, unit: Mbps, range: 1-5000.\nWhen InternetChargeType is PayByBandwidth, the bandwidth of the public network is the IPv6 address 1-5000.\nWhen InternetChargeType is PayByTraffic, public network bandwidth IPv6 addresses while IPv6 gateway restricted specifications.\nSmall (default free version), the public network bandwidth range 1-500.\nMedium (Enterprise Edition), the public network bandwidth range from 1 to 1000.\nLarge (Enterprise Edition), the public network bandwidth range 1-2000.",
      "MinValue": 1,
      "MaxValue": 5000
    },
    "Ipv6AddressId": {
      "Type": "String",
      "Description": "ID of IPv6 address."
    },
    "Ipv6GatewayId": {
      "Type": "String",
      "Description": "ID of IPv6 gateway."
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to instance. Max support 20 tags to add during create instance. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
    },
    "InternetChargeType": {
      "Type": "String",
      "Description": "IPv6 public network bandwidth billing, value:\nPayByTraffic: by using the traffic accounting.\nPayByBandwidth (default): Bandwidth billing.",
      "AllowedValues": [
        "PayByTraffic",
        "PayByBandwidth"
      ]
    }
  },
  "Resources": {
    "Ipv6InternetBandwidth": {
      "Type": "ALIYUN::VPC::Ipv6InternetBandwidth",
      "Properties": {
        "Bandwidth": {
          "Ref": "Bandwidth"
        },
        "Ipv6AddressId": {
          "Ref": "Ipv6AddressId"
        },
        "Ipv6GatewayId": {
          "Ref": "Ipv6GatewayId"
        },
        "Tags": {
          "Ref": "Tags"
        },
        "InternetChargeType": {
          "Ref": "InternetChargeType"
        }
      }
    }
  },
  "Outputs": {
    "InternetBandwidthId": {
      "Description": "Purchase of public network bandwidth.",
      "Value": {
        "Fn::GetAtt": [
          "Ipv6InternetBandwidth",
          "InternetBandwidthId"
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
  Bandwidth:
    Description: 'Public IPv6 address of bandwidth, unit: Mbps, range: 1-5000.

      When InternetChargeType is PayByBandwidth, the bandwidth of the public network
      is the IPv6 address 1-5000.

      When InternetChargeType is PayByTraffic, public network bandwidth IPv6 addresses
      while IPv6 gateway restricted specifications.

      Small (default free version), the public network bandwidth range 1-500.

      Medium (Enterprise Edition), the public network bandwidth range from 1 to 1000.

      Large (Enterprise Edition), the public network bandwidth range 1-2000.'
    MaxValue: 5000
    MinValue: 1
    Type: Number
  InternetChargeType:
    AllowedValues:
    - PayByTraffic
    - PayByBandwidth
    Description: 'IPv6 public network bandwidth billing, value:

      PayByTraffic: by using the traffic accounting.

      PayByBandwidth (default): Bandwidth billing.'
    Type: String
  Ipv6AddressId:
    Description: ID of IPv6 address.
    Type: String
  Ipv6GatewayId:
    Description: ID of IPv6 gateway.
    Type: String
  Tags:
    Description: Tags to attach to instance. Max support 20 tags to add during create
      instance. Each tag with two properties Key and Value, and Key is required.
    MaxLength: 20
    Type: Json
Resources:
  Ipv6InternetBandwidth:
    Properties:
      Bandwidth:
        Ref: Bandwidth
      InternetChargeType:
        Ref: InternetChargeType
      Ipv6AddressId:
        Ref: Ipv6AddressId
      Ipv6GatewayId:
        Ref: Ipv6GatewayId
      Tags:
        Ref: Tags
    Type: ALIYUN::VPC::Ipv6InternetBandwidth
Outputs:
  InternetBandwidthId:
    Description: Purchase of public network bandwidth.
    Value:
      Fn::GetAtt:
      - Ipv6InternetBandwidth
      - InternetBandwidthId
```

更多示例，请参见创建专有网络、创建专有网络中的交换机、在SNAT列表中添加SNAT条目、创建共享带宽实例、添加EIP到共享带宽中、创建IPv6网关和为IPv6地址购买公网带宽的组合示例：[JSON示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/VPC/JSON/SnatEntry.json)和[YAML示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/VPC/YAML/SnatEntry.yml)。

