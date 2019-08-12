# ALIYUN::MONGODB::Instance {#concept_48464_zh .concept}

ALIYUN::MONGODB::Instance is used to create an ApsaraDB for MongoDB instance.

## Syntax {#section_cfm_4m1_mfb .section}

```language-json
{
  "Type": "ALIYUN::MONGODB::Instance",
  "Properties": {
    "SrcDBInstanceId": String,
    "DBInstanceStorage": Integer,
    "DBInstanceDescription": String,
    "SecurityIPArray": String,
    "ZoneId": String,
    "VpcId" : String,
    "VSwitchId" : String,
    "BackupId": String,
    "NetworkType": String,
    "DBInstanceClass": String,
    "AccountPassword": String
  }
}
```

## Properties { .section}

|Name|Type|Required|Description|Validity|
|----|----|--------|-----------|--------|
|DBInstanceStorage|Integer|Yes|The storage capacity of the ApsaraDB for MongoDB instance.|Valid values: 5 to 1,000. Unit: GB. The value can be increased in increments of 5 GB.|
|DBInstanceClass|String|Yes|The specifications of the ApsaraDB for MongoDB instance.|Valid values: dds.mongo.mid, dds.mongo.standard, dds.mongo.large, dds.mongo.xlarge, dds.mongo.2xlarge, and dds.mongo.4xlarge.|
|SrcDBInstanceId|String|No|The ID of the instance that generates the backup set used to create the ApsaraDB for MongoDB instance.|None|
|DBInstanceDescription|String|No|The description of the ApsaraDB for MongoDB instance.|None|
|SecurityIPArray|String|No|The list of IP addresses allowed to access the ApsaraDB for MongoDB instance.| You must separate different IP addresses with commas \(,\) and ensure that there are no duplicates. You can add a maximum of 1,000 IP addresses.

 Supported formats include %, 0.0.0.0/0, 10.23.12.24, and 10.23.12.24/24. You can use the IP address format \(10.23.12.24\) or CIDR format \(10.23.12.24/24\). The suffix of a CIDR block can be in the range of 1 to 32. 0.0.0.0/0 indicates that no access limit is applied.

 No access limit is applied by default.

 |
|ZoneId|String|No|The ID of the zone where the ApsaraDB for MongoDB instance resides.|The zone of the VSwitch must be the same as that specified by ZoneId.|
|VpcId|String|No|The ID of the VPC to which the ApsaraDB for MongoDB instance belongs.|None|
|VSwitchId|String|No|The ID of the VSwitch in the VPC.|None|
|BackupId|String|No|The ID of the backup set used to create the ApsaraDB for MongoDB instance.|None|
|NetworkType|String|No|The network type of the ApsaraDB for MongoDB instance.| Valid values: CLASSIC and VPC.

 Default value: CLASSIC.

 |
|AccountPassword|String|No|The root account password.|The password must be 6 to 32 characters in length and can contain letters, digits, and underscores \(\_\).|
|EngineVersion|String|No|The version of the ApsaraDB for MongoDB instance.| Valid values: 3.2 and 3.4.

 Default value: 3.4.

 |
|StorageEngine|String|No|The storage engine of the ApsaraDB for MongoDB instance.| Valid values: WiredTiger and RocksDB.

 Default value: WiredTiger.

 |

## Response parameters { .section}

**Fn::GetAtt**

-   OrderId: the order ID of the ApsaraDB for MongoDB instance.
-   DBInstanceId: the ID of the ApsaraDB for MongoDB instance, which is globally unique.
-   DBInstanceStatus: the status of the ApsaraDB for MongoDB instance.

## Examples { .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "MongoDB": {
      "Type": "ALIYUN::MONGODB::Instance",
      "Properties": {
        "DBInstanceClass":"dds.mongo.mid",
        "DBInstanceStorage":"10",
        "VpcId": "vpc-25o8sqkwb",
        "VSwitchId": "vsw-25w8qld3m"
      }
    }
  },
  "Outputs": {
    "DBInstanceStatus": {
      "Description": "The status of the ApsaraDB for MongoDB instance.",
      "Value": {
        "Fn::GetAtt": [
          "MongoDB",
          "DBInstanceStatus"
        ]
      }
    },
    "InstanceId": {
      "Description": "The ID of the ApsaraDB for MongoDB instance.",
      "Value": {
        "Fn::GetAtt": [
          "MongoDB",
          "DBInstanceId"
        ]
      }
    }
  }
}
```

