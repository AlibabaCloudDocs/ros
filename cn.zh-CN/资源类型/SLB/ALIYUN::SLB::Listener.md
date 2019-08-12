# ALIYUN::SLB::Listener {#concept_51202_zh .concept}

ALIYUN::SLB::Listener 用于创建负载均衡监听（Listener）。

## 语法 {#section_vsm_3bz_lfb .section}

``` {#codeblock_f9g_wn4_qr7 .language-json}
{
  "Type": "ALIYUN::SLB::Listener",
  "Properties": {
    "AclStatus": String,
    "Protocol": String,
    "AclId": String,
    "ServerCertificateId": String,
    "HealthCheck": Map,
    "RequestTimeout": Integer,
    "IdleTimeout": Integer,
    "ListenerPort": Integer,
    "Bandwidth": Integer,
    "AclType": String,
    "BackendServerPort": Integer,
    "Scheduler": String,
    "LoadBalancerId": String,
    "CACertificateId": String,
    "Persistence": Map,
    "VServerGroupId": String
  }
}
```

## 属性 {#section_y45_lbz_lfb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|AclStatus|String|否|否|是否开启访问控制功能。|可用值: on, off（默认值）。|
|AclId|String|否|否|监听绑定的访问策略组ID。,当AclStatus参数的值为on时，该参数必选。|无。|
|AclType|String|否|否|访问控制类型： white：仅转发来自所选访问控制策略组中设置的IP地址或地址段的请求，白名单适用于应用只允许特定IP访问的场景。 设置白名单存在一定业务风险。,一旦设置白名单，就只有白名单中的IP可以访问负载均衡监听。,如果开启了白名单访问，但访问策略组中没有添加任何IP，则负载均衡监听不会转发请求。 black：来自所选访问控制策略组中设置的IP地址或地址段的所有请求都不会转发，黑名单适用于应用只限制某些特定IP访问的场景。 如果开启了黑名单访问，但访问策略组中没有添加任何IP，则负载均衡监听会转发全部请求。 当AclStatus参数的值为on时，该参数必选。|可用值: white, black。|
|Protocol|String|是|否|IP 协议。|可选值：http、https、tcp、udp。|
|ListenerPort|Integer|是|否|负载均衡实例前端使用的端口。|取值范围：1-65535。|
|Bandwidth|Integer|是|否|监听的带宽峰值。|取值：-1 / 1-1000 Mbps， 针对按固定带宽计费方式的公网类型实例， 不同 Listener 上的 Bandwidth 的峰值总和不能超出在创建负载均衡实例时设定的 Bandwidth 值，且不能将 Listener 上的 Bandwidth 值设置为 -1； 针对按使用流量计费方式的公网类型实例，可以选择将 Listener 上的 Bandwidth 值设置为 -1，表示不限制带宽峰值。|
|BackendServerPort|Integer|是|否|负载均衡实例后端使用的端口。|取值范围：1-65535。|
|LoadBalancerId|String|是|否|负载均衡实例的 ID。|无|
|HealthCheck|Map|否|否|健康检查设置。|无|
|Persistence|Map|否|否|相关参数的持久化。|无|
|Scheduler|String|否|否|调度算法。| 取值：wrr 和 wlc。

 默认值：wrr。

 |
|CACertificateId|String|否|否|CA 证书 ID。|只对 https 有效。|
|ServerCertificateId|String|否|否|服务器证书的 ID。|只对 https 有效，并且是必须的。|
|VServerGroupId|String|否|否|虚拟服务器组 ID。|无|
|RequestTimeout|Integer|否|否|指定请求超时时间。|取值范围为1-180秒。|
|IdleTimeout|Integer|否|否|指定连接空闲超时时间。|取值范围为1-60秒。|

## HealthCheck 语法 {#section_rwp_rbz_lfb .section}

``` {#codeblock_4mg_iqo_ycc .language-json}
"HealthCheck": {
  "Domain": String,
  "Interval": Integer,
  "URI": String,
  "HttpCode": String,
  "HealthyThreshold": Integer,
  "Timeout": Integer,
  "UnhealthyThreshold": Integer,
  "Port": Integer
}
```

## HealthCheck 属性 {#section_2za_snc_vkm .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Domain|String|否|否|用于健康检查的域名。| 取值：$\_ip、用户自定义字符串、空。

 自定义字符串规则：长度限制为 1-80 字符，只能包含字母、数字、连字符（-\)、和点号（.）。

 用户设置此参数为 $\_ip 或为空时，负载均衡会使用各后端服务器的私网 IP 当做健康检查使用的域名。

 |
|Interval|Integer|否|否|进行健康检查的时间间隔。|取值范围：1-5，单位：秒。|
|URI|String|否|否|用于健康检查的 URI。|取值：长度限制为 1-80 字符，必须以正斜线（/）开头，可包含字母、数字、连字符（-\)、正斜线（/）、点号（.）、百分号（%）、问号（?）、井号（\#）、和 and 符号（&）。|
|HttpCode|String|否|否|健康检查正常的 http 状态码。| 多个 http 状态码间用半角逗号（,）分割。

 可选值：http\_2xx、http\_3xx、http\_4xx、http\_5xx。

 默认值：http\_2xx。

 |
|HealthyThreshold|Integer|否|否|判定健康检查结果为 success 的阈值。即，健康检查连续成功多少次后，将后端服务器的健康检查状态由 fail 改为 success。|取值范围：1-10。|
|Timeout|Integer|否|否|每次健康检查响应的最大超时时间。| 取值范围：1-50，单位：秒。

 **说明：** 如果 Timeout 值小于 Interval 值，则 Timeout 无效，超时时间为 Interval 的值。

 |
|UnhealthyThreshold|Integer|否|否|判定健康检查结果为 fail 的阈值。即，健康检查连续失败多少次后，将后端服务器的健康检查状态由 success 改为 fail。|取值：1-10。|
|Port|Integer|否|否|用于健康检查的端口。|取值范围：0-65535。|

## Persistence 语法 {#section_8lm_sz6_buh .section}

``` {#codeblock_zls_dd3_bjp .language-json}
"Persistence": {
  "PersistenceTimeout": Integer,
  "CookieTimeout": Integer,
  "XForwardedFor": String,
  "Cookie": String,
  "StickySession": String,
  "StickySessionType": String
}
```

## Persistence 属性 {#section_1bw_bgv_atk .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|StickySession|String|是|否|是否开启会话保持。|可选值：on、off。|
|PersistenceTimeout|Integer|否|否|连接持久化的超时时间。| 取值范围： 0-1000（单位：秒）。

 默认值：0。0 表示关闭。

 |
|CookieTimeout|Integer|否|否|cookie 超时时间。| 该参数在 StickySession 为 on， 且 StickySessionType 为 insert 时为必选；其余情况下该参数会被忽略。

 取值范围： 1-86400（单位：秒）。

 |
|XForwardedFor|String|否|否|是否开启通过 X-Forwarded-For 的方式获取来访者真实 IP。| 可选值：on、off。

 默认值：on。

 |
|Cookie|String|否|否|服务器上配置的 cookie。| 仅在 StickySession 为 on，且 StickySessionType 为 server 时为必选；其余情况下该参数会被忽略。

 取值：遵守 RFC 2965，且长度为 1-200 字符的字符串。 只能包含 ASCII 英文字母和数字字符，不能包含逗号、分号或空格，也不能以美元符号（$）开头。

 |
|StickySessionType|String|否|否|cookie 的处理方式。| 该参数在 StickySession 为 on 时为必选；当 StickySession 为 off 时，此参数设置将被忽略。

 可选值：insert、server。

 设置为 insert，则表示由负载均衡插入； 设置为 server，则表示负载均衡从后端服务器学习。|

## 返回值 {#section_zrf_qcz_lfb .section}

**Fn::GetAtt**

-   LoadBalancerId：负载均衡实例的唯一标识。
-   ListenerPortsAndProtocol：数组格式，负载均衡实例前端使用的端口和协议。

## 示例 {#section_c4m_tcz_lfb .section}

``` {#codeblock_nim_eqf_vl3 .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "LoadBalancer": {
      "Type": "ALIYUN::SLB::LoadBalancer",
      "Properties": {
        "LoadBalancerName": "createdByHeat",
        "AddressType": "internet",
        "InternetChargeType": "paybybandwidth"
      }
    },
    "CreateListener": {
      "Type": "ALIYUN::SLB::Listener",
      "Properties": {
        "LoadBalancerId": {"Ref": "LoadBalancer"},
        "ListenerPort": "8094",
        "BackendServerPort": 8080,
        "Bandwidth": 1,
        "Protocol": "http",
        "HealthCheck": {
          "HealthyThreshold": 3,
          "UnhealthyThreshold": 3,
          "Interval": 2,
          "Timeout": 5,
          "HttpCode": "http_2xx,http_3xx,http_4xx,http_5xx"
        },
        "Scheduler": "wrr",
          "Persistence": {
          "PersistenceTimeout": 1,
          "XForwardedFor": 1,
          "StickySession": 1,
          "StickySessionType": 1,
          "CookieTimeout": 0,
          "Cookie": 1
        }
      }
    }
  },
  "Outputs": {
  "LoadBalanceDetails": {
     "Value": {"Fn::GetAtt": ["LoadBalancer", "LoadBalancerId"]}
  }
  }
}
```

