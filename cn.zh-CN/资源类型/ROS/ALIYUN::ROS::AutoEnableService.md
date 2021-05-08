# ALIYUN::ROS::AutoEnableService

ALIYUN::ROS::AutoEnableService类型用于自动开通云服务。

## 语法

```
{
  "Type": "ALIYUN::ROS::AutoEnableService",
  "Properties": {
    "ServiceName": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ServiceName|String|是|否|云服务名称|取值：-   ARMS：应用实时监控服务。
-   ApiGateway：API网关。
-   BatchCompute：批量计算。
-   BrainIndustrial：工业大脑。
-   CloudStorageGateway：云存储网关。
-   CMS：云监控。
-   CR：镜像容器服务。
-   CS：容器服务。
-   DataHub：数据总线。
-   DataWorks：数据工场。
-   EMAS：移动研发平台。
-   FC：函数计算。
-   FNF：Serverless工作流。
-   MaxCompute：大数据计算服务。
-   MNS：消息服务。
-   HBR：混合云备份。
-   IMM：智能媒体管理。
-   IOT：物联网平台。
-   KMS：密钥管理服务。
-   NLP：自然语言处理。
-   OSS：对象存储服务。
-   OTS：表格存储。
-   PrivateLink：私网连接。
-   PrivateZone：云解析。
-   RocketMQ：消息队列RocketMQ版。
-   SAE：应用引擎。
-   SLS：日志服务。
-   VS：视频监控。
-   Xtrace：链路追踪。 |

## 返回值

Fn::GetAtt

无

## 示例

`JSON`格式

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

`YAML`格式

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

更多示例，请参见：[JSON示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ROS/JSON/AutoEnableService.json)和[YAML示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ROS/YAML/AutoEnableService.yml)。

