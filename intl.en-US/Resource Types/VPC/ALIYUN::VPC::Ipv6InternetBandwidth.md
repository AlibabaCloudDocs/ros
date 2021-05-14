# ALIYUN::VPC::Ipv6InternetBandwidth

ALIYUN::VPC::Ipv6InternetBandwidth is used to purchase a public bandwidth plan for an IPv6 address.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Bandwidth|Integer|Yes|Yes|The public bandwidth of the IPv6 address.|-   Valid values when InternetChargeType is set to PayByBandwidth: 1 to 5000.
-   When InternetChargeType is set to PayByTraffic, the valid values of Bandwidth depend on the specification of the IPv6 gateway.
    -   Valid values when the specification is Small \(Free Edition\): 1 to 500.
    -   Valid values when the specification is Medium \(Enterprise Edition\): 1 to 1000.
    -   Valid values when the specification is Large \(Enhanced Enterprise Edition\): 1 to 2000.

Unit: Mbit/s. |
|Ipv6AddressId|String|Yes|No|The ID of the IPv6 address.|None|
|Ipv6GatewayId|String|Yes|No|The ID of the IPv6 gateway.|None|
|InternetChargeType|String|No|No|The billing method of the public bandwidth resources of the IPv6 gateway.|Default value: PayByBandwidth. Valid values: -   PayByTraffic
-   PayByBandwidth |
|Tags|List|No|Yes|The tags of the public bandwidth plan.|A maximum of 20 tags can be specified. For more information, see the [Tags properties](#section_3qi_zd5_v6i) section in this topic. |

## Tags syntax

```
"Tags": [
  {
    "Key": String,
    "Value": String
  }
]  
```

## Tags properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Key|String|Yes|No|The tag key.|The tag key must be 1 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|
|Value|String|No|No|The tag value.|The tag value must be 0 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|

## Response parameters

Fn::GetAtt

InternetBandwidthId: the ID of the public bandwidth plan.

## Examples

`JSON` format

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

`YAML` format

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

For more examples, visit [SnatEntry.json](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/VPC/JSON/SnatEntry.json) and [SnatEntry.yml](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/VPC/YAML/SnatEntry.yml). In the examples, the ALIYUN::ECS::VPC, ALIYUN::ECS::VSwitch, ALIYUN::VPC::SnatEntry, ALIYUN::VPC::CommonBandwidthPackage, ALIYUN::VPC::CommonBandwidthPackageIp, ALIYUN::VPC::Ipv6Gateway, and ALIYUN::VPC::Ipv6InternetBandwidth resource types are involved.

