# ALIYUN::IOT::ProductTopic

ALIYUN::IOT::ProductTopic类型用于为指定产品创建自定义Topic类。

## 语法

```
{
  "Type": "ALIYUN::IOT::ProductTopic",
  "Properties": {
    "Desc": String,
    "IotInstanceId": String,
    "TopicShortName": String,
    "Operation": String,
    "ProductKey": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Desc|String|否|是|Topic类的描述信息。|长度不超过100个字符。|
|IotInstanceId|String|否|否|实例ID。|公共实例无需指定参数，企业版实例需指定该参数。|
|TopicShortName|String|是|是|Topic类的自定义类目名称。|Topic类默认包含`_productKey_`和\_`deviceName_`两级类目，类目间以正斜线（/）分隔，其格式为：`productKey/deviceName/topicShortName`。每级类目的名称只能包含英文字母、数字和下划线（\_），且不能为空。 |
|Operation|String|是|是|设备对Topic类的操作权限。|取值：-   SUB：订阅。
-   PUB：发布。
-   ALL：发布和订阅。 |
|ProductKey|String|是|否|待创建Topic类的产品的ProductKey。|无|

## 返回值

Fn::GetAtt

TopicId：Topic ID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Desc": {
      "Type": "String",
      "Description": "The description of the topic category. You can enter a description with up to 100 characters.",
      "MaxLength": 100
    },
    "IotInstanceId": {
      "Type": "String",
      "Description": "Instance ID you purchased. Public instances do not need pass this property."
    },
    "TopicShortName": {
      "Type": "String",
      "Description": "The custom category hierarchy in the topic category. By default, a topic category contains two system defined category hierarchies: productKey and ${deviceName}. Forward slashes (/) are used to delimit the topic hierarchies. The format of a topic category is productKey/${deviceName}/topicShortName.\nNote The name of each category hierarchy can contain English letters, digits, and underscores (_), and cannot be empty."
    },
    "Operation": {
      "Type": "String",
      "Description": "Operation permissions of devices on the topic category. Value options:\nSUB: Subscribe. Devices can subscribe to the topics of this category.\nPUB: Publish. Devices can publish messages using the topics of this category.\nALL: Subscribe and publish. Devices can subscribe to and publish messages to the topics of this category.",
      "AllowedValues": [
        "ALL",
        "PUB",
        "SUB"
      ]
    },
    "ProductKey": {
      "Type": "String",
      "Description": "The unique identifier of the product for which you want to create a topic category."
    }
  },
  "Resources": {
    "ProductTopic": {
      "Type": "ALIYUN::IOT::ProductTopic",
      "Properties": {
        "Desc": {
          "Ref": "Desc"
        },
        "IotInstanceId": {
          "Ref": "IotInstanceId"
        },
        "TopicShortName": {
          "Ref": "TopicShortName"
        },
        "Operation": {
          "Ref": "Operation"
        },
        "ProductKey": {
          "Ref": "ProductKey"
        }
      }
    }
  },
  "Outputs": {
    "TopicId": {
      "Description": "Topic ID",
      "Value": {
        "Fn::GetAtt": [
          "ProductTopic",
          "TopicId"
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
  Desc:
    Type: String
    Description: >-
      The description of the topic category. You can enter a description with up
      to 100 characters.
    MaxLength: 100
  IotInstanceId:
    Type: String
    Description: >-
      Instance ID you purchased. Public instances do not need pass this
      property.
  TopicShortName:
    Type: String
    Description: >-
      The custom category hierarchy in the topic category. By default, a topic
      category contains two system defined category hierarchies: productKey and
      ${deviceName}. Forward slashes (/) are used to delimit the topic
      hierarchies. The format of a topic category is
      productKey/${deviceName}/topicShortName.

      Note The name of each category hierarchy can contain English letters,
      digits, and underscores (_), and cannot be empty.
  Operation:
    Type: String
    Description: >-
      Operation permissions of devices on the topic category. Value options:

      SUB: Subscribe. Devices can subscribe to the topics of this category.

      PUB: Publish. Devices can publish messages using the topics of this
      category.

      ALL: Subscribe and publish. Devices can subscribe to and publish messages
      to the topics of this category.
    AllowedValues:
      - ALL
      - PUB
      - SUB
  ProductKey:
    Type: String
    Description: >-
      The unique identifier of the product for which you want to create a topic
      category.
Resources:
  ProductTopic:
    Type: 'ALIYUN::IOT::ProductTopic'
    Properties:
      Desc:
        Ref: Desc
      IotInstanceId:
        Ref: IotInstanceId
      TopicShortName:
        Ref: TopicShortName
      Operation:
        Ref: Operation
      ProductKey:
        Ref: ProductKey
Outputs:
  TopicId:
    Description: Topic ID
    Value:
      'Fn::GetAtt':
        - ProductTopic
        - TopicId
```

