# ALIYUN::FC::Trigger {#concept_186474 .concept}

ALIYUN::FC::Trigger类型用于触发函数执行的方式。

在事件驱动的计算模型中，事件源是事件的生产者，函数是事件的处理者，而触发器提供了一种集中的和统一的方式来管理不同的事件源。在事件源中，当事件发生时，如果满足触发器定义的规则，事件源则调用触发器所对应的函数。

## 语法 {#section_11k_xli_tws .section}

```language-json
{
  "Type": "ALIYUN::FC::Trigger",
  "Properties": {
    "TriggerConfig": Map,
    "InvocationRole": String,
    "FunctionName": String,
    "ServiceName": String,
    "TriggerName": String,
    "TriggerType": String,
    "SourceArn": String,
    "Qualifier": String
  }
}
```

## 属性 {#section_diy_r57_op1 .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ServiceName|String|是|否|service名称。|长度为1-128字符。|
|FunctionName|String|是|否|function名称。|无|
|TriggerName|String|是|否|trigger名称。|无|
|TriggerType|String|是|否|trigger类型。|无|
|TriggerConfig|Map|是|是|trigger配置，针对不同的trigger类型，trigger配置会有所不同。|无|
|InvocationRole|String|是|是| event source，如OSS，使用该role去invoke function。

 例如：`"acs:ram::1234567890:role/fc-test"`。|无|
|SourceArn|String|是|是| event source的Aliyun Resource Name（ARN）。

 例如：`"acs:oss:cn-shanghai:12345:mybucket"`。|无|
|Qualifier|String|否|否|service版本。例如："LATEST"。|无|

## 返回值 {#section_v7c_aa1_nch .section}

 **Fn::GetAtt** 

TriggerId：系统为每个Trigger生成的唯一ID。

## 示例 {#section_03s_fe8_yvr .section}

``` {#codeblock_bbc_idm_ccl}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "Trigger": {
      "Type": "ALIYUN::FC::Trigger",
      "Properties": {
        "TriggerConfig": {
          "Ref": "TriggerConfig"
        },
        "InvocationRole": {
          "Ref": "InvocationRole"
        },
        "FunctionName": {
          "Ref": "FunctionName"
        },
        "ServiceName": {
          "Ref": "ServiceName"
        },
        "TriggerName": {
          "Ref": "TriggerName"
        },
        "TriggerType": {
          "Ref": "TriggerType"
        },
        "SourceArn": {
          "Ref": "SourceArn"
        },
        "Qualifier": {
          "Ref": "Qualifier"
        }
      }
    }
  },
  "Parameters": {
    "TriggerConfig": {
      "Type": "Json",
      "Description": "Event source specific trigger configuration. The value is different according to trigger type."
    },
    "InvocationRole": {
      "Type": "String",
      "Description": "The role grants event source the permission to run function on behalf of user. This is optional for some triggers.\nExample : \"acs:ram::1234567890:role/fc-test\""
    },
    "FunctionName": {
      "Type": "String",
      "Description": "Trigger name"
    },
    "ServiceName": {
      "MinLength": 1,
      "Type": "String",
      "Description": "Service name",
      "MaxLength": 128
    },
    "TriggerName": {
      "Type": "String",
      "Description": "Trigger name.\nExample : \"image_resize\""
    },
    "TriggerType": {
      "Type": "String",
      "Description": "Trigger type, e.g. oss, timer, logs. This determines how the trigger config is interpreted.\nExample : \"oss\""
    },
    "SourceArn": {
      "Type": "String",
      "Description": "The Aliyun Resource Name (ARN) of event source. This is optional for some triggers.\nExample : \"acs:oss:cn-shanghai:12345:mybucket\""
    },
    "Qualifier": {
      "Type": "String",
      "Description": "service version or alias.\nExample : \"LATEST\""
    }
  },
  "Outputs": {
    "TriggerId": {
      "Description": "The trigger ID",
      "Value": {
        "Fn::GetAtt": [
          "Trigger",
          "TriggerId"
        ]
      }
    }
  }
}
```

