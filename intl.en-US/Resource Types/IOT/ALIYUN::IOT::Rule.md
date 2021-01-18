# ALIYUN::IOT::Rule

ALIYUN::IOT::Rule is used to create a rule for a specified topic.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|TopicType|Integer|No|Yes|The type of the topic.|Valid values:-   0: the Thing Specification Language \(TSL\)-based communication topic or the basic communication topic specified in the ShortTopic parameter, such as the topic used to submit the status of OTA update batches.
-   1: the custom topic.
-   2: the topic that is used to submit device status changes. Format: `/as/mqtt/status/${productKey}/${deviceName}`. |
|IotInstanceId|String|No|No|The ID of the instance.|This parameter is required for Enterprise Edition instances, but not required for public instances.|
|ResourceGroupId|String|No|No|The ID of the resource group.|None|
|ShortTopic|String|No|Yes|The specific topic to which the rule is applied.|Format: `${deviceName}/topicShortName`. `${deviceName}` indicates the name of the device, and `topicShortName` indicates the custom name of the topic.|
|Select|String|No|Yes|The SQL SELECT statement that you want to execute. For more information, see [SQL statements](/intl.en-US/Communications/Data Forwarding/SQL statements.md).|Set this parameter to the content that follows the SELECT keyword. For example, if the SELECT statement is `SELECT a,b,c`, set this parameter to `a,b,c`.|
|DataType|String|No|No|The format of the data to be processed by the rule. The value of this parameter must be the same as the format of the device data to be processed.|Default value: JSON. Valid values:-   JSON: JSON data
-   BINARY: binary data

**Note:** If you set this parameter to BINARY, you cannot set the TopicType parameter to 0 or forward data to time series data storage in the instance, Time Series Database \(TSDB\), Tablestore, or ApsaraDB RDS. |
|RuleDesc|String|No|Yes|The description of the rule.|The description can be up to 100 characters in length.|
|Where|String|No|Yes|The condition that is used to trigger the rule. For more information, see [SQL statements](/intl.en-US/Communications/Data Forwarding/SQL statements.md).|Set this parameter to the content that follows the WHERE keyword. For example, if the WHERE statement is `WHERE a>10`, set this parameter to `a>10`.|
|ProductKey|String|No|No|The unique identifier of the product to which the rule applies.|None|
|Name|String|Yes|Yes|The name of the rule.|The name must be 1 to 30 characters in length and can contain Chinese characters, English letters, Japanese characters, digits, hyphens \(-\), and underscores \(\_\).**Note:** Each Chinese character or Japanese character uses 2 characters. |

## Response parameters

Fn::GetAtt

-   TopicType: the type of the topic. If no SQL statement is set for the rule, the value -1 is returned.
-   IotInstanceId: the ID of the instance.
-   ResourceGroupId: the ID of the resource group.
-   RuleId: the ID of the rule.
-   ShortTopic: the topic to which the rule is applied.
-   Select: the SQL SELECT statement that is executed.
-   DataType: the format of the data that is processed by the rule.
-   RuleDesc: the description of the rule.
-   Where: the condition that is used to trigger the rule.
-   ProductKey: the unique identifier of the product to which the rule applies.
-   name: the name of the rule.

## Examples

`JSON` format

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

`YAML` format

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

