# ALIYUN::FNF::Flow

ALIYUN::FNF::Flow is used to create a flow.

## Syntax

```
{
  "Type": "ALIYUN::FNF::Flow",
  "Properties": {
    "Definition": String,
    "RoleArn": String,
    "Description": String,
    "RequestId": String,
    "Name": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Definition|String|Yes|Yes|The definition of the flow. Example: `version: v1beta1\ntype: flow\nsteps: \n - type: pass\n name: mypass`.|It must comply with the FDL syntax. For more information, see [Overview](/intl.en-US/Flow Definition Language/Overview.md).|
|RoleArn|String|No|Yes|The Alibaba Cloud Resource Name \(ARN\) of the specified RAM role that Function Flow \(FnF\) assumes when it executes the flow.|None|
|Description|String|No|Yes|The description of the flow.|None|
|RequestId|String|No|Yes|The ID of the request.|If this parameter is not specified, the system generates a random value for it.|
|Name|String|Yes|No|The name of the flow.|The name must be unique in an Alibaba Cloud account. The name must be 1 to 128 characters in length and can contain letters, digits, underscores \(\_\), and hyphens \(-\). It must start with a letter or underscore \(\_\). |

## Response parameters

Fn::GetAtt

-   CreatedTime: the time when the flow was created.
-   LastModifiedTime: the time when the flow was last modified.
-   Id: the unique ID of the flow.
-   Name: the name of the flow.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Definition": {
      "Type": "String",
      "Description": "The definition of the created flow following the FDL syntax standard.",
      "Default": "version: v1beta1\ntype: flow\nsteps: \n  - type: pass\n    name: mypass"
    },
    "Description": {
      "Type": "String",
      "Description": "Create a description of the flow.",
      "Default": "Test FNF Flow"
    },
    "Name": {
      "Type": "String",
      "Description": "The name of the flow created. This name is unique under the account.",
      "Default": "TestFlow"
    }
  },
  "Resources": {
    "Flow": {
      "Type": "ALIYUN::FNF::Flow",
      "Properties": {
        "Definition": {
          "Ref": "Definition"
        },
        "Description": {
          "Ref": "Description"
        },
        "Name": {
          "Ref": "Name"
        }
      }
    }
  },
  "Outputs": {
    "CreatedTime": {
      "Description": "Flow creation time.",
      "Value": {
        "Fn::GetAtt": [
          "Flow",
          "CreatedTime"
        ]
      }
    },
    "LastModifiedTime": {
      "Description": "The most recently modified time of the flow.",
      "Value": {
        "Fn::GetAtt": [
          "Flow",
          "LastModifiedTime"
        ]
      }
    },
    "Id": {
      "Description": "The unique ID of the flow.",
      "Value": {
        "Fn::GetAtt": [
          "Flow",
          "Id"
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
  Definition:
    Type: String
    Description: The definition of the created flow following the FDL syntax standard.
    Default: |-
      version: v1beta1
      type: flow
      steps:
        - type: pass
          name: mypass
  Description:
    Type: String
    Description: Create a description of the flow.
    Default: Test FNF Flow
  Name:
    Type: String
    Description: The name of the flow created. This name is unique under the account.
    Default: TestFlow
Resources:
  Flow:
    Type: 'ALIYUN::FNF::Flow'
    Properties:
      Definition:
        Ref: Definition
      Description:
        Ref: Description
      Name:
        Ref: Name
Outputs:
  CreatedTime:
    Description: Flow creation time.
    Value:
      'Fn::GetAtt':
        - Flow
        - CreatedTime
  LastModifiedTime:
    Description: The most recently modified time of the flow.
    Value:
      'Fn::GetAtt':
        - Flow
        - LastModifiedTime
  Id:
    Description: The unique ID of the flow.
    Value:
      'Fn::GetAtt':
        - Flow
        - Id
```

