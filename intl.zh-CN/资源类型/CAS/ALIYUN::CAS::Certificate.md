# ALIYUN::CAS::Certificate {#concept_xsc_jmm_4fb .concept}

ALIYUN::CAS::Certificate类型用于添加证书。

## 语法 {#section_bnr_dxz_lfb .section}

``` {#codeblock_b6p_jsy_usj .language-json}
{
  "Type": "ALIYUN::CAS::Certificate",
  "Properties": {
    "Lang": String,
    "Cert": String,
    "SourceIp": String,
    "Name": String,
    "Key": String
  }
}
```

## 属性 {#section_syi_xjx_tf4 .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Lang|String|否|否|指定请求和接收消息的语言类型。|无。|
|Cert|String|是|否|指定证书内容。要使用PEM编码格式。|无。|
|SourceIp|String|否|否|指定请求的来源IP地址。|无。|
|Name|String|是|否|自定义证书名称。一个用户下的证书名称不能重复。|无。|
|Key|String|是|否|指定证书私钥内容。要使用PEM编码格式。|无。|

## 返回值 {#section_f33_q94_wux .section}

Fn::GetAtt

-   CertId: 证书ID。

## 示例 {#section_zhq_syz_lfb .section}

``` {#codeblock_npa_wbf_fxb .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "Certificate": {
      "Type": "ALIYUN::CAS::Certificate",
      "Properties": {
        "Lang": {
          "Ref": "Lang"
        },
        "Cert": {
          "Ref": "Cert"
        },
        "SourceIp": {
          "Ref": "SourceIp"
        },
        "Name": {
          "Ref": "Name"
        },
        "Key": {
          "Ref": "Key"
        }
      }
    }
  },
  "Parameters": {
    "Lang": {
      "Type": "String",
      "Description": "Specifies the language type for requesting and receiving messages."
    },
    "Cert": {
      "Type": "String",
      "Description": "Specify the content of the certificate. To use the PEM encoding format."
    },
    "SourceIp": {
      "Type": "String",
      "Description": "Specifies the source IP address of the request."
    },
    "Name": {
      "Type": "String",
      "Description": "Custom certificate name. The certificate name under a user cannot be duplicated."
    },
    "Key": {
      "Type": "String",
      "Description": "Specify the certificate private key content. To use the PEM encoding format."
    }
  },
  "Outputs": {
    "CertId": {
      "Description": "Certificate ID.",
      "Value": {
        "Fn::GetAtt": [
          "Certificate",
          "CertId"
        ]
      }
    }
  }
}
```

