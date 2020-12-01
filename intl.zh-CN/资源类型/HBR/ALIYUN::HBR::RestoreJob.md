# ALIYUN::HBR::RestoreJob

ALIYUN::HBR::RestoreJob类型用于创建恢复任务。

## 语法

```
{
  "Type": "ALIYUN::HBR::RestoreJob",
  "Properties": {
    "SnapshotId": String,
    "TargetClientId": String,
    "TargetPath": String,
    "SourceType": String,
    "SourceClientId": String,
    "TargetInstanceId": String,
    "VaultId": String,
    "SourceInstanceId": String,
    "RestoreType": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|SnapshotId|String|是|否|快照ID。|无|
|TargetClientId|String|是|否|目标客户端ID。|当RestoreType取值为FILE时该参数必须指定。|
|TargetPath|String|是|否|恢复路径，将备份数据恢复到指定目录。|示例值：`/`。|
|SourceType|String|是|否|源文件类型。|取值：-   FILE：本地文件。
-   ECS\_FILE：ECS文件。 |
|SourceClientId|String|是|否|源客户端ID。|当SourceType取值为FILE时该参数必须指定。|
|TargetInstanceId|String|是|否|目标客户端ID。|当RestoreType取值为ECS\_FILE时该参数必须指定。|
|VaultId|String|是|否|待恢复的源客户端所在的备份库。|无|
|SourceInstanceId|String|是|否|源实例ID。|当SourceType取值为ECS\_FILE时该参数必须指定。|
|RestoreType|String|是|否|恢复类型。|取值：-   FILE：本地文件。
-   ECS\_FILE：ECS文件。 |

## 返回值

Fn::GetAtt

-   Status：恢复任务状态。
-   SourceType：源文件类型。
-   RestoreId：恢复任务ID。
-   ErrorMessage：恢复任务错误信息。
-   RestoreType：恢复类型。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "SnapshotId": {
      "Type": "String",
      "Description": "Snapshot ID"
    },
    "TargetClientId": {
      "Type": "String",
      "Description": "Target client ID. It should be provided when RestoreType=FILE."
    },
    "TargetPath": {
      "Type": "String",
      "Description": "Target path. For instance, \"/\"."
    },
    "SourceType": {
      "Type": "String",
      "Description": "Source type",
      "AllowedValues": [
        "FILE",
        "ECS_FILE"
      ]
    },
    "SourceClientId": {
      "Type": "String",
      "Description": "Source client ID. It should be provided when SourceType=FILE."
    },
    "TargetInstanceId": {
      "Type": "String",
      "Description": "Source client ID. It should be provided when RestoreType=ECS_FILE."
    },
    "VaultId": {
      "Type": "String",
      "Description": "Vault ID"
    },
    "SourceInstanceId": {
      "Type": "String",
      "Description": "Source instance ID. It should be provided when SourceType=ECS_FILE."
    },
    "RestoreType": {
      "Type": "String",
      "Description": "Restore type",
      "AllowedValues": [
        "FILE",
        "ECS_FILE"
      ]
    }
  },
  "Resources": {
    "RestoreJob": {
      "Type": "ALIYUN::HBR::RestoreJob",
      "Properties": {
        "SnapshotId": {
          "Ref": "SnapshotId"
        },
        "TargetClientId": {
          "Ref": "TargetClientId"
        },
        "TargetPath": {
          "Ref": "TargetPath"
        },
        "SourceType": {
          "Ref": "SourceType"
        },
        "SourceClientId": {
          "Ref": "SourceClientId"
        },
        "TargetInstanceId": {
          "Ref": "TargetInstanceId"
        },
        "VaultId": {
          "Ref": "VaultId"
        },
        "SourceInstanceId": {
          "Ref": "SourceInstanceId"
        },
        "RestoreType": {
          "Ref": "RestoreType"
        }
      }
    }
  },
  "Outputs": {
    "Status": {
      "Description": "Restore job status",
      "Value": {
        "Fn::GetAtt": [
          "RestoreJob",
          "Status"
        ]
      }
    },
    "SourceType": {
      "Description": "Source type",
      "Value": {
        "Fn::GetAtt": [
          "RestoreJob",
          "SourceType"
        ]
      }
    },
    "RestoreId": {
      "Description": "Restore job ID",
      "Value": {
        "Fn::GetAtt": [
          "RestoreJob",
          "RestoreId"
        ]
      }
    },
    "ErrorMessage": {
      "Description": "Error message of restore job",
      "Value": {
        "Fn::GetAtt": [
          "RestoreJob",
          "ErrorMessage"
        ]
      }
    },
    "RestoreType": {
      "Description": "Restore type",
      "Value": {
        "Fn::GetAtt": [
          "RestoreJob",
          "RestoreType"
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
  SnapshotId:
    Type: String
    Description: Snapshot ID
  TargetClientId:
    Type: String
    Description: Target client ID. It should be provided when RestoreType=FILE.
  TargetPath:
    Type: String
    Description: 'Target path. For instance, "/".'
  SourceType:
    Type: String
    Description: Source type
    AllowedValues:
      - FILE
      - ECS_FILE
  SourceClientId:
    Type: String
    Description: Source client ID. It should be provided when SourceType=FILE.
  TargetInstanceId:
    Type: String
    Description: Source client ID. It should be provided when RestoreType=ECS_FILE.
  VaultId:
    Type: String
    Description: Vault ID
  SourceInstanceId:
    Type: String
    Description: Source instance ID. It should be provided when SourceType=ECS_FILE.
  RestoreType:
    Type: String
    Description: Restore type
    AllowedValues:
      - FILE
      - ECS_FILE
Resources:
  RestoreJob:
    Type: 'ALIYUN::HBR::RestoreJob'
    Properties:
      SnapshotId:
        Ref: SnapshotId
      TargetClientId:
        Ref: TargetClientId
      TargetPath:
        Ref: TargetPath
      SourceType:
        Ref: SourceType
      SourceClientId:
        Ref: SourceClientId
      TargetInstanceId:
        Ref: TargetInstanceId
      VaultId:
        Ref: VaultId
      SourceInstanceId:
        Ref: SourceInstanceId
      RestoreType:
        Ref: RestoreType
Outputs:
  Status:
    Description: Restore job status
    Value:
      'Fn::GetAtt':
        - RestoreJob
        - Status
  SourceType:
    Description: Source type
    Value:
      'Fn::GetAtt':
        - RestoreJob
        - SourceType
  RestoreId:
    Description: Restore job ID
    Value:
      'Fn::GetAtt':
        - RestoreJob
        - RestoreId
  ErrorMessage:
    Description: Error message of restore job
    Value:
      'Fn::GetAtt':
        - RestoreJob
        - ErrorMessage
  RestoreType:
    Description: Restore type
    Value:
      'Fn::GetAtt':
        - RestoreJob
        - RestoreType
```

