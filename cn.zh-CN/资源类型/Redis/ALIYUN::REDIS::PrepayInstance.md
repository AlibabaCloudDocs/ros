# ALIYUN::REDIS::PrepayInstance {#concept_qcv_sgh_tgb .concept}

ALIYUN::REDIS::PrepayInstance类型用于创建预付费云数据库 Redis 版实例。

## 语法 {#section_efw_ym1_mfb .section}

``` {#codeblock_iod_zyt_pen .language-json}
{
  "Type": "ALIYUN::REDIS::PrepayInstance",
  "Properties": {
    "VpcId": String,
    "EvictionPolicy": String,
    "Period": Integer,
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
|VpcId|String|否|否|专有网络 ID 。|无|
|EvictionPolicy|String|否|否|数据逐出策略。|可选值：noeviction、allkeys-lru、volatile-lru、allkeys-random、volatile-random和 volatile-ttl。|
|Period|Integer|否|否|预付费续费时长，单位是月。|取值范围为：1-9、12、24、36。|
|ZoneId|String|否|否|可用区ID。|无|
|InstanceClass|String|否|否|指定实例规格。| 容量：1G ，规格：redis.master.small.default

 容量：2G，规格：redis.master.mid.default

 容量：4G，redis.master.stand.default

 容量8G，规格：redis.master.large.default

 容量：16G，规格：redis.master.2xlarge.default

 容量：32G，规格：redis.master.4xlarge.default

 容量：64G，规格redis.master.8xlarge.default

 容量：128G，规格redis.sharding.2xlarge.default

 容量：256G，规格：redis.sharding.4xlarge.default

 |
|VSwitchId|String|否|否|专有网络下的虚拟交换机 ID 。|无|
|Password|String|否|否|指定密码。|长度为 8～30 个字符，需同时包含大写字母、小写字母和数字。|
|InstanceName|string|否|否|指定实例的名称。|必须以字母或汉字开始，可以包含字母、数字、汉字、下划线（\_）、连字符（-）和点号（.）。 长度范围: \[2, 128\]。|

## 返回值 {#section_d4s_5n1_mfb .section}

**Fn::GetAtt**

-   InstanceId：实例 ID （全局唯一）。
-   OrderId：订单ID。
-   ConnectionDomain：Redis 实例的连接域名。
-   Port：Redis 连接端口。

## 示例 {#section_jmm_wn1_mfb .section}

``` {#codeblock_uqn_qll_77e .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "InstanceName": {
      "Type": "String",
      "Description": "Display name of the instance, [2, 128] English or Chinese characters, must start with a letter or Chinese in size, can contain numbers, '_' or '.', '-'"
    },
    "VpcId": {
      "Type": "String",
      "Description": "The VPC id to create ecs instance."
    },
    "EvictionPolicy": {
      "Type": "String",
      "Description": "The eviction policy of cache data storage.",
      "AllowedValues": [
        "noeviction",
        "allkeys-lru",
        "volatile-lru",
        "allkeys-random",
        "volatile-random",
        "volatile-ttl"
      ]
    },
    "ZoneId": {
      "Type": "String",
      "Description": "The zone id of input region."
    },
    "VSwitchId": {
      "Type": "String",
      "Description": "The vSwitch Id to create ecs instance."
    },
    "Period": {
      "Type": "Number",
      "Description": "The period of order, when choose Prepaid required.optional value 1-9, 12, 24, 36, Unit in month.",
      "AllowedValues": [
        1,
        2,
        3,
        4,
        5,
        6,
        7,
        8,
        9,
        12,
        24,
        36
      ],
      "Default": 1
    },
    "InstanceClass": {
      "Type": "String",
      "Description": "Redis instance type. Refer the Redis instance type reference, such as 'redis.master.small.default', 'redis.master.4xlarge.default', 'redis.sharding.mid.default' etc"
    },
    "Password": {
      "Type": "String",
      "Description": "The password of redis instance.length 8 to 30 characters, need to contain both uppercase and lowercase letters and numbers"
    }
  },
  "Resources": {
    "KvPrepayInstance": {
      "Type": "ALIYUN::REDIS::PrepayInstance",
      "Properties": {
        "InstanceName": {
          "Ref": "InstanceName"
        },
        "VpcId": {
          "Ref": "VpcId"
        },
        "EvictionPolicy": {
          "Ref": "EvictionPolicy"
        },
        "ZoneId": {
          "Ref": "ZoneId"
        },
        "VSwitchId": {
          "Ref": "VSwitchId"
        },
        "Period": {
          "Ref": "Period"
        },
        "InstanceClass": {
          "Ref": "InstanceClass"
        },
        "Password": {
          "Ref": "Password"
        }
      }
    }
  },
  "Outputs": {
    "ConnectionDomain": {
      "Description": "Connection domain of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "KvPrepayInstance",
          "ConnectionDomain"
        ]
      }
    },
    "InstanceId": {
      "Description": "Instance id for created redis instance.",
      "Value": {
        "Fn::GetAtt": [
          "KvPrepayInstance",
          "InstanceId"
        ]
      }
    },
    "Port": {
      "Description": "Port of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "KvPrepayInstance",
          "Port"
        ]
      }
    },
    "OrderId": {
      "Description": "Order Id of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "KvPrepayInstance",
          "OrderId"
        ]
      }
    }
  }
}
```

