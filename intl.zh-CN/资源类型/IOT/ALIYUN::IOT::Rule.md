# ALIYUN::IOT::Rule

ALIYUN::IOT::Rule类型用于为指定Topic新建一个规则。

## 语法

```
{
  "Type": "ALIYUN::IOT::Rule",
  "Properties": {
    "TopicType": Integer,
    "IotInstanceId": String,
    "ResourceGroupId": String,
    "ShortTopic": String,
    "Select": String,
    "DataType": String,
    "RuleDesc": String,
    "Where": String,
    "ProductKey": String,
    "RuleAction": List,
    "StartRule": Boolean,
    "Name": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|TopicType|Integer|否|是|类型。|取值：-   0：ShortTopic参数描述中的基础通信Topic或物模型通信Topic，包含OTA升级批次状态通知Topic。
-   1：自定义Topic。
-   2：设备状态变化通知Topic，格式为`/as/mqtt/status/${productKey}/${deviceName}`。 |
|IotInstanceId|String|否|否|实例ID。|公共实例不指定该参数，企业版实例需指定该参数。|
|ResourceGroupId|String|否|否|资源组ID。|无|
|ShortTopic|String|否|是|应用该规则的具体Topic。|格式为：`${deviceName}/topicShortName`。其中，`${deviceName}`是具体设备的名称，`topicShortName`是Topic短名称。|
|Select|String|否|是|要执行的SQL Select语句。更多信息，请参见[SQL表达式](/intl.zh-CN/消息通信/云产品流转/SQL表达式.md)。|该参数取值为Select中的内容。例如：如果Select语句为`Select a,b,c`，则指定`a,b,c`。|
|DataType|String|否|否|规则处理的数据格式，需与待处理的设备数据格式一致。|取值：-   JSON（默认值）：JSON数据。
-   BINARY：二进制数据。

**说明：** 若指定BINARY，TopicType不能选择为0（基础通信Topic或物模型通信Topic），且不支持将数据转发至实例内的时序数据存储、时序数据库、表格存储和云数据库RDS版。 |
|RuleDesc|String|否|是|规则的描述信息。|长度不超过100个字符。|
|Where|String|否|是|规则的触发条件。更多信息，请参见[SQL表达式](/intl.zh-CN/消息通信/云产品流转/SQL表达式.md)。|该参数取值为Where中的内容。例如：如果Where语句为`Where a>10`，则指定`a>10`。|
|ProductKey|String|否|否|应用该规则的产品ProductKey。|无|
|RuleAction|List|否|是|规则动作。|更多信息，请参见[RuleAction属性](#section_plu_pfu_bgn)。|
|StartRule|Boolean|否|是|是否启用规则。|取值：-   true
-   false |
|Name|String|是|是|规则名称。|长度为1~30个字符。可包含汉字、英文字母、日文、数字、下划线（\_）和短划线（-）。**说明：** 一个汉字或日文占2个字符。 |

## RuleAction语法

```
"RuleAction": [
  {
    "ErrorActionFlag": String,
    "Configuration": String,
    "Type": String
  }
] 
```

## RuleAction属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ErrorActionFlag|String|否|否|规则动作是否为转发错误操作数据的转发动作，即转发流转到其他云产品失败且重试失败的数据。|取值：-   true
-   false |
|Configuration|String|是|否|规则动作的配置信息，传入格式为JSON String。|更多信息，请参见[CreateRuleAction](/intl.zh-CN/云端开发指南/云端API参考/云产品流转/CreateRuleAction.md)。|
|Type|String|是|否|规则动作类型。|更多信息，请参见[CreateRuleAction](/intl.zh-CN/云端开发指南/云端API参考/云产品流转/CreateRuleAction.md)。|

## 返回值

Fn::GetAtt

-   RuleId：规则ID。
-   ActionId：规则动作ID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "TopicType": {
      "Type": "Number",
      "Description": "0: The topic is a basic communication topic or TSL-based communication topic.\n1: The topic is a custom topic.\n2: The topic is used to submit device status changes. Syntax: /as/mqtt/status/${productKey}/${deviceName}."
    },
    "IotInstanceId": {
      "Type": "String",
      "Description": "The ID of the instance. This parameter is not required for public instances. However,\nthe parameter is required for the instances that you have purchased."
    },
    "ResourceGroupId": {
      "Type": "String",
      "Description": "The ID of the resource group to which the rule is assigned. You can view the resource\ngroup information in the Resource Management console.\nIf you do not specify this parameter, the rule is assigned to the default resource\ngroup."
    },
    "RuleAction": {
      "Type": "Json",
      "Description": "",
      "MinLength": 1,
      "MaxLength": 10
    },
    "ShortTopic": {
      "Type": "String",
      "Description": "The topic to which this rule is applied. Syntax: ${deviceName}/topicShortName. ${deviceName}specifies the name of the device, and topicShortNamespecifies the custom name of the topic.\nBasic communication topics or Thing Specification Language (TSL)-based communication\ntopics. Syntax: ${deviceName}/topicShortName. You can replace ${deviceName} with the + wildcard. The wildcard indicates that the topic applies to all devices under the\nproduct. Valid values of topicShortName:\n/thing/event/property/post: submits the property data of a device.\n/thing/event/${tsl.event.identifier}/post: submits the event data of a device.${tsl.event.identifier} specifies the identifier of an event in the TSL.\n/thing/lifecycle: submits device lifecycle changes.\n/thing/downlink/reply/message: sends a response to a request from IoT Platform.\n/thing/list/found: submits the data when a gateway detects a new sub-device.\n/thing/topo/lifecycle: submits device topology changes.\n/thing/event/property/history/post: submits historical property data of a device.\n/thing/event/${tsl.event.identifier}/post: submits the historical event data of a device.${tsl.event.identifier}specifies the identifier of an event in the TSL.\n/ota/upgrade: submits OTA update status.\n/ota/version/post: submits OTA module versions.\n/thing/deviceinfo/update: submits device tag changes.\n/edge/driver/${driver_id}/point_post: submits pass-through data from Link IoT Edge.${driver_id} specifies the ID of the driver that a device uses to access Link IoT Edge.\n${packageId}/${jobId}/ota/job/status: submits the status of OTA update batches. This topic is a basic communication topic.\n${packageId}specifies the ID of the firmware. ${jobId}specifies the ID of the update batch.\nCustom topics. Example:${deviceName}/user/get.\nYou can call theQueryProductTopicoperation to view all custom topics of the product.\nWhen you specify a custom topic, you can use the + and # wildcards.\nYou can replace ${deviceName} with the+ wildcard. The wildcard indicates that the topic applies to all devices under the\nproduct.\nYou can replace the fields that follow ${deviceName} with /user/#. The # wildcard indicates that the topic applies whatever values are specified for the fields that\nfollow/user.\nFor more information about how to use wildcards, see Wildcards in topics.\nTopic that is used to submit device status changes: ${deviceName}.\nYou can use the+wildcard. In this case, the status changes of all devices under the product are submitted."
    },
    "Select": {
      "Type": "String",
      "Description": "The SQL SELECT statement that you want to execute. For more information, seeSQL expressions.\nNote Specify the fields that follow the Select keyword for this parameter. For example, if the Select statement is Select a,b,c, specify a,b,c for this parameter."
    },
    "StartRule": {
      "Type": "Boolean",
      "Description": "Start the rule. The rule at least contains one rule action with normal data forward. ",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "DataType": {
      "Type": "String",
      "Description": "The format of the data to be processed by the rule. You must specify the format of\ndevice data to be processed for this parameter. Valid values:\nJSON: JSON data\nBINARY: binary data\nNote If you specifyBINARY, you cannot set the TopicType parameter to 0 and forward data to Table Store, Time Series Database (TSDB), or ApsaradDB\nfor RDS.\nDefault value: JSON.",
      "AllowedValues": [
        "BINARY",
        "JSON"
      ]
    },
    "RuleDesc": {
      "Type": "String",
      "Description": "The description of the rule. The description can be up to 100 characters in length.\nEach Chinese symbol occupies 1 characters."
    },
    "Where": {
      "Type": "String",
      "Description": "The condition that is used to trigger the rule. For more information, seeSQL expressions.\nNote Specify the fields that follow theWherekeyword for this parameter. For example, if the Where statement is Where a>10, specify a>10 for this parameter."
    },
    "ProductKey": {
      "Type": "String",
      "Description": "The ProductKey of the product to which the rule applies."
    },
    "Name": {
      "Type": "String",
      "Description": "The name of the rule. The name must be 1 to 30 characters in length and can contain\nEnglish letters, digits, underscores (_), and hyphens (-). Chinese language is also\nsupported. Each Chinese symbol occupies 2 characters."
    }
  },
  "Resources": {
    "Rule": {
      "Type": "ALIYUN::IOT::Rule",
      "Properties": {
        "TopicType": {
          "Ref": "TopicType"
        },
        "IotInstanceId": {
          "Ref": "IotInstanceId"
        },
        "ResourceGroupId": {
          "Ref": "ResourceGroupId"
        },
        "RuleAction": {
          "Ref": "RuleAction"
        },
        "ShortTopic": {
          "Ref": "ShortTopic"
        },
        "Select": {
          "Ref": "Select"
        },
        "StartRule": {
          "Ref": "StartRule"
        },
        "DataType": {
          "Ref": "DataType"
        },
        "RuleDesc": {
          "Ref": "RuleDesc"
        },
        "Where": {
          "Ref": "Where"
        },
        "ProductKey": {
          "Ref": "ProductKey"
        },
        "Name": {
          "Ref": "Name"
        }
      }
    }
  },
  "Outputs": {
    "ActionId": {
      "Description": "The ID of the rule action. ",
      "Value": {
        "Fn::GetAtt": [
          "Rule",
          "ActionId"
        ]
      }
    },
    "RuleId": {
      "Description": "The ID of the rule. ",
      "Value": {
        "Fn::GetAtt": [
          "Rule",
          "RuleId"
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
  TopicType:
    Type: Number
    Description: >-
      0: The topic is a basic communication topic or TSL-based communication
      topic.

      1: The topic is a custom topic.

      2: The topic is used to submit device status changes. Syntax:
      /as/mqtt/status/${productKey}/${deviceName}.
  IotInstanceId:
    Type: String
    Description: >-
      The ID of the instance. This parameter is not required for public
      instances. However,

      the parameter is required for the instances that you have purchased.
  ResourceGroupId:
    Type: String
    Description: >-
      The ID of the resource group to which the rule is assigned. You can view
      the resource

      group information in the Resource Management console.

      If you do not specify this parameter, the rule is assigned to the default
      resource

      group.
  RuleAction:
    Type: Json
    Description: ''
    MinLength: 1
    MaxLength: 10
  ShortTopic:
    Type: String
    Description: >-
      The topic to which this rule is applied. Syntax:
      ${deviceName}/topicShortName. ${deviceName}specifies the name of the
      device, and topicShortNamespecifies the custom name of the topic.

      Basic communication topics or Thing Specification Language (TSL)-based
      communication

      topics. Syntax: ${deviceName}/topicShortName. You can replace
      ${deviceName} with the + wildcard. The wildcard indicates that the topic
      applies to all devices under the

      product. Valid values of topicShortName:

      /thing/event/property/post: submits the property data of a device.

      /thing/event/${tsl.event.identifier}/post: submits the event data of a
      device.${tsl.event.identifier} specifies the identifier of an event in the
      TSL.

      /thing/lifecycle: submits device lifecycle changes.

      /thing/downlink/reply/message: sends a response to a request from IoT
      Platform.

      /thing/list/found: submits the data when a gateway detects a new
      sub-device.

      /thing/topo/lifecycle: submits device topology changes.

      /thing/event/property/history/post: submits historical property data of a
      device.

      /thing/event/${tsl.event.identifier}/post: submits the historical event
      data of a device.${tsl.event.identifier}specifies the identifier of an
      event in the TSL.

      /ota/upgrade: submits OTA update status.

      /ota/version/post: submits OTA module versions.

      /thing/deviceinfo/update: submits device tag changes.

      /edge/driver/${driver_id}/point_post: submits pass-through data from Link
      IoT Edge.${driver_id} specifies the ID of the driver that a device uses to
      access Link IoT Edge.

      ${packageId}/${jobId}/ota/job/status: submits the status of OTA update
      batches. This topic is a basic communication topic.

      ${packageId}specifies the ID of the firmware. ${jobId}specifies the ID of
      the update batch.

      Custom topics. Example:${deviceName}/user/get.

      You can call theQueryProductTopicoperation to view all custom topics of
      the product.

      When you specify a custom topic, you can use the + and # wildcards.

      You can replace ${deviceName} with the+ wildcard. The wildcard indicates
      that the topic applies to all devices under the

      product.

      You can replace the fields that follow ${deviceName} with /user/#. The #
      wildcard indicates that the topic applies whatever values are specified
      for the fields that

      follow/user.

      For more information about how to use wildcards, see Wildcards in topics.

      Topic that is used to submit device status changes: ${deviceName}.

      You can use the+wildcard. In this case, the status changes of all devices
      under the product are submitted.
  Select:
    Type: String
    Description: >-
      The SQL SELECT statement that you want to execute. For more information,
      seeSQL expressions.

      Note Specify the fields that follow the Select keyword for this parameter.
      For example, if the Select statement is Select a,b,c, specify a,b,c for
      this parameter.
  StartRule:
    Type: Boolean
    Description: >-
      Start the rule. The rule at least contains one rule action with normal
      data forward. 
    AllowedValues:
      - 'True'
      - 'true'
      - 'False'
      - 'false'
  DataType:
    Type: String
    Description: >-
      The format of the data to be processed by the rule. You must specify the
      format of

      device data to be processed for this parameter. Valid values:

      JSON: JSON data

      BINARY: binary data

      Note If you specifyBINARY, you cannot set the TopicType parameter to 0 and
      forward data to Table Store, Time Series Database (TSDB), or ApsaradDB

      for RDS.

      Default value: JSON.
    AllowedValues:
      - BINARY
      - JSON
  RuleDesc:
    Type: String
    Description: >-
      The description of the rule. The description can be up to 100 characters
      in length.

      Each Chinese symbol occupies 1 characters.
  Where:
    Type: String
    Description: >-
      The condition that is used to trigger the rule. For more information,
      seeSQL expressions.

      Note Specify the fields that follow theWherekeyword for this parameter.
      For example, if the Where statement is Where a>10, specify a>10 for this
      parameter.
  ProductKey:
    Type: String
    Description: The ProductKey of the product to which the rule applies.
  Name:
    Type: String
    Description: >-
      The name of the rule. The name must be 1 to 30 characters in length and
      can contain

      English letters, digits, underscores (_), and hyphens (-). Chinese
      language is also

      supported. Each Chinese symbol occupies 2 characters.
Resources:
  Rule:
    Type: 'ALIYUN::IOT::Rule'
    Properties:
      TopicType:
        Ref: TopicType
      IotInstanceId:
        Ref: IotInstanceId
      ResourceGroupId:
        Ref: ResourceGroupId
      RuleAction:
        Ref: RuleAction
      ShortTopic:
        Ref: ShortTopic
      Select:
        Ref: Select
      StartRule:
        Ref: StartRule
      DataType:
        Ref: DataType
      RuleDesc:
        Ref: RuleDesc
      Where:
        Ref: Where
      ProductKey:
        Ref: ProductKey
      Name:
        Ref: Name
Outputs:
  ActionId:
    Description: 'The ID of the rule action. '
    Value:
      'Fn::GetAtt':
        - Rule
        - ActionId
  RuleId:
    Description: 'The ID of the rule. '
    Value:
      'Fn::GetAtt':
        - Rule
        - RuleId         
```

