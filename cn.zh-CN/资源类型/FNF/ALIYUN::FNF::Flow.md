# ALIYUN::FNF::Flow

ALIYUN::FNF::Flow类型用于创建一个流程。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Definition|String|是|是|创建的流程的定义，例如：`version: v1beta1\ntype: flow\nsteps: \n - type: pass\n name: mypass`。|遵循FDL语法标准。详情请参见[基本介绍](/cn.zh-CN/流程定义语言/基本介绍.md)。|
|RoleArn|String|否|是|流程执行所需的资源描述符信息。|无|
|Description|String|否|是|创建流程的描述。|无|
|RequestId|String|否|是|请求ID。|如果不指定，系统会随机生成。|
|Name|String|是|否|创建的流程名称。|该名称在阿里云账号下唯一。 长度为1~128个字符，以英文字母或下划线（\_）开头，可包含英文字母、数字、下划线（\_）和短划线（-）。 |

## 返回值

Fn::GetAtt

-   CreatedTime：流程创建时间。
-   LastModifiedTime：流程最后更改时间。
-   Id：流程的唯一ID。
-   Name：流程名。

## 示例

`JSON`格式

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

`YAML`格式

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

