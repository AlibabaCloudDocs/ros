# ALIYUN::ECS::Invocation {#concept_omf_kfn_qgb .concept}

ALIYUN::ECS::Invocation类型用于为一台或多台ECS实例触发一条云助手命令。

## 语法 {#section_xyg_tn2_lfb .section}

```language-json
{
  "Type": "ALIYUN::ECS::Invocation",
  "Properties": {
    "Timed": Boolean,
    "Frequency": String,
    "CommandId": String,
    "InstanceIds": List
  }
}
```

## 属性 {#section_cgd_53n_4fb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Timed|Boolean|否|否|命令是否为周期执行。默认值：False|无|
|Frequency|String|否|否|周期任务的执行周期。该参数值结构以 [Cron 表达式](https://www.alibabacloud.com/help/faq-detail/64769.htm) 为准。|无|
|CommandId|String|是|否|命令 ID。|无|
|InstanceIds|List|是|否|执行命令的实例列表。最多能指定20台实例ID。|无|

## 返回值 {#section_fsg_t4n_4fb .section}

**FN::GetAtt**

-   InvokeId: 命令进程执行 ID。

## 示例 {#section_klp_54n_4fb .section}

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Timed": {
      "Type": "Boolean",
      "Description": "Whether it is timed execution. Default is False.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "Frequency": {
      "Type": "String",
      "Description": "The frequency of timing execution (the shortest frequency is performed every 1 minute). It iss mandatory when Timing is True.The value rule follows the rules of the cron expression. "
    },
    "CommandId": {
      "Type": "String",
      "Description": "The id of command."
    },
    "InstanceIds": {
      "Type": "CommaDelimitedList",
      "Description": "The instance id list. Select up to 20 instances at a time.Instances selected network type must be VPC network, status must be running"
    }
  },
  "Resources": {
    "Invocation": {
      "Type": "ALIYUN::ECS::Invocation",
      "Properties": {
        "Timed": {
          "Ref": "Timed"
        },
        "Frequency": {
          "Ref": "Frequency"
        },
        "CommandId": {
          "Ref": "CommandId"
        },
        "InstanceIds": {
          "Fn::Split": [
            ",",
            {
              "Ref": "InstanceIds"
            },
            {
              "Ref": "InstanceIds"
            }
          ]
        }
      }
    }
  },
  "Outputs": {
    "InvokeId": {
      "Description": "The id of command execution.",
      "Value": {
        "Fn::GetAtt": [
          "Invocation",
          "InvokeId"
        ]
      }
    }
  }
}
```

