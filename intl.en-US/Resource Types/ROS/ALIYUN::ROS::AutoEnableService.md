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
|ServiceName|String|Yes|No|The name of the Alibaba Cloud service.|Valid values:-   ARMS: Application Real-Time Monitoring Service \(ARMS\)
-   ApiGateway: API Gateway
-   BatchCompute: Batch Compute
-   BrainIndustrial: Industrial Brain
-   CloudStorageGateway: Cloud Storage Gateway \(CSG\)
-   CMS: CloudMonitor
-   CR: Container Registry
-   CS: Container Service for Kubernetes \(ACK\)
-   DataHub: DataHub
-   DataWorks: DataWorks
-   EMAS: Enterprise Mobile Application Studio \(EMAS\)
-   FC: Function Compute
-   FNF: Serverless Workflow
-   MaxCompute: MaxCompute
-   MNS: Message Service
-   HBR: Hybrid Backup Recovery \(HBR\)
-   IMM: Intelligent Media Management
-   IOT: IoT Platform
-   KMS: Key Management Service \(KMS\)
-   NLP: Natural Language Processing \(NLP\)
-   OSS: Object Storage Service \(OSS\)
-   OTS: Tablestore
-   PrivateLink: PrivateLink
-   PrivateZone: Alibaba Cloud DNS \(DNS\)
-   RocketMQ: Message Queue for Apache RocketMQ
-   SAE: Serverless App Engine \(SAE\)
-   SLS: Log Service
-   VS: Video Surveillance System
-   Xtrace: Tracing Analysis |

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
         "IOT",
         "EMAS",
         "MaxCompute",
         "BatchCompute",
         "IMM",
         "Xtrace",
         "DataWorks",
         "FNF",
         "FC",
         "KMS",
         "CS",
         "CR",
         "DataHub",
         "SLS",
         "CMS",
         "RocketMQ",
         "HBR",
         "ApiGateway",
         "NLP",
         "NAS",
         "OSS",
         "MNS",
         "ARMS",
         "SAE",
         "CloudStorageGateway",
         "PrivateZone",
         "DCDN",
         "VS",
         "AHAS",
         "BrainIndustrial",
         "OTS",
         "PrivateLink"
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
      - IOT
      - EMAS
      - MaxCompute
      - BatchCompute
      - IMM
      - Xtrace
      - DataWorks
      - FNF
      - FC
      - KMS
      - CS
      - CR
      - DataHub
      - SLS
      - CMS
      - RocketMQ
      - HBR
      - ApiGateway
      - NLP
      - NAS
      - OSS
      - MNS
      - ARMS
      - SAE
      - CloudStorageGateway
      - PrivateZone
      - DCDN
      - VS
      - AHAS
      - BrainIndustrial
      - OTS
      - PrivateLink
Resources:
  AutoEnableService:
    Type: 'ALIYUN::ROS::AutoEnableService'
    Properties:
      ServiceName:
        Ref: ServiceName
```

For more examples, visit [Instance.json](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ROS/JSON/AutoEnableService.json) and [Instance.yml](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ROS/YAML/AutoEnableService.yml).

