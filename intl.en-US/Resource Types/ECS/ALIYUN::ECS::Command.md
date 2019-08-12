# ALIYUN::ECS::Command {#concept_vbb_2ss_qgb .concept}

Creates a [cloud assistant](https://partners-intl.aliyun.com/help/doc-detail/64601.htm) command.

## Syntax {#section_xyg_tn2_lfb .section}

```language-json
{
  "Type": "ALIYUN::ECS::Command",
  "Properties": {
    "Name": String,
    "WorkingDir": String,
    "CommandContent": String,
    "Timeout": Integer,
    "Type": String,
    "Description": String
  }
}
```

## Properties {#section_cgd_53n_4fb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Name|String|No|Yes|The name of the command to be created. This parameter supports any character. The maximum length is 30 characters.|N/A|
|WorkingDir|String|No|Yes|The working directory where the command runs on ECS instances.|N/A|
|CommandContent|String|No|No| The Base64-encoded script of the command.

 If the `Type` is specified, this parameter must also be specified.

 This parameter must be Base64-encoded. The maximum size of the encoded script is 16 KB.

 |N/A|
|Timeout|Integer|No|Yes| The timeout value for running the command on ECS instances, measured in seconds.

 A timeout error occurs if the system does not respond to your command within the specified time. When this error occurs, the system stops the command by terminating the corresponding PID \(process ID\).

 Default value: 3600.

 |N/A|
|Type|String|Yes|No|The type of the command.

Valid values:-   RunBatScript: indicates creating a batch script for Windows instances.
-   RunPowerShellScript: indicates creating a PowerShell script for Windows instances.
-   RunShellScript: indicates creating a Shell script for Linux instances.

|N/A|
|Description|String|No|Yes|The description of the command. The description supports any character. The maximum length is 100 characters.|N/A|

## Response elements {#section_fsg_t4n_4fb .section}

**FN::GetAtt**

-   CommandId: indicates the ID of the created command.

## Example {#section_klp_54n_4fb .section}

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "WorkingDir": {
      "Type": "String",
      "Description": "The path where the command will be executed in the instance."
    },
    "CommandContent": {
      "Type": "String",
      "Description": "The content of the command. Content requires base64 encoding. Maximum size support 16KB."
    },
    "Type": {
      "Type": "String",
      "Description": "The type of command."
    },
    "Description": {
      "Type": "String",
      "Description": "The description of the command."
    },
    "Timeout": {
      "Type": "Number",
      "Description": "Total timeout when the command is executed in the instance. Input the time unit as second. Default is 3,600s."
    },
    "Name": {
      "Type": "String",
      "Description": "The name of the command."
    }
  },
  "Resources": {
    "Command": {
      "Type": "ALIYUN::ECS::Command",
      "Properties": {
        "WorkingDir": {
          "Ref": "WorkingDir"
        },
        "CommandContent": {
          "Ref": "CommandContent"
        },
        "Type": {
          "Ref": "Type"
        },
        "Description": {
          "Ref": "Description"
        },
        "Timeout": {
          "Ref": "Timeout"
        },
        "Name": {
          "Ref": "Name"
        }
      }
    }
  },
  "Outputs": {
    "CommandId": {
      "Description": "The id of created command.",
      "Value": {
        "Fn::GetAtt": [
          "Command",
          "CommandId"
        ]
      }
    }
  }
}
```

