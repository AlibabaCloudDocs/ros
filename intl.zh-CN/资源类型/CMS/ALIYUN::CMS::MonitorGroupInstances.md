# ALIYUN::CMS::MonitorGroupInstances

ALIYUN::CMS::MonitorGroupInstances类型用于添加资源到应用分组。

## 语法

```
{
  "Type": "ALIYUN::CMS::MonitorGroupInstances",
  "Properties": {
    "Instances": List,
    "GroupId": Integer
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Instances|List|是|否|资源实例|更多信息，请参见[Instances属性](#section_wzx_r0l_4fx)。|
|GroupId|Integer|是|否|应用分组ID|无|

## Instances语法

```
"Instances": [
  {
    "InstanceName": String,
    "Category": String,
    "InstanceId": String,
    "RegionId": String
  }
]
```

## Instances属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|InstanceName|String|是|否|实例名称。|无|
|Category|String|是|否|资源实例所属的云产品名称或规格。|取值：-   ecs：云服务器。
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
-   vpn：VPN网关。 |
|InstanceId|String|是|否|资源实例ID。|无|
|RegionId|String|是|否|实例所在的地域ID。|无|

## 返回值

Fn::GetAtt

GroupId：应用分组ID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Instances": {
      "Type": "Json"
    },
    "GroupId": {
      "Type": "Number",
      "Description": "The ID of the application group."
    }
  },
  "Resources": {
    "MonitorGroupInstances": {
      "Type": "ALIYUN::CMS::MonitorGroupInstances",
      "Properties": {
        "Instances": {
          "Ref": "Instances"
        },
        "GroupId": {
          "Ref": "GroupId"
        }
      }
    }
  },
  "Outputs": {
    "GroupId": {
      "Description": "The ID of the application group.",
      "Value": {
        "Fn::GetAtt": [
          "MonitorGroupInstances",
          "GroupId"
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
  Instances:
    Type: Json
  GroupId:
    Type: Number
    Description: The ID of the application group.
Resources:
  MonitorGroupInstances:
    Type: 'ALIYUN::CMS::MonitorGroupInstances'
    Properties:
      Instances:
        Ref: Instances
      GroupId:
        Ref: GroupId
Outputs:
  GroupId:
    Description: The ID of the application group.
    Value:
      'Fn::GetAtt':
        - MonitorGroupInstances
        - GroupId
```

