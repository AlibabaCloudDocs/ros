# ALIYUN::ClickHouse::DBCluster

ALIYUN::ClickHouse::DBCluster is used to create an ApsaraDB for a ClickHouse cluster.

## Syntax

```
{
  "Type": "ALIYUN::ClickHouse::DBCluster",
  "Properties": {
    "DbNodeStorageType": String,
    "DBNodeStorage": Integer,
    "EncryptionType": String,
    "Category": String,
    "ZoneId": String,
    "VSwitchId": String,
    "DBClusterDescription": String,
    "Period": String,
    "EncryptionKey": String,
    "DBClusterNetworkType": String,
    "DBClusterType": String,
    "VpcId": String,
    "DBClusterVersion": String,
    "DBNodeCount": Integer,
    "UsedTime": String,
    "PaymentType": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|DbNodeStorageType|String|Yes|No|The storage type of the node.|Valid values:-   cloud\_essd: enhanced SSD \(ESSD\)
-   cloud\_efficiency: ultra disk |
|DBNodeStorage|Integer|Yes|No|The storage capacity of the node.|Valid values: 100 to 10000. Unit: GB.

This value must be in 100 GB increments. |
|EncryptionType|String|No|No|The type of the encryption.|Set the value to CloudDisk. The value of CloudDisk indicates disk encryption.|
|Category|String|Yes|No|The edition of the cluster.|Valid values:-   Basic: Basic Edition
-   HighAvailability: Cluster Edition |
|ZoneId|String|No|No|The zone ID of the cluster.|You can call the [DescribeRegions]() operation to query the most recent zone list.|
|VSwitchId|String|No|No|The vSwitch ID of the cluster.|None|
|DBClusterDescription|String|No|No|The description of the cluster.|None|
|Period|String|No|No|The billing cycle of the subscription cluster.|Valid values:-   Year
-   Month

**Note:** This parameter must be specified when the PaymentType parameter is set to Prepaid. |
|EncryptionKey|String|No|No|The ID of the Key Management Service \(KMS\) key.|None|
|DBClusterNetworkType|String|Yes|No|The network type of the cluster.|Set the value to VPC.|
|DBClusterType|String|Yes|No|The type of the cluster instance.|Valid values:-   Common: common instance
-   Readonly: read-only instance
-   Guard: disaster recovery instance |
|VpcId|String|No|No|The ID of the virtual private cloud \(VPC\) to which the cluster belongs.|None|
|DBClusterVersion|String|Yes|No|The version of the cluster.|Set the value to 19.15.2.2.|
|DBNodeCount|Integer|Yes|No|The number of cluster nodes.|Valid values:-   Valid values for S series clusters: 1 to 48
-   Valid values for C series clusters: 1 to 24 |
|UsedTime|String|No|No|The subscription duration of the cluster.|Valid values:-   Valid values when Period is set to Month: 1, 2, 3, 4, 5, 6, 7, 8, and 9.
-   Valid values when Period is set to Year: 1, 2, and 3. |
|PaymentType|String|Yes|No|The billing method of the cluster.|Valid values:-   Postpaid: pay-as-you-go
-   Prepaid: subscription |

## Response parameters

Fn::GetAtt

-   DBClusterId: the ID of the cluster.
-   OrderId: the ID of the order.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "DbNodeStorageType": {
      "Type": "String",
      "Description": "Instance node storage type. Valid values:  cloud_essd, cloud_efficiency."
    },
    "DBNodeStorage": {
      "Type": "Number",
      "Description": "DBNodeStorage"
    },
    "EncryptionType": {
      "Type": "String",
      "Description": "Kms key type, only cloud disk encryption is supported and the value is CloudDisk."
    },
    "Category": {
      "Type": "String",
      "Description": "Series, value: Basic: Basic version"
    },
    "ZoneId": {
      "Type": "String",
      "Description": "ZoneId"
    },
    "VSwitchId": {
      "Type": "String",
      "Description": "VSwitchId"
    },
    "DBClusterDescription": {
      "Type": "String",
      "Description": "DBClusterDescription"
    },
    "Period": {
      "Type": "String",
      "Description": "Prepaid time period.If the payment type is Prepaid, this parameter is mandatory. Specify the prepaid cluster as a yearly or monthly type. Valid values:  Year, Month."
    },
    "EncryptionKey": {
      "Type": "String",
      "Description": "KMS key ID"
    },
    "DBClusterNetworkType": {
      "Type": "String",
      "Description": "Network type of the cluster instance, value: VPC"
    },
    "DBClusterType": {
      "Type": "String",
      "Description": "Cluster instance type, value:  Common: normal instance;  Readonly: read-only instance; Guard: disaster recovery instance"
    },
    "VpcId": {
      "Type": "String",
      "Description": "VpcId"
    },
    "DBClusterVersion": {
      "Type": "String",
      "Description": "Version, value:  19.15.2.2"
    },
    "DBNodeCount": {
      "Type": "Number",
      "Description": "Number of node groups"
    },
    "UsedTime": {
      "Type": "String",
      "Description": "When Period is Month, the value of UsedTime is [1-9].  When Period is Year, the value of UsedTime is [1-3]"
    },
    "PaymentType": {
      "Type": "String",
      "Description": "PayType"
    }
  },
  "Resources": {
    "ClickHouseDBCluster": {
      "Type": "ALIYUN::ClickHouse::DBCluster",
      "Properties": {
        "DbNodeStorageType": {
          "Ref": "DbNodeStorageType"
        },
        "DBNodeStorage": {
          "Ref": "DBNodeStorage"
        },
        "EncryptionType": {
          "Ref": "EncryptionType"
        },
        "Category": {
          "Ref": "Category"
        },
        "ZoneId": {
          "Ref": "ZoneId"
        },
        "VSwitchId": {
          "Ref": "VSwitchId"
        },
        "DBClusterDescription": {
          "Ref": "DBClusterDescription"
        },
        "Period": {
          "Ref": "Period"
        },
        "EncryptionKey": {
          "Ref": "EncryptionKey"
        },
        "DBClusterNetworkType": {
          "Ref": "DBClusterNetworkType"
        },
        "DBClusterType": {
          "Ref": "DBClusterType"
        },
        "VpcId": {
          "Ref": "VpcId"
        },
        "DBClusterVersion": {
          "Ref": "DBClusterVersion"
        },
        "DBNodeCount": {
          "Ref": "DBNodeCount"
        },
        "UsedTime": {
          "Ref": "UsedTime"
        },
        "PaymentType": {
          "Ref": "PaymentType"
        }
      }
    }
  },
  "Outputs": {
    "Category": {
      "Description": "Series, value: Basic: Basic version",
      "Value": {
        "Fn::GetAtt": [
          "ClickHouseDBCluster",
          "Category"
        ]
      }
    },
    "Port": {
      "Description": "Connection port",
      "Value": {
        "Fn::GetAtt": [
          "ClickHouseDBCluster",
          "Port"
        ]
      }
    },
    "DBClusterId": {
      "Description": "The id of DBCluster",
      "Value": {
        "Fn::GetAtt": [
          "ClickHouseDBCluster",
          "DBClusterId"
        ]
      }
    },
    "EncryptionKey": {
      "Description": "KMS key ID",
      "Value": {
        "Fn::GetAtt": [
          "ClickHouseDBCluster",
          "EncryptionKey"
        ]
      }
    },
    "DBClusterNetworkType": {
      "Description": "Network type of the cluster instance, value: VPC",
      "Value": {
        "Fn::GetAtt": [
          "ClickHouseDBCluster",
          "DBClusterNetworkType"
        ]
      }
    },
    "DBClusterType": {
      "Description": "Cluster instance type, value:  Common: normal instance;  Readonly: read-only instance; Guard: disaster recovery instance",
      "Value": {
        "Fn::GetAtt": [
          "ClickHouseDBCluster",
          "DBClusterType"
        ]
      }
    },
    "DBClusterVersion": {
      "Description": "Version, value:  19.15.2.2",
      "Value": {
        "Fn::GetAtt": [
          "ClickHouseDBCluster",
          "DBClusterVersion"
        ]
      }
    },
    "CommodityCode": {
      "Description": "Product Code",
      "Value": {
        "Fn::GetAtt": [
          "ClickHouseDBCluster",
          "CommodityCode"
        ]
      }
    },
    "DBNodeCount": {
      "Description": "Number of node groups",
      "Value": {
        "Fn::GetAtt": [
          "ClickHouseDBCluster",
          "DBNodeCount"
        ]
      }
    },
    "PaymentType": {
      "Description": "PayType",
      "Value": {
        "Fn::GetAtt": [
          "ClickHouseDBCluster",
          "PaymentType"
        ]
      }
    },
    "PublicConnectionString": {
      "Description": "Internet connection address",
      "Value": {
        "Fn::GetAtt": [
          "ClickHouseDBCluster",
          "PublicConnectionString"
        ]
      }
    },
    "LockReason": {
      "Description": "Reason for lock",
      "Value": {
        "Fn::GetAtt": [
          "ClickHouseDBCluster",
          "LockReason"
        ]
      }
    },
    "Bid": {
      "Description": "BusinessID",
      "Value": {
        "Fn::GetAtt": [
          "ClickHouseDBCluster",
          "Bid"
        ]
      }
    },
    "Engine": {
      "Description": "Engine",
      "Value": {
        "Fn::GetAtt": [
          "ClickHouseDBCluster",
          "Engine"
        ]
      }
    },
    "DBNodeStorage": {
      "Description": "DBNodeStorage",
      "Value": {
        "Fn::GetAtt": [
          "ClickHouseDBCluster",
          "DBNodeStorage"
        ]
      }
    },
    "DbNodeStorageType": {
      "Description": "Instance node storage type. Valid values:  cloud_essd, cloud_efficiency.",
      "Value": {
        "Fn::GetAtt": [
          "ClickHouseDBCluster",
          "DbNodeStorageType"
        ]
      }
    },
    "IsExpired": {
      "Description": "IsExpired",
      "Value": {
        "Fn::GetAtt": [
          "ClickHouseDBCluster",
          "IsExpired"
        ]
      }
    },
    "EncryptionType": {
      "Description": "Kms key type, only cloud disk encryption is supported and the value is CloudDisk.",
      "Value": {
        "Fn::GetAtt": [
          "ClickHouseDBCluster",
          "EncryptionType"
        ]
      }
    },
    "EngineVersion": {
      "Description": "EngineVersion",
      "Value": {
        "Fn::GetAtt": [
          "ClickHouseDBCluster",
          "EngineVersion"
        ]
      }
    },
    "StorageType": {
      "Description": "StorageType",
      "Value": {
        "Fn::GetAtt": [
          "ClickHouseDBCluster",
          "StorageType"
        ]
      }
    },
    "ZoneId": {
      "Description": "ZoneId",
      "Value": {
        "Fn::GetAtt": [
          "ClickHouseDBCluster",
          "ZoneId"
        ]
      }
    },
    "VSwitchId": {
      "Description": "VSwitchId",
      "Value": {
        "Fn::GetAtt": [
          "ClickHouseDBCluster",
          "VSwitchId"
        ]
      }
    },
    "DBClusterDescription": {
      "Description": "DBClusterDescription",
      "Value": {
        "Fn::GetAtt": [
          "ClickHouseDBCluster",
          "DBClusterDescription"
        ]
      }
    },
    "Period": {
      "Description": "Prepaid time period.If the payment type is Prepaid, this parameter is mandatory. Specify the prepaid cluster as a yearly or monthly type. Valid values:  Year, Month.",
      "Value": {
        "Fn::GetAtt": [
          "ClickHouseDBCluster",
          "Period"
        ]
      }
    },
    "LockMode": {
      "Description": "LockMode",
      "Value": {
        "Fn::GetAtt": [
          "ClickHouseDBCluster",
          "LockMode"
        ]
      }
    },
    "DBNodeClass": {
      "Description": "DBNodeClass",
      "Value": {
        "Fn::GetAtt": [
          "ClickHouseDBCluster",
          "DBNodeClass"
        ]
      }
    },
    "VpcId": {
      "Description": "VpcId",
      "Value": {
        "Fn::GetAtt": [
          "ClickHouseDBCluster",
          "VpcId"
        ]
      }
    },
    "VpcCloudInstanceId": {
      "Description": "VpcCloudInstanceId",
      "Value": {
        "Fn::GetAtt": [
          "ClickHouseDBCluster",
          "VpcCloudInstanceId"
        ]
      }
    },
    "ConnectionString": {
      "Description": "ConnectionString",
      "Value": {
        "Fn::GetAtt": [
          "ClickHouseDBCluster",
          "ConnectionString"
        ]
      }
    },
    "PublicPort": {
      "Description": "PublicPort",
      "Value": {
        "Fn::GetAtt": [
          "ClickHouseDBCluster",
          "PublicPort"
        ]
      }
    },
    "AliUid": {
      "Description": "AliUid",
      "Value": {
        "Fn::GetAtt": [
          "ClickHouseDBCluster",
          "AliUid"
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
  Category:
    Description: 'Series, value: Basic: Basic version'
    Type: String
  DBClusterDescription:
    Description: DBClusterDescription
    Type: String
  DBClusterNetworkType:
    Description: 'Network type of the cluster instance, value: VPC'
    Type: String
  DBClusterType:
    Description: 'Cluster instance type, value:  Common: normal instance;  Readonly:
      read-only instance; Guard: disaster recovery instance'
    Type: String
  DBClusterVersion:
    Description: 'Version, value:  19.15.2.2'
    Type: String
  DBNodeCount:
    Description: Number of node groups
    Type: Number
  DBNodeStorage:
    Description: DBNodeStorage
    Type: Number
  DbNodeStorageType:
    Description: 'Instance node storage type. Valid values:  cloud_essd, cloud_efficiency.'
    Type: String
  EncryptionKey:
    Description: KMS key ID
    Type: String
  EncryptionType:
    Description: Kms key type, only cloud disk encryption is supported and the value
      is CloudDisk.
    Type: String
  PaymentType:
    Description: PayType
    Type: String
  Period:
    Description: 'Prepaid time period.If the payment type is Prepaid, this parameter
      is mandatory. Specify the prepaid cluster as a yearly or monthly type. Valid
      values:  Year, Month.'
    Type: String
  UsedTime:
    Description: When Period is Month, the value of UsedTime is [1-9].  When Period
      is Year, the value of UsedTime is [1-3]
    Type: String
  VSwitchId:
    Description: VSwitchId
    Type: String
  VpcId:
    Description: VpcId
    Type: String
  ZoneId:
    Description: ZoneId
    Type: String
Resources:
  ClickHouseDBCluster:
    Properties:
      Category:
        Ref: Category
      DBClusterDescription:
        Ref: DBClusterDescription
      DBClusterNetworkType:
        Ref: DBClusterNetworkType
      DBClusterType:
        Ref: DBClusterType
      DBClusterVersion:
        Ref: DBClusterVersion
      DBNodeCount:
        Ref: DBNodeCount
      DBNodeStorage:
        Ref: DBNodeStorage
      DbNodeStorageType:
        Ref: DbNodeStorageType
      EncryptionKey:
        Ref: EncryptionKey
      EncryptionType:
        Ref: EncryptionType
      PaymentType:
        Ref: PaymentType
      Period:
        Ref: Period
      UsedTime:
        Ref: UsedTime
      VSwitchId:
        Ref: VSwitchId
      VpcId:
        Ref: VpcId
      ZoneId:
        Ref: ZoneId
    Type: ALIYUN::ClickHouse::DBCluster
Outputs:
  AliUid:
    Description: AliUid
    Value:
      Fn::GetAtt:
      - ClickHouseDBCluster
      - AliUid
  Bid:
    Description: BusinessID
    Value:
      Fn::GetAtt:
      - ClickHouseDBCluster
      - Bid
  Category:
    Description: 'Series, value: Basic: Basic version'
    Value:
      Fn::GetAtt:
      - ClickHouseDBCluster
      - Category
  CommodityCode:
    Description: Product Code
    Value:
      Fn::GetAtt:
      - ClickHouseDBCluster
      - CommodityCode
  ConnectionString:
    Description: ConnectionString
    Value:
      Fn::GetAtt:
      - ClickHouseDBCluster
      - ConnectionString
  DBClusterDescription:
    Description: DBClusterDescription
    Value:
      Fn::GetAtt:
      - ClickHouseDBCluster
      - DBClusterDescription
  DBClusterId:
    Description: The id of DBCluster
    Value:
      Fn::GetAtt:
      - ClickHouseDBCluster
      - DBClusterId
  DBClusterNetworkType:
    Description: 'Network type of the cluster instance, value: VPC'
    Value:
      Fn::GetAtt:
      - ClickHouseDBCluster
      - DBClusterNetworkType
  DBClusterType:
    Description: 'Cluster instance type, value:  Common: normal instance;  Readonly:
      read-only instance; Guard: disaster recovery instance'
    Value:
      Fn::GetAtt:
      - ClickHouseDBCluster
      - DBClusterType
  DBClusterVersion:
    Description: 'Version, value:  19.15.2.2'
    Value:
      Fn::GetAtt:
      - ClickHouseDBCluster
      - DBClusterVersion
  DBNodeClass:
    Description: DBNodeClass
    Value:
      Fn::GetAtt:
      - ClickHouseDBCluster
      - DBNodeClass
  DBNodeCount:
    Description: Number of node groups
    Value:
      Fn::GetAtt:
      - ClickHouseDBCluster
      - DBNodeCount
  DBNodeStorage:
    Description: DBNodeStorage
    Value:
      Fn::GetAtt:
      - ClickHouseDBCluster
      - DBNodeStorage
  DbNodeStorageType:
    Description: 'Instance node storage type. Valid values:  cloud_essd, cloud_efficiency.'
    Value:
      Fn::GetAtt:
      - ClickHouseDBCluster
      - DbNodeStorageType
  EncryptionKey:
    Description: KMS key ID
    Value:
      Fn::GetAtt:
      - ClickHouseDBCluster
      - EncryptionKey
  EncryptionType:
    Description: Kms key type, only cloud disk encryption is supported and the value
      is CloudDisk.
    Value:
      Fn::GetAtt:
      - ClickHouseDBCluster
      - EncryptionType
  Engine:
    Description: Engine
    Value:
      Fn::GetAtt:
      - ClickHouseDBCluster
      - Engine
  EngineVersion:
    Description: EngineVersion
    Value:
      Fn::GetAtt:
      - ClickHouseDBCluster
      - EngineVersion
  IsExpired:
    Description: IsExpired
    Value:
      Fn::GetAtt:
      - ClickHouseDBCluster
      - IsExpired
  LockMode:
    Description: LockMode
    Value:
      Fn::GetAtt:
      - ClickHouseDBCluster
      - LockMode
  LockReason:
    Description: Reason for lock
    Value:
      Fn::GetAtt:
      - ClickHouseDBCluster
      - LockReason
  PaymentType:
    Description: PayType
    Value:
      Fn::GetAtt:
      - ClickHouseDBCluster
      - PaymentType
  Period:
    Description: 'Prepaid time period.If the payment type is Prepaid, this parameter
      is mandatory. Specify the prepaid cluster as a yearly or monthly type. Valid
      values:  Year, Month.'
    Value:
      Fn::GetAtt:
      - ClickHouseDBCluster
      - Period
  Port:
    Description: Connection port
    Value:
      Fn::GetAtt:
      - ClickHouseDBCluster
      - Port
  PublicConnectionString:
    Description: Internet connection address
    Value:
      Fn::GetAtt:
      - ClickHouseDBCluster
      - PublicConnectionString
  PublicPort:
    Description: PublicPort
    Value:
      Fn::GetAtt:
      - ClickHouseDBCluster
      - PublicPort
  StorageType:
    Description: StorageType
    Value:
      Fn::GetAtt:
      - ClickHouseDBCluster
      - StorageType
  VSwitchId:
    Description: VSwitchId
    Value:
      Fn::GetAtt:
      - ClickHouseDBCluster
      - VSwitchId
  VpcCloudInstanceId:
    Description: VpcCloudInstanceId
    Value:
      Fn::GetAtt:
      - ClickHouseDBCluster
      - VpcCloudInstanceId
  VpcId:
    Description: VpcId
    Value:
      Fn::GetAtt:
      - ClickHouseDBCluster
      - VpcId
  ZoneId:
    Description: ZoneId
    Value:
      Fn::GetAtt:
      - ClickHouseDBCluster
      - ZoneId
```

