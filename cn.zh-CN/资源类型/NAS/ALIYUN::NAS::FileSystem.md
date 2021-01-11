# ALIYUN::NAS::FileSystem

ALIYUN::NAS::FileSystem类型用于创建文件系统。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ProtocolType|String|是|否|协议类型。|取值： -   NFS
-   SMB |
|StorageType|String|是|否|存储类型。|取值：-   当FileSystemType取值为standard时：
    -   Performance：性能型。
    -   Capacity：容量型。
-   当FileSystemType取值为extreme或cpfs时：
    -   standard：标准型。
    -   advance：高级型。 |
|DeletionForce|Boolean|否|是|是否强制删除。|取值：-   true
-   false（默认值） |
|Description|String|否|是|文件系统描述。|长度为2~128个字符。必须以英文字母或汉字开头，不能以`http://`和`https://`开头。可包含英文字母、汉字、数字、半角冒号（:）、下划线（\_）和短划线（-）。|
|ZoneId|String|否|否|可用区ID。|无|
|Tags|List|否|否|标签。|每个实例最多绑定20个标签。更多信息，请参见[Tags属性](#section_dqo_kff_kje)。 |
|SnapshotId|String|否|否|快照ID。|可以通过指定SnapshotId从指定快照创建NAS实例，目前仅支持极速型NAS。**说明：** 通过快照创建文件系统，创建的文件系统版本和快照源文件系统版本一致。如果快照的源文件系统版本是1，需要创建版本2性能规格的文件系统，可以先通过快照创建一个文件系统，然后再创建一个新的文件系统，把通过快照创建的文件系统中的数据拷贝到新创建的文件系统，拷贝完成后把业务迁移到新的文件系统即可。 |
|EncryptType|Integer|否|否|文件系统是否加密。使用KMS托管密钥，对文件系统落盘数据进行加密存储。 在读写加密数据时，无需解密。|当FileSystemType取值为standard或extreme时该参数有效。取值： -   0：不加密。
-   1：加密。 |
|Capacity|Integer|否|否|文件系统容量。|当FileSystemType取值为standard或extreme时该参数有效且必须指定。取值：-   当FileSystemType取值为extreme时：100~262,144。
-   当FileSystemType取值为cpfs时：2048~512,000。

单位：GB。 |
|FileSystemType|String|否|否|文件系统类型。|取值： -   standard（默认值）：通用型。
-   extreme：极速型。
-   cpfs：并行文件系统。 |
|VpcId|String|否|否|专有网络ID，指定VpcId和VSwitchId可以在创建文件系统实例的同时预配置一个默认挂载点。|当FileSystemType取值为cpfs时该参数必须指定。|
|Bandwidth|Integer|否|否|文件系统吞吐上限。|当FileSystemType取值为cpfs时该参数必须指定，取值根据Capacity确定。更多信息，请参见[CPFS购买页面](https://common-buy.aliyun.com/?commodityCode=nas_cpfs_post&regionId=cn-hangzhou)。 单位：MB/s。 |
|VSwitchId|String|否|否|交换机ID，指定VpcId和VSwitchId可以在创建文件系统实例的同时预配置一个默认挂载点。|当FileSystemType取值为cpfs时该参数必须指定。|
|Duration|Integer|否|否|包年包月时长。|当ChargeType取值为Subscription时该参数有效且必须指定。当包年包月实例到期时未进行续费，实例会自动到期释放。取值：-   1
-   2
-   3
-   6
-   12
-   36

单位：月。 |
|ChargeType|String|否|是|付费类型。|取值：-   PayAsYouGo：按量付费。
-   Subscription：包年包月。 |

## Tags语法

```
"Tags": [
  {
    "Key": String,
    "Value": String
  }
]  
```

## Tags属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Key|String|是|否|标签键。|长度为1~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或`https://` 。|
|Value|String|否|否|标签值。|长度为0~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或`https://` 。|

## 返回值

Fn::GetAtt

FileSystemId：文件系统ID。

## 示例

`JSON`格式

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

`YAML`格式

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

