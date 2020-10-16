# ALIYUN::CMS::MetricRuleTemplate

ALIYUN::CMS::MetricRuleTemplate类型用于创建报警模板。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|AlertTemplates|List|否|是|报警模板。|最多添加200个规则。详情请参见[AlertTemplates属性](#section_pb0_nap_yra)。 |
|Description|String|否|是|报警模板描述信息。|无|
|RestVersion|Integer|否|否|报警模板版本。|默认值为0。|
|TemplateId|Integer|否|否|克隆模版ID。|无|
|Name|String|是|否|报警模板名称。|无|

## AlertTemplates语法

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

## AlertTemplates属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|MetricName|String|是|是|监控项名称。|无|
|Category|String|是|是|产品名称或产品规格缩写。|取值：-   ecs：云服务器。
-   rds：阿里云关系型数据库。
-   ads：云原生数据仓库AnalyticDB MySQL版。
-   slb：负载均衡。
-   vpc：专有网络。
-   apigateway：API网关。
-   cdn：内容分发网络。
-   cs：容器服务Kubernetes版。
-   dcdn：全站加速。
-   ddos：DDoS高防。
-   eip：弹性公网IP。
-   elasticsearch：阿里云Elasticsearch。
-   emr：阿里云E-MapReduce。
-   ess：弹性伸缩。
-   hbase：云数据库HBase版。
-   iot\_edge：物联网边缘计算。
-   k8s\_pod：k8s pod。
-   kvstore\_sharding：Redis集群版。
-   kvstore\_splitrw：Redis读写分离版。
-   kvstore\_standard：Redis标准版。
-   memcache：云数据库Memcache版。
-   mns：消息服务。
-   mongodb：MongoDB副本实例。
-   mongodb\_cluster：MongoDB集群版本。
-   mongodb\_sharding：MongoDB分片集群。
-   mq\_topic：消息服务TOPIC。
-   ocs：云数据库Memcache版。
-   opensearch：开放搜索。
-   oss：对象存储服务。
-   polardb：云数据库PolarDB。
-   petadata：HybridDB for MySQL。
-   scdn：安全加速。
-   sharebandwidthpackages：共享带宽包。
-   sls：日志服务。
-   vpn：VPN网关。 |
|Escalations|Map|否|否|报警配置。|详情请参见[Escalations属性](#section_3x0_kr3_lat)。|
|Period|Integer|否|是|监控数据的聚合周期。|默认为监控项对应的最小频率，通常不需要指定。单位：秒。 |
|Webhook|String|否|否|报警发生时的回调URL地址。|无|
|Namespace|String|是|是|产品的数据命名空间。|详情请参见[DescribeMetricMetaList](/cn.zh-CN/API参考/云产品时序指标类监控数据/DescribeMetricMetaList.md)或[监控项使用说明](/cn.zh-CN/附录1 云产品监控项/概述.md)。|
|RuleName|String|是|是|报警规则的名称。|无|
|Selector|String|否|是|扩展字段选项。|无|

## Escalations语法

```
"Escalations": {
  "Critical": Map,
  "Info": Map,
  "Warn": Map
}
```

## Escalations属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Critical|Map|是|是|Critical级别报警设置。|详情请参见[Critical属性](#section_4db_qrf_mji)。|
|Info|Map|否|是|Info级别报警设置。|详情请参见[Info属性](#section_2s0_5ia_yf0)。|
|Warn|Map|否|是|Warn级别报警设置。|详情请参见[Warn属性](#section_rn9_rfq_axz)。|

## Critical语法

```
"Critical": {
  "ComparisonOperator": String,
  "Times": Integer,
  "Statistics": String,
  "Threshold": String
}
```

## Critical属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ComparisonOperator|String|是|是|阈值比较符。|取值：-   GreaterThanOrEqualToThreshold：大于等于。
-   GreaterThanThreshold：大于。
-   LessThanOrEqualToThreshold：小于等于。
-   LessThanThreshold：小于。
-   NotEqualToThreshold：不等。
-   GreaterThanYesterday：同比昨天时间上涨。
-   LessThanYesterday：同比昨天时间下降。
-   GreaterThanLastWeek：同比上周同一时间上涨。
-   LessThanLastWeek：同比上周同一时间下降。
-   GreaterThanLastPeriod：环比上周期上涨。
-   LessThanLastPeriod：环比上周期下降。 |
|Times|Integer|是|是|报警重试次数。|无|
|Statistics|String|是|是|报警统计方法。|无|
|Threshold|String|是|是|报警阈值。|无|

## Info语法

```
"Info": {
  "ComparisonOperator": String,
  "Times": Integer,
  "Statistics": String,
  "Threshold": String
}
```

## Info属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ComparisonOperator|String|是|是|阈值比较符。|取值：-   GreaterThanOrEqualToThreshold：大于等于。
-   GreaterThanThreshold：大于。
-   LessThanOrEqualToThreshold：小于等于
-   LessThanThreshold：小于。
-   NotEqualToThreshold：不等。
-   GreaterThanYesterday：同比昨天时间上涨。
-   LessThanYesterday：同比昨天时间下降。
-   GreaterThanLastWeek：同比上周同一时间上涨。
-   LessThanLastWeek：同比上周同一时间下降。
-   GreaterThanLastPeriod：环比上周期上涨。
-   LessThanLastPeriod：环比上周期下降。 |
|Times|Integer|是|是|报警重试次数。|无|
|Statistics|String|是|是|报警统计方法。|无|
|Threshold|String|是|是|报警阈值。|无|

## Warn语法

```
"Warn": {
  "ComparisonOperator": String,
  "Times": Integer,
  "Statistics": String,
  "Threshold": String
}
```

## Warn属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ComparisonOperator|String|是|是|阈值比较符。|取值：-   GreaterThanOrEqualToThreshold：大于等于。
-   GreaterThanThreshold：大于。
-   LessThanOrEqualToThreshold：小于等于。
-   LessThanThreshold：小于。
-   NotEqualToThreshold：不等。
-   GreaterThanYesterday：同比昨天时间上涨。
-   LessThanYesterday：同比昨天时间下降。
-   GreaterThanLastWeek：同比上周同一时间上涨。
-   LessThanLastWeek：同比上周同一时间下降。
-   GreaterThanLastPeriod：环比上周期上涨。
-   LessThanLastPeriod：环比上周期下降。 |
|Times|Integer|是|是|报警重试次数。|无|
|Statistics|String|是|是|报警统计方法。|无|
|Threshold|String|是|是|报警阈值。|无|

## 返回值

Fn::GetAtt

Id：报警模板ID。

## 示例

`JSON`格式

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

`YAML`格式

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

