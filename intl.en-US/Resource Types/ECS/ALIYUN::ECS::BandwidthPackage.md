# ALIYUN::ECS::BandwidthPackage {#concept_48472_zh .concept}

ALIYUN::ECS::BandwidthPackage is used to create a bandwidth package for a specified NAT Gateway.

## Syntax { .section}

```language-json
{
  "Type": "ALIYUN::ECS::BandwidthPackage",
  "Properties": {
    "Description": String,
    "NatGatewayId": String,
    "ZoneId": String,
    "BandwidthPackageName": String,
    "Bandwidth": Integer,
    "IpCount": Integer
  }
}
```

## Properties { .section}

|Name|Type|Required|Description|Validity|
|----|----|--------|-----------|--------|
|NatGatewayId|String|Yes|The ID of the NAT Gateway to which you want to bind the created bandwidth package.|None|
|Bandwidth|Integer|Yes|The bandwidth supported by the NAT Gateway.| Valid values: 5 to 5,000. Unit: Mbit/s.

 Default value: 5.

 |
|IpCount|Integer|Yes|The number of public IP addresses allocated for the NAT Gateway.|Valid values: 1 to 5.|
|Description|String|No|The description of the bandwidth package.|The description must be 2 to 256 characters in length. This parameter is empty by default.|
|ZoneId|String|No|The ID of the zone in which the NAT Gateway resides.|None|
|BandwidthPackageName|String|No|The name of the bandwidth package.|The name must be 2 to 128 characters in length and can contain letters, digits, underscores \(\_\), periods \(.\), and hyphens \(-\). It must start with a letter.|
|InternetChargeType|String|No|The billing method of the Internet bandwidth.|Valid values:-   PayByBandwidth: The network service is billed by fixed bandwidth.
-   PayByTraffic: The network service is billed by traffic usage.

Default value: PayByTraffic.

|

## Response parameters { .section}

**Fn::GetAtt**

-   BandwidthPackageId: the ID of the bandwidth package.
-   BandwidthPackageIps: all IP addresses included in the bandwidth package.

## Examples { .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "BandwidthPackage": {
      "Type": "ALIYUN::ECS::BandwidthPackage",
      "Properties": {
        "BandwidthPackageName": "pkg_2",
        "Description": "my_bandwidth",
        "NatGatewayId": "ngw-h1xoxepyf",
        "IpCount": 2,
        "Bandwidth": 5,
        "ZoneId": "cn-beijing-c"
      }
    }
  },
  "Outputs": {
    "BandwidthPackageId": {
         "Value": {"Fn::GetAttr": ["BandwidthPackage","BandwidthPackageId"]}
    },
    "BandwidthPackageIps": {
         "Value": {"Fn::GetAttr": ["BandwidthPackage","BandwidthPackageIps"]}
    }
  }
}
```

