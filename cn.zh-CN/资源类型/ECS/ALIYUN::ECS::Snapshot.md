# ALIYUN::ECS::Snapshot

ALIYUN::ECS::Snapshot类型用于创建磁盘快照。

## 语法

```
{
  "Type": "ALIYUN::ECS::Snapshot",
  "Properties": {
    "SnapshotName": String,
    "Timeout": Integer,
    "Description": String,
    "DiskId": String,
    "Tags": List,
    "InstantAccess": Boolean,
    "InstantAccessRetentionDays": Integer
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|DiskId|String|是|否|将要创建磁盘快照的磁盘ID。|无|
|SnapshotName|String|否|否|快照的显示名称。|长度为2~128个字符。必须以英文字母或汉字开头，不能以`http://`和`https://`开头。可包含英文字母、汉字、数字、半角冒号（:）、下划线（\_）或短划线（-）。为防止和自动快照的名称冲突，不能以auto开头。 |
|Timeout|Integer|否|否|创建快照的超时时间。|设置此时间会延长创建资源栈的超时时间。如果快照在指定的时间内没有创建完成，则整个资源栈将创建失败。请根据磁盘的大小，数据的多少，设置合理的超时时间。取值范围：200~1440。

默认值：200。

单位：分钟。 |
|Description|String|否|否|快照的描述。|快照的描述。长度为2~256个字符，不能以`http://`和`https://`开头。默认值：空。 |
|Tags|List|否|是|标签。|最多支持添加20个标签。更多信息，请参见[Tags属性](#section_ttw_qfo_o7h)。 |
|InstantAccess|Boolean|否|否|是否开启快照极速可用功能。|取值：-   true：开启。仅ESSD云盘支持开启该功能。
-   false（默认值）：关闭。即创建普通快照。 |
|InstantAccessRetentionDays|Integer|否|否|设置快照极速可用功能的保留时间，保留时间到期后快照将自动释放。|该参数仅在InstantAccess取值为true时生效。取值范围：1~65,535。

单位：天。|

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
|Key|String|是|否|标签键。|长度为1~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或者`https://` 。|
|Value|String|否|否|标签值。|长度为0~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或者`https://` 。|

## 返回值

Fn::GetAtt

SnapshotId：快照ID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "InstantAccess": {
      "Type": "Boolean",
      "Description": "Specifies whether to enable the instant access feature. Valid values: \ntrue: enables the instant access feature. This feature can be enabled only for enhanced SSDs (ESSDs) \nfalse: disables the instant access feature. If InstantAccess is set to false, normal snapshots are created.\nDefault value: false.\nNote This parameter and the Category parameter cannot be specified at the same time. \nFor more information, see the \"Description\" section in this topic.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "Description": {
      "Type": "String",
      "Description": "The description of a snapshot can be 2 to 256 characters in length and cannot begin with http:// or https://. The description will appear on the console. By default, the value is zero."
    },
    "Timeout": {
      "Type": "Number",
      "Description": "The number of minutes to wait for create snapshot.",
      "MinValue": 200,
      "MaxValue": 1440,
      "Default": 200
    },
    "SnapshotName": {
      "Type": "String",
      "Description": "The name of the snapshot, [2, 128] English or Chinese characters. It must begin with an uppercase/lowercase letter or a Chinese character, and may contain numbers, '_' or '-'. It cannot begin with http:// or https://."
    },
    "InstantAccessRetentionDays": {
      "Type": "Number",
      "Description": "Specifies the retention period of the instant access feature. After the retention period ends, \nthe snapshot is automatically released. This parameter takes effect only when InstantAccess \nis set to true. Unit: days.\nValid values: 1 to 65535. By default, the value of \nthis parameter is the same as that of RetentionDays."
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to instance. Max support 20 tags to add during create instance. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
    },
    "DiskId": {
      "Type": "String",
      "Description": "Indicates the ID of the specified disk."
    }
  },
  "Resources": {
    "Snapshot": {
      "Type": "ALIYUN::ECS::Snapshot",
      "Properties": {
        "InstantAccess": {
          "Ref": "InstantAccess"
        },
        "Description": {
          "Ref": "Description"
        },
        "Timeout": {
          "Ref": "Timeout"
        },
        "SnapshotName": {
          "Ref": "SnapshotName"
        },
        "InstantAccessRetentionDays": {
          "Ref": "InstantAccessRetentionDays"
        },
        "Tags": {
          "Ref": "Tags"
        },
        "DiskId": {
          "Ref": "DiskId"
        }
      }
    }
  },
  "Outputs": {
    "SnapshotId": {
      "Description": "The snapshot ID.",
      "Value": {
        "Fn::GetAtt": [
          "Snapshot",
          "SnapshotId"
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
    Description: The description of a snapshot can be 2 to 256 characters in length
      and cannot begin with http:// or https://. The description will appear on the
      console. By default, the value is zero.
    Type: String
  DiskId:
    Description: Indicates the ID of the specified disk.
    Type: String
  InstantAccess:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Description: "Specifies whether to enable the instant access feature. Valid values:\
      \ \ntrue: enables the instant access feature. This feature can be enabled only\
      \ for enhanced SSDs (ESSDs) \nfalse: disables the instant access feature. If\
      \ InstantAccess is set to false, normal snapshots are created.\nDefault value:\
      \ false.\nNote This parameter and the Category parameter cannot be specified\
      \ at the same time. \nFor more information, see the \"Description\" section\
      \ in this topic."
    Type: Boolean
  InstantAccessRetentionDays:
    Description: "Specifies the retention period of the instant access feature. After\
      \ the retention period ends, \nthe snapshot is automatically released. This\
      \ parameter takes effect only when InstantAccess \nis set to true. Unit: days.\n\
      Valid values: 1 to 65535. By default, the value of \nthis parameter is the same\
      \ as that of RetentionDays."
    Type: Number
  SnapshotName:
    Description: The name of the snapshot, [2, 128] English or Chinese characters.
      It must begin with an uppercase/lowercase letter or a Chinese character, and
      may contain numbers, '_' or '-'. It cannot begin with http:// or https://.
    Type: String
  Tags:
    Description: Tags to attach to instance. Max support 20 tags to add during create
      instance. Each tag with two properties Key and Value, and Key is required.
    MaxLength: 20
    Type: Json
  Timeout:
    Default: 200
    Description: The number of minutes to wait for create snapshot.
    MaxValue: 1440
    MinValue: 200
    Type: Number
Resources:
  Snapshot:
    Properties:
      Description:
        Ref: Description
      DiskId:
        Ref: DiskId
      InstantAccess:
        Ref: InstantAccess
      InstantAccessRetentionDays:
        Ref: InstantAccessRetentionDays
      SnapshotName:
        Ref: SnapshotName
      Tags:
        Ref: Tags
      Timeout:
        Ref: Timeout
    Type: ALIYUN::ECS::Snapshot
Outputs:
  SnapshotId:
    Description: The snapshot ID.
    Value:
      Fn::GetAtt:
      - Snapshot
      - SnapshotId
```

更多示例，请参见挂载ECS磁盘和创建磁盘快照的组合示例：[JSON示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ECS/JSON/DiskAttachment.json)和[YAML示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ECS/YAML/DiskAttachment.yml)。

