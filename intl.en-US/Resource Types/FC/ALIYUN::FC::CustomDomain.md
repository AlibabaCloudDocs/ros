# ALIYUN::FC::CustomDomain {#concept_xsc_jmm_4fb .concept}

ALIYUN::FC::CustomDomain is used to create a custom domain name.

## Syntax {#section_bnr_dxz_lfb .section}

``` {#codeblock_63x_otb_ouw .language-json}
{
  "Type": "ALIYUN::FC::CustomDomain",
  "Properties": {
    "ApiVersion": String,
    "Protocol": String,
    "RouteConfig": Map,
    "CertConfig": Map,
    "DomainName": String
  }
}
```

## Properties {#section_ms1_ejh_j5s .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|ApiVersion|String|No|Yes|The API version to be used.|None|
|Protocol|String|Yes|Yes|The protocol type supported by the custom domain name. Valid values: HTTP and HTTP,HTTPS.|None|
|RouteConfig|Map|No|Yes|The routing table that maps paths to functions when the functions are invoked with the custom domain name.|None|
|CertConfig|Map|No|Yes|The HTTPS certificate information.|None|
|DomainName|String|Yes|No|The custom domain name.|None|

## RouteConfig syntax {#section_rx1_6bh_1y4 .section}

``` {#codeblock_q2e_6vj_p9j .language-json}
"RouteConfig": {
  "Routes": List
}
```

## RouteConfig properties {#section_22v_dyx_x8m .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Routes|List|Yes|Yes|An array of routes.|None|

## CertConfig syntax {#section_m1j_qg3_072 .section}

``` {#codeblock_ynh_4po_on7 .language-json}
"CertConfig": {
  "CertName": String,
  "PrivateKey": String,
  "Certificate": String
}
```

## CertConfig properties {#section_b4z_hlt_lsk .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|CertName|String|Yes|Yes|The name of the certificate.|None|
|PrivateKey|String|Yes|Yes|The private key of the certificate.|None|
|Certificate|String|Yes|Yes|The certificate.|None|

## Response parameters {#section_tga_j7s_mui .section}

**Fn::GetAtt**

DomainName: the domain name.

## Examples {#section_zhq_syz_lfb .section}

``` {#codeblock_6aa_ts1_sbz .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "CustomDomain": {
      "Type": "ALIYUN::FC::CustomDomain",
      "Properties": {
        "CertConfig": {
          "Ref": "CertConfig"
        },
        "Protocol": {
          "Ref": "Protocol"
        },
        "RouteConfig": {
          "Ref": "RouteConfig"
        },
        "ApiVersion": {
          "Ref": "ApiVersion"
        },
        "DomainName": {
          "Ref": "DomainName"
        }
      }
    }
  },
  "Parameters": {
    "CertConfig": {
      "Type": "Json",
      "Description": "Certificate information"
    },
    "Protocol": {
      "Type": "String",
      "Description": "Valid values: HTTP and HTTP,HTTPS"
    },
    "RouteConfig": {
      "Type": "Json",
      "Description": "The routing table that maps paths to functions when the functions are invoked with the custom domain name."
    },
    "ApiVersion": {
      "Type": "String",
      "Description": "API version"
    },
    "DomainName": {
      "Type": "String",
      "Description": "Domain name"
    }
  },
  "Outputs": {
    "DomainName": {
      "Description": "Domain name",
      "Value": {
        "Fn::GetAtt": [
          "CustomDomain",
          "DomainName"
        ]
      }
    }
  }
}
```

