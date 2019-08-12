# ALIYUN::REDIS::Instance {#concept_51193_zh .concept}

ALIYUN::REDIS::Instance 类型可用于创建云数据库 Redis 版实例。

## 语法 {#section_efw_ym1_mfb .section}

``` {#codeblock_p4v_ul6_5zc .language-json}
{
  "Type": "ALIYUN::REDIS::Instance",
  "Properties": {
    "VpcId": String,
    "EvictionPolicy": String,
    "ZoneId": String,
    "InstanceClass": String,
    "VSwitchId": String,
    "EngineVersion": String,
    "Password": String,
    "InstanceName": String
  }
}
```

## 属性 {#section_lyg_1n1_mfb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|EngineVersion|String|否|否|数据库版本。默认值：2.8。|可用值: 2.8, 4.0, 5.0|
|InstanceClass|String|否|否|指定实例的规格| 容量：1G ，规格：redis.master.small.default

 容量：2G，规格：redis.master.mid.default

 容量：4G，redis.master.stand.default

 容量8G，规格：redis.master.large.default

 容量：16G，规格：redis.master.2xlarge.default

 容量：32G，规格：redis.master.4xlarge.default

 容量：64G，规格redis.master.8xlarge.default

 容量：128G，规格redis.sharding.2xlarge.default

 容量：256G，规格：redis.sharding.4xlarge.default

 |
|VpcId|String|否|否|专有网络 ID 。|无|
|EvictionPolicy|String|否|否|数据逐出策略 。|可选值：noeviction、allkeys-lru、volatile-lru、allkeys-random、volatile-random和 volatile-ttl。|
|ZoneId|String|否|否|可用区ID。|无|
|VSwitchId|String|否|否|专有网络下的虚拟交换机 ID 。|无|
|Password|String|否|否|指定密码 。|长度为 8～30 个字符，需同时包含大写字母、小写字母和数字。|
|InstanceName|String|否|否|指定实例的名称。|必须以字母或汉字开始，可以包含字母、数字、汉字、下划线（\_）、连字符（-）、和点号（.）。 长度范围: \[2, 128\]。|

## 返回值 {#section_d4s_5n1_mfb .section}

**Fn::GetAtt**

-   InstanceId：创建的实例ID。
-   OrderId: 实例订单ID。
-   ConnectionDomain: Redis实例的内网连接地址。
-   Port: Redis服务端口。

## 示例 {#section_jmm_wn1_mfb .section}

``` {#codeblock_p51_ill_g8e .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "CreateInstance": {
      "Type": "ALIYUN::REDIS::Instance",
      "Properties": {
        "InstanceName": "createdByHeat",
        "Password": "1234****",
        "ZoneId": "cn-beijing-a",
        "InstanceClass": "redis.master.small.default",
        "EvictionPolicy": "noeviction",
      }
    }
  },
  "Outputs": {
    "InstanceDetails": {
         "Value": {"Fn::GetAtt": ["CreateInstance", "InstanceId"]}
    }
  }
}
```

