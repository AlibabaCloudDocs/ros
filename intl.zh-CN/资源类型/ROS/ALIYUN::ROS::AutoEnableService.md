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
|ServiceName|String|是|否|云服务名称|取值：-   ApiGateway：API网关。
-   AHAS：应用高可用服务。
-   BatchCompute：批量计算。
-   EMAS：移动研发平台。
-   HBR：混合云备份。
-   IMM：智能媒体管理。
-   KMS：密钥管理服务。
-   NAS：文件存储。
-   NLP：自然语言处理。
-   OSS：对象存储服务。
-   OTS：表格存储。
-   RocketMQ：消息队列 RocketMQ 版
-   SLS：日志服务。 |

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

