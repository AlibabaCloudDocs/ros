# ALIYUN::SLB::Listener

ALIYUN::SLB::Listener is used to create a listener for a Server Load Balancer \(SLB\) instance.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|MasterSlaveServerGroupId|String|No|No|The ID of the primary/secondary server group.|None|
|AclStatus|String|No|No|Specifies whether to enable access control.|Default value: on. Valid values: -   on
-   off |
|AclId|String|No|No|The ID of the network access control list \(ACL\) that is associated with the listener.|This parameter is required when the AclStatus parameter is set to on.|
|AclType|String|No|No|The type of the ACL.|Valid values: -   white: specifies the ACL as a whitelist. Only requests from the IP addresses or CIDR blocks in the ACL are forwarded. Whitelists are applicable to scenarios where you want an application to be accessed only from specific IP addresses. Risks may occur if the whitelist is improperly set. After a whitelist is configured, only the IP addresses specified in the whitelist are able to access the SLB listener. If a whitelist is enabled without IP addresses specified, the SLB listener does not forward requests.
-   black: specifies the ACL as a blacklist. All requests from the IP addresses or CIDR blocks in the ACL are rejected. Blacklists apply to scenarios that require you to block access from specific IP addresses to an application. If a blacklist is enabled but the corresponding ACL does not contain IP addresses, the SLB listener forwards all requests. This parameter is required when the AclStatus parameter is set to on. |
|Protocol|String|Yes|No|The Internet protocol over which the listener forwards requests.|Valid values: -   http
-   https
-   tcp
-   udp |
|ListenerPort|Integer|Yes|No|The frontend port that is used by the SLB instance.|Valid values: 1 to 65535.|
|Bandwidth|Integer|Yes|No|The bandwidth limit of the listener.|Valid values: 1 to 1000 and -1. Unit: Mbit/s.

The value must meet the following requirements:

-   For a pay-by-bandwidth Internet-facing SLB instance, this parameter cannot be set to -1. The sum of bandwidth limit values that you specify for all listeners of the SLB instance cannot exceed the bandwidth limit of the SLB instance.
-   For a pay-by-data-transfer Internet-facing SLB instance, this value can be set to -1. This indicates that the bandwidth is unlimited. |
|BackendServerPort|Integer|Yes|No|The backend port that is used by the SLB instance.|Valid values: 1 to 65535.|
|LoadBalancerId|String|Yes|No|The ID of the SLB instance.|None|
|HealthCheck|Map|No|No|The health check settings of the listener.|For more information, see [HealthCheck properties](#section_2za_snc_vkm).|
|Persistence|Map|No|Yes|The persistence properties.|For more information, see [Persistence properties](#section_1bw_bgv_atk).|
|Scheduler|String|No|No|The scheduling algorithm.|Default value: wrr. Valid values: -   wrr
-   wlc |
|CACertificateId|String|No|No|The ID of the CA certificate.|This parameter is valid only when the Protocol parameter is set to https.|
|ServerCertificateId|String|No|Yes|The ID of the server certificate.|This parameter is required and valid only when the Protocol parameter is set to https.|
|VServerGroupId|String|No|No|The ID of the vServer group.|None|
|RequestTimeout|Integer|No|No|The timeout period of a request.|Valid values: 1 to 180. Unit: seconds. |
|IdleTimeout|Integer|No|No|The timeout period of idle connections.|Valid values: 1 to 60. Unit: seconds. |
|HttpConfig|Map|No|No|The HTTP configurations.|For more information, see [HttpConfig properties](#section_iz0_jz0_x1b).|
|Description|String|No|No|The description of the listener.|The description must be 1 to 80 characters in length and can contain letters, digits, hyphens \(-\), forward slashes \(/\), periods \(.\),and underscores \(\_\).|
|PortRange|List|No|No|The range of ports on which the SLB instance listens.|Set StartPort to 1 and EndPort to 65535. For more information, see [PortRange property](#section_e47_s0b_2es). |

## HealthCheck syntax

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
  "Port": Integer
}
```

## HealthCheck properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Domain|String|No|No|The domain name that is used for health checks.|Valid values: -   $\_ip
-   Custom string: A custom string must be 1 to 80 characters in length and can contain letters, digits, hyphens \(-\), and periods \(.\).
-   An empty string

**Note:** When this parameter is set to $\_ip or left empty, the SLB instance uses the private IP addresses of backend servers as the domain names for health checks. |
|Interval|Integer|No|No|The interval between two consecutive health checks.|Valid values: 1 to 5. Unit: seconds. |
|URI|String|No|No|The URI that is used for health checks.|The URI must be 1 to 80 characters in length and can contain letters, digits, hyphens \(-\), forward slashes \(/\), periods \(.\), percent signs \(%\), question marks \(?\), number signs \(\#\), and ampersands \(&\). It must start with a forward slash \(/\).|
|HttpCode|String|No|No|The HTTP status code that indicates the health check is successful.|Default value: http\_2xx. Valid values: -   http\_2xx
-   http\_3xx
-   http\_4xx
-   http\_5xx

Separate multiple HTTP status codes with commas \(,\). |
|HealthyThreshold|Integer|No|No|The threshold that is used to determine that the backend servers are healthy. This value indicates the number of consecutive successful health checks required before the health status of a backend server can be changed from fail to success.|Valid values: 1 to 10.|
|HealthCheckType|String|No|No|The health check type.|Valid values:-   tcp
-   http |
|Timeout|Integer|No|No|The maximum amount of time to wait for a health check response.|Valid values: 1 to 50.

Unit: seconds.

**Note:** This parameter is valid only when its value is greater than or equal to that of the Interval parameter. Otherwise, this parameter is overridden by the Interval value. |
|UnhealthyThreshold|Integer|No|No|The threshold that is used to determine that the backend servers are unhealthy. This value indicates the number of consecutive failed health checks required before the health status of a backend server can be changed from success to fail.|Valid values: 1 to 10.|
|Port|Integer|No|No|The port used for health checks.|Valid values: 0 to 65535.|

## Persistence syntax

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

## Persistence properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|StickySession|String|No|Yes|Specifies whether to enable session persistence.|Valid values: -   on
-   off |
|PersistenceTimeout|Integer|No|Yes|The maximum amount of time to wait for session persistence.|Valid values: 0 to 1000. Default value: 0. A value of 0 indicates that connection persistence is disabled.

Unit: seconds. |
|CookieTimeout|Integer|No|Yes|The maximum amount of time to wait before the session cookie expires.|Valid values: 1 to 86400.

Unit: seconds.

**Note:** This parameter is required when the StickySession parameter is set to on and the StickySessionType parameter is set to insert. |
|XForwardedFor|String|No|Yes|Specifies whether to use the X-Forwarded-For header field to obtain the real IP address of a client.|Set the value to on.|
|XForwardedFor\_proto|String|No|Yes|Specifies whether to use the X-Forwarded-Proto header field to obtain the listener protocol of the SLB instance.|Default value: off. Valid values:-   on
-   off |
|XForwardedFor\_SLBID|String|No|Yes|Specifies whether to use the SLB-ID header field to obtain the ID of the SLB instance.|Default value: off. Valid values:-   on
-   off |
|XForwardedFor\_SLBIP|String|No|Yes|Specifies whether to use the SLB-IP header field to obtain the real IP address of a client.|Default value: off. Valid values:-   on
-   off |
|Cookie|String|No|Yes|The cookie to be configured on the backend server.|The cookie must be 1 to 200 characters in length. It cannot start with a dollar sign \($\). The cookie can contain letters and digits. It cannot contain commas \(,\), semicolons \(;\), or spaces. **Note:** This parameter is required when the StickySession parameter is set to on and the StickySessionType parameter is set to server. |
|StickySessionType|String|No|Yes|The method that is used to handle a cookie.|Valid values:-   insert: inserts a cookie.
-   server: rewrites a cookie.

**Note:** This parameter is required when the StickySession parameter is set to on. |

## HttpConfig syntax

```
"HttpConfig": {
  "ForwardPort": Integer,
  "ListenerForward": String
}
```

## HttpConfig properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ForwardPort|Integer|No|No|The port that is used to redirect HTTP requests to HTTPS.|Valid values: 1 to 65535. Default value: 443. |
|ListenerForward|String|No|No|Specifies whether to enable redirection from HTTP to HTTPS.|Default value: off. Valid values: -   on
-   off |

## PortRange syntax

```
"PortRange": [
  {
    "StartPort": Integer,
    "EndPort": Integer
  }
]
```

## PortRange property

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|StartPort|Integer|Yes|No|The start of the port range.|Set the value to 1.|
|EndPort|Integer|Yes|No|The end of the port range.|Set the value to 65535.|

## Response parameters

Fn::GetAtt

-   LoadBalancerId: the unique ID of the SLB instance.
-   ListenerPortsAndProtocol: the ports and protocols used by the SLB listener.

## Examples

`JSON` format

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

`YAML` format

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

For more examples, visit [Listener.json](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/SLB/JSON/Listener.json) and [Listener.yml](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/SLB/YAML/Listener.yml). In the examples, the ALIYUN::SLB::Listener, ALIYUN::SLB::LoadBalancerClone, ALIYUN::SLB::Certificate, ALIYUN::SLB::DomainExtension, ALIYUN::SLB::VServerGroup, ALIYUN::SLB::Rule, and ALIYUN::SLB::BackendServerToVServerGroupAddition resource types are involved.

