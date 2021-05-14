# ALIYUN::KAFKA::Instance

ALIYUN::KAFKA::Instance is used to create a Message Queue for Apache Kafka instance.

## Syntax

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
    "PayType": String,
    "Tags": List
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|DeployType|Integer|Yes|No|The type of the network in which to deploy the instance.|Valid values:-   4: Internet and Virtual Private Cloud \(VPC\)
-   5: VPC |
|DiskType|String|Yes|No|The category of the disk.|Valid values:-   0: ultra disk
-   1: standard SSD |
|DeployOption|Map|No|No|The information about the deployment options.|For more information, see the [DeployOption properties](#section_n9x_w7i_uc2) section in this topic.|
|EipMax|Integer|No|Yes|The public traffic for the instance.|This parameter is required when the DeployType parameter is set to 4. Valid values: 1 to 160. |
|SpecType|String|No|Yes|The edition of the instance.|Valid values:-   normal: Standard Edition \(High Write\)
-   professional: Professional Edition \(High Write\)
-   professionalForHighRead: Professional Edition \(High Read\) |
|IoMax|Integer|No|Yes|The peak traffic of the instance.|You must specify one of the IoMax and IoMaxSpec parameters. If you specify both the IoMax and IoMaxSpec parameters, the IoMaxSpec parameter prevails. We recommend that you specify only the IoMaxSpec parameter. For more information about the valid values, see [Billing](/intl.en-US/Pricing/Billing.md). |
|IoMaxSpec|String|No|Yes|The traffic specifications of the instance.|You must specify one of the IoMax and IoMaxSpec parameters. If you specify both the IoMax and IoMaxSpec parameters, the IoMaxSpec parameter prevails. We recommend that you specify only the IoMaxSpec parameter. For more information about the valid values, see [Billing](/intl.en-US/Pricing/Billing.md). |
|DiskSize|Integer|Yes|Yes|The size of the disk.|Valid values: 500 to 96000. Unit: GB. |
|TopicQuota|Integer|Yes|Yes|The number of topics.|Valid values: 50 to 79.|
|PayType|String|No|No|The billing unit of the subscription instance.|Valid values:-   Hour
-   Month |
|Tags|List|No|Yes|The tags of the instance.|A maximum of 20 tags can be specified. For more information, see the [Tags properties](#section_zsa_dbk_p3s) section in this topic. |

## Tags syntax

```
"Tags": [
  {
    "Key": String,
    "Value": String
  }
]  
```

## Tags properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Key|String|Yes|No|The tag key.|The tag key must be 1 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|
|Value|String|No|No|The tag value.|The tag value must be 0 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|

## DeployOption syntax

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

## DeployOption properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|IsEipInner|Boolean|No|No|Specifies whether the instance supports elastic IP addresses \(EIPs\).|Valid values:-   true
-   false

This parameter must be consistent with the instance type. Set the parameter to true for instances of the Internet and VPC type or to false for instances of the VPC type. |
|DeployModule|String|Yes|No|The type of the network in which to deploy the instance.|Valid values:-   vpc: VPC
-   eip: Internet and VPC |
|VpcId|String|No|No|The VPC ID of the instance.|None|
|ZoneId|String|No|No|The zone ID of the instance.|None|
|VSwitchId|String|Yes|No|The vSwitch ID of the instance.|None|
|SecurityGroup|String|No|No|The security group of the instance.|If you leave this parameter empty, Message Queue for Apache Kafka configures a security group for the instance.|
|Name|String|No|No|The name of the instance.|None|
|IsSetUserAndPassword|Boolean|No|No|Specifies whether to set a new username and password.|This parameter takes effect only when the DeployType parameter is set to 4. Valid values:-   true
-   false |
|Username|String|No|No|The username that is used to connect to the instance.|This parameter takes effect only when the DeployType parameter is set to 4.

The username must be 8 to 40 characters in length, and can contain letters and digits. |
|Password|String|No|No|The password that is used to connect to the instance.|This parameter takes effect only when the DeployType parameter is set to 4.

The password must be 8 to 40 characters in length, and must contain lowercase letters, uppercase letters, and digits. |

## Response parameters

Fn::GetAtt

-   InstanceId: the ID of the instance.
-   OrderId: the order ID.
-   name: the name of the instance.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "DeployType": {
      "Type": "Number",
      "Description": "The deployment mode of the Message Queue for Apache Kafka instance. Valid values: \n  4: Instance of the public type \n  5: Instance of the VPC type",
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
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to instance. Max support 20 tags to add during create instance. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
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
        },
        "Tags": {
          "Ref": "Tags"
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
    },
    "Name": {
      "Description": "Name of the instance.",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
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
  DeployOption:
    Description: If you want to deploy instance after create at once, the VSwitchId
      and DeployModule parameters is required
    Type: Json
  DeployType:
    AllowedValues:
    - 4
    - 5
    Description: "The deployment mode of the Message Queue for Apache Kafka instance.\
      \ Valid values: \n  4: Instance of the public type \n  5: Instance of the VPC\
      \ type"
    Type: Number
  DiskSize:
    Description: The size of the disk to be configured for the Message Queue for Apache
      Kafka instance.
    Type: Number
  DiskType:
    AllowedValues:
    - '0'
    - '1'
    Description: "The type of the disk to be configured for the Message Queue for\
      \ Apache Kafka instance. Valid values: \n0: Ultra disk \n1: SSD"
    Type: String
  EipMax:
    Description: "The public traffic to be configured for the Message Queue for Apache\
      \ Kafka instance. \nThis parameter must be specified when the DeployType parameter\
      \ is set to 4."
    Type: Number
  IoMax:
    Description: "The peak traffic to be configured for the Message Queue for Apache\
      \ Kafka instance. \nFor more information about the value range, see Billing."
    Type: Number
  IoMaxSpec:
    Description: "Flow specification (recommended) \nThe IoMax and IoMaxSpec must\
      \ be optional. \nWhen filling in at the same time, subject to IoMaxSpec. \n\
      It is recommended that you only fill in the flow specification \n"
    Type: String
  PayType:
    AllowedValues:
    - Hour
    - Month
    Default: Hour
    Description: Pay by hour or month.
    Type: String
  SpecType:
    AllowedValues:
    - normal
    - professional
    - professionalForHighRead
    Description: "The edition of the Message Queue for Apache Kafka instance. Valid\
      \ values: \nprofessional: Professional Edition \nnormal: Normal version"
    Type: String
  Tags:
    Description: Tags to attach to instance. Max support 20 tags to add during create
      instance. Each tag with two properties Key and Value, and Key is required.
    MaxLength: 20
    Type: Json
  TopicQuota:
    Description: "The number of topics to be configured for the Message Queue for\
      \ Apache Kafka instance. \nThe default value of this parameter varies with different\
      \ peak traffic values. \nAdditional fees are charged if the default values are\
      \ exceeded.\n Different specifications have different default values, and extra\
      \ fees are charged. \nFor more information, see Billing."
    Type: Number
Resources:
  Instance:
    Properties:
      DeployOption:
        Ref: DeployOption
      DeployType:
        Ref: DeployType
      DiskSize:
        Ref: DiskSize
      DiskType:
        Ref: DiskType
      EipMax:
        Ref: EipMax
      IoMax:
        Ref: IoMax
      IoMaxSpec:
        Ref: IoMaxSpec
      PayType:
        Ref: PayType
      SpecType:
        Ref: SpecType
      Tags:
        Ref: Tags
      TopicQuota:
        Ref: TopicQuota
    Type: ALIYUN::KAFKA::Instance
Outputs:
  InstanceId:
    Description: 'Id of the instance. '
    Value:
      Fn::GetAtt:
      - Instance
      - InstanceId
  Name:
    Description: Name of the instance.
    Value:
      Fn::GetAtt:
      - Instance
      - Name
  OrderId:
    Description: 'Id of the order. '
    Value:
      Fn::GetAtt:
      - Instance
      - OrderId
```

For more examples, visit [Instance.json](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/Kafka/JSON/Instance.json) and [Instance.yml](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/Kafka/YAML/Instance.yml). In the examples, the ALIYUN::KAFKA::Instance and ALIYUN::KAFKA::Topic resource types are involved.

