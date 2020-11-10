# ALIYUN::CMS::MetricRuleTemplate

ALIYUN::CMS::MetricRuleTemplate is used to create an alert template.

## Syntax

```
{
  "Type": "ALIYUN::CMS::MetricRuleTemplate",
  "Properties": {
    "AlertTemplates": List,
    "Description": String,
    "RestVersion": Integer,
    "TemplateId": Integer,
    "Name": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|AlertTemplates|List|No|Yes|The details of alert rules that are generated based on the alert template.|A maximum of 200 alert rules can be specified.For more information, see [AlertTemplates properties](#section_pb0_nap_yra). |
|Description|String|No|Yes|The description of the alert template.|None|
|RestVersion|Integer|No|No|The version of the alert template.|Default value: 0.|
|TemplateId|Integer|No|No|The ID of the template to be cloned.|None|
|Name|String|Yes|No|The name of the alert template.|None|

## AlertTemplates syntax

```
"AlertTemplates": [
  {
    "MetricName": String,
    "Category": String,
    "Escalations": Map,
    "Period": Integer,
    "Webhook": String,
    "Namespace": String,
    "RuleName": String,
    "Selector": String
  }
]
```

## AlertTemplates properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|MetricName|String|Yes|Yes|The name of the metric.|None|
|Category|String|Yes|Yes|The abbreviation of the service name.|Valid values:-   ecs: Elastic Compute Service \(ECS\)
-   rds: ApsaraDB RDS
-   ads: AnalyticDB for MySQL
-   slb: Server Load Balancer \(SLB\)
-   vpc: Virtual Private Cloud \(VPC\)
-   apigateway: API Gateway
-   cdn: Alibaba Cloud CDN \(CDN\)
-   cs: Container Service for Kubernetes \(ACK\)
-   dcdn: Dynamic Route for CDN \(DCDN\)
-   ddos: Anti-DDoS Premium
-   eip: Elastic IP Address \(EIP\)
-   elasticsearch: Elasticsearch
-   emr: E-MapReduce \(EMR\)
-   ess: Auto Scaling \(ESS\)
-   hbase: ApsaraDB for HBase
-   iot\_edge: IoT Edge
-   k8s\_pod: pods in Container Service for Kubernetes
-   kvstore\_sharding: ApsaraDB for Redis that uses the cluster master-replica architecture
-   kvstore\_splitrw: ApsaraDB for Redis that uses the read/write splitting architecture
-   kvstore\_standard: ApsaraDB for Redis that uses the standard master-replica architecture
-   memcache: ApsaraDB for Memcache
-   mns: Message Service \(MNS\)
-   mongodb: ApsaraDB for MongoDB that uses the replica set architecture
-   mongodb\_cluster: ApsaraDB for MongoDB that uses the standalone architecture
-   mongodb\_sharding: ApsaraDB for MongoDB that uses the sharded cluster architecture
-   mq\_topic: MNS topics
-   ocs: ApsaraDB for Memcache of earlier versions
-   opensearch: Open Search
-   oss: Object Storage Service \(OSS\)
-   polardb: PolarDB
-   petadata: HybridDB for MySQL
-   scdn: Secure CDN \(SCDN\)
-   sharebandwidthpackages: EIP Bandwidth Plan
-   sls: Log Service
-   vpn: VPN Gateway |
|Escalations|Map|No|No|The alert settings.|For more information, see [Escalations properties](#section_3x0_kr3_lat).|
|Period|Integer|No|Yes|The aggregation period of monitoring data.|The default value is the lowest frequency at which the metric is polled. Typically, you do not need to specify the aggregation period.Unit: seconds. |
|Webhook|String|No|No|The webhook address to which a POST request is sent when an alert is triggered.|None|
|Namespace|String|Yes|Yes|The namespace of the service.|For more information, see [DescribeMetricMetaList](/intl.en-US/API Reference/Monitoring data on time series metrics of cloud services/DescribeMetricMetaList.md) or [Instructions](/intl.en-US/Appendix 1: Metrics/Overview.md).|
|RuleName|String|Yes|Yes|The name of the alert rule.|None|
|Selector|String|No|Yes|The extended resource dimensions.|None|

## Escalations syntax

```
"Escalations": {
  "Critical": Map,
  "Info": Map,
  "Warn": Map
}
```

## Escalations properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Critical|Map|Yes|Yes|The settings for critical alerts.|For more information, see [Critical properties](#section_4db_qrf_mji).|
|Info|Map|No|Yes|The settings for info-level alerts.|For more information, see [Info properties](#section_2s0_5ia_yf0).|
|Warn|Map|No|Yes|The settings for warn-level alerts.|For more information, see [Warn properties](#section_rn9_rfq_axz).|

## Critical syntax

```
"Critical": {
  "ComparisonOperator": String,
  "Times": Integer,
  "Statistics": String,
  "Threshold": String
}
```

## Critical properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ComparisonOperator|String|Yes|Yes|The comparison operator of the threshold for critical alerts.|Valid values:-   GreaterThanOrEqualToThreshold
-   GreaterThanThreshold
-   LessThanOrEqualToThreshold
-   LessThanThreshold
-   NotEqualToThreshold
-   GreaterThanYesterday
-   LessThanYesterday
-   GreaterThanLastWeek
-   LessThanLastWeek
-   GreaterThanLastPeriod
-   LessThanLastPeriod |
|Times|Integer|Yes|Yes|The number of times for which the metric value must exceed the threshold consecutively before an alert is triggered.|None|
|Statistics|String|Yes|Yes|The statistical method for critical alerts.|None|
|Threshold|String|Yes|Yes|The threshold for critical alerts.|None|

## Info syntax

```
"Info": {
  "ComparisonOperator": String,
  "Times": Integer,
  "Statistics": String,
  "Threshold": String
}
```

## Info properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ComparisonOperator|String|Yes|Yes|The comparison operator of the threshold for info-level alerts.|Valid values:-   GreaterThanOrEqualToThreshold
-   GreaterThanThreshold
-   LessThanOrEqualToThreshold
-   LessThanThreshold
-   NotEqualToThreshold
-   GreaterThanYesterday
-   LessThanYesterday
-   GreaterThanLastWeek
-   LessThanLastWeek
-   GreaterThanLastPeriod
-   LessThanLastPeriod |
|Times|Integer|Yes|Yes|The number of times for which the metric value must exceed the threshold consecutively before an alert is triggered.|None|
|Statistics|String|Yes|Yes|The statistical method for info-level alerts.|None|
|Threshold|String|Yes|Yes|The threshold for info-level alerts.|None|

## Warn syntax

```
"Warn": {
  "ComparisonOperator": String,
  "Times": Integer,
  "Statistics": String,
  "Threshold": String
}
```

## Warn properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ComparisonOperator|String|Yes|Yes|The comparison operator of the threshold for warn-level alerts.|Valid values:-   GreaterThanOrEqualToThreshold
-   GreaterThanThreshold
-   LessThanOrEqualToThreshold
-   LessThanThreshold
-   NotEqualToThreshold
-   GreaterThanYesterday
-   LessThanYesterday
-   GreaterThanLastWeek
-   LessThanLastWeek
-   GreaterThanLastPeriod
-   LessThanLastPeriod |
|Times|Integer|Yes|Yes|The number of times for which the metric value must exceed the threshold consecutively before an alert is triggered.|None|
|Statistics|String|Yes|Yes|The statistical method for warn-level alerts.|None|
|Threshold|String|Yes|Yes|The threshold for warn-level alerts.|None|

## Response parameters

Fn::GetAtt

Id: the ID of the alert template.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "AlertTemplates": {
      "Type": "Json",
      "Description": "Valid values of N: 0 to 200.",
      "MinLength": 0,
      "MaxLength": 200
    },
    "Description": {
      "Type": "String",
      "Description": "The description of the alert template."
    },
    "RestVersion": {
      "Type": "Number",
      "Description": "The version of the alert template. Call DescribeMetricRuleTemplateList or DescribeMetricRuleTemplateAttribute\nto obtain information about the alert templates. The combination of version and ID\nuniquely identifies an alert template."
    },
    "TemplateId": {
      "Type": "Number",
      "Description": "The ID of the alert template."
    },
    "Name": {
      "Type": "String",
      "Description": "The name of the alert template."
    }
  },
  "Resources": {
    "MetricRuleTemplate": {
      "Type": "ALIYUN::CMS::MetricRuleTemplate",
      "Properties": {
        "AlertTemplates": {
          "Ref": "AlertTemplates"
        },
        "Description": {
          "Ref": "Description"
        },
        "RestVersion": {
          "Ref": "RestVersion"
        },
        "TemplateId": {
          "Ref": "TemplateId"
        },
        "Name": {
          "Ref": "Name"
        }
      }
    }
  },
  "Outputs": {
    "Id": {
      "Description": "Alarm template ID.",
      "Value": {
        "Fn::GetAtt": [
          "MetricRuleTemplate",
          "Id"
        ]
      }
    }
  }
}
```

`YAML` format

```
ROSTemplateFormatVersion: '2015-09-01'
Parameters:
  AlertTemplates:
    Type: Json
    Description: 'Valid values of N: 0 to 200.'
    MinLength: 0
    MaxLength: 200
  Description:
    Type: String
    Description: The description of the alert template.
  RestVersion:
    Type: Number
    Description: >-
      The version of the alert template. Call DescribeMetricRuleTemplateList or
      DescribeMetricRuleTemplateAttribute

      to obtain information about the alert templates. The combination of
      version and ID

      uniquely identifies an alert template.
  TemplateId:
    Type: Number
    Description: The ID of the alert template.
  Name:
    Type: String
    Description: The name of the alert template.
Resources:
  MetricRuleTemplate:
    Type: 'ALIYUN::CMS::MetricRuleTemplate'
    Properties:
      AlertTemplates:
        Ref: AlertTemplates
      Description:
        Ref: Description
      RestVersion:
        Ref: RestVersion
      TemplateId:
        Ref: TemplateId
      Name:
        Ref: Name
Outputs:
  Id:
    Description: Alarm template ID.
    Value:
      'Fn::GetAtt':
        - MetricRuleTemplate
        - Id
```

