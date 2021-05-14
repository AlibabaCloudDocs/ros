# ALIYUN::ECS::Snapshot

ALIYUN::ECS::Snapshot is used to create a disk snapshot.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|DiskId|String|Yes|No|The ID of the disk for which you want to create the snapshot.|None|
|SnapshotName|String|No|No|The name of the snapshot.|The name must be 2 to 128 characters in length and can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with `http://` or `https://`. The name cannot start with auto because a snapshot whose name starts with auto is recognized as an automatic snapshot. |
|Timeout|Integer|No|No|The timeout period of the snapshot creation task.|If this parameter is specified, the timeout period to create a stack is extended. If the snapshot is not created within the specified timeout period, the entire stack cannot be created. Set this parameter based on the disk size and data volume. Valid values: 200 to 1440.

Default value: 200.

Unit: minutes. |
|Description|String|No|No|The description of the snapshot.|The description must be 2 to 256 characters in length and cannot start with `http://` or `https://`. This parameter is empty by default. |
|Tags|List|No|Yes|The tags of the snapshot.|A maximum of 20 tags can be specified. For more information, see the [Tags properties](#section_ttw_qfo_o7h) section in this topic. |
|InstantAccess|Boolean|No|No|Specifies whether to enable the instant access feature.|Default value: false. Valid values:-   true: The instant access feature is enabled. This feature can be enabled only for enhanced SSDs \(ESSDs\).
-   false: The instant access feature is disabled. If InstantAccess is set to false, normal snapshots are created. |
|InstantAccessRetentionDays|Integer|No|No|Specifies the retention period of the instant access feature. After the retention period ends, the snapshot is automatically released.|This parameter is valid only when InstantAccess is set to true. Valid values: 1 to 65535.

Unit: days.|

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
|Key|String|Yes|No|The tag key.|The tag key must be 1 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|
|Value|String|No|No|The tag value.|The tag value must be 0 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|

## Response parameters

Fn::GetAtt

SnapshotId: the ID of the snapshot.

## Examples

`JSON` format

```
{
"ROSTemplateFormatVersion": "2015-09-01",
  "Parameters":
{
    "InstantAccess": {
      "Type":
"Boolean",
      "Description": "Specifies whether to enable the instant access feature.
Valid values: \ntrue: enables the instant access feature.
This feature can be enabled only for enhanced SSDs (ESSDs) \nfalse: disables the instant access feature. If InstantAccess is set to false, normal snapshots are created.\nDefault value: false.\nNote This parameter and the Category parameter cannot be specified at the same time. \nFor more information, see the \"Description\" section in this topic.", "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "Description": {
      "Type": "String",
      "Description":
"The description of a snapshot can be 2 to 256 characters in length and cannot begin with http:// or https://. The description will appear on the console.
By default, the value is zero."
},
    "Timeout":
{
      "Type":
"Number",
      "Description":
"The number of minutes to wait for create snapshot.",
"MinValue":
200,
      "MaxValue": 1440,
      "Default":
200
    },
    "SnapshotName": {
      "Type":
"String",
      "Description": "The name of the snapshot, [2, 128] English or Chinese characters. It must begin with an uppercase/lowercase letter or a Chinese character, and may contain numbers, '_' or '-'. It cannot begin with http:// or https://." },
    "InstantAccessRetentionDays":
{
      "Type":
"Number",
      "Description": "Specifies the retention period of the instant access feature.
After the retention period ends, \nthe snapshot is automatically released. This parameter takes effect only when InstantAccess \nis set to true.
Unit: days.\nValid values: 1 to 65535.
By default, the value of \nthis parameter is the same as that of RetentionDays." },
    "Tags":
{
      "Type": "Json",
      "Description":
"Tags to attach to instance. Max support 20 tags to add during create instance.
Each tag with two properties Key and Value, and Key is required.",
"MaxLength": 20
    },
    "DiskId":
{
      "Type": "String",
      "Description":
"Indicates the ID of the specified disk." }
  },
  "Resources": {
    "Snapshot": {
      "Type":
"ALIYUN::ECS::Snapshot",
      "Properties":
{
        "InstantAccess": {
          "Ref":
"InstantAccess"
        },
        "Description": {
          "Ref":
"Description"
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
        "Tags":
{
          "Ref":
"Tags"
        },
        "DiskId": {
          "Ref":
"DiskId"
        }
      }
    }
  },
  "Outputs": {
    "SnapshotId":
{
      "Description": "The snapshot ID.", "Value": {
        "Fn::GetAtt":
[
          "Snapshot",
          "SnapshotId"
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
Description: The description of a snapshot can be 2 to 256 characters in length
      and cannot begin with http:// or https://.
The description will appear on the
      console. By default, the value is zero.
Type: String
  DiskId:
Description: Indicates the ID of the specified disk.
Type:
String
  InstantAccess: AllowedValues:
- 'True'
    - 'true'
    - 'False'
    - 'false'
    Description: "Specifies whether to enable the instant access feature.
Valid values:\
\ \ntrue: enables the instant access feature.
This feature can be enabled only\
      \ for enhanced SSDs (ESSDs) \nfalse: disables the instant access feature.
If\
      \ InstantAccess is set to false, normal snapshots are created.\nDefault value:\
\ false.\nNote This parameter and the Category parameter cannot be specified\
      \ at the same time.
\nFor more information, see the \"Description\" section\
      \ in this topic."
Type: Boolean
  InstantAccessRetentionDays: Description:
"Specifies the retention period of the instant access feature. After\
      \ the retention period ends, \nthe snapshot is automatically released.
This\
      \ parameter takes effect only when InstantAccess \nis set to true. Unit: days.\n\
      Valid values:
1 to 65535.
By default, the value of \nthis parameter is the same\
      \ as that of RetentionDays."
Type: Number
  SnapshotName:
Description:
The name of the snapshot, [2, 128] English or Chinese characters. It must begin with an uppercase/lowercase letter or a Chinese character, and
      may contain numbers, '_' or '-'. It cannot begin with http:// or https://.
Type:
String
  Tags: Description: Tags to attach to instance.
Max support 20 tags to add during create
      instance. Each tag with two properties Key and Value, and Key is required.
MaxLength: 20
    Type:
Json
  Timeout: Default: 200
    Description:
The number of minutes to wait for create snapshot.
MaxValue: 1440
    MinValue:
200
    Type:
Number
Resources: Snapshot:
Properties:
Description: Ref:
Description
      DiskId: Ref:
DiskId
      InstantAccess:
Ref: InstantAccess
      InstantAccessRetentionDays: Ref:
InstantAccessRetentionDays
      SnapshotName: Ref:
SnapshotName
      Tags: Ref:
Tags
      Timeout: Ref:
Timeout
    Type:
ALIYUN::ECS::Snapshot
Outputs: SnapshotId:
Description: The snapshot ID.
Value: Fn::GetAtt:
- Snapshot
      - SnapshotId  
```

For more examples, visit [DiskAttachment.json](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ECS/JSON/DiskAttachment.json) and [DiskAttachment.yml](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ECS/YAML/DiskAttachment.yml). In the examples, the ALIYUN::ECS::DiskAttachment and ALIYUN::ECS::Snapshot resource types are involved.

