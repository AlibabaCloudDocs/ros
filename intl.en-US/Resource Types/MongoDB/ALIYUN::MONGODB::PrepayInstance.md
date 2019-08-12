# ALIYUN::MONGODB::PrepayInstance {#concept_jks_dys_qgb .concept}

ALIYUN::MONGODB::PrepayInstance is used to create a pre-paid ApsaraDB for MongoDB instance.

## Syntax {#section_cfm_4m1_mfb .section}

```language-json
{
  "Type": "ALIYUN::MONGODB::PrepayInstance",
  "Properties": {
    "SrcDBInstanceId":  String,
    "DBInstanceStorage":  Integer,
    "DBInstanceDescription": String,
    "Period": Integer,
    "ZoneId": String,
    "VpcId": String,
    "SecurityIPArray": String,
    "VSwitchId": String,
    "EngineVersion": String,
    "StorageEngine": String,
    "BackupId": String,
    "DBInstanceClass": String,
    "NetworkType": String,
    "AccountPassword": String
  }
}
```

## Properties {#section_uvy_fys_qgb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|SrcDBInstanceId|String|No|No|The ID of the instance that generates the backup set used to create the ApsaraDB for MongoDB instance.|None|
|DBInstanceStorage|Integer|Yes|No|The storage capacity of the ApsaraDB for MongoDB instance.|Valid values: 5 to 1,000. Unit: GB. The value can be increased in increments of 5 GB.|
|DBInstanceDescription|String|No|No|The description of the ApsaraDB for MongoDB instance.|None|
|Period|Integer|Yes|No|The subscription period.| Valid values: 1, 2, 3, 4, 5, 6, 7, 8, 9, 12, 24, and 36. Unit: month.

 Default value: 1.

 |
|ZoneId|String|No|No|The ID of the zone where the ApsaraDB for MongoDB instance resides.|The zone of the VSwitch must be the same as that specified by ZoneId.|
|VpcId|String|No|No|The ID of the VPC to which the ApsaraDB for MongoDB instance belongs.|None|
|SecurityIPArray|String|No|No|The list of IP addresses allowed to access the ApsaraDB for MongoDB instance.| You must separate different IP addresses with commas \(,\) and ensure that there are no duplicates. You can add a maximum of 1,000 IP addresses.

 Supported formats include %, 0.0.0.0/0, 10.23.12.24, and 10.23.12.24/24. You can use the IP address format \(10.23.12.24\) or CIDR format \(10.23.12.24/24\). The suffix of a CIDR block can be in the range of 1 to 32.

 0.0.0.0/0 indicates that no access limit is applied.

 No access limit is applied by default.

 |
|VSwitchId|String|No|No|The ID of the VSwitch in the VPC.|None|
|EngineVersion|String|No|No|The version of the ApsaraDB for MongoDB instance.|Valid values: 3.2 and 3.4.|
|StorageEngine|String|No|No|The storage engine of the ApsaraDB for MongoDB instance.| Valid values: WiredTiger and RocksDB.

 Default value: WiredTiger.

 |
|BackupId|String|No|No|The ID of the backup set used to create the ApsaraDB for MongoDB instance.|None|
|DBInstanceClass|String|Yes|No|The specifications of the ApsaraDB for MongoDB instance.|Valid values: dds.mongo.mid, dds.mongo.standard, dds.mongo.large, dds.mongo.xlarge, dds.mongo.2xlarge, and dds.mongo.4xlarge.|
|NetworkType|String|No|No|The network type of the ApsaraDB for MongoDB instance.| Valid values: CLASSIC and VPC.

 Default value: CLASSIC.

 |
|AccountPassword|String|No|No|The root account password.|The password must be 6 to 32 characters in length and can contain letters, digits, and underscores \(\_\).|

## Response parameters {#section_gwy_fys_qgb .section}

**FN:GetAtt**

-   OrderId: the order ID of the created ApsaraDB for MongoDB instance.
-   ConnectionURI: the URI used to connect to the ApsaraDB for MongoDB instance.
-   DBInstanceId: the ID of the ApsaraDB for MongoDB instance, which is globally unique.
-   DBInstanceStatus: the status of the ApsaraDB for MongoDB instance.
-   ReplicaSetName: the name of the replica set.

## Examples {#section_iwy_fys_qgb .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "EngineVersion": {
      "Type": "String",
      "Description": "The version of an ApsaraDB for MongoDB instance. Valid values: 3.2 and 3.4.",
      "AllowedValues": [
        "3.2",
        "3.4"
      ],
      "Default": "3.4"
    },
    "ZoneId": {
      "Type": "String",
      "Description": "The ID of the zone where the ApsaraDB for MongoDB instance resides."
    },
    "DBInstanceClass": {
      "Type": "String",
      "Description": "The specifications of the ApsaraDB for MongoDB instance. Make sure that the specifications are correct."
    },
    "VSwitchId": {
      "Type": "String",
      "Description": "The ID of the VSwitch used for the ApsaraDB for MongoDB instance."
    },
    "SecurityIPArray": {
      "Type": "String",
      "Description": "The list of IP addresses allowed to access the ApsaraDB for MongoDB instance."
    },
    "Period": {
      "Type": "Number",
      "Description": "The subscription period. Valid values: 1, 2, 3, 4, 5, 6, 7, 8, 9, 12, 24, and 36. Unit: month.",
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
    "BackupId": {
      "Type": "String",
      "Description": "The ID of the backup set used to create the ApsaraDB for MongoDB instance."
    },
    "StorageEngine": {
      "Type": "String",
      "Description": "The storage engine of the ApsaraDB for MongoDB instance. Valid values: WiredTiger and RocksDB.",
      "AllowedValues": [
        "WiredTiger",
        "RocksDB"
      ],
      "Default": "WiredTiger"
    },
    "AccountPassword": {
      "Type": "String",
      "Description": "The root account password. The password must be 6 to 32 characters in length and can contain letters, digits, and underscores (_)."
    },
    "VpcId": {
      "Type": "String",
      "Description": "The ID of the VPC to which the ApsaraDB for MongoDB instance belongs."
    },
    "NetworkType": {
      "Type": "String",
      "Description": "The network type of the ApsaraDB for MongoDB instance. Valid values: CLASSIC and VPC. Default value: CLASSIC.",
      "AllowedValues": [
        "CLASSIC",
        "VPC"
      ]
    },
    "DBInstanceStorage": {
      "Type": "Number",
      "Description": "The storage capacity of the ApsaraDB for MongoDB instance. Valid values: 5 to 1,000. Unit: GB. The value can be increased in increments of 5 GB."
    },
    "SrcDBInstanceId": {
      "Type": "String",
      "Description": "The ID of the instance that generates the backup set used to create the ApsaraDB for MongoDB instance."
    },
    "DBInstanceDescription": {
      "Type": "String",
      "Description": "The description of the ApsaraDB for MongoDB instance."
    }
  },
  "Resources": {
    "MongoPrepayInstance": {
      "Type": "ALIYUN::MONGODB::PrepayInstance",
      "Properties": {
        "EngineVersion": {
          "Ref": "EngineVersion"
        },
        "ZoneId": {
          "Ref": "ZoneId"
        },
        "DBInstanceClass": {
          "Ref": "DBInstanceClass"
        },
        "VSwitchId": {
          "Ref": "VSwitchId"
        },
        "SecurityIPArray": {
          "Ref": "SecurityIPArray"
        },
        "Period": {
          "Ref": "Period"
        },
        "BackupId": {
          "Ref": "BackupId"
        },
        "StorageEngine": {
          "Ref": "StorageEngine"
        },
        "AccountPassword": {
          "Ref": "AccountPassword"
        },
        "VpcId": {
          "Ref": "VpcId"
        },
        "NetworkType": {
          "Ref": "NetworkType"
        },
        "DBInstanceStorage": {
          "Ref": "DBInstanceStorage"
        },
        "SrcDBInstanceId": {
          "Ref": "SrcDBInstanceId"
        },
        "DBInstanceDescription": {
          "Ref": "DBInstanceDescription"
        }
      }
    }
  },
  "Outputs": {
    "DBInstanceStatus": {
      "Description": "The status of the ApsaraDB for MongoDB instance.",
      "Value": {
        "Fn::GetAtt": [
          "MongoPrepayInstance",
          "DBInstanceStatus"
        ]
      }
    },
    "DBInstanceId": {
      "Description": "The ID of the ApsaraDB for MongoDB instance.",
      "Value": {
        "Fn::GetAtt": [
          "MongoPrepayInstance",
          "DBInstanceId"
        ]
      }
    },
    "ConnectionURI": {
      "Description": "The URI used to connect to the ApsaraDB for MongoDB instance.",
      "Value": {
        "Fn::GetAtt": [
          "MongoPrepayInstance",
          "ConnectionURI"
        ]
      }
    },
    "ReplicaSetName": {
      "Description": "The name of the replica set.",
      "Value": {
        "Fn::GetAtt": [
          "MongoPrepayInstance",
          "ReplicaSetName"
        ]
      }
    },
    "OrderId": {
      "Description": "The order ID of the created ApsaraDB for MongoDB instance.", 
      "Value": {
        "Fn::GetAtt": [
          "MongoPrepayInstance",
          "OrderId"
        ]
      }
    }
  }
}
```

