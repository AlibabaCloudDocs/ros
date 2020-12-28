# ALIYUN::ROS::AutoEnableService

ALIYUN::ROS::AutoEnableService is used to activate an Alibaba Cloud service.

## Syntax

```
{
  "Type": "ALIYUN::ROS::AutoEnableService",
  "Properties": {
    "ServiceName": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ServiceName|String|Yes|No|The name of the Alibaba Cloud service.|Valid values:-   ApiGateway: API Gateway
-   AHAS: Application High Availability Service \(AHAS\)
-   BatchCompute: BatchCompute
-   EMAS: Enterprise Mobile Application Studio \(EMAS\)
-   HBR: Hybrid Backup Recovery \(HBR\)
-   IMM: Intelligent Media Management \(IMM\)
-   KMS: Key Management Service \(KMS\)
-   NAS: Apsara File Storage NAS \(NAS\)
-   NLP: Natural Language Processing \(NLP\)
-   OSS: Object Storage Service \(OSS\)
-   OTS: Tablestore
-   RocketMQ: Message Queue for Apache RocketMQ
-   SLS: Log Service
-   ARMS: Application Real-Time Monitoring Service \(ARMS\)
-   CMS: Cloud Monitor
-   DataHub: DataHub
-   FC: Function Compute
-   PrivateLink: PrivateLink |

## Response parameters

Fn::GetAtt

None

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "ServiceName": {
      "Type": "String",
      "Description": "Which service to enable. Valid values:\nApiGateway: API Gateway\nBatchCompute: Batch Compute\nEMAS: Enterprise Mobile Application Studio\nNAS: Network Attached Storage\nHBR: Hybrid Backup Recovery\nNLP: Natural Language Processing\nOSS: Object Storage Service\nOTS: Table Store\nSLS: Log Service\n",
      "AllowedValues": [
        "ApiGateway",
        "NAS",
        "EMAS",
        "SLS",
        "BatchCompute",
        "NLP",
        "OSS",
        "OTS",
        "HBR"
      ]
    }
  },
  "Resources": {
    "AutoEnableService": {
      "Type": "ALIYUN::ROS::AutoEnableService",
      "Properties": {
        "ServiceName": {
          "Ref": "ServiceName"
        }
      }
    }
  }
}
```

`YAML` format

```
ROSTemplateFormatVersion: '2015-09-01'
Parameters:
  ServiceName:
    Type: String
    Description: |
      Which service to enable. Valid values:
      ApiGateway: API Gateway
      BatchCompute: Batch Compute
      EMAS: Enterprise Mobile Application Studio
      NAS: Network Attached Storage
      HBR: Hybrid Backup Recovery
      NLP: Natural Language Processing
      OSS: Object Storage Service
      OTS: Table Store
      SLS: Log Service
    AllowedValues:
      - ApiGateway
      - NAS
      - EMAS
      - SLS
      - BatchCompute
      - NLP
      - OSS
      - OTS
      - HBR
Resources:
  AutoEnableService:
    Type: 'ALIYUN::ROS::AutoEnableService'
    Properties:
      ServiceName:
        Ref: ServiceName
```

