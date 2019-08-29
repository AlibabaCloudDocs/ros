# ALIYUN::ESS::AlarmTask {#concept_kb5_svz_qgb .concept}

ALIYUN::ESS::AlarmTask is used to create a monitoring alarm task.

## Syntax {#section_xxx_ff1_mfb .section}

```language-json
{
  "Type": "ALIYUN::ESS::AlarmTask",
  "Properties": {
    "Statistics": String,
    "Name": String,
    "EvaluationCount": Integer,
    "Period": Integer,
    "MetricType": String,
    "ComparisonOperator": String,
    "Dimensions": List,
    "ScalingGroupId": String,
    "AlarmAction": List,
    "Threshold": Number,
    "MetricName": String,
    "GroupId": Integer,
    "Description": String
  }
}
```

## Properties {#section_gmr_gf1_mfb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Statistics|String|No|No|The method used to calculate monitoring data. The statistics must be appropriate for the metric chosen.|Valid values: Average, Minimum, and Maximum. Default value: Average.|
|Name|String|No|Yes|The name of the alarm rule.|None|
|EvaluationCount|Integer|No|No|The number of consecutive times that the threshold needs to be exceeded before an alarm is triggered. Default value: 3.|Minimum value: 1.|
|Period|Integer|No|No|The metric query period, which must be appropriate for the metric chosen. Unit: second. Default value: 300.|Valid values: 60, 120, 300, and 900.|
|MetricType|String|No|No|The metric type.|Valid values: system and custom.|
|ComparisonOperator|String|No|No|The alarm comparison operator used to define a condition in the alarm rule.|Valid values: <=, <, \>, and \> =.|
|Dimensions|List|No|No|The list of instances associated with the alarm rule.|You must include at least one instance in the list.|
|ScalingGroupId|String|Yes|No|The ID of the scaling group.|None|
|AlarmAction|List|Yes|Yes|The list of alarm actions.|You must include one to five alarm actions in the list.|
|Threshold|Number|Yes|No|The alarm threshold, which must be a numeric value.|None|
|MetricName|String|Yes|No|The metric name of a service. For more information, see the metrics defined for each service.|None|
|GroupId|Integer|No|No|The ID of the group to which the alarm rule belongs.|None|
|Description|String|No|Yes|The description of the alarm rule.|None|

## Dimensions syntax { .section}

```
"Dimensions": [
  {
    "DimensionKey": String,
    "DimensionValue": String 
  }
]
```

## Dimensions properties { .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|DimensionValue|String|Yes|No|None|None|
|DimensionKey|String|Yes|No|None|None|

## Response parameters {#section_x4l_kf1_mfb .section}

**Fn::GetAtt**

-   AlarmTaskId: the ID of the alarm task.

## Examples {#section_mmh_mf1_mfb .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "ComparisonOperator": {
      "Type": "String",
      "Description": "Comparison Operator",
      "AllowedValues": [
        ">=",
        "<=",
        ">",
        "<"
      ]
    },
    "Description": {
      "Type": "String",
      "Description": "Description"
    },
    "ScalingGroupId": {
      "Type": "String",
      "Description": "The ID of the scaling group."
    },
    "MetricType": {
      "Type": "String",
      "Description": "Metric Type",
      "AllowedValues": [
        "system",
        "custom"
      ]
    },
    "EvaluationCount": {
      "Type": "Number",
      "Description": "Evaluation Count",
      "MinValue": 1
    },
    "Period": {
      "Type": "Number",
      "Description": "Period",
      "AllowedValues": [
        60,
        120,
        300,
        900
      ]
    },
    "Dimensions": {
      "Type": "CommaDelimitedList",
      "Description": "Dimensions",
      "MinLength": 1
    },
    "Statistics": {
      "Type": "String",
      "Description": "Statistics",
      "AllowedValues": [
        "Average",
        "Minimum",
        "Maximum"
      ]
    },
    "Name": {
      "Type": "String",
      "Description": "Name"
    },
    "GroupId": {
      "Type": "Number",
      "Description": "Group Id"
    },
    "MetricName": {
      "Type": "String",
      "Description": "Metric Name"
    },
    "AlarmAction": {
      "Type": "CommaDelimitedList",
      "Description": "Alarm Actions",
      "MinLength": 1,
      "MaxLength": 5
    },
    "Threshold": {
      "Type": "Number",
      "Description": "Threshold"
    }
  },
  "Resources": {
    "AlarmTask": {
      "Type": "ALIYUN::ESS::AlarmTask",
      "Properties": {
        "ComparisonOperator": {
          "Ref": "ComparisonOperator"
        },
        "Description": {
          "Ref": "Description"
        },
        "ScalingGroupId": {
          "Ref": "ScalingGroupId"
        },
        "MetricType": {
          "Ref": "MetricType"
        },
        "EvaluationCount": {
          "Ref": "EvaluationCount"
        },
        "Period": {
          "Ref": "Period"
        },
        "Dimensions": {
          "Fn::Split": [
            ",",
            {
              "Ref": "Dimensions"
            },
            {
              "Ref": "Dimensions"
            }
          ]
        },
        "Statistics": {
          "Ref": "Statistics"
        },
        "Name": {
          "Ref": "Name"
        },
        "GroupId": {
          "Ref": "GroupId"
        },
        "MetricName": {
          "Ref": "MetricName"
        },
        "AlarmAction": {
          "Fn::Split": [
            ",",
            {
              "Ref": "AlarmAction"
            },
            {
              "Ref": "AlarmAction"
            }
          ]
        },
        "Threshold": {
          "Ref": "Threshold"
        }
      }
    }
  },
  "Outputs": {
    "AlarmTaskId": {
      "Description": "The alarm task ID",
      "Value": {
        "Fn::GetAtt": [
          "AlarmTask",
          "AlarmTaskId"
        ]
      }
    }
  }
}
```

