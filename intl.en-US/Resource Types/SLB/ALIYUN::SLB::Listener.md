# ALIYUN::SLB::Listener {#concept_51202_zh .concept}

ALIYUN::SLB::Listener is used to create a listener for an SLB instance.

## Syntax {#section_vsm_3bz_lfb .section}

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

## Properties {#section_y45_lbz_lfb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|AclStatus|String|No|No|Specifies whether to enable access control on the listener to be created.|Valid values: on and off. Default value: off.|
|AclId|String|No|No|The ID of the access control list \(ACL\) associated with the listener. This parameter is required when the AclStatus parameter is set to on.|None|
|AclType|String|No|No|The filter type of the specified ACL. white: specifies the ACL as a whitelist. Only requests from the IP addresses or CIDR blocks in the ACL are forwarded. Whitelists are applicable in scenarios where you want an application to only be accessed from specific IP addresses. Configuring a whitelist poses risks to your services. After a whitelist is configured, only the IP addresses in the whitelist are able to access the SLB listener. If a whitelist is enabled without any IP addresses specified in the ACL, the SLB listener will not forward any requests. black: specifies the ACL as a blacklist. Requests from the IP addresses or CIDR blocks in the ACL are not forwarded. Blacklists are applicable in scenarios where you want an application to only be denied access from specific IP addresses. If a blacklist is enabled without any IP addresses specified in the ACL, the SLB listener will forward all requests. This parameter is required when the AclStatus parameter is set to on.|Valid values: white and black|
|Protocol|String|Yes|No|The Internet protocol over which the listener will forward requests.|Valid values: http, https, tcp, and udp|
|ListenerPort|Integer|Yes|No|The front-end port number used by the SLB instance.|Valid values: 1 to 65535|
|Bandwidth|Integer|Yes|No|The peak bandwidth of the listener. Unit: Mbit/s.|Valid values: -1 and \[1, 1000\]. A value of -1 specifies unlimited bandwidth. For an SLB instance that is connected to the public network and billed by fixed bandwidth, this parameter cannot be set to -1 and the sum of peak bandwidths assigned to different listeners cannot exceed the bandwidth value specified when the SLB instance is created. For an SLB instance that is connected to the public network and billed by traffic, this parameter can be set to -1.|
|BackendServerPort|Integer|Yes|No|The back-end port number used by the SLB instance.|Valid values: 1 to 65535|
|LoadBalancerId|String|Yes|No|The ID of the SLB instance.|None|
|HealthCheck|Map|No|No|The health check settings of the listener.|None|
|Persistence|Map|No|No|Specifies persistence properties.|None|
|Scheduler|String|No|No|The algorithm used to direct traffic to individual servers.| Valid values: wrr and wlc

 Default value: wrr

 |
|CACertificateId|String|No|No|The ID of the CA certificate.|This parameter is only valid for HTTPS listeners.|
|ServerCertificateId|String|No|No|The ID of the server certificate.|This parameter is only valid for HTTPS listeners, and is required.|
|VServerGroupId|String|No|No|The ID of the VServer group.|None|
|RequestTimeout|Integer|No|No|The request timeout period. Unit: seconds.|Valid values: 1 to 180|
|IdleTimeout|Integer|No|No|The idle connection timeout period. Unit: seconds.|Valid values: 1 to 60|

## HealthCheck syntax {#section_rwp_rbz_lfb .section}

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

## HealthCheck properties {#section_2za_snc_vkm .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Domain|String|No|No|The domain name used for health checks.| The value can be $\_ip, a custom string, or an empty string.

 A custom string must be 1 to 80 characters in length and can only contain letters, digits, hyphens \(-\), and periods \(.\).

 When this parameter is set to $\_ip or left blank, the SLB instance uses the private IP addresses of back-end servers as the domain names for health checks.

 |
|Interval|Integer|No|No|The time interval between consecutive health checks. Unit: seconds.|Valid values: 1 to 5|
|URI|String|No|No|The URI used for health checks.|The value must be 1 to 80 characters in length and can contain letters, digits, hyphens \(-\), forward slashes \(/\), periods \(.\), percent signs \(%\), question marks \(?\), number signs \(\#\), and ampersands \(&\). It must start with a forward slash \(/\).|
|HttpCode|String|No|No|The HTTP status code that indicates a positive health status of the back-end servers.| Use commas \(,\) to separate multiple HTTP status codes.

 Valid values: http\_2xx, http\_3xx, http\_4xx, and http\_5xx

 Default value: http\_2xx

 |
|HealthyThreshold|Integer|No|No|The threshold used to determine that the back-end servers are healthy. This value indicates the number of consecutive successful health checks required before the health status of a back-end server can be changed from fail to success.|Valid values: 1 to 10|
|Timeout|Integer|No|No|The length of time to wait for the response from a health check. Unit: seconds.| Valid values: 1 to 50

 **Note:** This parameter is only valid when its value is greater than or equal to that of the Interval parameter. Otherwise, this parameter will be overridden by the Interval value.

 |
|UnhealthyThreshold|Integer|No|No|The threshold used to determine that the back-end servers are unhealthy. This value indicates the number of consecutive failed health checks required before the health status of a back-end server can be changed from success to fail.|Valid values: 1 to 10|
|Port|Integer|No|No|The port number used for health checks.|Valid values: 0 to 65535|

## Persistence syntax {#section_8lm_sz6_buh .section}

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

## Persistence properties {#section_1bw_bgv_atk .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|StickySession|String|Yes|No|Specifies whether to enable session persistence.|Valid values: on and off|
|PersistenceTimeout|Integer|No|No|The maximum duration that the client can be connected to the server. Unit: seconds.| Valid values: 0 to 1000.

 The default value is 0, which indicates that connection persistence is disabled.

 |
|CookieTimeout|Integer|No|No|The maximum duration a cookie can be retained before it expires. Unit: seconds.| This parameter is required when the StickySession parameter is set to on and the StickySessionType parameter is set to insert. In other cases, this parameter is ignored.

 Valid values: 1 to 86400

 |
|XForwardedFor|String|No|No|Specifies whether to use the X-Forwarded-For header field to obtain the real IP address of the client.| Valid values: on and off

 Default value: on

 |
|Cookie|String|No|No|The cookie configured on the back-end server.| This parameter is required when the StickySession parameter is set to on and the StickySessionType parameter is set to server. In other cases, this parameter is ignored.

 The parameter value must be 1 to 200 characters in length and follow the RFC 2965 standard. It can only contain ASCII characters. It cannot contain commas \(,\), semicolons \(;\), or spaces, and cannot start with a dollar sign \($\).

 |
|StickySessionType|String|No|No|The method used to handle the cookie.| This parameter is required when the StickySession parameter is set to on. When the StickySession parameter is set to off, this parameter is ignored.

 Valid values: insert and server

 insert specifies SLB to add a cookie to the first response from a back-end server. Then, the next request contains the cookie and the listener distributes the request to the same back-end server. server specifies SLB to overwrite the original cookie when a new cookie is set. The next time the client carries the new cookie to access SLB, the listener distributes the request to the previously recorded back-end server.|

## Response parameters {#section_zrf_qcz_lfb .section}

**Fn::GetAtt**

-   LoadBalancerId: the unique ID of the SLB instance.
-   ListenerPortsAndProtocol: an array consisting of the ports and protocols used by the SLB listener.

## Examples {#section_c4m_tcz_lfb .section}

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

