# ALIYUN::ESS::ScalingRule

ALIYUN::ESS::ScalingRule is used to create a scaling rule.

## Syntax

```
{
  "Type": "ALIYUN::ESS::ScalingRule",
  "Properties": {
    "AdjustmentValue": Integer,
    "Cooldown": Integer,
    "ScalingGroupId": String,
    "AdjustmentType": String,
    "ScalingRuleName": String,
    "MetricName": String,
    "PredictiveTaskBufferTime": Integer,
    "ScalingRuleType": String,
    "PredictiveValueBuffer": Integer,
    "TargetValue": Number,
    "StepAdjustment": List,
    "PredictiveValueBehavior": String,
    "DisableScaleIn": Boolean,
    "InitialMaxSize": Integer,
    "MinAdjustmentMagnitude": Integer,
    "EstimatedInstanceWarmup": Integer,
    "PredictiveScalingMode": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|AdjustmentValue|Integer|No|Yes|The number of ECS instances to increase or decrease when scaling occurs. This parameter takes effect only when the ScalingRuleType parameter is set to SimpleScalingRule or StepScalingRule.

|Valid values based on the AdjustmentType value: -   Valid values when the AdjustmentType parameter is set to QuantityChangeInCapacity: -500 to 500
-   Valid values when the AdjustmentType parameter is set to PercentChangeInCapacity: - 100 to 10000
-   Valid values when the AdjustmentType parameter is set to TotalCapacity: 0 to 1000

**Note:** The number of ECS instances to be adjusted in a single scaling activity cannot exceed 500. |
|Cooldown|Integer|No|Yes|The cooldown period of the scaling rule. This parameter takes effect only when the ScalingRuleType parameter is set to SimpleScalingRule.|Valid values: 0 to 86400.Unit: seconds.

This parameter is empty by default. |
|ScalingGroupId|String|Yes|No|The ID of the scaling group to which the scaling rule belongs.|None|
|AdjustmentType|String|No|Yes|The adjustment method of the scaling rule. This parameter takes effect only when the ScalingRuleType parameter is set to SimpleScalingRule or StepScalingRule.|Valid values: -   QuantityChangeInCapacity: increases or decreases the specified number of ECS instances in a scaling group.
-   PercentChangeInCapacity: increases or decreases the specified percentage of ECS instances in a scaling group.
-   TotalCapacity: increases or decreases the number of ECS instances in a scaling group by or to a specific number. |
|ScalingRuleName|String|No|Yes|The name of the scaling rule.|The name must be 2 to 64 characters in length and can contain digits, letters, underscores \(\_\), hyphens \(-\), and periods \(.\). It must start with a digit or letter.If this parameter is not specified, the ScalingRuleId value is used by default. |
|MetricName|String|No|No|The predefined metric to monitor. This parameter is required and applicable only when the ScalingRuleType parameter is set to TargetTrackingScalingRule or PredictiveScalingRule.|-   Valid values when the ScalingRuleType parameter is set to TargetTrackingScalingRule:
    -   CpuUtilization: the average CPU utilization
    -   ClassicInternetRx: the average Internet inbound traffic over the classic network
    -   ClassicInternetTx: the average Internet outbound traffic over the classic network
    -   VpcInternetRx: the average Internet inbound traffic over the VPC
    -   VpcInternetTx: the average Internet outbound traffic over the VPC
    -   IntranetRx: the average inbound traffic over the internal network
    -   IntranetTx: the average outbound traffic over the internal network
-   Valid values when the ScalingRuleType parameter is set to PredictiveScalingRule:
    -   CpuUtilization: the average CPU utilization
    -   IntranetRx: the average inbound traffic over the internal network
    -   IntranetTx: the average outbound traffic over the internal network |
|PredictiveTaskBufferTime|Integer|No|No|The buffer period ahead of the prediction task execution time. By default, all scheduled tasks that are automatically created for a predictive scaling rule are executed on the hour. You can set a buffer period to execute prediction tasks ahead of schedule, so that resources can be prepared in advance.|Valid values: 0 to 60.Unit: minutes.

Default value: 0.|
|ScalingRuleType|String|No|No|The type of the scaling rule.|Default value: SimpleScalingRule. Valid values:-   SimpleScalingRule: scales ECS instances based on the values of AdjustmentType and AdjustmentValue.
-   TargetTrackingScalingRule: dynamically calculates the number of ECS instances to be scaled and tries to keep the value of a predefined metric close to TargetValue.
-   StepScalingRule: scales ECS instances in steps based on specified thresholds and metric values.
-   PredictiveScalingRule: uses machine learning to analyze historical monitoring data of the scaling group and predict the future values of metrics. The rule then automatically creates scheduled tasks to set the boundary values for the scaling group. |
|PredictiveValueBuffer|Integer|No|No|The ratio of the increment to the predicted value when PredictiveValueBehavior is set to PredictiveValueOverrideMaxWithBuffer. If the predicted value increased by this ratio is greater than the initial maximum capacity, the value after the increase is used as the maximum value for prediction tasks.|Valid values: 0 to 100.Default value: 0. |
|TargetValue|Number|No|No|The metric value that you expect. This parameter takes effect only when the ScalingRuleType parameter is set to TargetTrackingScalingRule or PredictiveScalingRule.|The value must be greater than 0 and can have a maximum of three decimal places.|
|StepAdjustment|List|No|No|The step adjustments for step scaling.|For more information, see [StepAdjustment properties](#section_suj_znp_48c).|
|PredictiveValueBehavior|String|No|No|The action taken on the predicted maximum value.|Default value: MaxOverridePredictiveValue. Valid values:-   MaxOverridePredictiveValue: uses the initial maximum capacity as the maximum value for prediction tasks when the predicted value is greater than the initial maximum capacity.
-   PredictiveValueOverrideMax: uses the predicted value as the maximum value for prediction tasks when the predicted value is greater than the initial maximum capacity.
-   PredictiveValueOverrideMaxWithBuffer: increases the predicted value by a ratio, which is specified by PredictiveValueBuffer. If the value after the increase is greater than the initial maximum capacity, the value after the increase is used as the maximum value for prediction tasks. |
|DisableScaleIn|Boolean|No|No|Specifies whether to disable scale-in. This parameter takes effect only when the ScalingRuleType parameter is set to TargetTrackingScalingRule.|Default value: false. Valid values:-   true
-   false |
|InitialMaxSize|Integer|No|No|The maximum number of ECS instances in the scaling group, which is used together with the PredictiveValueBehavior parameter.|The default value of this parameter is the value of MaxSize.|
|MinAdjustmentMagnitude|Integer|No|No|The minimum number of ECS instances to be adjusted in the scaling rule.|This parameter takes effect only when the ScalingRuleType parameter is set to SimpleScalingRule or StepScalingRule, and the AdjustmentType parameter is set to PercentChangeInCapacity.|
|EstimatedInstanceWarmup|Integer|No|No|The warm-up period of the ECS instances. This parameter takes effect only when the ScalingRuleType parameter is set to TargetTrackingScalingRule or StepScalingRule.|Valid values: 0 to 86400.Unit: seconds.

Default value: 300.The system adds ECS instances that are in the warm-up state to the scaling group, but does not report monitoring data to Cloud Monitor during the warm-up period.

**Note:** When the system calculates the number of ECS instances to be adjusted, the system does not count ECS instances in the warm-up state as part of the current capacity of the scaling group. |
|PredictiveScalingMode|String|No|No|The mode of the predictive scaling rule.|Default value: PredictAndScale. Valid values:-   PredictAndScale: generates predicted results and creates prediction tasks.
-   PredictOnly: generates predicted results but does not create prediction tasks. |

## StepAdjustment syntax

```
"StepAdjustment": [
  {
    "MetricIntervalUpperBound": Number,
    "ScalingAdjustment": Integer,
    "MetricIntervalLowerBound": Number
  }
]
```

## StepAdjustment properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|MetricIntervalUpperBound|Number|No|No|The upper limit value specified in the step adjustment. This parameter takes effect only when the ScalingRuleType parameter is set to StepScalingRule.|Valid values: -9.999999E18 to 9.999999E18|
|ScalingAdjustment|Integer|No|No|The specified number of ECS instances to be adjusted in the step adjustment. This parameter takes effect only when the ScalingRuleType parameter is set to StepScalingRule.|None|
|MetricIntervalLowerBound|Number|No|No|The lower limit value specified in the step adjustment. This parameter takes effect only when the ScalingRuleType parameter is set to StepScalingRule.|Valid values: -9.999999E18 to 9.999999E18|

## Response parameters

Fn::GetAtt

-   ScalingRuleAri: the unique identifier of the scaling rule.
-   ScalingRuleId: the ID of the scaling rule. This ID is a globally unique identifier \(GUID\) generated by the system.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "TargetValue": {
      "Type": "Number",
      "Description": "The target value of a metric. This parameter is required and applicable only to target tracking scaling rules and predictive scaling rules. The value of TargetValue must be greater than 0 and can have a maximum of three decimal places."
    },
    "Cooldown": {
      "Type": "Number",
      "Description": "Cool-down time of a scaling rule. Value range: [0, 86,400], in seconds. The default value is empty.",
      "MinValue": 0,
      "MaxValue": 86400
    },
    "ScalingGroupId": {
      "Type": "String",
      "Description": "ID of the scaling group of a scaling rule."
    },
    "PredictiveValueBehavior": {
      "Type": "String",
      "Description": "The action taken on the predicted maximum value. Valid values:\n- MaxOverridePredictiveValue: uses the initial maximum capacity as the maximum value for forecast tasks when the predicted value is greater than the initial maximum capacity.\n - PredictiveValueOverrideMax: uses the predicted value as the maximum value for forecast tasks when the predicted value is greater than the initial maximum capacity.\n - PredictiveValueOverrideMaxWithBuffer: increases the predicted value with a ratio, which is specified by PredictiveValueBuffer. If the value after the increase is greater than the initial maximum capacity, the value after the increase is used as the maximum value for forecast tasks.\n Default value: MaxOverridePredictiveValue",
      "AllowedValues": [
        "MaxOverridePredictiveValue",
        "PredictiveValueOverrideMax",
        "PredictiveValueOverrideMaxWithBuffer"
      ]
    },
    "MinAdjustmentMagnitude": {
      "Type": "Number",
      "Description": "The minimum number of ECS instances to be adjusted in a scaling rule. This parameter takes effect only when the scaling rule type is SimpleScalingRule or StepScalingRule and AdjustmentType is PercentChangeInCapacity.",
      "MinValue": 0,
      "MaxValue": 20
    },
    "DisableScaleIn": {
      "Type": "Boolean",
      "Description": "Specifies whether to disable scale-in. This parameter is applicable only to target tracking scaling rules.\n Default value: false",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "StepAdjustment": {
      "Type": "Json",
      "Description": ""
    },
    "AdjustmentType": {
      "Type": "String",
      "Description": "Adjustment mode of a scaling rule. Optional values:\n- QuantityChangeInCapacity: It is used to increase or decrease a specified number of ECS instances.\n- PercentChangeInCapacity: It is used to increase or decrease a specified proportion of ECS instances.\n- TotalCapacity: It is used to adjust the quantity of ECS instances in the current scaling group to a specified value.",
      "AllowedValues": [
        "QuantityChangeInCapacity",
        "PercentChangeInCapacity",
        "TotalCapacity"
      ]
    },
    "MetricName": {
      "Type": "String",
      "Description": "The predefined metric to monitor. This parameter is required and applicable only to target tracking scaling rules and predictive scaling rules.\nValid values of a target tracking scaling rule:\n- CpuUtilization: the average CPU utilization- ClassicInternetRx: the average public network inbound traffic over the classic network\n- ClassicInternetTx: the average public network outbound traffic over the classic network\n- VpcInternetRx: the average public network inbound traffic over the VPC\n- VpcInternetTx: the average public network outbound traffic over the VPC\n- IntranetRx: the average internal network inbound traffic\n- IntranetTx: the average internal network outbound traffic\nValid values of a predictive scaling rule:\n- CpuUtilization: the average CPU utilization\n- IntranetRx: the average internal network inbound traffic\n- IntranetTx: the average internal network outbound traffic",
      "AllowedValues": [
        "CpuUtilization",
        "ClassicInternetRx",
        "ClassicInternetTx",
        "VpcInternetRx",
        "VpcInternetTx",
        "IntranetRx",
        "IntranetTx"
      ]
    },
    "ScalingRuleName": {
      "Type": "String",
      "Description": "Name shown for the scaling group, which is a string containing 2 to 40 English or Chinese characters. It must begin with a number, a letter (case-insensitive) or a Chinese character and can contain numbers, \"_\", \"-\" or \". \". The account name in the same scaling group is unique in the same region. If this parameter value is not specified, the default value is ScalingRuleId.",
      "AllowedPattern": "^[a-zA-Z0-9\\u4e00-\\u9fa5][-_.a-zA-Z0-9\\u4e00-\\u9fa5]{1,63}$"
    },
    "AdjustmentValue": {
      "Type": "Number",
      "Description": "Adjusted value of a scaling rule. Value range:\n- QuantityChangeInCapacity: [-500, 500]\n- PercentChangeInCapacity: [-100, 10000]\n- TotalCapacity: [0, 1000]",
      "MinValue": -500,
      "MaxValue": 10000
    },
    "InitialMaxSize": {
      "Type": "Number",
      "Description": "The maximum number of ECS instances in the scaling group, which is used together with PredictiveValueBehavior.\n Default value: the same as the value of MaxSize",
      "MinValue": 0,
      "MaxValue": 1000
    },
    "ScalingRuleType": {
      "Type": "String",
      "Description": "The type of the scaling rule. Valid values:\n- SimpleScalingRule: scales ECS instances based on the values of AdjustmentType and AdjustmentValue.\n- TargetTrackingScalingRule: dynamically calculates the number of ECS instances to be adjusted and tries to keep the value of a predefined monitoring metric close to TargetValue.\n- StepScalingRule: scales ECS instances in steps based on specified thresholds and metric values.\n- PredictiveScalingRule: uses machine learning to analyze historical monitoring data of the scaling group and then predicts the future values of monitored metrics, the rule then automatically creates scheduled tasks to set the boundary values for the scaling group.\n If this parameter value is not specified, the default value is SimpleScalingRule.",
      "AllowedValues": [
        "SimpleScalingRule",
        "TargetTrackingScalingRule",
        "StepScalingRule",
        "PredictiveScalingRule"
      ]
    },
    "EstimatedInstanceWarmup": {
      "Type": "Number",
      "Description": "The warm-up period of the ECS instances. This parameter is applicable to target tracking scaling rules and step scaling rules. The system adds ECS instances that are in the warm-up state to the scaling group, but does not report monitoring data during the warm-up period to CloudMonitor.\nNote: When calculating the number of ECS instances to be adjusted, the system does not count ECS instances in the warm-up state as part of the current capacity of the scaling group.\nValid values: 0 to 86400. Unit: seconds. Default value: 300.",
      "MinValue": 0,
      "MaxValue": 86400
    },
    "PredictiveScalingMode": {
      "Type": "String",
      "Description": "The mode of the predictive scaling rule. Valid values:\n- PredictAndScale: generates forecasts and creates forecast tasks.\n- PredictOnly: generates forecasts but does not create forecast tasks.\nDefault value: PredictAndScale",
      "AllowedValues": [
        "PredictAndScale",
        "PredictOnly"
      ]
    },
    "PredictiveTaskBufferTime": {
      "Type": "Number",
      "Description": "The amount of buffer time ahead of the forecast task execution time. By default, all scheduled tasks that are automatically created for a predictive scaling rule are executed at the beginning of each hour. You can set a buffer time to execute forecast tasks ahead of schedule, so that resources can be prepared in advance. Valid values: 0 to 60. Unit: minutes.\n Default value: 0",
      "MinValue": 0,
      "MaxValue": 60
    },
    "PredictiveValueBuffer": {
      "Type": "Number",
      "Description": "The ratio of the increment to the predicted value when PredictiveValueBehavior is set to PredictiveValueOverrideMaxWithBuffer. When the value after the increase is greater than the initial maximum capacity, the value after the increase is used for forecast tasks. Valid values: 0 to 100\n Default value: 0",
      "MinValue": 0,
      "MaxValue": 100
    }
  },
  "Resources": {
    "ScalingRule": {
      "Type": "ALIYUN::ESS::ScalingRule",
      "Properties": {
        "TargetValue": {
          "Ref": "TargetValue"
        },
        "Cooldown": {
          "Ref": "Cooldown"
        },
        "ScalingGroupId": {
          "Ref": "ScalingGroupId"
        },
        "PredictiveValueBehavior": {
          "Ref": "PredictiveValueBehavior"
        },
        "MinAdjustmentMagnitude": {
          "Ref": "MinAdjustmentMagnitude"
        },
        "DisableScaleIn": {
          "Ref": "DisableScaleIn"
        },
        "StepAdjustment": {
          "Ref": "StepAdjustment"
        },
        "AdjustmentType": {
          "Ref": "AdjustmentType"
        },
        "MetricName": {
          "Ref": "MetricName"
        },
        "ScalingRuleName": {
          "Ref": "ScalingRuleName"
        },
        "AdjustmentValue": {
          "Ref": "AdjustmentValue"
        },
        "InitialMaxSize": {
          "Ref": "InitialMaxSize"
        },
        "ScalingRuleType": {
          "Ref": "ScalingRuleType"
        },
        "EstimatedInstanceWarmup": {
          "Ref": "EstimatedInstanceWarmup"
        },
        "PredictiveScalingMode": {
          "Ref": "PredictiveScalingMode"
        },
        "PredictiveTaskBufferTime": {
          "Ref": "PredictiveTaskBufferTime"
        },
        "PredictiveValueBuffer": {
          "Ref": "PredictiveValueBuffer"
        }
      }
    }
  },
  "Outputs": {
    "ScalingRuleAri": {
      "Description": "Unique identifier of a scaling rule.",
      "Value": {
        "Fn::GetAtt": [
          "ScalingRule",
          "ScalingRuleAri"
        ]
      }
    },
    "ScalingRuleId": {
      "Description": "ID of a scaling rule, generated by the system and globally unique.",
      "Value": {
        "Fn::GetAtt": [
          "ScalingRule",
          "ScalingRuleId"
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
  TargetValue:
    Type: Number
    Description: >-
      The target value of a metric. This parameter is required and applicable
      only to target tracking scaling rules and predictive scaling rules. The
      value of TargetValue must be greater than 0 and can have a maximum of
      three decimal places.
  Cooldown:
    Type: Number
    Description: >-
      Cool-down time of a scaling rule. Value range: [0, 86,400], in seconds.
      The default value is empty.
    MinValue: 0
    MaxValue: 86400
  ScalingGroupId:
    Type: String
    Description: ID of the scaling group of a scaling rule.
  PredictiveValueBehavior:
    Type: String
    Description: >-
      The action taken on the predicted maximum value. Valid values:

      - MaxOverridePredictiveValue: uses the initial maximum capacity as the
      maximum value for forecast tasks when the predicted value is greater than
      the initial maximum capacity.
       - PredictiveValueOverrideMax: uses the predicted value as the maximum value for forecast tasks when the predicted value is greater than the initial maximum capacity.
       - PredictiveValueOverrideMaxWithBuffer: increases the predicted value with a ratio, which is specified by PredictiveValueBuffer. If the value after the increase is greater than the initial maximum capacity, the value after the increase is used as the maximum value for forecast tasks.
       Default value: MaxOverridePredictiveValue
    AllowedValues:
      - MaxOverridePredictiveValue
      - PredictiveValueOverrideMax
      - PredictiveValueOverrideMaxWithBuffer
  MinAdjustmentMagnitude:
    Type: Number
    Description: >-
      The minimum number of ECS instances to be adjusted in a scaling rule. This
      parameter takes effect only when the scaling rule type is
      SimpleScalingRule or StepScalingRule and AdjustmentType is
      PercentChangeInCapacity.
    MinValue: 0
    MaxValue: 20
  DisableScaleIn:
    Type: Boolean
    Description: >-
      Specifies whether to disable scale-in. This parameter is applicable only
      to target tracking scaling rules.
       Default value: false
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
  StepAdjustment:
    Type: Json
    Description: ''
  AdjustmentType:
    Type: String
    Description: >-
      Adjustment mode of a scaling rule. Optional values:

      - QuantityChangeInCapacity: It is used to increase or decrease a specified
      number of ECS instances.

      - PercentChangeInCapacity: It is used to increase or decrease a specified
      proportion of ECS instances.

      - TotalCapacity: It is used to adjust the quantity of ECS instances in the
      current scaling group to a specified value.
    AllowedValues:
      - QuantityChangeInCapacity
      - PercentChangeInCapacity
      - TotalCapacity
  MetricName:
    Type: String
    Description: >-
      The predefined metric to monitor. This parameter is required and
      applicable only to target tracking scaling rules and predictive scaling
      rules.

      Valid values of a target tracking scaling rule:

      - CpuUtilization: the average CPU utilization- ClassicInternetRx: the
      average public network inbound traffic over the classic network

      - ClassicInternetTx: the average public network outbound traffic over the
      classic network

      - VpcInternetRx: the average public network inbound traffic over the VPC

      - VpcInternetTx: the average public network outbound traffic over the VPC

      - IntranetRx: the average internal network inbound traffic

      - IntranetTx: the average internal network outbound traffic

      Valid values of a predictive scaling rule:

      - CpuUtilization: the average CPU utilization

      - IntranetRx: the average internal network inbound traffic

      - IntranetTx: the average internal network outbound traffic
    AllowedValues:
      - CpuUtilization
      - ClassicInternetRx
      - ClassicInternetTx
      - VpcInternetRx
      - VpcInternetTx
      - IntranetRx
      - IntranetTx
  ScalingRuleName:
    Type: String
    Description: >-
      Name shown for the scaling group, which is a string containing 2 to 40
      English or Chinese characters. It must begin with a number, a letter
      (case-insensitive) or a Chinese character and can contain numbers, "_",
      "-" or ".". The account name in the same scaling group is unique in the
      same region. If this parameter value is not specified, the default value
      is ScalingRuleId.
    AllowedPattern: '^[a-zA-Z0-9\u4e00-\u9fa5][-_.a-zA-Z0-9\u4e00-\u9fa5]{1,63}$'
  AdjustmentValue:
    Type: Number
    Description: |-
      Adjusted value of a scaling rule. Value range:
      - QuantityChangeInCapacity: [-500, 500]
      - PercentChangeInCapacity: [-100, 10000]
      - TotalCapacity: [0, 1000]
    MinValue: -500
    MaxValue: 10000
  InitialMaxSize:
    Type: Number
    Description: >-
      The maximum number of ECS instances in the scaling group, which is used
      together with PredictiveValueBehavior.
       Default value: the same as the value of MaxSize
    MinValue: 0
    MaxValue: 1000
  ScalingRuleType:
    Type: String
    Description: >-
      The type of the scaling rule. Valid values:

      - SimpleScalingRule: scales ECS instances based on the values of
      AdjustmentType and AdjustmentValue.

      - TargetTrackingScalingRule: dynamically calculates the number of ECS
      instances to be adjusted and tries to keep the value of a predefined
      monitoring metric close to TargetValue.

      - StepScalingRule: scales ECS instances in steps based on specified
      thresholds and metric values.

      - PredictiveScalingRule: uses machine learning to analyze historical
      monitoring data of the scaling group and then predicts the future values
      of monitored metrics, the rule then automatically creates scheduled tasks
      to set the boundary values for the scaling group.
       If this parameter value is not specified, the default value is SimpleScalingRule.
    AllowedValues:
      - SimpleScalingRule
      - TargetTrackingScalingRule
      - StepScalingRule
      - PredictiveScalingRule
  EstimatedInstanceWarmup:
    Type: Number
    Description: >-
      The warm-up period of the ECS instances. This parameter is applicable to
      target tracking scaling rules and step scaling rules. The system adds ECS
      instances that are in the warm-up state to the scaling group, but does not
      report monitoring data during the warm-up period to CloudMonitor.

      Note: When calculating the number of ECS instances to be adjusted, the
      system does not count ECS instances in the warm-up state as part of the
      current capacity of the scaling group.

      Valid values: 0 to 86400. Unit: seconds. Default value: 300.
    MinValue: 0
    MaxValue: 86400
  PredictiveScalingMode:
    Type: String
    Description: |-
      The mode of the predictive scaling rule. Valid values:
      - PredictAndScale: generates forecasts and creates forecast tasks.
      - PredictOnly: generates forecasts but does not create forecast tasks.
      Default value: PredictAndScale
    AllowedValues:
      - PredictAndScale
      - PredictOnly
  PredictiveTaskBufferTime:
    Type: Number
    Description: >-
      The amount of buffer time ahead of the forecast task execution time. By
      default, all scheduled tasks that are automatically created for a
      predictive scaling rule are executed at the beginning of each hour. You
      can set a buffer time to execute forecast tasks ahead of schedule, so that
      resources can be prepared in advance. Valid values: 0 to 60. Unit:
      minutes.
       Default value: 0
    MinValue: 0
    MaxValue: 60
  PredictiveValueBuffer:
    Type: Number
    Description: >-
      The ratio of the increment to the predicted value when
      PredictiveValueBehavior is set to PredictiveValueOverrideMaxWithBuffer.
      When the value after the increase is greater than the initial maximum
      capacity, the value after the increase is used for forecast tasks. Valid
      values: 0 to 100
       Default value: 0
    MinValue: 0
    MaxValue: 100
Resources:
  ScalingRule:
    Type: 'ALIYUN::ESS::ScalingRule'
    Properties:
      TargetValue:
        Ref: TargetValue
      Cooldown:
        Ref: Cooldown
      ScalingGroupId:
        Ref: ScalingGroupId
      PredictiveValueBehavior:
        Ref: PredictiveValueBehavior
      MinAdjustmentMagnitude:
        Ref: MinAdjustmentMagnitude
      DisableScaleIn:
        Ref: DisableScaleIn
      StepAdjustment:
        Ref: StepAdjustment
      AdjustmentType:
        Ref: AdjustmentType
      MetricName:
        Ref: MetricName
      ScalingRuleName:
        Ref: ScalingRuleName
      AdjustmentValue:
        Ref: AdjustmentValue
      InitialMaxSize:
        Ref: InitialMaxSize
      ScalingRuleType:
        Ref: ScalingRuleType
      EstimatedInstanceWarmup:
        Ref: EstimatedInstanceWarmup
      PredictiveScalingMode:
        Ref: PredictiveScalingMode
      PredictiveTaskBufferTime:
        Ref: PredictiveTaskBufferTime
      PredictiveValueBuffer:
        Ref: PredictiveValueBuffer
Outputs:
  ScalingRuleAri:
    Description: Unique identifier of a scaling rule.
    Value:
      'Fn::GetAtt':
        - ScalingRule
        - ScalingRuleAri
  ScalingRuleId:
    Description: 'ID of a scaling rule, generated by the system and globally unique.'
    Value:
      'Fn::GetAtt':
        - ScalingRule
        - ScalingRuleId
```

