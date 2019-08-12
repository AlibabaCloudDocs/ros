# ALIYUN::ECS::Invocation {#concept_omf_kfn_qgb .concept}

Initiates a cloud assistant command for ECS instances.

## Syntax {#section_xyg_tn2_lfb .section}

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

## Properties {#section_cgd_53n_4fb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Timed|Boolean|No|No|Specifies whether the command is repeatedly implemented. Default value: False.|N/A|
|Frequency|String|No|No|The frequency of a recurring command task. The parameter uses a [Cron expression](https://partners-intl.aliyun.com/help/faq-detail/64769.htm).|N/A|
|CommandId|String|Yes|No|The ID of the command.|N/A|
|InstanceIds|List|Yes|No|The list of instances for which you want to implement the command. A maximum of 20 instances can be specified at a time.|N/A|

## Response elements {#section_fsg_t4n_4fb .section}

**FN::GetAtt**

-   InvokeId: indicates the ID of the command invoked.

## Example {#section_klp_54n_4fb .section}

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Timed": {
      "Type": "Boolean",
      "Description": "Whether it is a timed execution. Default is False.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "Frequency": {
      "Type": "String",
      "Description": "The frequency of timed execution (the shortest frequency is performed every 1 minute). It is mandatory when Timing is True.The value rule follows the rules of the cron expression. "
    },
    "CommandId": {
      "Type": "String",
      "Description": "The id of command."
    },
    "InstanceIds": {
      "Type": "CommaDelimitedList",
      "Description": "The instance id list. Select up to 20 instances at a time.The network type for all instances must be a VPC network, and the status must be set to running"
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

