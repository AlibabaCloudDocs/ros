# ALIYUN::SLB::Listener

ALIYUN::SLB::Listener用于创建负载均衡监听（Listener）。

## 语法

```
{
  "Type": "ALIYUN::SLB::Listener",
  "Properties": {
    "MasterSlaveServerGroupId": String,
    "AclStatus": String,
    "Protocol": String,
    "AclId": String,
    "ServerCertificateId": String,
    "HealthCheck": Map,
    "RequestTimeout": Integer,
    "IdleTimeout": Integer,
    "ListenerPort": Integer,
    "HttpConfig": Map,
    "Bandwidth": Integer,
    "AclType": String,
    "BackendServerPort": Integer,
    "Scheduler": String,
    "LoadBalancerId": String,
    "CACertificateId": String,
    "Persistence": Map,
    "VServerGroupId": String,
    "Description": String,
    "PortRange": List
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|MasterSlaveServerGroupId|String|否|否|主备服务器组ID。|无|
|AclStatus|String|否|否|是否开启访问控制功能。|取值： -   on（默认值）
-   off |
|AclId|String|否|否|监听绑定的访问策略组ID。|当AclStatus取值为on时，该参数为必选参数。|
|AclType|String|否|否|访问控制类型。|取值： -   white：仅转发来自所选访问控制策略组中设置的IP地址或地址段的请求。白名单适用于应用只允许特定IP访问的场景。设置白名单存在一定业务风险。一旦设置白名单，只有白名单中的IP可以访问负载均衡监听。如果开启了白名单访问，但访问策略组中没有添加任何IP，则负载均衡监听不会转发请求。
-   black：来自所选访问控制策略组中设置的IP地址或地址段的所有请求都不会转发。黑名单适用于应用只限制某些特定IP访问的场景。如果开启了黑名单访问，但访问策略组中没有添加任何IP，则负载均衡监听会转发全部请求。当AclStatus参数取值为on时，该参数为必选参数。 |
|Protocol|String|是|否|网络协议。|取值： -   http
-   https
-   tcp
-   udp |
|ListenerPort|Integer|是|否|负载均衡实例前端使用的端口。|取值范围：1~65,535。|
|Bandwidth|Integer|是|否|监听的带宽峰值。|取值范围：-1或1~1000。单位：Mbps。

取值说明：

-   针对按固定带宽计费方式的公网类型实例，不同Listener上的Bandwidth的峰值总和不能超出在创建负载均衡实例时设定的Bandwidth值，且不能将Listener上的Bandwidth值设置为-1。
-   针对按使用流量计费方式的公网类型实例，可以选择将Listener上的Bandwidth值设置为-1，表示不限制带宽峰值。 |
|BackendServerPort|Integer|是|否|负载均衡实例后端使用的端口。|取值范围：1~65,535。|
|LoadBalancerId|String|是|否|负载均衡实例的ID。|无|
|HealthCheck|Map|否|否|健康检查设置。|更多信息，请参见[HealthCheck属性](#section_2za_snc_vkm)。|
|Persistence|Map|否|是|相关参数的持久化。|更多信息，请参见[Persistence属性](#section_1bw_bgv_atk)。|
|Scheduler|String|否|否|调度算法。|取值： -   wrr（默认值）
-   wlc |
|CACertificateId|String|否|否|CA证书ID。|只对HTTPS协议有效。|
|ServerCertificateId|String|否|是|服务器证书的ID。|只对HTTPS协议有效，且必须指定该参数。|
|VServerGroupId|String|否|否|服务器组ID。|无|
|RequestTimeout|Integer|否|否|指定请求超时时间。|取值范围：1~180。 单位：秒。 |
|IdleTimeout|Integer|否|否|指定连接空闲超时时间。|取值范围：1~60。 单位：秒。 |
|HttpConfig|Map|否|否|用于配置HTTP协议。|更多信息，请参见[HttpConfig属性](#section_iz0_jz0_x1b)。|
|Description|String|否|否|监听的描述信息。|长度为1~80个字符。可包含英文字母、汉字、数字、短划线（-）、正斜线（/）、半角句号（.）和下划线（\_）。|
|PortRange|List|否|否|监听的端口范围。|目前仅支持开启全端口监听，即 StartPort=1，EndPort=65,535。更多信息，请参见[PortRange属性](#section_e47_s0b_2es)。 |

## HealthCheck 语法

```
"HealthCheck": {
  "Domain": String,
  "Interval": Integer,
  "URI": String,
  "HttpCode": String,
  "HealthyThreshold": Integer,
  "HealthCheckType": String,
  "Timeout": Integer,
  "UnhealthyThreshold": Integer,
  "Port": Integer,
  "Switch": String
}
```

## HealthCheck属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Domain|String|否|否|用于健康检查的域名。|取值： -   $\_ip
-   用户自定义字符串：长度为1~80个字符。可包含英文字母、数字、短划线（-）和半角句号（.）。
-   空

**说明：** 用户设置此参数为$\_ip或空时，负载均衡会使用各后端服务器的私网IP当做健康检查使用的域名。 |
|Interval|Integer|否|否|进行健康检查的时间间隔。|取值范围：1~5。 单位：秒。 |
|URI|String|否|否|用于健康检查的URI。|长度为1~80个字符。必须以正斜线（/）开头，可包含英文字母、数字、短划线（-）、正斜线（/）、半角句号（.）、百分号（%）、问号（?）、井号（\#）和and（&）。|
|HttpCode|String|否|否|健康检查正常的HTTP状态码。|取值： -   http\_2xx（默认值）
-   http\_3xx
-   http\_4xx
-   http\_5xx

多个HTTP状态码间用半角逗号（,）分隔。 |
|HealthyThreshold|Integer|否|否|判定健康检查结果为success的阈值。即，健康检查连续成功多少次后，将后端服务器的健康检查状态由fail改为success。|取值范围：1~10。|
|HealthCheckType|String|否|否|健康检查类型|取值：-   tcp
-   http |
|Timeout|Integer|否|否|每次健康检查响应的最大超时时间。|取值范围：1~50。

单位：秒。

**说明：** 如果Timeout值小于Interval值，则Timeout无效，超时时间为Interval的值。 |
|UnhealthyThreshold|Integer|否|否|判定健康检查结果为fail的阈值，即健康检查连续失败多少次后，将后端服务器的健康检查状态由success改为fail。|取值范围：1~10。|
|Port|Integer|否|否|用于健康检查的端口。|取值范围：0~65,535。|
|Switch|String|否|否|是否启用健康检查。|取值：-   on：启用健康检查。
-   off：禁用健康检查。

**说明：** 当前仅对HTTP或HTTPS协议有效。如果未设置Switch，默认将禁用健康检查，除非已经配置了健康检查项目。 |

## Persistence语法

```
"Persistence": {
  "PersistenceTimeout": Integer,
  "CookieTimeout": Integer,
  "XForwardedFor": String,
  "XForwardedFor_SLBID": String,
  "XForwardedFor_proto": String,
  "XForwardedFor_SLBIP": String,
  "Cookie": String,
  "StickySession": String,
  "StickySessionType": String
}
```

## Persistence属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|StickySession|String|否|是|是否开启会话保持。|取值： -   on
-   off |
|PersistenceTimeout|Integer|否|是|连接持久化的超时时间。|取值范围：0~1000。 默认值：0。表示关闭。

单位：秒。 |
|CookieTimeout|Integer|否|是|Cookie超时时间。|取值范围：1~86,400。

单位：秒。

**说明：** 当StickySession为on且StickySessionType为insert时，该参数必选。 |
|XForwardedFor|String|否|是|是否开启通过X-Forwarded-For的方式获取来访者真实IP。|取值： on。|
|XForwardedFor\_proto|String|否|是|是否通过X-Forwarded-Proto头字段获取负载均衡实例的监听协议。|取值：-   on
-   off（默认值） |
|XForwardedFor\_SLBID|String|否|是|是否通过SLB-ID头字段获取负载均衡实例ID。|取值：-   on
-   off（默认值） |
|XForwardedFor\_SLBIP|String|否|是|是否通过SLB-IP头字段获取客户端请求的真实IP。|取值：-   on
-   off（默认值） |
|Cookie|String|否|是|服务器上配置的Cookie。|长度为1~200个字符，不能以美元符号（$）开头。可包含英文字母和数字，不能包含半角逗号（,）、半角分号（;）和空格（ ）。**说明：** 当StickySession为on且StickySessionType为server时，该参数必选。 |
|StickySessionType|String|否|是|Cookie的处理方式。|取值：-   insert：植入Cookie。
-   server：重写Cookie。

**说明：** 当StickySession的值为on时，必须指定该参数。 |

## HttpConfig语法

```
"HttpConfig": {
  "ForwardPort": Integer,
  "ListenerForward": String
}
```

## HttpConfig属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ForwardPort|Integer|否|否|HTTP到HTTPS监听转发端口。|取值范围：1~65,535。 默认值：443。 |
|ListenerForward|String|否|否|是否将HTTP启用为HTTPS转发。|取值： -   on
-   off（默认值） |

## PortRange语法

```
"PortRange": [
  {
    "StartPort": Integer,
    "EndPort": Integer
  }
]
```

## PortRange属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|StartPort|Integer|是|否|起始端口。|取值：1。|
|EndPort|Integer|是|否|结束端口。|取值：65,535。|

## 返回值

Fn::GetAtt

-   LoadBalancerId：负载均衡实例的唯一标识。
-   ListenerPortsAndProtocol：负载均衡实例前端使用的端口和协议。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "RequestTimeout": {
      "Type": "Number",
      "Description": "Specify the request timeout in seconds. Valid value: 1-180 If no response is received from the backend server during the specified timeout period, Server Load Balancer will stop waiting and send an HTTP 504 error to the client.",
      "MinValue": 1,
      "MaxValue": 180
    },
    "ListenerPort": {
      "Type": "Number",
      "Description": "Port for front listener. Range from 0 to 65535.",
      "MinValue": 0,
      "MaxValue": 65535
    },
    "VServerGroupId": {
      "Type": "String",
      "Description": "The id of the VServerGroup which use in listener."
    },
    "Description": {
      "Type": "String",
      "Description": "The description of the listener.It must be 1 to 80 characters in length and can contain letters, digits, hyphens (-), forward slashes (/), periods (.), and underscores (_). Chinese characters are supported.",
      "MaxLength": 80
    },
    "CACertificateId": {
      "Type": "String",
      "Description": "CA server certificate id, for https listener only."
    },
    "Scheduler": {
      "Type": "String",
      "Description": "The scheduling algorithm. Valid values:\nwrr: Backend servers that have higher weights receive more requests than those that have lower weights.\nwlc: Requests are distributed based on the combination of the weights and connections to backend servers. If two backend servers have the same weight, the backend server that has fewer connections receives more requests.\nrr: Requests are distributed to backend servers in sequence.\nsch: specifies consistent hashing that is based on source IP addresses. Requests from the same source IP address are distributed to the same backend server.\ntch: specifies consistent hashing that is based on four factors: source IP address, destination IP address, source port number, and destination port number. Requests that contain the same preceding information are distributed to the same backend server.\nDefault: wrr",
      "AllowedValues": [
        "wrr",
        "wlc",
        "rr",
        "sch",
        "tch"
      ],
      "Default": "wrr"
    },
    "AclId": {
      "Type": "String",
      "Description": "The ID of the access control list associated with the listener to be created.\nIf the value of the AclStatus parameter is on, this parameter is required."
    },
    "HealthCheck": {
      "Type": "Json",
      "Description": "The properties of health checking setting."
    },
    "IdleTimeout": {
      "Type": "Number",
      "Description": "Specify the idle connection timeout in seconds. Valid value: 1-60 If no request is received during the specified timeout period, Server Load Balancer will temporarily terminate the connection and restart the connection when the next request comes.",
      "MinValue": 1,
      "MaxValue": 60
    },
    "LoadBalancerId": {
      "Type": "String",
      "Description": "The id of load balancer to create listener."
    },
    "BackendServerPort": {
      "Type": "Number",
      "Description": "Backend server can listen on ports from 1 to 65535.",
      "MinValue": 1,
      "MaxValue": 65535
    },
    "Persistence": {
      "Type": "Json",
      "Description": "The properties of persistence."
    },
    "PortRange": {
      "Type": "Json",
      "Description": "Port range, only supports TCP or UDP listener. ListenerPort should be 0 when PortRange is specified.",
      "MinLength": 1,
      "MaxLength": 1
    },
    "AclStatus": {
      "Type": "String",
      "Description": "Indicates whether to enable access control.\nValid values: on | off. Default value: off",
      "AllowedValues": [
        "on",
        "off"
      ],
      "Default": "off"
    },
    "Bandwidth": {
      "Type": "Number",
      "Description": "The bandwidth of network, unit in Mbps(Million bits per second). If the specified load balancer with \"LOAD_BALANCE_ID\" is charged by \"paybybandwidth\" and is created in classic network, each Listener's bandwidth must be greater than 0 and the sum of all of its Listeners' bandwidth can't be greater than the bandwidth of the load balancer.",
      "MinValue": -1,
      "MaxValue": 1000
    },
    "MasterSlaveServerGroupId": {
      "Type": "String",
      "Description": "The id of the MasterSlaveServerGroup which use in listener."
    },
    "ServerCertificateId": {
      "Type": "String",
      "Description": "Server certificate id, for https listener only, this properties is required."
    },
    "HttpConfig": {
      "Type": "Json",
      "Description": "Config for http protocol."
    },
    "AclType": {
      "Type": "String",
      "Description": "The access control type:\n* white: Indicates a whitelist. Only requests from IP addresses or CIDR blocks in the selected access control lists are forwarded. This applies to scenarios in which an application only allows access from specific IP addresses.\nEnabling a whitelist poses some risks to your services.\nAfter a whitelist is enabled, only the IP addresses in the list can access the listener.\nIf you enable a whitelist without adding any IP addresses in the list, no requests are forwarded.\n* black: Indicates a blacklist. Requests from IP addresses or CIDR blocks in the selected access control lists are not forwarded (that is, they are blocked). This applies to scenarios in which an application only denies access from specific IP addresses.\nIf you enable a blacklist without adding any IP addresses in the list, all requests are forwarded.\n\nIf the value of the AclStatus parameter is on, this parameter is required.",
      "AllowedValues": [
        "white",
        "black"
      ]
    },
    "Protocol": {
      "Type": "String",
      "Description": "The load balancer transport protocol to use for routing: http, https, tcp, or udp.",
      "AllowedValues": [
        "http",
        "https",
        "tcp",
        "udp"
      ]
    }
  },
  "Resources": {
    "Listener": {
      "Type": "ALIYUN::SLB::Listener",
      "Properties": {
        "RequestTimeout": {
          "Ref": "RequestTimeout"
        },
        "ListenerPort": {
          "Ref": "ListenerPort"
        },
        "VServerGroupId": {
          "Ref": "VServerGroupId"
        },
        "Description": {
          "Ref": "Description"
        },
        "CACertificateId": {
          "Ref": "CACertificateId"
        },
        "Scheduler": {
          "Ref": "Scheduler"
        },
        "AclId": {
          "Ref": "AclId"
        },
        "HealthCheck": {
          "Ref": "HealthCheck"
        },
        "IdleTimeout": {
          "Ref": "IdleTimeout"
        },
        "LoadBalancerId": {
          "Ref": "LoadBalancerId"
        },
        "BackendServerPort": {
          "Ref": "BackendServerPort"
        },
        "Persistence": {
          "Ref": "Persistence"
        },
        "PortRange": {
          "Ref": "PortRange"
        },
        "AclStatus": {
          "Ref": "AclStatus"
        },
        "Bandwidth": {
          "Ref": "Bandwidth"
        },
        "MasterSlaveServerGroupId": {
          "Ref": "MasterSlaveServerGroupId"
        },
        "ServerCertificateId": {
          "Ref": "ServerCertificateId"
        },
        "HttpConfig": {
          "Ref": "HttpConfig"
        },
        "AclType": {
          "Ref": "AclType"
        },
        "Protocol": {
          "Ref": "Protocol"
        }
      }
    }
  },
  "Outputs": {
    "ListenerPortsAndProtocol": {
      "Description": "The collection of listener.",
      "Value": {
        "Fn::GetAtt": [
          "Listener",
          "ListenerPortsAndProtocol"
        ]
      }
    },
    "LoadBalancerId": {
      "Description": "The id of load balancer",
      "Value": {
        "Fn::GetAtt": [
          "Listener",
          "LoadBalancerId"
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
  AclId:
    Description: 'The ID of the access control list associated with the listener to
      be created.

      If the value of the AclStatus parameter is on, this parameter is required.'
    Type: String
  AclStatus:
    AllowedValues:
    - 'on'
    - 'off'
    Default: 'off'
    Description: 'Indicates whether to enable access control.

      Valid values: on | off. Default value: off'
    Type: String
  AclType:
    AllowedValues:
    - white
    - black
    Description: 'The access control type:

      * white: Indicates a whitelist. Only requests from IP addresses or CIDR blocks
      in the selected access control lists are forwarded. This applies to scenarios
      in which an application only allows access from specific IP addresses.

      Enabling a whitelist poses some risks to your services.

      After a whitelist is enabled, only the IP addresses in the list can access the
      listener.

      If you enable a whitelist without adding any IP addresses in the list, no requests
      are forwarded.

      * black: Indicates a blacklist. Requests from IP addresses or CIDR blocks in
      the selected access control lists are not forwarded (that is, they are blocked).
      This applies to scenarios in which an application only denies access from specific
      IP addresses.

      If you enable a blacklist without adding any IP addresses in the list, all requests
      are forwarded.


      If the value of the AclStatus parameter is on, this parameter is required.'
    Type: String
  BackendServerPort:
    Description: Backend server can listen on ports from 1 to 65535.
    MaxValue: 65535
    MinValue: 1
    Type: Number
  Bandwidth:
    Description: The bandwidth of network, unit in Mbps(Million bits per second).
      If the specified load balancer with "LOAD_BALANCE_ID" is charged by "paybybandwidth"
      and is created in classic network, each Listener's bandwidth must be greater
      than 0 and the sum of all of its Listeners' bandwidth can't be greater than
      the bandwidth of the load balancer.
    MaxValue: 1000
    MinValue: -1
    Type: Number
  CACertificateId:
    Description: CA server certificate id, for https listener only.
    Type: String
  Description:
    Description: The description of the listener.It must be 1 to 80 characters in
      length and can contain letters, digits, hyphens (-), forward slashes (/), periods
      (.), and underscores (_). Chinese characters are supported.
    MaxLength: 80
    Type: String
  HealthCheck:
    Description: The properties of health checking setting.
    Type: Json
  HttpConfig:
    Description: Config for http protocol.
    Type: Json
  IdleTimeout:
    Description: 'Specify the idle connection timeout in seconds. Valid value: 1-60
      If no request is received during the specified timeout period, Server Load Balancer
      will temporarily terminate the connection and restart the connection when the
      next request comes.'
    MaxValue: 60
    MinValue: 1
    Type: Number
  ListenerPort:
    Description: Port for front listener. Range from 0 to 65535.
    MaxValue: 65535
    MinValue: 0
    Type: Number
  LoadBalancerId:
    Description: The id of load balancer to create listener.
    Type: String
  MasterSlaveServerGroupId:
    Description: The id of the MasterSlaveServerGroup which use in listener.
    Type: String
  Persistence:
    Description: The properties of persistence.
    Type: Json
  PortRange:
    Description: Port range, only supports TCP or UDP listener. ListenerPort should
      be 0 when PortRange is specified.
    MaxLength: 1
    MinLength: 1
    Type: Json
  Protocol:
    AllowedValues:
    - http
    - https
    - tcp
    - udp
    Description: 'The load balancer transport protocol to use for routing: http, https,
      tcp, or udp.'
    Type: String
  RequestTimeout:
    Description: 'Specify the request timeout in seconds. Valid value: 1-180 If no
      response is received from the backend server during the specified timeout period,
      Server Load Balancer will stop waiting and send an HTTP 504 error to the client.'
    MaxValue: 180
    MinValue: 1
    Type: Number
  Scheduler:
    AllowedValues:
    - wrr
    - wlc
    - rr
    - sch
    - tch
    Default: wrr
    Description: 'The scheduling algorithm. Valid values:

      wrr: Backend servers that have higher weights receive more requests than those
      that have lower weights.

      wlc: Requests are distributed based on the combination of the weights and connections
      to backend servers. If two backend servers have the same weight, the backend
      server that has fewer connections receives more requests.

      rr: Requests are distributed to backend servers in sequence.

      sch: specifies consistent hashing that is based on source IP addresses. Requests
      from the same source IP address are distributed to the same backend server.

      tch: specifies consistent hashing that is based on four factors: source IP address,
      destination IP address, source port number, and destination port number. Requests
      that contain the same preceding information are distributed to the same backend
      server.

      Default: wrr'
    Type: String
  ServerCertificateId:
    Description: Server certificate id, for https listener only, this properties is
      required.
    Type: String
  VServerGroupId:
    Description: The id of the VServerGroup which use in listener.
    Type: String
Resources:
  Listener:
    Properties:
      AclId:
        Ref: AclId
      AclStatus:
        Ref: AclStatus
      AclType:
        Ref: AclType
      BackendServerPort:
        Ref: BackendServerPort
      Bandwidth:
        Ref: Bandwidth
      CACertificateId:
        Ref: CACertificateId
      Description:
        Ref: Description
      HealthCheck:
        Ref: HealthCheck
      HttpConfig:
        Ref: HttpConfig
      IdleTimeout:
        Ref: IdleTimeout
      ListenerPort:
        Ref: ListenerPort
      LoadBalancerId:
        Ref: LoadBalancerId
      MasterSlaveServerGroupId:
        Ref: MasterSlaveServerGroupId
      Persistence:
        Ref: Persistence
      PortRange:
        Ref: PortRange
      Protocol:
        Ref: Protocol
      RequestTimeout:
        Ref: RequestTimeout
      Scheduler:
        Ref: Scheduler
      ServerCertificateId:
        Ref: ServerCertificateId
      VServerGroupId:
        Ref: VServerGroupId
    Type: ALIYUN::SLB::Listener
Outputs:
  ListenerPortsAndProtocol:
    Description: The collection of listener.
    Value:
      Fn::GetAtt:
      - Listener
      - ListenerPortsAndProtocol
  LoadBalancerId:
    Description: The id of load balancer
    Value:
      Fn::GetAtt:
      - Listener
      - LoadBalancerId
            
```

更多示例，请参见创建负载均衡监听、克隆负载均衡实例、上传证书、创建扩展域名、创建服务器组并添加后端服务器到负载均衡实例、为HTTP或HTTPS监听添加转发规则和将后端服务器添加到服务器组的组合示例：[JSON示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/SLB/JSON/Listener.json)和[YAML示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/SLB/YAML/Listener.yml)。

