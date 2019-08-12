# ALIYUN::REDIS::PrepayInstance {#concept_qcv_sgh_tgb .concept}

ALIYUN::REDIS::PrepayInstance is used to create a pre-paid ApsaraDB for Redis instance.

## Syntax {#section_efw_ym1_mfb .section}

```language-json
{
  "Type": "ALIYUN::REDIS::PrepayInstance",
  "Properties": {
    "VpcId":  String,
    "EvictionPolicy":  String,
    "Period": Integer,
    "ZoneId": String,
    "InstanceClass": String,
    "VSwitchId": String,
    "Password": String,
    "InstanceName": String
  }
}
```

## Properties {#section_lyg_1n1_mfb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|VpcId|String|No|No|The ID of the VPC to which the ApsaraDB for Redis instance belongs.|None|
|EvictionPolicy|String|No|No|The data eviction policy for the ApsaraDB for Redis instance.|Valid values: noeviction, allkeys-lru, volatile-lru, allkeys-random, volatile-random, and volatile-ttl.|
|Period|Integer|No|No|The renewal period of the subscription-based instance. Unit: month.|Valid values: 1, 2, 3, 4, 5, 6, 7, 8, 9, 12, 24, and 36.|
|ZoneId|String|No|No|The ID of the zone where the ApsaraDB for Redis instance resides.|None|
|InstanceClass|String|No|No|The specifications of the ApsaraDB for Redis instance.| Capacity: 1 GB. Specifications: redis.master.small.default.

 Capacity: 2 GB. Specifications: redis.master.mid.default.

 Capacity: 4 GB. Specifications: redis.master.stand.default.

 Capacity: 8 GB. Specifications: redis.master.large.default.

 Capacity: 16 GB. Specifications: redis.master. 2xlarge.default.

 Capacity: 32 GB. Specifications: redis.master. 4xlarge.default.

 Capacity: 64 GB. Specifications: redis.master. 8xlarge.default.

 Capacity: 128 GB. Specifications: redis.sharding. 2xlarge.default.

 Capacity: 256 GB. Specifications: redis.sharding. 4xlarge.default.

 |
|VSwitchId|String|No|No|The ID of the VSwitch in the VPC.|None|
|Password|String|No|No|The password used to log on to the ApsaraDB for Redis instance.|The password must be 8 to 30 characters in length and must contain both digits and letters.|
|InstanceName|String|No|No|The name of the ApsaraDB for Redis instance.|The name must be 2 to 128 characters in length and can contain letters, digits, underscores \(\_\), hyphens \(-\), and periods \(.\). It must start with a letter.|

## Response parameters {#section_d4s_5n1_mfb .section}

**Fn::GetAtt**

-   InstanceId: the ID of the ApsaraDB for Redis instance, which is globally unique.
-   OrderId: the order ID of the ApsaraDB for Redis instance.
-   ConnectionDomain: the domain name used to connect to the ApsaraDB for Redis instance.
-   Port: the port used to connect to the ApsaraDB for Redis instance.

## Examples {#section_jmm_wn1_mfb .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "InstanceName": {
      "Type": "String",
      "Description": "The name of the ApsaraDB for Redis instance. The name must be 2 to 128 characters in length and can contain letters, digits, underscores (_), hyphens (-), and periods (.). It must start with a letter."
    },
    "VpcId": {
      "Type": "String",
      "Description": "The ID of the VPC to which the ApsaraDB for Redis instance belongs."
    },
    "EvictionPolicy": {
      "Type": "String",
      "Description": "The eviction policy of cache data storage.",
      Alliwedvalues ":[
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
      "Description": "The ID of the zone where the ApsaraDB for Redis instance resides."
    },
    "VSwitchId": {
      "Type": "String",
      "Description": "The ID of the VSwitch used for the ApsaraDB for Redis instance."
    },
    "Period": {
      "Type": "Number",
      "Description": "The renewal period of the subscription-based instance. Valid values: 1, 2, 3, 4, 5, 6, 7, 8, 9, 12, 24, and 36. Unit: month.",
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
      "Description": "The specifications of the ApsaraDB for Redis instance. Refer to the ApsaraDB for Redis instance types, such as redis.master.small.default, redis.master.4xlarge.default,  and redis.sharding.mid.default."
    },
    "Password": {
      "Type": "String",
      "Description": "The password used to log on to the ApsaraDB for Redis instance. The password must be 8 to 30 characters in length and must contain both digits and letters."
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
      "Description": "The domain name used to connect to the ApsaraDB for Redis instance.",
      "Value": {
        "Fn::GetAtt": [
          "KvPrepayInstance",
          "ConnectionDomain"
        ]
      }
    },
    "InstanceId": {
      "Description": "The ID of the ApsaraDB for Redis instance.",
      "Value": {
        "Fn::GetAtt": [
          "KvPrepayInstance",
          "InstanceId"
        ]
      }
    },
    "Port": {
      "Description": "The port used to connect to the ApsaraDB for Redis instance.",
      "Value": {
        "Fn::GetAtt": [
          "KvPrepayInstance",
          "Port"
        ]
      }
    },
    "OrderId": {
      "Description": "The order ID of the ApsaraDB for Redis instance.",
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

