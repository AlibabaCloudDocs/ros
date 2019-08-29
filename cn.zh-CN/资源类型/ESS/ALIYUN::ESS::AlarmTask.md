# ALIYUN::ESS::AlarmTask {#concept_kb5_svz_qgb .concept}

ALIYUN::ESS::AlarmTask类型用于创建监控项报警任务。

## 语法 {#section_xxx_ff1_mfb .section}

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

## 属性 {#section_gmr_gf1_mfb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Statistics|String|否|否|统计方法，必须与定义的metric一致，例如Average。|可选值：Average,Minimum,Maximum|
|Name|String|否|是|报警规则名称。|无|
|EvaluationCount|Integer|否|否|连续探测几次都满足阈值条件时报警，默认3次。|最小为1。|
|Period|Integer|否|否|查询指标的周期，必须与定义的metric一致，默认300，单位为秒|可用值：60，120，300，900。|
|MetricType|String|否|否|标准类型。|可用值：sytem，custom。|
|ComparisonOperator|String|否|否|报警比较符。|只能为以下几种<=，<，\>，\>=|
|Dimensions|List|否|否|报警规则对应实例列表。|最少一个。|
|ScalingGroupId|String|是|否|伸缩组ID。|无|
|AlarmAction|List|是|是|报警动作列表。|最少1个，最多5个。|
|Threshold|Number|是|否|报警阈值，目前只开放数值类型功能。|无|
|MetricName|String|是|否|相应产品对应的监控项名称，参考各产品metric定义。|无|
|GroupId|Integer|否|否|组ID。|无|
|Description|String|否|是|描述。|无|

## Dimensions语法 { .section}

```
"Dimensions": [
  {
    "DimensionKey": String,
    "DimensionValue": String 
  }
]
```

## Dimensions属性 { .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|DimensionValue|String|是|否|无|无|
|DimensionKey|String|是|否|无|无|

## 返回值 {#section_x4l_kf1_mfb .section}

**Fn::GetAtt**

-   AlarmTaskId：报警任务ID。

## 示例 {#section_mmh_mf1_mfb .section}

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

