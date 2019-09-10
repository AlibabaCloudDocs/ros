# ALIYUN::VPC::SslVpnClientCert {#concept_xsc_jmm_4fb .concept}

ALIYUN::VPC::SslVpnClientCert类型用于调用CreateSslVpnClientCert接口创建SSL-VPN客户端证书。

## 语法 {#section_bnr_dxz_lfb .section}

``` {#codeblock_42y_0kt_mcu .language-json}
{
  "Type": "ALIYUN::VPC::SslVpnClientCert",
  "Properties": {
    "Name": String,
    "SslVpnServerId": String
  }
}
```

## 属性 {#section_z06_lf6_ug6 .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Name|String|否|是|客户端证书的名称。长度为2-128个字符，必须以字母或中文开头，可包含数字，点号（.），下划线（\_）和短横线（-）。但不能以http://或https://开头。|无。|
|SslVpnServerId|String|是|否|SSL-VPN服务端的ID。|无。|

## 返回值 {#section_otu_vjp_0cv .section}

**Fn::GetAtt**

-   SslVpnClientCertId: 客户端证书的ID。

## 示例 {#section_zhq_syz_lfb .section}

``` {#codeblock_s84_uzb_aco .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "SslVpnClientCert": {
      "Type": "ALIYUN::VPC::SslVpnClientCert",
      "Properties": {
        "Name": {
          "Ref": "Name"
        },
        "SslVpnServerId": {
          "Ref": "SslVpnServerId"
        }
      }
    }
  },
  "Parameters": {
    "Name": {
      "MinLength": 2,
      "Type": "String",
      "Description": "The name of the client certificate.\nThe length is 2-128 characters and must start with a letter or Chinese. It can contain numbers, periods (.), underscores (_), and dashes (-). But it can't start with http:// or https://.",
      "MaxLength": 128
    },
    "SslVpnServerId": {
      "Type": "String",
      "Description": "ID of the SSL-VPN server."
    }
  },
  "Outputs": {
    "SslVpnClientCertId": {
      "Description": "The ID of the client certificate.",
      "Value": {
        "Fn::GetAtt": [
          "SslVpnClientCert",
          "SslVpnClientCertId"
        ]
      }
    }
  }
}
```

