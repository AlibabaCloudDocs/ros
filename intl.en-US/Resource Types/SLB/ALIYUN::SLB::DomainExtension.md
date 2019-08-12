# ALIYUN::SLB::DomainExtension {#concept_o1m_2g3_tgb .concept}

Creates a domain name extension.

## Syntax {#section_ey2_ycz_lfb .section}

```language-json
{
  "Type": "ALIYUN::SLB::DomainExtension",
  "Properties": {
    "Domain":  String,
    "ListenerPort": Integer,
    "ServerCertificateId": String,
    "LoadBalancerId": String
  }
}
```

## Properties {#section_n13_22z_lfb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Domain|String|Yes|No|The domain name.|N/A|
|ListenerPort|Integer|Yes|No|The frontend port used to receive requests and forward the requests to backend servers over the HTTPS protocol.|Valid values: 1 to 65535.|
|ServerCertificateId|String|Yes|Yes|The ID of the certificate that is issued for the domain name.|N/A|
|LoadBalancerId|String|Yes|No|The SLB instance ID.|N/A|

## Response elements {#section_wfc_q2z_lfb .section}

**Fn::GetAtt**

-   DomainExtensionId: indicates the ID of the domain name extension.
-   ListenerPort: indicates the frontend port used to receive requests and forward the requests to backend servers..

## Example {#section_lcd_s2z_lfb .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "DomainExtension": {
      "Type": "ALIYUN::SLB::DomainExtension",
      "Properties": {
        "Domain": "*.example1.com",
        "ListenerPort": "443",
        "ServerCertificateId": "123157908552****_166f8204689_1714763408_70998****",
        "LoadBalancerId": "lb-bp1o94dp5i6earr9g****"
      }
    }
  },
  "Outputs": {
    "DomainExtensionId": {
      "Value": {
        "Fn::GetAtt": [
          "DomainExtension",
          "DomainExtensionId"
        ]
      }
    },
    "ListenerPort": {
      "Value": {
        "Fn::GetAtt": [
          "DomainExtension",
          "ListenerPort"
        ]
      }
    }
  }
}
```

