# ALIYUN::ECS::BandwidthPackage {#concept_48472_zh .concept}

ALIYUN::ECS::BandwidthPackage类型用于创建 NAT 网关使用的带宽包。

## 语法 { .section}

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

## 属性 { .section}

|属性名称|类型|必须|描述|约束|
|----|--|--|--|--|
|NatGatewayId|String|是|带宽包要绑定的 NAT 网关 ID。|无|
|Bandwidth|Integer|是|带宽大小。| 取值范围：\[5, 5000\]， 单位：Mbps。

 默认值是 5 Mbps。

 |
|IpCount|Integer|是|分配公网 IP 的个数。|取值范围：\[1, 5\]。|
|Description|String|否|带宽包描述。|参数长度 \[2, 256\]。默认为空。|
|ZoneId|String|否|所属地域下的可用区。|无|
|BandwidthPackageName|String|否|带宽包的名称。|必须以英文字母或汉字开始，可以包含英文字母、数字、汉字、下划线（\_）、点号（.）、连字符（-）。参数值长度为 \[2, 128\]。|
|InternetChargeType|String|否|网络计费类型。|取值范围：-   PayByBandwidth：按固定带宽计费
-   PayByTraffic：按使用流量计费

默认值：PayByTraffic。

|

## 返回值 { .section}

**Fn::GetAtt**

-   BandwidthPackageId：带宽包的 ID。
-   BandwidthPackageIps：带宽包的所有 IP。

## 示例 { .section}

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

