# ALIYUN::ECS::NatGateway {#concept_48469_zh .concept}

ALIYUN::ECS::NatGateway is used to create a NAT Gateway for a VPC.

## Syntax {#section_tfd_hv2_lfb .section}

```language-json
{
  "Type": "ALIYUN::ECS::NatGateway",
  "Properties": {
    "VpcId": String,
    "Description": String,
    "NatGatewayName": String,
    "VSwitchId": String,
    "BandwidthPackage": List,
    "Spec": String
  }
}
```

## Properties { .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|VpcId|String|Yes|No|The ID of the VPC for which you want to create a NAT Gateway.|None|
|VSwitchId|String|Yes|No|The ID of the VSwitch in the VPC.|None|
|BandwidthPackage|List|No|No|The list of bandwidth packages created for the NAT Gateway.|You can create a maximum of four bandwidth packages.|
|Description|String|No|No|The description of the NAT Gateway.|The description must be 2 to 256 characters in length. Default value: null.|
|NatGatewayName|String|No|No|The name of the NAT Gateway.|The name must be 2 to 128 characters in length and can contain letters, digits, underscores \(\_\), periods \(.\), and hyphens \(-\). It must start with a letter.|
|Spec|String|No|No|The specifications of the NAT Gateway.|Valid values: Small, Middle, and Large.|

## BandwidthPackage syntax { .section}

```language-json
"BandwidthPackage": [
  {
    "Bandwidth": Integer,
    "ZoneId": String,
    "IpCount": Integer
  }
]
```

## BandwidthPackage properties { .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Bandwidth|Integer|No|No|The bandwidth size of the NAT Gateway.| Valid values: 5 to 5000. Unit: Mbit/s.

 Default value: 5.

 |
|ZoneId|String|No|No|The ID of the zone where the NAT Gateway resides.|None|
|IpCount|Integer|No|No|The number of assigned public IP addresses.|Valid values: 1 to 5.|
|InternetChargeType|String|No|No|The billing method of the network bandwidth. Default value: PayByTraffic.

 |Valid values: -   PayByTraffic: The network service is billed by traffic usage.
-   PayByBandwidth: The network service is billed by fixed bandwidth.

 |

## Response parameters { .section}

**Fn::GetAtt**

-   ForwardTableId: the ID of the forwarding table.
-   SNatTableId: the ID of the SNAT table.
-   NatGatewayId: the unique ID of the NAT Gateway.
-   BandwidthPackageIds: the list of all bandwidth package IDs.
-   BandwidthPackageIps: the list of IP addresses included in all bandwidth packages.

## Examples { .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "NatGateway": {
      "Type": "ALIYUN::ECS::NatGateway",
      "Properties": {
        "NatGatewayName": "nat_gateway_1",
        "Description": "my nat gateway",
        "VpcId": "vpc-25o8s****",
        "VSwitchId": "vsw-25rc1****",
        "Spec": "Small",
        "BandwidthPackage": [
           {
              "IpCount": 1,
              "Bandwidth": 5,
              "ZoneId": "cn-beijing-c"
           },
           {
              "IpCount": 1,
              "Bandwidth": 5,
              "ZoneId": "cn-beijing-c"
           },
           {
              "IpCount": 1,
              "Bandwidth": 5,
              "ZoneId": "cn-beijing-c"
           },
           {
              "IpCount": 1,
              "Bandwidth": 5,
              "ZoneId": "cn-beijing-c"
           },
           {
              "IpCount": 1,
              "Bandwidth": 5,
              "ZoneId": "cn-beijing-c"
           }
        ]
      }
    }
  },
  "Outputs": {
    "NatGatewayId": {
         "Value": {"Fn::GetAttr": ["NatGateway","NatGatewayId"]}
    },
    "BandwidthPackageIds": {
         "Value": {"Fn::GetAttr": ["NatGateway","BandwidthPackageIds"]}
    },
    "ForwardTableId": {
         "Value": {"Fn::GetAttr": ["NatGateway","ForwardTableId"]}
    },
    "SNatTableId": {
         "Value": {"Fn::GetAttr": ["NatGateway", "SNatTableId"]}
    }
  }
}
```

