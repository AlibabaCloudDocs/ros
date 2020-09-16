# ALIYUN::ECS::Invocation

ALIYUN::ECS::Invocation is used to run a Cloud Assistant command for one or more ECS instances.

## Syntax

```
{
  "Type": "ALIYUN::ECS::Invocation",
  "Properties": {
    "Timed": Boolean,
    "Frequency": String,
    "CommandId": String,
    "Parameters": Map,
    "InstanceIds": List
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Timed|Boolean|No|No|Specifies whether to run the command on a periodic basis.|Default value: false. Valid values: -   true
-   false |
|Frequency|String|No|No|The frequency at which the command is run. For more information about the value specifications, see [Cron expression](https://www.alibabacloud.com/help/faq-detail/64769.htm).|The interval between two recurring tasks cannot be less than 10 seconds. This parameter is required if the Timed parameter is set to true.|
|CommandId|String|Yes|No|The ID of the command.|None|
|InstanceIds|List|Yes|No|The IDs of the instances for which you want to run the command.|A maximum of 50 instance IDs can be specified.|
|Parameters|Map|No|No|The values of the custom parameters when the custom parameter feature is enabled. The values are key-value pairs. Example: `{"name": "Jack", "accessKey": "LTAIdyv******aRY"}`|Valid number of custom parameters: 0 to 10. The key of Map cannot be an empty string. It can be up to 64 characters in length. The value of Map can be an empty string.

After the custom parameters and the original command content are Base64 encoded, the total size cannot exceed 16 KB.

The set of custom parameter names must be a subset of the parameter set that is defined when you created the command. You can use empty strings to represent the parameters that are not passed in. |

## Response parameters

Fn::GetAtt

InvokeId: the invocation ID of the command.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Parameters": {
      "Type": "Json",
      "Description": "The key-value pairs of custom parameters passed in when the script contains custom parameters.\nNumber of custom parameters: 0 to 10.\nThe key cannot be an empty string. It can be up to 64 characters in length.\nThe value can be an empty string.\nAfter the custom parameters and the original script content are Base64 encoded, the total size cannot exceed 16 KB.\nThe set of custom parameter names must be a subset of the parameter set that is defined when you created the script. You can use an empty string to represent the parameters that are not passed in.\nDefault value: null, indicating that this parameter is canceled and customer parameters are disabled.",
      "MaxLength": 10
    },
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
      "Description": "The instance id list. Select up to 20 instances at a time.Instances status must be running."
    }
  },
  "Resources": {
    "Invocation": {
      "Type": "ALIYUN::ECS::Invocation",
      "Properties": {
        "Parameters": {
          "Ref": "Parameters"
        },
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
          "Ref": "InstanceIds"
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

`YAML` format

```
ROSTemplateFormatVersion: '2015-09-01'
Parameters:
  Parameters:
    Type: Json
    Description: >-
      The key-value pairs of custom parameters passed in when the script
      contains custom parameters.
      Number of custom parameters: 0 to 10.
      The key cannot be an empty string. It can be up to 64 characters in
      length.
      The value can be an empty string.
      After the custom parameters and the original script content are Base64
      encoded, the total size cannot exceed 16 KB.
      The set of custom parameter names must be a subset of the parameter set
      that is defined when you created the script. You can use an empty string
      to represent the parameters that are not passed in.
      Default value: null, indicating that this parameter is canceled and
      customer parameters are disabled.
    MaxLength: 10
  Timed:
    Type: Boolean
    Description: Whether it is timed execution. Default is False.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
  Frequency:
    Type: String
    Description: >-
      The frequency of timing execution (the shortest frequency is performed
      every 1 minute). It iss mandatory when Timing is True.The value rule
      follows the rules of the cron expression.
  CommandId:
    Type: String
    Description: The id of command.
  InstanceIds:
    Type: CommaDelimitedList
    Description: >-
      The instance id list. Select up to 20 instances at a time.Instances status
      must be running.
Resources:
  Invocation:
    Type: 'ALIYUN::ECS::Invocation'
    Properties:
      Parameters:
        Ref: Parameters
      Timed:
        Ref: Timed
      Frequency:
        Ref: Frequency
      CommandId:
        Ref: CommandId
      InstanceIds:
        Ref: InstanceIds
Outputs:
  InvokeId:
    Description: The id of command execution.
    Value:
      'Fn::GetAtt':
        - Invocation
        - InvokeId
```

