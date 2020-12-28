# ALIYUN::CMS::GroupMetricRule

ALIYUN::CMS::GroupMetricRule类型用于创建应用分组报警规则。

## 语法

```
{
  "Type": "ALIYUN::CMS::GroupMetricRule",
  "Properties": {
    "NoEffectiveInterval": String,
    "SilenceTime": Integer,
    "Category": String,
    "RuleId": String,
    "Dimensions": String,
    "Period": Integer,
    "EffectiveInterval": String,
    "Namespace": String,
    "GroupId": String,
    "MetricName": String,
    "Escalations": Map,
    "EmailSubject": String,
    "Webhook": String,
    "RuleName": String,
    "Interval": Integer
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|NoEffectiveInterval|String|否|是|报警规则非生效时间范围。|无|
|SilenceTime|Integer|否|是|一直处于报警状态的通知沉默周期。|单位：秒。最小值：3600秒（1小时）。

默认值：86,400秒（1天）。 |
|Category|String|是|否|产品名称或产品规格缩写。|取值：-   ecs：云服务器。
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
-   mongodb：云数据库MongoDB版副本集实例。
-   mongodb\_cluster：云数据库MongoDB版单节点实例。
-   mongodb\_sharding：云数据库MongoDB版分片集群实例。
-   mq\_topic：消息服务TOPIC。
-   ocs：云数据库Memcache版。
-   opensearch：开放搜索。
-   oss：对象存储服务。
-   polardb：云数据库PolarDB。
-   petadata：HybridDB for MySQL。
-   scdn：安全加速。
-   sharebandwidthpackages：共享带宽包。
-   sls：日志服务。
-   vpn：VPN网关。

**说明：** 云监控接入的产品会不断增加，包括但不仅限于上述产品 |
|RuleId|String|是|否|报警规则ID。|由调用者统一生成以保证其唯一性。|
|Dimensions|String|否|是|扩展资源维度。|设置到组的报警规则会将组的实例资源全部关联到该报规则里。此参数设置除了实例外还可以设置更深一级的资源，例如想为应用分组下所有实例的根分区的磁盘使用率，此时可以设置为`[ {"dskName":"/"} ]`。|
|Period|Integer|否|是|监控数据的聚合周期。|取值：60或60的整数倍。单位：秒。

默认值：300秒。

**说明：** 根据设置的报警统计方法，设置成300秒即表示将原始上报的5分钟监控数据平均值为1个点（假设原始上报监控数据为1分钟）作为是否报警的参考。 |
|EffectiveInterval|String|否|是|报警规则的生效时间范围。|无|
|Namespace|String|是|否|产品的数据命名空间。更多信息，请参见[DescribeMetricMetaList](/cn.zh-CN/API参考/云产品时序指标类监控数据/DescribeMetricMetaList.md)或[云服务主要监控项]()。|无|
|GroupId|String|是|是|应用分组的ID。|无|
|MetricName|String|是|是|监控项名称。更多信息，请参见[DescribeMetricMetaList](/cn.zh-CN/API参考/云产品时序指标类监控数据/DescribeMetricMetaList.md)或[云服务主要监控项]()。|无|
|Escalations|Map|是|是|报警配置。|更多信息，请参见[Escalations属性](#section_yv0_94o_q3a)。|
|EmailSubject|String|否|是|报警邮件主题。|无|
|Webhook|String|否|是|出现报警时触发的回调地址。|无|
|RuleName|String|是|是|报警规则名称。|无|
|Interval|Integer|否|是|报警规则的探测周期，即报警系统多长时间检查一次是否要触发报警规则，默认为监控项的最小频率。|单位：秒。

建议将报警的探测周期和上报数据周期保持一致，报警规则的探测周期小于上报周期会导致数据不足而不能触发报警。|

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
|Critical|Map|否|是|Critical级别报警设置。|更多信息，请参见[Critical属性](#section_0a4_d9i_w5t)。|
|Info|Map|否|是|Info级别报警设置。|更多信息，请参见[Info属性](#section_fsn_8sl_e0p)。|
|Warn|Map|否|是|Warn级别报警设置。|更多信息，请参见[Warn属性](#section_jwe_etr_6xq)。|

## Critical语法

```
"Critical": {
  "ComparisonOperator": String,
  "Times": Integer,
  "Statistics": String,
  "Threshold": Integer
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
|Statistics|String|是|是|报警统计方法。|级别统计方法的取值，请参见[DescribeSystemEventMetaList](/cn.zh-CN/API参考/云产品事件类监控数据/DescribeSystemEventMetaList.md)。|
|Threshold|Integer|是|是|报警阈值。|无|

## Info语法

```
"Info": {
  "ComparisonOperator": String,
  "Times": Integer,
  "Statistics": String,
  "Threshold": Integer
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
|Statistics|String|是|是|报警统计方法。|级别统计方法的取值，请参见[DescribeSystemEventMetaList](/cn.zh-CN/API参考/云产品事件类监控数据/DescribeSystemEventMetaList.md)。|
|Threshold|Integer|是|是|报警阈值。|无|

## Warn语法

```
"Warn": {
  "ComparisonOperator": String,
  "Times": Integer,
  "Statistics": String,
  "Threshold": Integer
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
|Statistics|String|是|是|报警统计方法。|级别统计方法的取值，请参见[DescribeSystemEventMetaList](/cn.zh-CN/API参考/云产品事件类监控数据/DescribeSystemEventMetaList.md)。|
|Threshold|Integer|是|是|报警阈值。|无|

## 返回值

Fn::GetAtt

RuleId：报警规则ID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "NoEffectiveInterval": {
      "Type": "String",
      "Description": "The period when the alert rule is ineffective."
    },
    "SilenceTime": {
      "Type": "Number",
      "Description": "The duration of the mute period during which new alerts are not sent even if the trigger\nconditions are met. Unit: second. Default value: 86400. Minimum value: 60.",
      "MinValue": 60
    },
    "Category": {
      "Type": "String",
      "Description": "The abbreviation of the service name. Valid values:\nECS (including Alibaba Cloud and non-Alibaba Cloud hosts)\nRDS (ApsaraDB for RDS)\nADS (AnalyticDB)\nSLB (Server Load Balancer)\nVPC (Virtual Private Cloud)\nAPIGATEWAY (API Gateway)\nCDN\nCS (Container Service for Swarm)\nDCDN (Dynamic Route for CDN)\nDDoS (distributed denial of service)\nEIP (Elastic IP)\nELASTICSEARCH (Elasticsearch)\nEMR (E-MapReduce)\nESS (Auto Scaling)\nHBASE (ApsaraDB for HBase)\nIOT_EDGE (IoT Edge)\nK8S_POD (k8s pod)\nKVSTORE_SHARDING (ApsaraDB for Redis cluster version)\nKVSTORE_SPLITRW (ApsaraDB for Redis read/write splitting version)\nKVSTORE_STANDARD (ApsaraDB for Redis standard version)\nMEMCACHE (ApsaraDB for Memcache)\nMNS (Message Service)\nMONGODB (ApsaraDB for MongoDB replica set instances)\nMONGODB_CLUSTER (ApsaraDB for MongoDB cluster version)\nMONGODB_SHARDING (ApsaraDB for MongoDB sharded clusters)\nMQ_TOPIC (Message Service topic)\nOCS (original version of ApsaraDB for Memcache)\nOPENSEARCH (Open Search)\nOSS (Object Storage Service)\nPOLARDB (ApsaraDB for POLARDB)\nPETADATA (HybridDB for MySQL)\nSCDN (Secure Content Delivery Network)\nSHAREBANDWIDTHPACKAGES (shared bandwidth package)\nSLS (Log Service)\nVPN (VPN Gateway)"
    },
    "RuleId": {
      "Type": "String",
      "Description": "The ID of the alert rule. The IDs of alert rules are generated by callers to ensure\nuniqueness."
    },
    "Dimensions": {
      "Type": "String",
      "Description": "The expended resource dimensions."
    },
    "Period": {
      "Type": "Number",
      "Description": "The aggregation period. Unite: second."
    },
    "EffectiveInterval": {
      "Type": "String",
      "Description": "The period when the alert rule is effective."
    },
    "Namespace": {
      "Type": "String",
      "Description": "The data namespace of the service. For more information, call DescribeMetricMetaList\nor see Preset metrics reference."
    },
    "GroupId": {
      "Type": "String",
      "Description": "The ID of application group."
    },
    "MetricName": {
      "Type": "String",
      "Description": "The name of the metric. For more information, call DescribeMetricMetaList or see Preset metrics reference."
    },
    "Escalations": {
      "Type": "Json"
    },
    "EmailSubject": {
      "Type": "String",
      "Description": "The subject of the alert notification email."
    },
    "Webhook": {
      "Type": "String",
      "Description": "The URL of the callback triggered when an alert occurs."
    },
    "RuleName": {
      "Type": "String",
      "Description": "The name of the alert rule."
    },
    "Interval": {
      "Type": "Number",
      "Description": "The detection period of alerts."
    }
  },
  "Resources": {
    "GroupMetricRule": {
      "Type": "ALIYUN::CMS::GroupMetricRule",
      "Properties": {
        "NoEffectiveInterval": {
          "Ref": "NoEffectiveInterval"
        },
        "SilenceTime": {
          "Ref": "SilenceTime"
        },
        "Category": {
          "Ref": "Category"
        },
        "RuleId": {
          "Ref": "RuleId"
        },
        "Dimensions": {
          "Ref": "Dimensions"
        },
        "Period": {
          "Ref": "Period"
        },
        "EffectiveInterval": {
          "Ref": "EffectiveInterval"
        },
        "Namespace": {
          "Ref": "Namespace"
        },
        "GroupId": {
          "Ref": "GroupId"
        },
        "MetricName": {
          "Ref": "MetricName"
        },
        "Escalations": {
          "Ref": "Escalations"
        },
        "EmailSubject": {
          "Ref": "EmailSubject"
        },
        "Webhook": {
          "Ref": "Webhook"
        },
        "RuleName": {
          "Ref": "RuleName"
        },
        "Interval": {
          "Ref": "Interval"
        }
      }
    }
  },
  "Outputs": {
    "RuleId": {
      "Description": "Rule ID.",
      "Value": {
        "Fn::GetAtt": [
          "GroupMetricRule",
          "RuleId"
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
  NoEffectiveInterval:
    Type: String
    Description: The period when the alert rule is ineffective.
  SilenceTime:
    Type: Number
    Description: >-
      The duration of the mute period during which new alerts are not sent even
      if the trigger
      conditions are met. Unit: second. Default value: 86400. Minimum value: 60.
    MinValue: 60
  Category:
    Type: String
    Description: |-
      The abbreviation of the service name. Valid values:
      ECS (including Alibaba Cloud and non-Alibaba Cloud hosts)
      RDS (ApsaraDB for RDS)
      ADS (AnalyticDB)
      SLB (Server Load Balancer)
      VPC (Virtual Private Cloud)
      APIGATEWAY (API Gateway)
      CDN
      CS (Container Service for Swarm)
      DCDN (Dynamic Route for CDN)
      DDoS (distributed denial of service)
      EIP (Elastic IP)
      ELASTICSEARCH (Elasticsearch)
      EMR (E-MapReduce)
      ESS (Auto Scaling)
      HBASE (ApsaraDB for HBase)
      IOT_EDGE (IoT Edge)
      K8S_POD (k8s pod)
      KVSTORE_SHARDING (ApsaraDB for Redis cluster version)
      KVSTORE_SPLITRW (ApsaraDB for Redis read/write splitting version)
      KVSTORE_STANDARD (ApsaraDB for Redis standard version)
      MEMCACHE (ApsaraDB for Memcache)
      MNS (Message Service)
      MONGODB (ApsaraDB for MongoDB replica set instances)
      MONGODB_CLUSTER (ApsaraDB for MongoDB cluster version)
      MONGODB_SHARDING (ApsaraDB for MongoDB sharded clusters)
      MQ_TOPIC (Message Service topic)
      OCS (original version of ApsaraDB for Memcache)
      OPENSEARCH (Open Search)
      OSS (Object Storage Service)
      POLARDB (ApsaraDB for POLARDB)
      PETADATA (HybridDB for MySQL)
      SCDN (Secure Content Delivery Network)
      SHAREBANDWIDTHPACKAGES (shared bandwidth package)
      SLS (Log Service)
      VPN (VPN Gateway)
  RuleId:
    Type: String
    Description: >-
      The ID of the alert rule. The IDs of alert rules are generated by callers
      to ensure

      uniqueness.
  Dimensions:
    Type: String
    Description: The expended resource dimensions.
  Period:
    Type: Number
    Description: 'The aggregation period. Unite: second.'
  EffectiveInterval:
    Type: String
    Description: The period when the alert rule is effective.
  Namespace:
    Type: String
    Description: >-
      The data namespace of the service. For more information, call
      DescribeMetricMetaList
      or see Preset metrics reference.
  GroupId:
    Type: String
    Description: The ID of application group.
  MetricName:
    Type: String
    Description: >-
      The name of the metric. For more information, call DescribeMetricMetaList
      or see Preset metrics reference.
  Escalations:
    Type: Json
  EmailSubject:
    Type: String
    Description: The subject of the alert notification email.
  Webhook:
    Type: String
    Description: The URL of the callback triggered when an alert occurs.
  RuleName:
    Type: String
    Description: The name of the alert rule.
  Interval:
    Type: Number
    Description: The detection period of alerts.
Resources:
  GroupMetricRule:
    Type: 'ALIYUN::CMS::GroupMetricRule'
    Properties:
      NoEffectiveInterval:
        Ref: NoEffectiveInterval
      SilenceTime:
        Ref: SilenceTime
      Category:
        Ref: Category
      RuleId:
        Ref: RuleId
      Dimensions:
        Ref: Dimensions
      Period:
        Ref: Period
      EffectiveInterval:
        Ref: EffectiveInterval
      Namespace:
        Ref: Namespace
      GroupId:
        Ref: GroupId
      MetricName:
        Ref: MetricName
      Escalations:
        Ref: Escalations
      EmailSubject:
        Ref: EmailSubject
      Webhook:
        Ref: Webhook
      RuleName:
        Ref: RuleName
      Interval:
        Ref: Interval
Outputs:
  RuleId:
    Description: Rule ID.
    Value:
      'Fn::GetAtt':
        - GroupMetricRule
        - RuleId
```

