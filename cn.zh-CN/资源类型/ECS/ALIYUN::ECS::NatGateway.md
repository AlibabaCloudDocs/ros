# ALIYUN::ECS::NatGateway {#concept_48469_zh .concept}

ALIYUN::ECS::NatGateway 类型用于创建专有网络的 NAT 网关。

## 语法 {#section_tfd_hv2_lfb .section}

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

## 属性 { .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|VpcId|string|是|否|指定创建 NAT 网关的专有网络 ID 。|无|
|VSwitchId|string|是|否|指定 VpcId 下的虚拟交换机 ID。|无|
|BandwidthPackage|list|否|否|为 NAT 网关创建的带宽包 。|最多创建 4 个带宽包。|
|Description|string|否|否|指定 NAT 网关的描述。|长度为 2-256 个字符。默认是空。|
|NatGatewayName|string|否|否|指定 NAT 网关的名称。|必须以字母或汉字开始，可以包含字母、数字、汉字、下划线（\_）、点号（.）和连字符（-）, 长度范围为 2-128 个字符。|
|Spec|string|否|否|NAT 网关的规格。|允许的可选值：Small, Middle, Large 。|

## BandwidthPackage 语法 { .section}

```language-json
"BandwidthPackage": [
  {
    "Bandwidth": Integer,
    "ZoneId": String,
    "IpCount": Integer
  }
]
```

## BandwidthPackage 属性 { .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Bandwidth|integer|否|否|带宽大小 。| 取值范围：\[5-5000\]， 单位：Mbps。

 默认值是 5 Mbps。

 |
|ZoneId|string|否|否|指定所在 region 下的可用区。|无|
|IpCount|integer|否|否|指定分配公网 IP 数量。|取值范围：\[1,5\]。|
|InternetChargeType|string|否|否|网络计费方式。 默认值：PayByTraffic。

 |取值范围： -   PayByTraffic：按流量计费。
-   PayByBandwidth：按带宽计费。

 |

## 返回值 { .section}

**Fn::GetAtt**

-   ForwardTableId：端口转发表 ID。
-   SNatTableId：SNat 源地址转换表 ID。
-   NatGatewayId：Nat 网关的唯一 ID。
-   BandwidthPackageIds：所有的带宽包 ID。
-   BandwidthPackageIps：所有带宽包中的 IP 地址。

## 示例 { .section}

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

