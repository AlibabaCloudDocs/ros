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
|Select|String|否|是|要执行的SQL Select语句。更多信息，请参见[SQL表达式](/cn.zh-CN/消息通信/云产品流转/SQL表达式.md)。|该参数取值为Select中的内容。例如：如果Select语句为`Select a,b,c`，则指定`a,b,c`。|
|DataType|String|否|否|规则处理的数据格式，需与待处理的设备数据格式一致。|取值：-   JSON（默认值）：JSON数据。
-   BINARY：二进制数据。

**说明：** 若指定BINARY，TopicType不能选择为0（基础通信Topic或物模型通信Topic），且不支持将数据转发至实例内的时序数据存储、时序数据库、表格存储和云数据库RDS版。 |
|RuleDesc|String|否|是|规则的描述信息。|长度不超过100个字符。|
|Where|String|否|是|规则的触发条件。更多信息，请参见[SQL表达式](/cn.zh-CN/消息通信/云产品流转/SQL表达式.md)。|该参数取值为Where中的内容。例如：如果Where语句为`Where a>10`，则指定`a>10`。|
|ProductKey|String|否|否|应用该规则的产品ProductKey。|无|
|Name|String|是|是|规则名称。|长度为1~30个字符。可包含汉字、英文字母、日文、数字、下划线（\_）和短划线（-）。**说明：** 一个汉字或日文占2个字符。 |

## 返回值

Fn::GetAtt

-   TopicType：Topic类型。若未设置过规则SQL语句，则返回-1。
-   IotInstanceId：实例ID。
-   ResourceGroupId：资源组ID。
-   RuleId：规则ID。
-   ShortTopic：规则处理的消息来源的具体Topic。
-   Select：规则SQL语句中的Select内容。
-   DataType：该规则的数据类型。
-   RuleDesc：规则的描述信息。
-   Where：规则SQL语句中的Where查询条件。
-   ProductKey：应用规则的产品ProductKey。
-   Name：规则名称。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "TopicType": {
      "Type": "Number",
      "Description": "0: The topic is a basic communication topic or TSL-based communication topic. 1: The topic is a custom topic. 2: The topic is used to submit device status changes. Syntax: /as/mqtt/status/${productKey}/${deviceName}."
    },
    "IotInstanceId": {
      "Type": "String",
      "Description": "The ID of the instance. This parameter is not required for public instances. However, the parameter is required for the instances that you have purchased."
    },
    "ResourceGroupId": {
      "Type": "String",
      "Description": "The ID of the resource group to which the rule is assigned. You can view the resource group information in the Resource Management console.  If you do not specify this parameter, the rule is assigned to the default resource group."
    },
    "ShortTopic": {
      "Type": "String",
      "Description": "The topic to which this rule is applied. Syntax: ${deviceName}/topicShortName. ${deviceName}specifies the name of the device, and topicShortNamespecifies the custom name of the topic.  Basic communication topics or Thing Specification Language (TSL)-based communication topics. Syntax: ${deviceName}/topicShortName. You can replace ${deviceName} with the + wildcard. The wildcard indicates that the topic applies to all devices under the product. Valid values of topicShortName: /thing/event/property/post: submits the property data of a device. /thing/event/${tsl.event.identifier}/post: submits the event data of a device.${tsl.event.identifier} specifies the identifier of an event in the TSL. /thing/lifecycle: submits device lifecycle changes. /thing/downlink/reply/message: sends a response to a request from IoT Platform. /thing/list/found: submits the data when a gateway detects a new sub-device. /thing/topo/lifecycle: submits device topology changes. /thing/event/property/history/post: submits historical property data of a device. /thing/event/${tsl.event.identifier}/post: submits the historical event data of a device.${tsl.event.identifier}specifies the identifier of an event in the TSL. /ota/upgrade: submits OTA update status. /ota/version/post: submits OTA module versions. /thing/deviceinfo/update: submits device tag changes. /edge/driver/${driver_id}/point_post: submits pass-through data from Link IoT Edge.${driver_id} specifies the ID of the driver that a device uses to access Link IoT Edge.  ${packageId}/${jobId}/ota/job/status: submits the status of OTA update batches. This topic is a basic communication topic. ${packageId}specifies the ID of the firmware. ${jobId}specifies the ID of the update batch.  Custom topics. Example:${deviceName}/user/get.  You can call theQueryProductTopicoperation to view all custom topics of the product.  When you specify a custom topic, you can use the + and # wildcards.  You can replace ${deviceName} with the+ wildcard. The wildcard indicates that the topic applies to all devices under the product. You can replace the fields that follow ${deviceName} with /user/#. The # wildcard indicates that the topic applies whatever values are specified for the fields that follow/user.  For more information about how to use wildcards, see Wildcards in topics.  Topic that is used to submit device status changes: ${deviceName}.  You can use the+wildcard. In this case, the status changes of all devices under the product are submitted."
    },
    "Select": {
      "Type": "String",
      "Description": "The SQL SELECT statement that you want to execute. For more information, seeSQL expressions."
    },
    "DataType": {
      "Type": "String",
      "Description": "The format of the data to be processed by the rule. You must specify the format of device data to be processed for this parameter. Valid values:  JSON: JSON data BINARY: binary data"
    },
    "RuleDesc": {
      "Type": "String",
      "Description": "The description of the rule. The description can be up to 100 characters in length. Each Chinese symbol occupies 1 characters."
    },
    "Where": {
      "Type": "String",
      "Description": "The condition that is used to trigger the rule. For more information, seeSQL expressions."
    },
    "ProductKey": {
      "Type": "String",
      "Description": "The ProductKey of the product to which the rule applies."
    },
    "Name": {
      "Type": "String",
      "Description": "The name of the rule. The name must be 1 to 30 characters in length and can contain English letters, digits, underscores (_), and hyphens (-). Chinese language is also supported. Each Chinese symbol occupies 2 characters."
    }
  },
  "Resources": {
    "IotRule": {
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
        "ShortTopic": {
          "Ref": "ShortTopic"
        },
        "Select": {
          "Ref": "Select"
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
    "TopicType": {
      "Description": "0: The topic is a basic communication topic or TSL-based communication topic. 1: The topic is a custom topic. 2: The topic is used to submit device status changes. Syntax: /as/mqtt/status/${productKey}/${deviceName}.",
      "Value": {
        "Fn::GetAtt": [
          "IotRule",
          "TopicType"
        ]
      }
    },
    "IotInstanceId": {
      "Description": "The ID of the instance. This parameter is not required for public instances. However, the parameter is required for the instances that you have purchased.",
      "Value": {
        "Fn::GetAtt": [
          "IotRule",
          "IotInstanceId"
        ]
      }
    },
    "ResourceGroupId": {
      "Description": "The ID of the resource group to which the rule is assigned. You can view the resource group information in the Resource Management console.  If you do not specify this parameter, the rule is assigned to the default resource group.",
      "Value": {
        "Fn::GetAtt": [
          "IotRule",
          "ResourceGroupId"
        ]
      }
    },
    "RuleId": {
      "Description": "The ID of the rule. The rule ID is generated by the rules engine if the call was successful.",
      "Value": {
        "Fn::GetAtt": [
          "IotRule",
          "RuleId"
        ]
      }
    },
    "ShortTopic": {
      "Description": "The topic to which this rule is applied. Syntax: ${deviceName}/topicShortName. ${deviceName}specifies the name of the device, and topicShortNamespecifies the custom name of the topic.  Basic communication topics or Thing Specification Language (TSL)-based communication topics. Syntax: ${deviceName}/topicShortName. You can replace ${deviceName} with the + wildcard. The wildcard indicates that the topic applies to all devices under the product. Valid values of topicShortName: /thing/event/property/post: submits the property data of a device. /thing/event/${tsl.event.identifier}/post: submits the event data of a device.${tsl.event.identifier} specifies the identifier of an event in the TSL. /thing/lifecycle: submits device lifecycle changes. /thing/downlink/reply/message: sends a response to a request from IoT Platform. /thing/list/found: submits the data when a gateway detects a new sub-device. /thing/topo/lifecycle: submits device topology changes. /thing/event/property/history/post: submits historical property data of a device. /thing/event/${tsl.event.identifier}/post: submits the historical event data of a device.${tsl.event.identifier}specifies the identifier of an event in the TSL. /ota/upgrade: submits OTA update status. /ota/version/post: submits OTA module versions. /thing/deviceinfo/update: submits device tag changes. /edge/driver/${driver_id}/point_post: submits pass-through data from Link IoT Edge.${driver_id} specifies the ID of the driver that a device uses to access Link IoT Edge.  ${packageId}/${jobId}/ota/job/status: submits the status of OTA update batches. This topic is a basic communication topic. ${packageId}specifies the ID of the firmware. ${jobId}specifies the ID of the update batch.  Custom topics. Example:${deviceName}/user/get.  You can call theQueryProductTopicoperation to view all custom topics of the product.  When you specify a custom topic, you can use the + and # wildcards.  You can replace ${deviceName} with the+ wildcard. The wildcard indicates that the topic applies to all devices under the product. You can replace the fields that follow ${deviceName} with /user/#. The # wildcard indicates that the topic applies whatever values are specified for the fields that follow/user.  For more information about how to use wildcards, see Wildcards in topics.  Topic that is used to submit device status changes: ${deviceName}.  You can use the+wildcard. In this case, the status changes of all devices under the product are submitted.",
      "Value": {
        "Fn::GetAtt": [
          "IotRule",
          "ShortTopic"
        ]
      }
    },
    "Select": {
      "Description": "The SQL SELECT statement that you want to execute. For more information, seeSQL expressions.",
      "Value": {
        "Fn::GetAtt": [
          "IotRule",
          "Select"
        ]
      }
    },
    "DataType": {
      "Description": "The format of the data to be processed by the rule. You must specify the format of device data to be processed for this parameter. Valid values:  JSON: JSON data BINARY: binary data",
      "Value": {
        "Fn::GetAtt": [
          "IotRule",
          "DataType"
        ]
      }
    },
    "RuleDesc": {
      "Description": "The description of the rule. The description can be up to 100 characters in length. Each Chinese symbol occupies 1 characters.",
      "Value": {
        "Fn::GetAtt": [
          "IotRule",
          "RuleDesc"
        ]
      }
    },
    "Where": {
      "Description": "The condition that is used to trigger the rule. For more information, seeSQL expressions.",
      "Value": {
        "Fn::GetAtt": [
          "IotRule",
          "Where"
        ]
      }
    },
    "ProductKey": {
      "Description": "The ProductKey of the product to which the rule applies.",
      "Value": {
        "Fn::GetAtt": [
          "IotRule",
          "ProductKey"
        ]
      }
    },
    "Name": {
      "Description": "The name of the rule. The name must be 1 to 30 characters in length and can contain English letters, digits, underscores (_), and hyphens (-). Chinese language is also supported. Each Chinese symbol occupies 2 characters.",
      "Value": {
        "Fn::GetAtt": [
          "IotRule",
          "Name"
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
      topic. 1: The topic is a custom topic. 2: The topic is used to submit
      device status changes. Syntax:
      /as/mqtt/status/${productKey}/${deviceName}.
  IotInstanceId:
    Type: String
    Description: >-
      The ID of the instance. This parameter is not required for public
      instances. However, the parameter is required for the instances that you
      have purchased.
  ResourceGroupId:
    Type: String
    Description: >-
      The ID of the resource group to which the rule is assigned. You can view
      the resource group information in the Resource Management console.  If you
      do not specify this parameter, the rule is assigned to the default
      resource group.
  ShortTopic:
    Type: String
    Description: >-
      The topic to which this rule is applied. Syntax:
      ${deviceName}/topicShortName. ${deviceName}specifies the name of the
      device, and topicShortNamespecifies the custom name of the topic.  Basic
      communication topics or Thing Specification Language (TSL)-based
      communication topics. Syntax: ${deviceName}/topicShortName. You can
      replace ${deviceName} with the + wildcard. The wildcard indicates that the
      topic applies to all devices under the product. Valid values of
      topicShortName: /thing/event/property/post: submits the property data of a
      device. /thing/event/${tsl.event.identifier}/post: submits the event data
      of a device.${tsl.event.identifier} specifies the identifier of an event
      in the TSL. /thing/lifecycle: submits device lifecycle changes.
      /thing/downlink/reply/message: sends a response to a request from IoT
      Platform. /thing/list/found: submits the data when a gateway detects a new
      sub-device. /thing/topo/lifecycle: submits device topology changes.
      /thing/event/property/history/post: submits historical property data of a
      device. /thing/event/${tsl.event.identifier}/post: submits the historical
      event data of a device.${tsl.event.identifier}specifies the identifier of
      an event in the TSL. /ota/upgrade: submits OTA update status.
      /ota/version/post: submits OTA module versions. /thing/deviceinfo/update:
      submits device tag changes. /edge/driver/${driver_id}/point_post: submits
      pass-through data from Link IoT Edge.${driver_id} specifies the ID of the
      driver that a device uses to access Link IoT Edge. 
      ${packageId}/${jobId}/ota/job/status: submits the status of OTA update
      batches. This topic is a basic communication topic. ${packageId}specifies
      the ID of the firmware. ${jobId}specifies the ID of the update batch. 
      Custom topics. Example:${deviceName}/user/get.  You can call
      theQueryProductTopicoperation to view all custom topics of the product. 
      When you specify a custom topic, you can use the + and # wildcards.  You
      can replace ${deviceName} with the+ wildcard. The wildcard indicates that
      the topic applies to all devices under the product. You can replace the
      fields that follow ${deviceName} with /user/#. The # wildcard indicates
      that the topic applies whatever values are specified for the fields that
      follow/user.  For more information about how to use wildcards, see
      Wildcards in topics.  Topic that is used to submit device status changes:
      ${deviceName}.  You can use the+wildcard. In this case, the status changes
      of all devices under the product are submitted.
  Select:
    Type: String
    Description: >-
      The SQL SELECT statement that you want to execute. For more information,
      seeSQL expressions.
  DataType:
    Type: String
    Description: >-
      The format of the data to be processed by the rule. You must specify the
      format of device data to be processed for this parameter. Valid values: 
      JSON: JSON data BINARY: binary data
  RuleDesc:
    Type: String
    Description: >-
      The description of the rule. The description can be up to 100 characters
      in length. Each Chinese symbol occupies 1 characters.
  Where:
    Type: String
    Description: >-
      The condition that is used to trigger the rule. For more information,
      seeSQL expressions.
  ProductKey:
    Type: String
    Description: The ProductKey of the product to which the rule applies.
  Name:
    Type: String
    Description: >-
      The name of the rule. The name must be 1 to 30 characters in length and
      can contain English letters, digits, underscores (_), and hyphens (-).
      Chinese language is also supported. Each Chinese symbol occupies 2
      characters.
Resources:
  IotRule:
    Type: 'ALIYUN::IOT::Rule'
    Properties:
      TopicType:
        Ref: TopicType
      IotInstanceId:
        Ref: IotInstanceId
      ResourceGroupId:
        Ref: ResourceGroupId
      ShortTopic:
        Ref: ShortTopic
      Select:
        Ref: Select
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
  TopicType:
    Description: >-
      0: The topic is a basic communication topic or TSL-based communication
      topic. 1: The topic is a custom topic. 2: The topic is used to submit
      device status changes. Syntax:
      /as/mqtt/status/${productKey}/${deviceName}.
    Value:
      'Fn::GetAtt':
        - IotRule
        - TopicType
  IotInstanceId:
    Description: >-
      The ID of the instance. This parameter is not required for public
      instances. However, the parameter is required for the instances that you
      have purchased.
    Value:
      'Fn::GetAtt':
        - IotRule
        - IotInstanceId
  ResourceGroupId:
    Description: >-
      The ID of the resource group to which the rule is assigned. You can view
      the resource group information in the Resource Management console.  If you
      do not specify this parameter, the rule is assigned to the default
      resource group.
    Value:
      'Fn::GetAtt':
        - IotRule
        - ResourceGroupId
  RuleId:
    Description: >-
      The ID of the rule. The rule ID is generated by the rules engine if the
      call was successful.
    Value:
      'Fn::GetAtt':
        - IotRule
        - RuleId
  ShortTopic:
    Description: >-
      The topic to which this rule is applied. Syntax:
      ${deviceName}/topicShortName. ${deviceName}specifies the name of the
      device, and topicShortNamespecifies the custom name of the topic.  Basic
      communication topics or Thing Specification Language (TSL)-based
      communication topics. Syntax: ${deviceName}/topicShortName. You can
      replace ${deviceName} with the + wildcard. The wildcard indicates that the
      topic applies to all devices under the product. Valid values of
      topicShortName: /thing/event/property/post: submits the property data of a
      device. /thing/event/${tsl.event.identifier}/post: submits the event data
      of a device.${tsl.event.identifier} specifies the identifier of an event
      in the TSL. /thing/lifecycle: submits device lifecycle changes.
      /thing/downlink/reply/message: sends a response to a request from IoT
      Platform. /thing/list/found: submits the data when a gateway detects a new
      sub-device. /thing/topo/lifecycle: submits device topology changes.
      /thing/event/property/history/post: submits historical property data of a
      device. /thing/event/${tsl.event.identifier}/post: submits the historical
      event data of a device.${tsl.event.identifier}specifies the identifier of
      an event in the TSL. /ota/upgrade: submits OTA update status.
      /ota/version/post: submits OTA module versions. /thing/deviceinfo/update:
      submits device tag changes. /edge/driver/${driver_id}/point_post: submits
      pass-through data from Link IoT Edge.${driver_id} specifies the ID of the
      driver that a device uses to access Link IoT Edge. 
      ${packageId}/${jobId}/ota/job/status: submits the status of OTA update
      batches. This topic is a basic communication topic. ${packageId}specifies
      the ID of the firmware. ${jobId}specifies the ID of the update batch. 
      Custom topics. Example:${deviceName}/user/get.  You can call
      theQueryProductTopicoperation to view all custom topics of the product. 
      When you specify a custom topic, you can use the + and # wildcards.  You
      can replace ${deviceName} with the+ wildcard. The wildcard indicates that
      the topic applies to all devices under the product. You can replace the
      fields that follow ${deviceName} with /user/#. The # wildcard indicates
      that the topic applies whatever values are specified for the fields that
      follow/user.  For more information about how to use wildcards, see
      Wildcards in topics.  Topic that is used to submit device status changes:
      ${deviceName}.  You can use the+wildcard. In this case, the status changes
      of all devices under the product are submitted.
    Value:
      'Fn::GetAtt':
        - IotRule
        - ShortTopic
  Select:
    Description: >-
      The SQL SELECT statement that you want to execute. For more information,
      seeSQL expressions.
    Value:
      'Fn::GetAtt':
        - IotRule
        - Select
  DataType:
    Description: >-
      The format of the data to be processed by the rule. You must specify the
      format of device data to be processed for this parameter. Valid values: 
      JSON: JSON data BINARY: binary data
    Value:
      'Fn::GetAtt':
        - IotRule
        - DataType
  RuleDesc:
    Description: >-
      The description of the rule. The description can be up to 100 characters
      in length. Each Chinese symbol occupies 1 characters.
    Value:
      'Fn::GetAtt':
        - IotRule
        - RuleDesc
  Where:
    Description: >-
      The condition that is used to trigger the rule. For more information,
      seeSQL expressions.
    Value:
      'Fn::GetAtt':
        - IotRule
        - Where
  ProductKey:
    Description: The ProductKey of the product to which the rule applies.
    Value:
      'Fn::GetAtt':
        - IotRule
        - ProductKey
  Name:
    Description: >-
      The name of the rule. The name must be 1 to 30 characters in length and
      can contain English letters, digits, underscores (_), and hyphens (-).
      Chinese language is also supported. Each Chinese symbol occupies 2
      characters.
    Value:
      'Fn::GetAtt':
        - IotRule
        - Name
```

