# ALIYUN::FNF::Flow {#concept_xsc_jmm_4fb .concept}

ALIYUN::FNF::Flow类型用于调用CreateFlow创建一个流程。

## 语法 {#section_bnr_dxz_lfb .section}

``` {#codeblock_klf_fjz_jl2 .language-json}
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

## 属性 {#section_v1m_r76_g84 .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Definition|String|是|是|创建的流程的定义，遵循FDL语法标准。|无。|
|RoleArn|String|否|是|可选参数，流程执行所需的资源描述符信息，用于在任务执行时FnF进行assumerole。|无。|
|Description|String|是|是|创建流程的描述。|无。|
|RequestId|String|否|是|您这次请求的指定RequestID。如果不指定，系统会帮您随机生成。|无。|
|Name|String|是|否|创建的流程名称。该名称在账户下唯一。|无。|

## 返回值 {#section_757_sgw_ib6 .section}

Fn::GetAtt

-   CreatedTime：流程创建时间。
-   LastModifiedTime：流程最后更改时间。
-   Id：流程的唯一ID。

## 示例 {#section_zhq_syz_lfb .section}

``` {#codeblock_301_s30_lzg .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "Flow": {
      "Type": "ALIYUN::FNF::Flow",
      "Properties": {
        "Definition": {
          "Ref": "Definition"
        },
        "RoleArn": {
          "Ref": "RoleArn"
        },
        "Description": {
          "Ref": "Description"
        },
        "Name": {
          "Ref": "Name"
        },
        "RequestId": {
          "Ref": "RequestId"
        }
      }
    }
  },
  "Parameters": {
    "Definition": {
      "Type": "String",
      "Description": "The definition of the created flow following the FDL syntax standard."
    },
    "RoleArn": {
      "Type": "String",
      "Description": "Optional parameter, the resource descriptor information required for the execution of the flow, used to perform the assume role during FnF execution."
    },
    "Description": {
      "Type": "String",
      "Description": "Create a description of the flow."
    },
    "Name": {
      "Type": "String",
      "Description": "The name of the flow created. This name is unique under the account."
    },
    "RequestId": {
      "Type": "String",
      "Description": "The specified Request ID for this request. If not specified, our system will help you generate a random one."
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

