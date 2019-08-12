# ALIYUN::SLB::Certificate {#concept_evv_l5h_tgb .concept}

Uploads the server certificate and CA certificate \(if required\) to the SLB instance.

**Note:** 

-   You can only upload one CA certificate at a time. CertificateType: CA.
-   You can only upload one server certificate and the matching private key at a time. Certificate type: Server.

## Syntax {#section_ey2_ycz_lfb .section}

```language-json
{
  "Type": "ALIYUN::SLB::Certificate",
  "Properties": {
    "CertificateName": String,
    "Certificate": String,
    "AliCloudCertificateName": String,
    "PrivateKey": String,
    "AliCloudCertificateId": String,
    "CertificateType": String
  }
}
```

## Properties {#section_n13_22z_lfb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|CertificateName|String|No|Yes|The certificate name.|N/A|
|Certificate|String|Yes|No|The certificate.|N/A|
|AliCloudCertificateName|String|No|No|The name of the Alibaba Cloud certificate.|N/A|
|PrivateKey|String|No|No|The private key to be uploaded.|N/A|
|AliCloudCertificateId|String|No|No|The ID of the Alibaba cloud certificate. This parameter is m required if you use a certificate from Alibaba Cloud SSL Certificates Service.|N/A|
|CertificateType|String|No|No|The certificate type.|Valid value: Server.|

## Response elements {#section_wfc_q2z_lfb .section}

**Fn::GetAtt**

-   CertificateId: indicates the certificate ID.
-   Fingerprint: indicates the certificate fingerprint.

## Example {#section_lcd_s2z_lfb .section}

```language-json
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

