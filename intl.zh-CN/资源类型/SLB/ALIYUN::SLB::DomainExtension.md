# ALIYUN::SLB::DomainExtension {#concept_o1m_2g3_tgb .concept}

ALIYUN::SLB::DomainExtension类型用于创建扩展域名。

## 语法 {#section_ey2_ycz_lfb .section}

``` {#codeblock_75o_kze_1nh .language-json}
{
  "Type": "ALIYUN::SLB::DomainExtension",
  "Properties": {
    "Domain": String,
    "ListenerPort": Integer,
    "ServerCertificateId": String,
    "LoadBalancerId": String
  }
}
```

## 属性 {#section_n13_22z_lfb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Domain|String|是|否|域名。|无|
|ListenerPort|Integer|是|否|负载均衡实例HTTPS监听的前端端口。|取值：1~65535。|
|ServerCertificateId|String|是|是|与域名对应的证书ID。|无|
|LoadBalancerId|String|是|否|负载均衡实例的ID。|无|

## 返回值 {#section_wfc_q2z_lfb .section}

**Fn::GetAtt**

-   DomainExtensionId: 创建的扩展域名ID。
-   ListenerPort: 负载均衡实例前端使用的端口。

## 示例 {#section_lcd_s2z_lfb .section}

``` {#codeblock_tfp_fwz_x3w .language-json}
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

