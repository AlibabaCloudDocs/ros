# ALIYUN::MEMCACHE::Instance {#concept_48456_zh .concept}

ALIYUN::MEMCACHE::Instance is used to create an ApsaraDB for Memcache instance.

## Syntax {#section_ysq_3m1_mfb .section}

```language-json
{
  "Type": "ALIYUN::MEMCACHE::Instance",
  "Properties": {
    "VpcId": String,
    "Capacity": Integer,
    "PrivateIpAddr": String,
    "ZoneId": String,
    "SecurityIPArray": String,
    "VSwitchId": String,
    "NetworkType": String,
    "Password": String,
    "InstanceName": String
  }
}
```

## Properties { .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Capacity|Integer|Yes|No|The storage capacity of the ApsaraDB for Memcache instance.| Valid values: 1024, 2048, 4096, 8192, 16384, and 32768.

 Unit: MB.

 |
|Password|String|Yes|No|The password used to log on to the instance.|The password must be 8 to 30 characters in length and must contain uppercase letters, lowercase letters, and digits.|
|VpcId|String|No|No|The ID of the VPC to which the instance belongs.|None|
|PrivateIpAddr|String|No|No|The private IP address of the instance in the specified VPC.|The private IP address must belong to the CIDR block specified by VpcId and VSwitchId.|
|ZoneId|String|No|No|The ID of the zone where the instance resides.|None|
|SecurityIPArray|String|No|No|The list of IP addresses that are allowed to access the instance.| You must separate different IP addresses with commas \(,\) and ensure that there are no duplicates. You can add a maximum of 1,000 IP addresses.

 Supported formats include %, 0.0.0.0/0, 10.23.XX.XX, and 10.23.XX.XX/24. You can use the IP address format \(10.23.XX.XX\), or CIDR format \(10.23.XX.XX/24\), where the suffix can be in the range of 1 to 32.

 0.0.0.0/0 indicates that no access limit is applied. No access limit is applied by default.

 |
|VSwitchId|String|No|No|The ID of the VSwitch in the specified VPC.|None|
|NetworkType|String|No|No|The network type of the instance.|Valid values: CLASSIC and VPC.|
|InstanceName|String|No|No|The name of the instance.|The name can be up to 128 characters in length.|

## Response parameters { .section}

**Fn::GetAtt**

-   InstanceStatus: the status of the created instance.
-   InstanceId: the ID of the created instance.
-   ConnectionDomain: the domain name used to connect to the instance.
-   QPS: the maximum queries per second \(QPS\) of the instance.
-   InstanceName: the name of the instance.
-   PrivateIpAddress: the private IP address of the instance in the VPC. Classic networks do not have private IP addresses.

## Examples { .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "OcsInstance": {
      "Type": "ALIYUN::MEMCACHE::Instance",
      "Properties": {
        "Password": "YU76sdfs****",
        "Capacity": 1024,
        "VpcId": "vpc-25o8s****",
        "VSwitchId": "vsw-25rc1****",
        "ZoneId": "cn-beijing-c"
      }
    }
  },
  "Outputs": {
    "ConnectionDomain": {
      "Description": "Intranet connection string",
      "Value": {
        "Fn::GetAtt": [
          "OcsInstance",
          "ConnectionDomain"
        ]
      }
    },
    "PrivateIpAddress": {
      "Description": "Private IP address",
      "Value": {
        "Fn::GetAtt": [
          "OcsInstance",
          "PrivateIpAddress"
        ]
      }
    }
  }
}			
```

