# ALIYUN::KAFKA::Instance

ALIYUN::KAFKA::Instance类型用于创建Kafka实例。

## 语法

```
{
  "Type": "ALIYUN::KAFKA::Instance",
  "Properties": {
    "DeployType": Integer,
    "DiskType": String,
    "DeployOption": Map,
    "EipMax": Integer,
    "SpecType": String,
    "IoMax": Integer,
    "IoMaxSpec": String,
    "DiskSize": Integer,
    "TopicQuota": Integer,
    "PayType": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|DeployType|Integer|是|否|部署类型。|取值：-   4：公网和VPC实例。
-   5：VPC实例。 |
|DiskType|String|是|否|磁盘类型。|取值：-   0：高效云盘。
-   1：SSD。 |
|DeployOption|Map|否|否|部署选项。|更多信息，请参见[DeployOption属性](#section_n9x_w7i_uc2)。|
|EipMax|Integer|否|是|公网流量。|当DeployType取值为4时，需指定该参数。取值范围：1~160。 |
|SpecType|String|否|是|规格类型。|取值：-   normal：标准版（高写版）。
-   professional：专业版（高写版）。
-   professionalForHighRead：专业版（高读版）。 |
|IoMax|Integer|否|是|流量峰值（不推荐）。|流量峰值和流量规格必须指定其中一个参数。如果同时指定，以流量规格为准。建议您只填写流量规格。取值范围，请参见[计费说明](/intl.zh-CN/产品定价/计费说明.md)。 |
|IoMaxSpec|String|否|是|流量规格（推荐）。|流量峰值和流量规格必须指定其中一个参数。如果同时指定，以流量规格为准。建议您只填写流量规格。取值范围，请参见[计费说明](/intl.zh-CN/产品定价/计费说明.md)。 |
|DiskSize|Integer|是|是|磁盘容量。|取值范围：500~96,000。单位：GB。 |
|TopicQuota|Integer|是|是|Topic的数量。|取值范围：50~79。|
|PayType|String|否|否|付费类型。|取值：-   Hour：按小时付费。
-   Month：按月付费。 |

## DeployOption语法

```
"DeployOption": {
  "IsEipInner": Boolean,
  "VpcId": String,
  "ZoneId": String,
  "VSwitchId": String,
  "SecurityGroup": String,
  "DeployModule": String,
  "Name": String,
  "IsSetUserAndPassword": Boolean,
  "Username": String,
  "Password": String
}
```

## DeployOption属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|IsEipInner|Boolean|否|否|是否支持EIP。|取值：-   true：支持EIP。
-   false：不支持EIP。

EIP支持情况必须与实例类型一致。即公网和VPC实例取值为true，VPC实例取值为false。 |
|DeployModule|String|是|否|部署模式。|取值：-   vpc：VPC实例的部署模式。
-   eip：公网和VPC实例的部署模式。 |
|VpcId|String|否|否|实例部署的专有网络ID。|无|
|ZoneId|String|否|否|实例部署的可用区ID。|无|
|VSwitchId|String|是|否|实例部署的交换机ID。|无|
|SecurityGroup|String|否|否|实例的安全组。|不填写时，消息队列Kafka版会自动为您的实例配置安全组。|
|Name|String|否|否|实例名称。|无|
|IsSetUserAndPassword|Boolean|否|否|是否设置新的用户名和密码。|仅支持公网和VPC实例。取值：-   true
-   false |
|Username|String|否|否|用户名。|仅支持公网和VPC实例。

长度为8~40个字符，可包含英文字母和数字。 |
|Password|String|否|否|用户密码。|仅支持公网和VPC实例。

长度为8~40个字符，可包含英文字母和数字，且必须同时包含小写字母、大写字母和数字。 |

## 返回值

Fn::GetAtt

-   InstanceId：实例ID。
-   OrderId：订单ID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "DeployType": {
      "Type": "Number",
      "Description": "The deployment mode of the Message Queue for Apache Kafka instance. Valid values: \n  4: Instance of the public type \n  5: Instance of the VPC type",
      "AllowedValues": [
        4,
        5
      ]
    },
    "DiskType": {
      "Type": "String",
      "Description": "The type of the disk to be configured for the Message Queue for Apache Kafka instance. Valid values: \n0: Ultra disk \n1: SSD",
      "AllowedValues": [
        "0",
        "1"
      ]
    },
    "DeployOption": {
      "Type": "Json",
      "Description": "If you want to deploy instance after create at once, the VSwitchId and DeployModule parameters is required"
    },
    "EipMax": {
      "Type": "Number",
      "Description": "The public traffic to be configured for the Message Queue for Apache Kafka instance. \nThis parameter must be specified when the DeployType parameter is set to 4."
    },
    "SpecType": {
      "Type": "String",
      "Description": "The edition of the Message Queue for Apache Kafka instance. Valid values: \nprofessional: Professional Edition \nnormal: Normal version",
      "AllowedValues": [
        "normal",
        "professional",
        "professionalForHighRead"
      ]
    },
    "IoMax": {
      "Type": "Number",
      "Description": "The peak traffic to be configured for the Message Queue for Apache Kafka instance. \nFor more information about the value range, see Billing."
    },
    "IoMaxSpec": {
      "Type": "String",
      "Description": "Flow specification (recommended) \nThe IoMax and IoMaxSpec must be optional. \nWhen filling in at the same time, subject to IoMaxSpec. \nIt is recommended that you only fill in the flow specification \n"
    },
    "DiskSize": {
      "Type": "Number",
      "Description": "The size of the disk to be configured for the Message Queue for Apache Kafka instance."
    },
    "TopicQuota": {
      "Type": "Number",
      "Description": "The number of topics to be configured for the Message Queue for Apache Kafka instance. \nThe default value of this parameter varies with different peak traffic values. \nAdditional fees are charged if the default values are exceeded.\n Different specifications have different default values, and extra fees are charged. \nFor more information, see Billing."
    },
    "PayType": {
      "Type": "String",
      "Description": "Pay by hour or month.",
      "AllowedValues": [
        "Hour",
        "Month"
      ],
      "Default": "Hour"
    }
  },
  "Resources": {
    "Instance": {
      "Type": "ALIYUN::KAFKA::Instance",
      "Properties": {
        "DeployType": {
          "Ref": "DeployType"
        },
        "DiskType": {
          "Ref": "DiskType"
        },
        "DeployOption": {
          "Ref": "DeployOption"
        },
        "EipMax": {
          "Ref": "EipMax"
        },
        "SpecType": {
          "Ref": "SpecType"
        },
        "IoMax": {
          "Ref": "IoMax"
        },
        "IoMaxSpec": {
          "Ref": "IoMaxSpec"
        },
        "DiskSize": {
          "Ref": "DiskSize"
        },
        "TopicQuota": {
          "Ref": "TopicQuota"
        },
        "PayType": {
          "Ref": "PayType"
        }
      }
    }
  },
  "Outputs": {
    "InstanceId": {
      "Description": "Id of the instance. ",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "InstanceId"
        ]
      }
    },
    "OrderId": {
      "Description": "Id of the order. ",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "OrderId"
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
  DeployType:
    Type: Number
    Description: >-
      The deployment mode of the Message Queue for Apache Kafka instance. Valid
      values: 
        4: Instance of the public type 
        5: Instance of the VPC type
    AllowedValues:
      - 4
      - 5
  DiskType:
    Type: String
    Description: >-
      The type of the disk to be configured for the Message Queue for Apache
      Kafka instance. Valid values: 

      0: Ultra disk 

      1: SSD
    AllowedValues:
      - '0'
      - '1'
  DeployOption:
    Type: Json
    Description: >-
      If you want to deploy instance after create at once, the VSwitchId and
      DeployModule parameters is required
  EipMax:
    Type: Number
    Description: >-
      The public traffic to be configured for the Message Queue for Apache Kafka
      instance. 

      This parameter must be specified when the DeployType parameter is set to
      4.
  SpecType:
    Type: String
    Description: |-
      The edition of the Message Queue for Apache Kafka instance. Valid values: 
      professional: Professional Edition 
      normal: Normal version
    AllowedValues:
      - normal
      - professional
      - professionalForHighRead
  IoMax:
    Type: Number
    Description: >-
      The peak traffic to be configured for the Message Queue for Apache Kafka
      instance. 

      For more information about the value range, see Billing.
  IoMaxSpec:
    Type: String
    Description: |
      Flow specification (recommended) 
      The IoMax and IoMaxSpec must be optional. 
      When filling in at the same time, subject to IoMaxSpec. 
      It is recommended that you only fill in the flow specification 
  DiskSize:
    Type: Number
    Description: >-
      The size of the disk to be configured for the Message Queue for Apache
      Kafka instance.
  TopicQuota:
    Type: Number
    Description: >-
      The number of topics to be configured for the Message Queue for Apache
      Kafka instance. 

      The default value of this parameter varies with different peak traffic
      values. 

      Additional fees are charged if the default values are exceeded.
       Different specifications have different default values, and extra fees are charged. 
      For more information, see Billing.
  PayType:
    Type: String
    Description: Pay by hour or month.
    AllowedValues:
      - Hour
      - Month
    Default: Hour
Resources:
  Instance:
    Type: 'ALIYUN::KAFKA::Instance'
    Properties:
      DeployType:
        Ref: DeployType
      DiskType:
        Ref: DiskType
      DeployOption:
        Ref: DeployOption
      EipMax:
        Ref: EipMax
      SpecType:
        Ref: SpecType
      IoMax:
        Ref: IoMax
      IoMaxSpec:
        Ref: IoMaxSpec
      DiskSize:
        Ref: DiskSize
      TopicQuota:
        Ref: TopicQuota
      PayType:
        Ref: PayType
Outputs:
  InstanceId:
    Description: 'Id of the instance. '
    Value:
      'Fn::GetAtt':
        - Instance
        - InstanceId
  OrderId:
    Description: 'Id of the order. '
    Value:
      'Fn::GetAtt':
        - Instance
        - OrderId     
```

