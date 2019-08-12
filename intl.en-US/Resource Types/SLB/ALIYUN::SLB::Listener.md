# ALIYUN::SLB::Listener {#concept_51202_zh .concept}

Creates a listener for your server load balancer \(SLB\) instance.

## Syntax {#section_vsm_3bz_lfb .section}

```language-json
{
  "Type" : "ALIYUN::SLB::Listener",
  "Properties" : {
    "Protocol" : String,
    "HealthCheck" : Map,
    "ListenerPort" : Integer,
    "Persistence" : Map,
    "Bandwidth" : Integer,
    "BackendServerPort" : Integer,
    "Scheduler" : String,
    "LoadBalancerId" : String,
    "CACertificateId" : String,
    "ServerCertificateId" : String,
    "VServerGroupId" : String
  }
}
```

## Properties {#section_y45_lbz_lfb .section}

|Property Name|Type|Required|Editable|Description|Validity|
|-------------|----|--------|--------|-----------|--------|
|Protocol|String|Yes|No|The IP protocol.|Valid values: http | https | tcp | udp.|
|ListenerPort|Integer|Yes|No|The frontend port used to receive requests and forward the requests to backend servers.|Value range: 1 to 65535.|
|Bandwidth|Integer|Yes|No|The peak bandwidth of the SLB listener.|Valid values: -1 | 1 to 1000. Unit: Mbit/s. For an instance that is connected to the public network and billed by bandwidth, the parameter cannot be set to -1, and the sum of the peak bandwidth assigned to each listener cannot exceed the bandwidth limit specified when the SLB instance is created. For an instance that is connected to the public network and billed by traffic, the parameter can be set to –1, indicating that no peak bandwidth limit is applied.|
|BackendServerPort|Integer|Yes|No|The backend port used to receive requests.|Value range: 1 to 65535.|
|LoadBalancerId|String|Yes|No|The ID of the SLB instance.|N/A|
|HealthCheck|Map|No|No|The health check settings.|N/A|
|Persistence|Map|No|No|Specifies persistence properties.|N/A|
|Scheduler|String|No|No|The algorithm for directing traffic to individual servers.| Valid values: wrr | wlc.

 Default value: wrr.

 |
|CACertificateId|String|No|No|The ID of a certificate issued by a certification authority \(CA\).|The CA certificate is only applicable to HTTPS listeners.|
|ServerCertificateId|String|No|No|The ID of the server certificate.|This parameter is required and only applicable to HTTPS listeners.|
|VServerGroupId|String|No|No|The ID of the VServer group.|N/A|

## HealthCheck syntax {#section_rwp_rbz_lfb .section}

```language-json
"HealthCheck" : {
  "Domain" : String,
  "Interval" : Integer,
  "URI" : String,
  "HttpCode" : String,
  "HealthyThreshold" : Integer,
  "Timeout" : Integer,
  "UnhealthyThreshold" : Integer,
  "Port" : Integer
}
```

## HealthCheck properties { .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Domain|String|No|No|The domain name used for health checks.| Valid values: $\_ip | custom string | null.

 A custom string must be 1 to 80 characters in length and can contain letters, digits, hyphens \(-\), and periods \(.\) only.

 When this parameter is set to $\_ip or null, the SLB instance uses the private IP addresses of backend servers as the domains for health checks.

 |
|Interval|Integer|No|No|The time interval between two consecutive health checks.|Value range: 1 to 5. Unit: second.|
|URI|String|No|No|The URI used for health checks.|The value must be 1 to 80 characters in length, including letters, digits, hyphens \(-\), slashes \(/\), periods \(.\), percent signs \(%\), question marks \(?\), number signs \(\#\), and ampersands \(&\). It must start with a slash \(/\).|
|HttpCode|String|No|No|The HTTP status code that indicates a positive health status of the servers.| Use half-width commas \(,\) to separate multiple HTTP status codes.

 Valid values: http\_2xx | http\_3xx | http\_4xx | http\_5xx.

 Default value: http\_2xx.

 |
|HealthyThreshold|Integer|No|No|The threshold used to determine that the servers are in a healthy state. This value indicates the number of consecutive successful health checks that are required to change the health status of the backend servers from fail to success.|Value range: 1 to 10.|
|Timeout|Integer|No|No|The maximum response time for a health check.| Value range: 1 to 50. Unit: second.

 **Note:** This parameter is only applicable when the Timeout value is equal to or greater than the Interval value. Otherwise, this parameter is overridden by the Interval value.

 |
|UnhealthyThreshold|Integer|No|No|The threshold used to determine that the servers are not in a healthy state. This value indicates the number of consecutive failed health checks that are required to change the health status of the backend servers from success to fail.|Value range: 1 to 10.|
|Port|Integer|No|No|The port used for health checks.|Value range: 0 to 65535.|

## Persistence syntax { .section}

```language-json
"Persistence" : {
  "PersistenceTimeout" : Integer,
  "CookieTimeout" : Integer,
  "XForwardedFor" : String,
  "Cookie" : String,
  "StickySession" : String,
  "StickySessionType" : String,
}
```

## Persistence properties { .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|StickySession|String|Yes|No|Specifies whether to enable session persistence.|Valid values: on | off.|
|PersistenceTimeout|Integer|No|No|The maximum duration the client is connected to the server.| Value range: 0 to 1000. Unit: second.

 Default value: 0. The value 0 indicates that the connection is disabled.

 |
|CookieTimeout|Integer|No|No|The maximum duration a cookie can be retained before it expires.| This parameter is required if the StickySession parameter is set to on and the StickySessionType parameter is set to insert. In other cases, this parameter is inapplicable.

 Value range: 1 to 86400. Unit: second.

 |
|XForwardedFor|String|No|No|Specifies whether to use the X-Forwarded-For record to obtain visitors' real IP addresses.| Valid values: on | off.

 Default value: on.

 |
|Cookie|String|No|No|A cookie set by the server.| This parameter is required when the StickySession parameter is set to on and the StickySessionType parameter is set to server. In other cases, this parameter is inapplicable.

 The parameter must be 1 to 200 characters in length and follow the RFC 2965 standard. It can contain only ASCII characters, excluding commas \(,\), semicolons \(;\), or spaces, and cannot start with a dollar sign \($\).

 |
|StickySessionType|String|No|No|The method used to handle cookies.| This parameter is required when the StickySession parameter is set to on. When the StickySession parameter is set to off, this parameter is inapplicable.

Valid values: insert | server.

The value insert indicates that the SLB instance inserts cookies into the response message that is returned by the backend servers. The value "server" indicates that the SLB instance reads cookies from the backend servers.|

## Response elements {#section_zrf_qcz_lfb .section}

**Fn::GetAtt**

-   LoadBalancerId: indicates the unique ID of the SLB instance.
-   ListenerPortsAndProtocol: indicates the ports and protocols used by the SLB listener, displayed in an array.

## Example {#section_c4m_tcz_lfb .section}

```language-json
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
     "Value" : {"Fn::GetAtt": ["LoadBalancer", "LoadBalancerId"]}
  }
  }
}
```

