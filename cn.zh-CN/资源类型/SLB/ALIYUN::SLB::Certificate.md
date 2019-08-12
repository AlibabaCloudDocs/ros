# ALIYUN::SLB::Certificate {#concept_evv_l5h_tgb .concept}

ALIYUN::SLB::Certificate类型用于用于上传证书，支持 ServerCertificate 和 CACertificate 两种证书。

**说明：** 

-   一次只能上传一份CA证书内容\("CertificateType": "CA"\)。
-   一次只能上传一份服务器证书和对应的私钥\("CertificateType": "Server"\)。

## 语法 {#section_ey2_ycz_lfb .section}

``` {#codeblock_biw_tg9_t9z .language-json}
{
  "Type": "ALIYUN::SLB::Certificate",
  "Properties": {
    "CertificateName": String,
    "Certificate": String,
    "AliCloudCertificateName": String,
    "PrivateKey": String,
    "ResourceGroupId": String,
    "CertificateType": String,
    "AliCloudCertificateId": String
  }
}
```

## 属性 {#section_n13_22z_lfb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ResourceGroupId|String|否|否|资源组ID。|无。|
|CertificateName|String|否|是|证书名称。|无|
|Certificate|String|是|否|证书。|无|
|AliCloudCertificateName|String|否|否|阿里云的云上证书名称。|无|
|PrivateKey|String|否|否|需要上传的私钥。|无|
|AliCloudCertificateId|String|否|否|阿里云的云上证书ID。使用阿里云的云上证书，该参数必选。|无|
|CertificateType|String|否|否|证书类型。|取值： "Server"|

## 返回值 {#section_wfc_q2z_lfb .section}

**Fn::GetAtt**

-   CertificateId: 证书ID。
-   Fingerprint: 证书的指纹。

## 示例 {#section_lcd_s2z_lfb .section}

``` {#codeblock_cq9_6ec_nfm .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "CertificateType": {
      "Type": "String",
      "Description": "The type of the certificate.",
      "AllowedValues": [
        "Server",
        "CA"
      ],
      "Default": "Server"
    },
    "AliCloudCertificateName": {
      "Type": "String",
      "Description": "The name of the Alibaba Cloud certificate."
    },
    "PrivateKey": {
      "Type": "String",
      "Description": "The private key."
    },
    "CertificateName": {
      "Type": "String",
      "Description": "The name of the certificate."
    },
    "Certificate": {
      "Type": "String",
      "Description": "The content of the certificate public key."
    },
    "AliCloudCertificateId": {
      "Type": "String",
      "Description": "The ID of the Alibaba Cloud certificate."
    }
  },
  "Resources": {
    "Certificate": {
      "Type": "ALIYUN::SLB::Certificate",
      "Properties": {
        "CertificateType": {
          "Ref": "CertificateType"
        },
        "AliCloudCertificateName": {
          "Ref": "AliCloudCertificateName"
        },
        "PrivateKey": {
          "Ref": "PrivateKey"
        },
        "CertificateName": {
          "Ref": "CertificateName"
        },
        "Certificate": {
          "Ref": "Certificate"
        },
        "AliCloudCertificateId": {
          "Ref": "AliCloudCertificateId"
        }
      }
    }
  },
  "Outputs": {
    "Fingerprint": {
      "Description": "The fingerprint of the certificate.",
      "Value": {
        "Fn::GetAtt": [
          "Certificate",
          "Fingerprint"
        ]
      }
    },
    "CertificateId": {
      "Description": "The ID of the certificate.",
      "Value": {
        "Fn::GetAtt": [
          "Certificate",
          "CertificateId"
        ]
      }
    }
  }
}
```

