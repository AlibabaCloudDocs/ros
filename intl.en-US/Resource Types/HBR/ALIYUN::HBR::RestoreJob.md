# ALIYUN::HBR::RestoreJob

ALIYUN::HBR::RestoreJob is used to create a restore job.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|SnapshotId|String|Yes|No|The ID of the snapshot.|None|
|TargetClientId|String|Yes|No|The ID of the destination client.|This parameter is required when the RestoreType parameter is set to FILE.|
|TargetPath|String|Yes|No|The destination directory to which the backup data is restored.|Example: `/`.|
|SourceType|String|Yes|No|The type of the source file.|Valid values:-   FILE: on-premises file
-   ECS\_FILE: ECS file |
|SourceClientId|String|Yes|No|The ID of the source client.|This parameter is required when the SourceType parameter is set to FILE.|
|TargetInstanceId|String|Yes|No|The ID of the destination client.|This parameter is required when the RestoreType parameter is set to ECS\_FILE.|
|VaultId|String|Yes|No|The backup vault where the source client is deployed.|None|
|SourceInstanceId|String|Yes|No|The ID of the source instance.|This parameter is required when the SourceType parameter is set to ECS\_FILE.|
|RestoreType|String|Yes|No|The type of the destination file.|Valid values:-   FILE: on-premises file
-   ECS\_FILE: ECS file |

## Response parameters

Fn::GetAtt

-   Status: the status of the restore job.
-   SourceType: the type of the source file.
-   RestoreId: the ID of the restore job.
-   ErrorMessage: The error message returned due to the restore task exception.
-   The type of the destination file.

## Examples

`JSON` format

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

`YAML` format

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

