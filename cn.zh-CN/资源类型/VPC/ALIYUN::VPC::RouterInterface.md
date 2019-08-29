# ALIYUN::VPC::RouterInterface {#concept_54430_zh .concept}

ALIYUN::VPC::RouterInterface 用于创建路由器接口。

## 语法 {#section_irh_mfz_lfb .section}

```language-json
{
  "Type": "ALIYUN::VPC::RouterInterface",
  "Properties": {
    "OppositeRegionId": String,
    "Description": String,
    "HealthCheckSourceIp": String,
    "RouterType": String,
    "AccessPointId": String,
    "RouterId": String,
    "Role": String,
    "OppositeInterfaceOwnerId": String,
    "OppositeAccessPointId": String,
    "HealthCheckTargetIp": String,
    "OppositeRouterId": String,
    "Spec": String,
    "OppositeRouterType": String,
    "Name": String,
    "PricingCycle": String, 
    "Period": Number, 
    "AutoPay": Boolean, 
    "InstanceChargeType": String
  }
}
```

## 属性 { .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|RouterId|string|是|否|路由器 ID。|无|
|Role|string|是|否|连接中扮演的角色，即，是连接发起端还是连接接受端。| 可选值：InitiatingSide 和 AcceptingSide。

 如果 RouterType 是 VBR，该值必须指定为 InitiatingSide。

 如果 OppositeRouterType 指定为 VBR，该值必须是 AcceptingSide。

 |
|RouterType|string|否|否|所属的路由器类型。|可选值：VRouter 和 VBR。|
|AccessPointId|string|否|否|所属的接入点 ID。|RouterType 是 VBR 时，必填，而且创建后不允许修改。在 RouterType 是 VRouter 时，不能填。|
|Spec|string|否|否|路由器接口的规格。

可用的规格和对应的带宽如下：-   Mini.2：2Mbps
-   Mini.5：5Mbps
-   Small.1：10Mbps
-   Small.2：20Mbps
-   Small.5：50Mbps
-   Middle.1：100Mbps
-   Middle.2：200Mbps
-   Middle.5：500Mbps
-   Large.1：1000 Mbps
-   Large.2：2000Mbps
-   Large.5：5000 Mbps
-   Xlarge.1：10000Mbps

| 如果 Role 被指定为 InitiatingSide, 则该值必须指定。

 如果 Role 被指定为 AcceptingSide, 该值默认为 Negative。

 |
|OppositeRegionId|string|否|否|要连接的对端所在的地域。|无|
|OppositeInterfaceOwnerId|string|否|否|连接对端路由器接口的持有者账号 ID。|默认是当前用户的 ID。|
|OppositeRouterId|string|否|否|要连接的对端的路由器的ID。|无|
|OppositeRouterType|string|否|否|要连接的对端路由器接口所属的路由器类型。|可选值：VRouter 和 VBR。如果 RouterType 指定为 VBR，该值必须是 VRouter。|
|OppositeAccessPointId|string|否|否|对端所属的接入点 ID。| 在 OppositeRouterType 是 VBR 时，必填，而且创建后不允许修改。

 在OppositeRouterType 是 VRouter 时，不能填。

 在 OppositeRouterType 是 VBR 时，OppositeRouterId 所指定的 VBR 必须在 OppositeAccessPointId 所指定的接入点内。

 |
|Description|string|否|否|路由器接口描述。|长度范围 \[2, 256\] 个字符。不填则为空，默认为空。不能以 http:// 和 https:// 开头。|
|Name|string|否|否|路由器接口显示名称。|长度范围 \[2, 128\] 字符。必须以大小字母或中文开头，可包含字母、汉字、数字、点号（.）、下划线（\_）、和连字符（-）。不能以 http:// 和 https:// 开头。|
|HealthCheckSourceIp|string|否|否|专线容灾和 ECMP 场景下用来做专线健康检查的 Packet 的源 IP。|只对本端是 VRouter，而且对端是 VBR 的路由器接口有效。必须是本端 VRouter 所在的 VPC 内的一个未被使用的 IP。HealthCheckSourceIp 与 HealthCheckTargetIp 必须同时指定，或同时不指定。|
|HealthCheckTargetIp|string|否|否|专线容灾和 ECMP 场景下用来做专线健康检查的 Packet 的目标 IP。|只对本端是 VRouter，而且对端是 VBR 的路由器接口有效。通常可以用专线用户端 CPE 的 IP（也就是对端 RI 所在的 VBR 上的 PeerGatewayIp）。也可以指定专线用户端的其他 IP。HealthCheckSourceIp 与 HealthCheckTargetIp 必须同时指定，或同时不指定。|
|PricingCycle|String|否|否|预付费的计费周期。|取值：-   Month：按月付费
-   Year：按年付费。

|
|Period|Number|否|否|购买时长。|取值：-   当选择按月付费时，取值范围为 1-9
-   当选择按年付费时，取值范围为1-3

|
|AutoPay|Boolean|否|否|自动付款。| 取值：True | False。

 默认值：False。

 |
|InstanceChargeType|String|否|否|实例的付费类型。|取值：-   Postpaid：后付费（按量付费）；
-   Prepaid：预付费（包年包月）。

|

## 返回值 { .section}

**Fn::GetAtt**

RouterInterfaceId：路由器接口 ID。

## 示例 { .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "RouterInterface": {
      "Type": "ALIYUN::VPC::RouterInterface",
      "Properties": {
        "Name": "RouterInterface_1",
        "Description": "VPC initiator RouterInterface",
        "RouterId": "vrt-2ze2i147e5n0bicoefwsb",
        "Role": "AcceptingSide",
        "OppositeRegionId": "cn-beijing",
        "HealthCheckSourceIp": "10.0.0.120",
        "HealthCheckTargetIp": "192.168.1.24"
      }
    }
  },
  "Outputs": {
    "RouterInterfaceId": {
      "Value": {"Fn::GetAtt": ["RouterInterface", "RouterInterfaceId"]}
    }
  }
}
```

