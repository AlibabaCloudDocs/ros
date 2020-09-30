# ALIYUN::MONGODB::Instance

ALIYUN::MONGODB::Instance is used to create or clone an ApsaraDB for MongoDB replica set instance.

## Syntax

```
{
  "Type": "ALIYUN::MONGODB::Instance",
  "Properties": {
    "DatabaseNames": String,
    "VpcPasswordFree": Boolean,
    "ReadonlyReplicas": Integer,
    "BusinessInfo": String,
    "AccountPassword": String,
    "VpcId": String,
    "AutoRenew": Boolean,
    "ResourceGroupId": String,
    "VSwitchId": String,
    "StorageEngine": String,
    "SrcDBInstanceId": String,
    "ReplicationFactor": Integer,
    "ZoneId": String,
    "EngineVersion": String,
    "RestoreTime": String,
    "DBInstanceStorage": Integer,
    "DBInstanceDescription": String,
    "CouponNo": String,
    "Period": Integer,
    "SecurityIPArray": String,
    "ChargeType": String,
    "BackupId": String,
    "DBInstanceClass": String,
    "NetworkType": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|VpcPasswordFree|Boolean|No|No|Specifies whether to enable the password-free feature for access to the instance from a VPC.|Valid values: -   true
-   false |
|DBInstanceStorage|Integer|Yes|No|The storage capacity of the instance.|Valid values: 5 to 1000. The value must be a multiple of 5 GB.

Unit: GB.|
|DBInstanceClass|String|Yes|No|The type of the instance.|For more information, see [Instance types](/intl.en-US/Product Introduction/Instance types.md).|
|SrcDBInstanceId|String|No|No|The ID of the source instance.|This parameter can be specified only when this operation is called to clone instances. This parameter must be specified with one of the BackupId and RestoreTime parameters.|
|DBInstanceDescription|String|No|No|The description of the instance.|The description must be 2 to 256 characters in length and can contain letters, digits, underscores \(\_\), and hyphens \(-\). It must start with a letter.|
|SecurityIPArray|String|No|No|The list of IP addresses that can access the instance.|If you enter more than one entry, separate them with commas \(,\). Each entry must be unique in the whitelist. The whitelist can contain up to 1,000 entries.

Supported formats include 0.0.0.0/0, 10.23.XX.XX \(IP address format\), and 10.23.XX.XX/24 \(CIDR format\). /24 indicates the length of the prefix in the CIDR block. A prefix length can be in the range of 1 to 32.

The default value is 0.0.0.0/0, which indicates that no access limit is applied. |
|ZoneId|String|No|No|The zone ID of the instance.|For more information, see [DescribeRegions](/intl.en-US/API Reference/Region management/DescribeRegions.md). This parameter must be set to the zone ID of the VSwitch in the VPC.|
|VpcId|String|No|No|The ID of the VPC.|This parameter takes effect only when the NetworkType parameter is set to VPC.|
|VSwitchId|String|No|No|The ID of the VSwitch in the VPC.|This parameter takes effect only when the NetworkType parameter is set to VPC.|
|BackupId|String|No|No|The ID of the backup set.|This parameter can be specified only when this operation is called to clone instances. This parameter must be specified with the SrcDBInstanceId parameter.|
|NetworkType|String|No|No|The network type of the instance.|Default value: CLASSIC. Valid values: -   CLASSIC
-   VPC |
|AccountPassword|String|No|No|The password of the root user.|-   The password must be 8 to 32 characters in length
-   and can contain letters, digits, and special characters. Special characters include

    ```
! # $ % ^ & * ( ) _ + - =
    ``` |
|EngineVersion|String|No|No|The version of the database.|Default value: 3.4. Valid values:-   3.2
-   3.4
-   4.0 |
|StorageEngine|String|No|No|The storage engine of the instance.|For more information about storage engines and versions of instances, see [MongoDB versions and storage engines](/intl.en-US/Product Introduction/MongoDB versions and storage engines.md). Default value: WiredTiger. Valid values:

-   WiredTiger
-   RocksDB
-   TerarkDB |
|ReplicationFactor|Integer|No|No|The number of nodes in the replica set instance.|Default value: 3. Valid values:-   3
-   5
-   7 |
|DatabaseNames|String|No|No|The database name.|None|
|ReadonlyReplicas|Integer|No|No|The number of read-only nodes.|Valid values:-   1
-   2
-   3
-   4
-   5 |
|BusinessInfo|String|No|No|The business information.|This parameter is an additional parameter.|
|ResourceGroupId|String|No|No|The ID of the resource group.|None|
|AutoRenew|Boolean|No|No|Specifies whether to enable auto-renewal for the instance.|Default value: false. Valid values: -   true
-   false |
|RestoreTime|String|No|No|The time to restore data when you clone an instance|Specify the time in the ISO 8601 standard in the yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC. This parameter can be specified only when this operation is called to clone instances. This parameter must be specified with the SrcDBInstanceId and BackupId parameters. You can specify any time in the last seven days for data cloning. |
|CouponNo|String|No|No|The coupon code.|Default value: youhuiquan\_promotion\_option\_id\_for\_blank.|
|Period|Integer|No|No|The subscription period of the instance.|Unit: months. Valid values: 1, 2, 3, 4, 5, 6, 7, 8, 9, 12, 24, and 36.

Default value: 1.

This parameter takes effect only when the ChargeType parameter is set to PrePaid. |
|ChargeType|String|No|No|The unit of the billing method of the instance.|Valid values: -   PostPaid: pay-as-you-go
-   PrePaid: subscription |

## Response parameters

Fn::GetAtt

-   OrderId: the order ID of the instance.
-   DBInstanceId: the unique ID of the instance.
-   DBInstanceStatus: the status of the instance.
-   ConnectionURI: the connection URI.
-   ReplicaSetName: the name of the replica set.

## Examples

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "MongoDB": {
      "Type": "ALIYUN::MONGODB::Instance",
      "Properties": {
        "DBInstanceClass":"dds.mongo.mid",
        "DBInstanceStorage":"10",
        "VpcId": "vpc-25o8s****",
        "VSwitchId": "vsw-25w8q****"
      }
    }
  },
  "Outputs": {
    "DBInstanceStatus": {
      "Description": "Status of mongodb instance.",
      "Value": {
        "Fn::GetAtt": [
          "MongoDB",
          "DBInstanceStatus"
        ]
      }
    },
    "InstanceId": {
      "Description": "The instance id of created mongodb instance.",
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

