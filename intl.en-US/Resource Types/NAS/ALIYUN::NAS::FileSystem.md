# ALIYUN::NAS::FileSystem

ALIYUN::NAS::FileSystem is used to create a file system.

## Syntax

```
{
  "Type": "ALIYUN::NAS::FileSystem",
  "Properties": {
    "SnapshotId": String,
    "Description": String,
    "StorageType": String,
    "DeletionForce": Boolean,
    "EncryptType": Integer,
    "VpcId": String,
    "ZoneId": String,
    "Capacity": Integer,
    "Tags": List,
    "ProtocolType": String,
    "FileSystemType": String,
    "Bandwidth": Integer,
    "VSwitchId": String,
    "Duration": Integer,
    "ChargeType": String
  }
}  
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ProtocolType|String|Yes|No|The protocol type.|Valid values: -   NFS
-   SMB |
|StorageType|String|Yes|No|The storage type.|-   Valid values when FileSystemType is set to standard:
    -   Performance
    -   Capacity
-   Valid values when FileSystemType is set to extreme or cpfs:
    -   standard
    -   advance |
|DeletionForce|Boolean|No|Yes|Specifies whether to forcibly delete all mount targets on the file system and then delete the file system.|Default value: false. Valid values:-   true
-   false |
|Description|String|No|Yes|The description of the file system.|The description must be 2 to 128 characters in length and can contain letters, digits, colons\(:\), underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with `http://` or `https://`.|
|ZoneId|String|No|No|The ID of the zone.|None|
|Tags|List|No|No|The list of one or more tags of the file system.|You can bind up to 20 tags to each file system.For more information, see [Tags properties](#section_dqo_kff_kje). |
|SnapshotId|String|No|No|The ID of the snapshot.|You can specify this parameter to create the NAS file system from the specified snapshot. This parameter takes effect only for Extreme NAS.**Note:** If you create a file system from a snapshot, the version of the file system is the same as the version of the source file system of the snapshot. If the version of the source file system of a snapshot is 1 and you want to create a file system of version 2, perform the following operations: Create a file system \(File System 1\) from the snapshot. Create another file system \(File System 2\) whose version is 2. Migrate data from File System 1 to File System 2. Switch your business from File System 1 to File System 2. |
|EncryptType|Integer|No|No|Specifies whether to encrypt the file system. You can use keys that are hosted by Key Management Service \(KMS\) to encrypt data that is stored in a file system. Data is automatically decrypted when you access encrypted data.|This parameter takes effect only when the FileSystemType parameter is set to standard or extreme. Valid values: -   0: The file system is not encrypted.
-   1: The file system is encrypted. |
|Capacity|Integer|No|No|The capacity of the file system.|This parameter takes effect only when the FileSystemType parameter is set to standard or extreme. -   Valid values when FileSystemType is set to extreme: 100 to 262144.
-   Valid values when FileSystemType is set to cpfs: 2048 to 512000.

Unit: GB. |
|FileSystemType|String|No|No|The type of the file system.|Default value: standard. Valid values: -   standard
-   extreme
-   cpfs |
|VpcId|String|No|No|The ID of the VPC. If you specify the VpcId and VSwitchId parameters, a default mount target is pre-configured when the file system is created.|This parameter is required when the FileSystemType parameter is set to cpfs.|
|Bandwidth|Integer|No|No|The maximum throughput of the file system.|This parameter is required when the FileSystemType parameter is set to cpfs. The value of this parameter is determined by the Capacity parameter. For more information, see the [CPFS buy page](https://common-buy.aliyun.com/?commodityCode=nas_cpfs_post&regionId=cn-hangzhou). Unit: Mbit/s. |
|VSwitchId|String|No|No|The ID of the vSwitch. If you specify the VpcId and VSwitchId parameters, a default mount target is pre-configured when the file system is created.|This parameter is required when the FileSystemType parameter is set to cpfs.|
|Duration|Integer|No|No|The subscription period of the file system.|This parameter is valid and required only when the ChargeType parameter is set to Subscription. If you do not renew a subscription file system before it expires, the file system is released. Valid values:-   1
-   2
-   3
-   6
-   12
-   36

Unit: months. |
|ChargeType|String|No|Yes|The billing method of the file system.|Valid values:-   PayAsYouGo
-   Subscription |

## Tags syntax

```
"Tags": [
  {
    "Key": String,
    "Value": String
  }
]  
```

## Tags properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Key|String|Yes|No|The key of the tag.|The tag key must be 1 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|
|Value|String|No|No|The value of the tag.|The tag value must be 0 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|

## Response parameters

Fn::GetAtt

FileSystemId: the ID of the file system.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Description": {
      "Type": "String",
      "Description": "File system description (space characters are not allowed)"
    },
    "StorageType": {
      "Type": "String",
      "Description": "The file system type. Currently includes the Performance type and the Capacity type"
    },
    "ZoneId": {
      "Type": "String",
      "Description": "Zone ID."
    },
    "VSwitchId": {
      "Type": "String",
      "Description": "VSwitch ID."
    },
    "Duration": {
      "Type": "Number",
      "Description": "The period of subscription in months. Required and valid when ChargeType is Subscription.\nWhen the annual and monthly subscription instance expires without renewal, the instance will automatically expire and be released."
    },
    "SnapshotId": {
      "Type": "String",
      "Description": "Snapshot ID."
    },
    "DeletionForce": {
      "Type": "Boolean",
      "Description": "Whether delete all mount targets on the file system and then delete file system. Default is false",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ],
      "Default": false
    },
    "EncryptType": {
      "Type": "Number",
      "Description": "Specifies whether to encrypt data. You can use keys that are hosted by Key Management Service (KMS) to encrypt data stored on a file system. Data is automatically decrypted when you access encrypted data. Valid values:\n0: specifies that no encryption is applied to data on the file system.\n1: specifies that encryption is applied to data on the file system."
    },
    "VpcId": {
      "Type": "String",
      "Description": "Vpc ID."
    },
    "Capacity": {
      "Type": "Number",
      "Description": "File system capacity, the unit is GB. Required and valid when FileSystemType=extreme or cpfs."
    },
    "ProtocolType": {
      "Type": "String",
      "Description": "Type of protocol used. Currently includes the NFS type and the SMB type",
      "AllowedValues": [
        "NFS",
        "SMB"
      ]
    },
    "ChargeType": {
      "Type": "String",
      "Description": "Type of payment:\nPayAsYouGo (pay as you go)\nSubscription",
      "AllowedValues": [
        "PayAsYouGo",
        "Subscription"
      ]
    },
    "FileSystemType": {
      "Type": "String",
      "Description": "File system type. Allowed values: standard, extreme, cpfs"
    },
    "Bandwidth": {
      "Type": "Number",
      "Description": "Maximum file system throughput, unit is MB/s. Required and valid only when FileSystemType=cpfs."
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to filesystem. Max support 20 tags to add during create filesystem. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
    }
  },
  "Resources": {
    "FileSystem": {
      "Type": "ALIYUN::NAS::FileSystem",
      "Properties": {
        "Description": {
          "Ref": "Description"
        },
        "StorageType": {
          "Ref": "StorageType"
        },
        "ZoneId": {
          "Ref": "ZoneId"
        },
        "VSwitchId": {
          "Ref": "VSwitchId"
        },
        "Duration": {
          "Ref": "Duration"
        },
        "SnapshotId": {
          "Ref": "SnapshotId"
        },
        "DeletionForce": {
          "Ref": "DeletionForce"
        },
        "EncryptType": {
          "Ref": "EncryptType"
        },
        "VpcId": {
          "Ref": "VpcId"
        },
        "Capacity": {
          "Ref": "Capacity"
        },
        "ProtocolType": {
          "Ref": "ProtocolType"
        },
        "ChargeType": {
          "Ref": "ChargeType"
        },
        "FileSystemType": {
          "Ref": "FileSystemType"
        },
        "Bandwidth": {
          "Ref": "Bandwidth"
        },
        "Tags": {
          "Ref": "Tags"
        }
      }
    }
  },
  "Outputs": {
    "FileSystemId": {
      "Description": "ID of the file system created",
      "Value": {
        "Fn::GetAtt": [
          "FileSystem",
          "FileSystemId"
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
  Description:
    Type: String
    Description: File system description (space characters are not allowed)
  StorageType:
    Type: String
    Description: >-
      The file system type. Currently includes the Performance type and the
      Capacity type
  ZoneId:
    Type: String
    Description: Zone ID.
  VSwitchId:
    Type: String
    Description: VSwitch ID.
  Duration:
    Type: Number
    Description: >-
      The period of subscription in months. Required and valid when ChargeType
      is Subscription.

      When the annual and monthly subscription instance expires without renewal,
      the instance will automatically expire and be released.
  SnapshotId:
    Type: String
    Description: Snapshot ID.
  DeletionForce:
    Type: Boolean
    Description: >-
      Whether delete all mount targets on the file system and then delete file
      system. Default is false
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
    Default: false
  EncryptType:
    Type: Number
    Description: >-
      Specifies whether to encrypt data. You can use keys that are hosted by Key
      Management Service (KMS) to encrypt data stored on a file system. Data is
      automatically decrypted when you access encrypted data. Valid values:

      0: specifies that no encryption is applied to data on the file system.

      1: specifies that encryption is applied to data on the file system.
  VpcId:
    Type: String
    Description: Vpc ID.
  Capacity:
    Type: Number
    Description: >-
      File system capacity, the unit is GB. Required and valid when
      FileSystemType=extreme or cpfs.
  ProtocolType:
    Type: String
    Description: Type of protocol used. Currently includes the NFS type and the SMB type
    AllowedValues:
      - NFS
      - SMB
  ChargeType:
    Type: String
    Description: |-
      Type of payment:
      PayAsYouGo (pay as you go)
      Subscription
    AllowedValues:
      - PayAsYouGo
      - Subscription
  FileSystemType:
    Type: String
    Description: 'File system type. Allowed values: standard, extreme, cpfs'
  Bandwidth:
    Type: Number
    Description: >-
      Maximum file system throughput, unit is MB/s. Required and valid only when
      FileSystemType=cpfs.
  Tags:
    Type: Json
    Description: >-
      Tags to attach to filesystem. Max support 20 tags to add during create
      filesystem. Each tag with two properties Key and Value, and Key is
      required.
    MaxLength: 20
Resources:
  FileSystem:
    Type: 'ALIYUN::NAS::FileSystem'
    Properties:
      Description:
        Ref: Description
      StorageType:
        Ref: StorageType
      ZoneId:
        Ref: ZoneId
      VSwitchId:
        Ref: VSwitchId
      Duration:
        Ref: Duration
      SnapshotId:
        Ref: SnapshotId
      DeletionForce:
        Ref: DeletionForce
      EncryptType:
        Ref: EncryptType
      VpcId:
        Ref: VpcId
      Capacity:
        Ref: Capacity
      ProtocolType:
        Ref: ProtocolType
      ChargeType:
        Ref: ChargeType
      FileSystemType:
        Ref: FileSystemType
      Bandwidth:
        Ref: Bandwidth
      Tags:
        Ref: Tags
Outputs:
  FileSystemId:
    Description: ID of the file system created
    Value:
      'Fn::GetAtt':
        - FileSystem
        - FileSystemId
```

