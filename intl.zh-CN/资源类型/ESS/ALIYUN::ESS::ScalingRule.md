# ALIYUN::ESS::ScalingRule

ALIYUN::ESS::ScalingRule类型用于创建伸缩规则。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|AdjustmentValue|Integer|否|是|伸缩规则的调整值，适用于简单规则和步进规则。

|不同调整方式对应的取值范围： -   QuantityChangeInCapacity：-500~500。
-   PercentChangeInCapacity：-100~10,000。
-   TotalCapacity：0~1000。

**说明：** 任何情况下，单次调整的ECS实例台数都不能超过500。 |
|Cooldown|Integer|否|是|伸缩规则的冷却时间，仅适用于简单规则。|取值范围：0~86400。单位：秒。

默认值：空。 |
|ScalingGroupId|String|是|否|伸缩规则所属的伸缩组ID。|无|
|AdjustmentType|String|否|是|伸缩规则的调整方式，适用于简单规则和步进规则。|取值： -   QuantityChangeInCapacity：增加或减少指定数量的ECS实例。
-   PercentChangeInCapacity：增加或减少指定比例的ECS实例。
-   TotalCapacity： 将当前伸缩组的ECS实例数量调整到指定数量。 |
|ScalingRuleName|String|否|是|伸缩规则的名称。|长度为2~64个字符，以数字、字母或汉字开头。可包含数字、字母、汉字、下划线（\_）、短划线（-）和英文句点（.）。如果没有指定该参数，默认为ScalingRuleId的取值。 |
|MetricName|String|否|否|预定义监控项，适用于目标追踪规则和预测规则。|取值：-   目标追踪规则：
    -   CpuUtilization：平均CPU使用率。
    -   ClassicInternetRx：经典网络公网入流量平均值。
    -   ClassicInternetTx：经典网络公网出流量平均值。
    -   VpcInternetRx：专有网络公网入流量平均值。
    -   VpcInternetTx：专有网络公网出流量平均值。
    -   IntranetRx：内网入流量平均值。
    -   IntranetTx ：内网出流量平均值。
-   预测规则：
    -   CpuUtilization：平均CPU使用率。
    -   IntranetRx：内网入流量平均值。
    -   IntranetTx ：内网出流量平均值。 |
|PredictiveTaskBufferTime|Integer|否|否|预测规则自动创建的预测任务，默认在整点执行。您可以设置预启动时间提前执行预测任务，预先准备资源。|取值范围：0~60。单位：分钟。

默认值：0。|
|ScalingRuleType|String|否|否|伸缩规则类型。|取值：-   SimpleScalingRule（默认值）：简单规则。根据调整方式（AdjustmentType）和调整值（AdjustmentValue）调整ECS实例数量。
-   TargetTrackingScalingRule：目标追踪规则。根据预定义监控项（MetricName）动态计算需要扩缩容的ECS实例数量，尽量将预定义监控项的指标值维持在目标值（TargetValue）附近。
-   StepScalingRule： 步进规则，根据阈值和指标值提供分步扩展方式。
-   PredictiveScalingRule：预测规则，基于机器学习能力分析伸缩组的历史监控数据预测未来监控指标值，并支持自动创建定时任务设置伸缩组边界。 |
|PredictiveValueBuffer|Integer|否|否|PredictiveValueBehavior为PredictiveValueOverrideMaxWithBuffer时生效，预测值会按照该比例增加，当增加后的值大于初始最大值时，会采用增加后的值。|取值范围：0~100。默认值：0。 |
|TargetValue|Number|否|否|目标值，适用于目标追踪规则和预测规则。|TargetValue最多保留小数点后三位，且必须大于0。|
|StepAdjustment|List|否|否|分步步骤。|详情请参见[StepAdjustment属性](#section_suj_znp_48c)。|
|PredictiveValueBehavior|String|否|否|预测规则最大值处理方式。|取值：-   MaxOverridePredictiveValue（默认值）：初始最大值会覆盖预测值。预测值大于初始最大值时，预测任务的最大值采用初始最大值。
-   PredictiveValueOverrideMax：预测值会覆盖初始最大值。预测值大于初始最大值时， 预测任务的最大值采用预测值。
-   PredictiveValueOverrideMaxWithBuffer：预测值会附加一定比例。预测值会按照PredictiveValueBuffer比例增加，当增加后的值大于初始最大值时，会采用增加后的值。 |
|DisableScaleIn|Boolean|否|否|是否禁用缩容，仅适用于目标追踪规则。|取值：-   true
-   false（默认值） |
|InitialMaxSize|Integer|否|否|伸缩组实例数上限，和PredictiveValueBehavior结合使用。|默认值为伸缩组最大实例数（MaxSize的取值）。|
|MinAdjustmentMagnitude|Integer|否|否|伸缩规则最小调整实例数。|仅当伸缩规则类型为SimpleScalingRule或StepScalingRule，且AdjustmentType为PercentChangeInCapacity时该参数生效。|
|EstimatedInstanceWarmup|Integer|否|否|实例预热时间，适用于目标追踪规则和步进规则。|取值范围：0~86,400。单位：秒。

默认值：300。处于预热状态的ECS实例将正常的加入伸缩组，但是期间将不会向云监控上报监控数据。

**说明：** 动态计算需要扩缩容的ECS实例数量时，处于预热状态的实例不计入现有实例数量。 |
|PredictiveScalingMode|String|否|否|预测规则的模式。|取值：-   PredictAndScale（默认值）：产生预测结果并创建预测任务。
-   PredictOnly：产生预测结果，但不会创建预测任务。 |

## StepAdjustment语法

```
"StepAdjustment": [
  {
    "MetricIntervalUpperBound": Number,
    "ScalingAdjustment": Integer,
    "MetricIntervalLowerBound": Number
  }
]
```

## StepAdjustment属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|MetricIntervalUpperBound|Number|否|否|分步步骤的上边界，仅适用于步进规则。|取值范围：-9.999999E18~9.999999E18。|
|ScalingAdjustment|Integer|否|否|分步步骤对应的实例扩展数量，仅适用于步进规则。|无|
|MetricIntervalLowerBound|Number|否|否|分步步骤的下边界，仅适用于步进规则。|取值范围：-9.999999E18~9.999999E18。|

## 返回值

Fn::GetAtt

-   ScalingRuleAri：伸缩规则的唯一标识符。
-   ScalingRuleId：伸缩规则的ID。由系统生成，全局唯一。

## 示例

`JSON`格式

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
      "Description": "Name shown for the scaling group, which is a string containing 2 to 40 English or Chinese characters. It must begin with a number, a letter (case-insensitive) or a Chinese character and can contain numbers, \"_\", \"-\" or \".\". The account name in the same scaling group is unique in the same region. If this parameter value is not specified, the default value is ScalingRuleId.",
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

`YAML`格式

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

