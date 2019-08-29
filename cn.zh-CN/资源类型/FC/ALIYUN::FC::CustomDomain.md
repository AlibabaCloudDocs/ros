# ALIYUN::FC::CustomDomain {#concept_xsc_jmm_4fb .concept}

ALIYUN::FC::CustomDomain类型用于自定义域名。

## 语法 {#section_bnr_dxz_lfb .section}

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

## 属性 {#section_ms1_ejh_j5s .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ApiVersion|String|否|是|API 版本。|无。|
|Protocol|String|是|是|HTTP 或 HTTP，HTTPS。|无。|
|RouteConfig|Map|否|是|路由表：自定义域名访问时的 path 到 function 的映射。|无。|
|CertConfig|Map|否|是|HTTPS 证书信息。|无。|
|DomainName|String|是|否|域名。|无。|

## RouteConfig 语法 {#section_rx1_6bh_1y4 .section}

``` {#codeblock_q2e_6vj_p9j .language-json}
"RouteConfig": {
  "Routes": List
}
```

## RouteConfig 属性 {#section_22v_dyx_x8m .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Routes|List|是|是|路由的数组。|无。|

## CertConfig 语法 {#section_m1j_qg3_072 .section}

``` {#codeblock_ynh_4po_on7 .language-json}
"CertConfig": {
  "CertName": String,
  "PrivateKey": String,
  "Certificate": String
}
```

## CertConfig 属性 {#section_b4z_hlt_lsk .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|CertName|String|是|是|证书的自定义名字。|无。|
|PrivateKey|String|是|是|私钥。|无。|
|Certificate|String|是|是|证书。|无。|

## 返回值 {#section_tga_j7s_mui .section}

**Fn::GetAtt**

DomainName：域名。

## 示例 {#section_zhq_syz_lfb .section}

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
      "Description": "certificate info"
    },
    "Protocol": {
      "Type": "String",
      "Description": "HTTP or HTTP,HTTPS"
    },
    "RouteConfig": {
      "Type": "Json",
      "Description": "Routing table: path to function mapping when a function is called with a custom domain name"
    },
    "ApiVersion": {
      "Type": "String",
      "Description": "api version"
    },
    "DomainName": {
      "Type": "String",
      "Description": "domain name"
    }
  },
  "Outputs": {
    "DomainName": {
      "Description": "domain name",
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

