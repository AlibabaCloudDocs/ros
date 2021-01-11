# ALIYUN::IOT::RuleAction

ALIYUN::IOT::RuleAction类型用于在指定的规则下创建一个规则动作。

## 语法

```
{
  "Type": "ALIYUN::IOT::RuleAction",
  "Properties": {
    "ErrorActionFlag": Boolean,
    "Type": String,
    "IotInstanceId": String,
    "Configuration": String,
    "RuleId": Integer
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ErrorActionFlag|Boolean|否|否|规则动作是否转发错误操作数据（转发流转到其他云产品失败且重试失败的数据）。|取值：-   true：转发错误操作数据。
-   false（默认值）：不转发错误操作数据。 |
|Type|String|是|是|规则动作类型。数据格式为二进制的规则，即规则的DataType参数是BINARY。不支持转发数据至表格存储（Table Store）。|取值：-   REPUBLISH：将根据规则处理后的Topic数据转发至另一个物联网平台Topic。
-   AMQP：数据流转到AMQP消费组。
-   DATAHUB：将根据规则处理后的Topic数据转发至阿里云DataHub，进行流式数据处理。
-   ONS：将根据规则处理后的Topic数据转发至阿里云消息队列RocketMQ，进行消息分发。
-   MNS：将根据规则处理后的Topic数据发送至阿里云消息服务中，进行消息传输。
-   FC：将根据规则处理后的Topic数据发送至阿里云函数计算服务，进行事件计算。
-   OTS：将根据规则处理后的Topic数据发送至阿里云表格存储（Tablestore），进行NoSQL数据存储。 |
|IotInstanceId|String|否|否|实例ID。|公共实例和企业版实例需要指定该参数。|
|Configuration|String|是|是|规则动作的配置信息。|格式为JSON字符串。不同规则动作类型所需内容不同。更多信息，请参见[CreateRuleAction](/cn.zh-CN/云端开发指南/云端API参考/云产品流转/CreateRuleAction.md)。|
|RuleId|Integer|是|否|要为其创建动作的规则ID。|无|

## 返回值

Fn::GetAtt

ActionId：规则动作ID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "ErrorActionFlag": {
      "Type": "Boolean",
      "Description": "Indicates whether the rule action forwarded error operation data. Error operation\ndata indicates that the rule engine failed to forward data from the IoT Platform topic\nto the destination cloud service. A data forwarding failure indicates that forwarding\nretries also failed. Valid values:\ntrue: forwards error operation data.\nfalse: forwards normal data instead of error operation data.\nDefault value: false.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "Type": {
      "Type": "String",
      "Description": "The type of the rule action. Valid values:\nMNS: forwards data in the topics that have been processed by the rule engine to Message\nService (MNS) for message transmission.\nFC: forwards data in the topics that have been processed by the rule engine to Function\nCompute for event computing.\nREPUBLISH: forwards data in the topics that have been processed by the rule engine to another\nIoT Platform topic.\nAMQP: forwards data to AMQP consumer groups.\nOTS: forwards data in the topics that have been processed by the rule engine to Table\nStore for NoSQL data storage.\nNote\nRules of the binary data format (the DataType parameter is set toBINARY) do not support forwarding data to Table Store.\nDestination Alibaba Cloud services that are supported by the rule engine vary based\non regions. For more information about the regions and destination cloud services\nthat are supported by the rule engine, see Regions and zones.",
      "AllowedValues": [
        "AMQP",
        "DATAHUB",
        "FC",
        "MNS",
        "ONS",
        "OTS",
        "REPUBLISH"
      ]
    },
    "Configuration": {
      "Type": "String",
      "Description": "The configurations of the rule action. You must specify a JSON string. The configurations\nfor different types of rule actions are different. For more information about required\nsyntax and examples, see the following tables."
    },
    "IotInstanceId": {
      "Type": "String",
      "Description": "The ID of the instance. This parameter is not required for public instances. However,\nthe parameter is required for the instances that you have purchased."
    },
    "RuleId": {
      "Type": "Number",
      "Description": "The ID of the rule for which you want to create an action. You can use either of the\nfollowing methods to view the rule ID: 1. Log on to the IoT Platform console and choose Rules>Data Forwarding. 2. Call the ListRule operation."
    }
  },
  "Resources": {
    "RuleAction": {
      "Type": "ALIYUN::IOT::RuleAction",
      "Properties": {
        "ErrorActionFlag": {
          "Ref": "ErrorActionFlag"
        },
        "Type": {
          "Ref": "Type"
        },
        "Configuration": {
          "Ref": "Configuration"
        },
        "IotInstanceId": {
          "Ref": "IotInstanceId"
        },
        "RuleId": {
          "Ref": "RuleId"
        }
      }
    }
  },
  "Outputs": {
    "ActionId": {
      "Description": "The ID of the rule action. ",
      "Value": {
        "Fn::GetAtt": [
          "RuleAction",
          "ActionId"
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
  ErrorActionFlag:
    Type: Boolean
    Description: >-
      Indicates whether the rule action forwarded error operation data. Error
      operation

      data indicates that the rule engine failed to forward data from the IoT
      Platform topic

      to the destination cloud service. A data forwarding failure indicates that
      forwarding

      retries also failed. Valid values:

      true: forwards error operation data.

      false: forwards normal data instead of error operation data.

      Default value: false.
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
  Type:
    Type: String
    Description: >-
      The type of the rule action. Valid values:

      MNS: forwards data in the topics that have been processed by the rule
      engine to Message

      Service (MNS) for message transmission.

      FC: forwards data in the topics that have been processed by the rule
      engine to Function

      Compute for event computing.

      REPUBLISH: forwards data in the topics that have been processed by the
      rule engine to another

      IoT Platform topic.

      AMQP: forwards data to AMQP consumer groups.

      OTS: forwards data in the topics that have been processed by the rule
      engine to Table

      Store for NoSQL data storage.

      Note

      Rules of the binary data format (the DataType parameter is set toBINARY)
      do not support forwarding data to Table Store.

      Destination Alibaba Cloud services that are supported by the rule engine
      vary based

      on regions. For more information about the regions and destination cloud
      services

      that are supported by the rule engine, see Regions and zones.
    AllowedValues:
      - AMQP
      - DATAHUB
      - FC
      - MNS
      - ONS
      - OTS
      - REPUBLISH
  Configuration:
    Type: String
    Description: >-
      The configurations of the rule action. You must specify a JSON string. The
      configurations

      for different types of rule actions are different. For more information
      about required

      syntax and examples, see the following tables.
  IotInstanceId:
    Type: String
    Description: >-
      The ID of the instance. This parameter is not required for public
      instances. However,

      the parameter is required for the instances that you have purchased.
  RuleId:
    Type: Number
    Description: >-
      The ID of the rule for which you want to create an action. You can use
      either of the

      following methods to view the rule ID: 1. Log on to the IoT Platform
      console and choose Rules>Data Forwarding. 2. Call the ListRule operation.
Resources:
  RuleAction:
    Type: 'ALIYUN::IOT::RuleAction'
    Properties:
      ErrorActionFlag:
        Ref: ErrorActionFlag
      Type:
        Ref: Type
      Configuration:
        Ref: Configuration
      IotInstanceId:
        Ref: IotInstanceId
      RuleId:
        Ref: RuleId
Outputs:
  ActionId:
    Description: 'The ID of the rule action. '
    Value:
      'Fn::GetAtt':
        - RuleAction
        - ActionId
```

