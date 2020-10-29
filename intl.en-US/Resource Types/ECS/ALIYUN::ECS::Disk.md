# ALIYUN::ECS::Disk

ALIYUN::ECS::Disk is used to create a disk for an ECS instance.

## Syntax

```
{
  "Type": "ALIYUN::ECS::Disk",
  "Properties": {
    "StorageSetId": String,
    "Description": String,
    "Tags": List,
    "AutoSnapshotPolicyId": String,
    "Encrypted": Boolean,
    "DiskName": String,
    "DiskCategory": String,
    "ResourceGroupId": String,
    "KMSKeyId": String,
    "DeleteAutoSnapshot": Boolean,
    "SnapshotId": String,
    "StorageSetPartitionNumber": Integer,
    "PerformanceLevel": String,
    "ZoneId": String,
    "Size": Integer
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ResourceGroupId|String|No|No|The ID of the resource group to which the ECS instance belongs.|None|
|ZoneId|String|Yes|No|The ID of the zone.|None|
|DiskName|String|No|No|The name of the disk.|The name must be 2 to 128 characters in length and can contain letters, digits, periods \(.\), underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with `http://` or `https://`. The name of a disk is displayed in the console. |
|Description|String|No|No|The description of the disk.|The description must be 2 to 256 characters in length. It cannot start with `http://` or `https://`.The description of a disk is displayed in the console. |
|Tags|List|No|No|The custom tags of the ECS instance.|A maximum of 20 tags can be specified in the `[{"Key": "tagKey", "Value": "tagValue"},{"Key": "tagKey2", "Value": "tagValue2"}]` format.For more information, see [Tags properties](#section_inj_lxd_lfb). |
|DiskCategory|String|No|No|The type of the data disk.|Default value: cloud. Valid values: -   cloud: basic disk
-   cloud\_efficiency: ultra disk
-   cloud\_ssd: standard SSD
-   cloud\_essd: enhanced SSD \(ESSD\) |
|SnapshotId|String|No|No|The ID of the snapshot that is used to create the data disk.|If both this parameter and the Size parameter are specified, this parameter takes effect.The actual size of the created disk is the size of the specified snapshot.

**Note:** The snapshots created on or before July 15, 2013 cannot be used to create disks. |
|PerformanceLevel|String|No|No|The performance level of the ESSD.|Valid values: -   PL1: A single ESSD can deliver up to 50,000 random read/write IOPS.
-   PL2: A single ESSD can deliver up to 100,000 random read/write IOPS.
-   PL3: A single ESSD can deliver up to 1,000,000 random read/write IOPS.

For more information about performance levels of ESSDs, see [Enhanced SSDs](/intl.en-US/Block Storage/Block Storage overview/Enhanced SSDs.md).|
|Size|Integer|No|No|The size of the disk.|-   Valid values when DiskCategory is set to cloud: 5 to 2000.
-   Valid values when DiskCategory is set to cloud\_efficiency: 20 to 32768.
-   Valid values when DiskCategory is set to cloud\_ssd: 20 to 32768.
-   Valid values when DiskCategory is set to cloud\_essd: 20 to 32768.

Unit: GiB.

The value of this parameter must be greater than or equal to the size of the specified snapshot. |
|AutoSnapshotPolicyId|String|No|No|The ID of the automatic snapshot policy.|None|
|Encrypted|Boolean|No|No|Specifies whether to encrypt the disk.|Default value: false. Valid values: -   true
-   false |
|DeleteAutoSnapshot|Boolean|No|No|Specifies whether to delete automatic snapshots of the disk when the disk is released.|Default value: true. Valid values: -   true
-   false |
|StorageSetId|String|No|No|The ID of the storage set.|None|
|KMSKeyId|String|No|No|The ID of the KMS key used by the disk.|None|
|StorageSetPartitionNumber|Integer|No|No|The number of partitions in the storage set.|None|

## Tags syntax

```
"Tags" : [
  {
    "Value" : String,
    "Key" : String
  }
]
```

## Tags properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Key|String|Yes|No|The key of the tag.|The tag key must be 1 to 128 characters in length. It cannot start with `acs:` or `aliyun`. It cannot contain `http://` or `https://`.|
|Value|String|No|No|The value of the tag.|The tag key must be 0 to 128 characters in length and cannot start with `acs:` or `aliyun`. It cannot contain `http://` or `https://`.|

## Response parameters

Fn::GetAtt

-   DiskId: the ID of the created disk.
-   Status: the status of the created disk.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion" : "2015-09-01",
  "Resources" : {
    "DataDisk": {
      "Type": "ALIYUN::ECS::Disk",
      "Properties": {
        "Size": 10,
        "ZoneId": "cn-beijing-a",
        "DiskName": "DataDisk",
        "Description": "ECSDataDisk"
      }
    }
  },
  "Outputs": {
    "DiskId": {
         "Value" : {"Fn::GetAtt": ["DataDisk","DiskId"]}
    },
    "Status": {
         "Value" : {"Fn::GetAtt": ["DataDisk","Status"]}
    }
  }
}
```

`YAML` format

```
ROSTemplateFormatVersion: '2015-09-01'
Resources:
  DataDisk:
    Type: 'ALIYUN::ECS::Disk'
    Properties:
      Size: 10
      ZoneId: cn-beijing-a
      DiskName: DataDisk
      Description: ECSDataDisk
Outputs:
  DiskId:
    Value:
      'Fn::GetAtt':
        - DataDisk
        - DiskId
  Status:
    Value:
      'Fn::GetAtt':
        - DataDisk
        - Status
```

