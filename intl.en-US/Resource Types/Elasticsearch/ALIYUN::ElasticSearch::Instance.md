# ALIYUN::ElasticSearch::Instance

ALIYUN::ElasticSearch::Instance is used to create an Elasticsearch cluster.

**Note:** An Elasticsearch cluster requires about 1 hour to be created and 0.5 to 3 hours to be updated. We recommend that you set the timeout period to 300 minutes for the stack creation request.

## Syntax

```
{
  "Type": "ALIYUN::ElasticSearch::Instance",
  "Properties": {
    "KibanaWhitelist": List,
    "PublicWhitelist": List,
    "VSwitchId": String,
    "InstanceChargeType": String,
    "Period": Integer,
    "Version": String,
    "DataNode": Map,
    "PrivateWhitelist": List,
    "ResourceGroupId": String,
    "EnablePublic": Boolean,
    "Password": String,
    "MasterNode": Map,
    "Tags": List,
    "Description": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|KibanaWhitelist|List|No|Yes|The whitelist of IP addresses that can access Kibana.|None|
|PublicWhitelist|List|No|Yes|The whitelist of public IP addresses that can access the Elasticsearch cluster.|None|
|VSwitchId|String|Yes|No|The vSwitch ID of the cluster.|None|
|InstanceChargeType|String|No|No|The billing method of the Elasticsearch cluster.|Valid values: -   PrePaid: subscription
-   PostPaid: pay-as-you-go |
|Period|Integer|No|No|The subscription period of the Elasticsearch cluster.|Default value: 1. Valid values:-   1
-   2
-   3
-   4
-   5
-   6
-   7
-   8
-   9
-   12
-   24
-   36

Unit: months. |
|Version|String|Yes|No|The version of the Elasticsearch cluster.|Value values: -   5.5.3\_with\_X-Pack
-   6.3\_with\_X-Pack
-   6.7\_with\_X-Pack |
|ResourceGroupId|String|No|Yes|The ID of the resource group.|None|
|EnablePublic|Boolean|No|Yes|Specifies whether to enable the public network access feature for the Elasticsearch cluster.|Valid values:-   true
-   false |
|DataNode|Map|Yes|Yes|The data node configurations of the Elasticsearch cluster.|For more information, see [DataNode properties](#section_427_fa1_6fy).|
|PrivateWhitelist|List|No|Yes|The whitelist of IP addresses that can access the Elasticsearch cluster in a VPC.|None|
|Password|String|Yes|Yes|The password of the Elasticsearch cluster.|The password must be 8 to 32 characters in length and must contain at least three of the following character types: uppercase letters, lowercase letters, digits, and special characters. Special characters include `! @ # $ % & * ( ) _ + - =`|
|MasterNode|Map|No|Yes|The primary node configurations of the Elasticsearch cluster.|If this parameter is specified, one or more dedicated primary nodes are created. For more information, see [MasterNode properties](#section_hk7_njb_52o). |
|Tags|List|No|Yes|The tags of the Elasticsearch cluster.|A maximum of 20 tags can be specified. For more information, see [Tags properties](#section_y4s_brf_qh3). |
|Description|String|No|Yes|The description of the Elasticsearch cluster.|The description must be 0 to 30 characters in length and can contain letters, digits, underscores \(\_\), and hyphens \(-\). It must start with a digit or letter.|

## DataNode syntax

```
"DataNode": {
  "Amount": Integer,
  "DiskSize": Integer,
  "Spec": String,
  "DiskType": String
}
```

## DataNode properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Amount|Integer|Yes|Yes|The number of data nodes in the Elasticsearch cluster.|Valid values: 2 to 50.|
|DiskSize|Integer|Yes|Yes|The disk size of the data node.|Value values: -   Maximum value when DiskType is set to cloud\_ssd: 2048. This value is equivalent to 2 TB.
-   Maximum value when DiskType is set to cloud\_efficiency: 5120. This value is equivalent to 5 TB. Valid values when DiskType is set to cloud\_efficiency and the size of data to be stored is greater than 2,048 GiB:
    -   2560GiB
    -   3072GiB
    -   3584GiB
    -   4096GiB
    -   4608GiB
    -   5120GiB

Unit: GiB. |
|Spec|String|Yes|Yes|The specifications of the data node of the Elasticsearch cluster.|None|
|DiskType|String|Yes|Yes|The disk type of the data node.|Valid values: -   cloud\_ssd
-   cloud\_efficiency |

## MasterNode syntax

```
"MasterNode": {
  "Amount": Integer,
  "DiskSize": Integer,
  "Spec": String,
  "DiskType": String
}
```

## MasterNode properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Amount|Integer|No|Yes|The number of primary nodes.|Default value: 3.|
|DiskSize|Integer|No|No|The disk size of the primary node.|Default value: 20.|
|Spec|String|Yes|No|The specifications of the primary node.|None|
|DiskType|String|No|No|The disk type of the primary node.|None|

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
|Key|String|Yes|No|The key of the tag.|The tag key must be 1 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|
|Value|String|No|No|The value of the tag.|The tag value must be 0 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|

## Response parameters

Fn::GetAtt

-   Status: the status of the Elasticsearch cluster.
-   KibanaDomain: the Kibana IP address of the Elasticsearch cluster.
-   PublicDomain: the public IP address of the Elasticsearch cluster.
-   Domain: the internal IP address of the Elasticsearch cluster.
-   InstanceId: the ID of the Elasticsearch cluster.
-   KibanaPort: the port number that is used to connect to the Kibana console.
-   Port: the port number that is used to connect to the Elasticsearch cluster.
-   VSwitchId: the vSwitch ID of the Elasticsearch cluster.
-   Version: the version of the Elasticsearch cluster.
-   InstanceChargeType: the billing method of the Elasticsearch cluster.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "MasterNode": {
      "Type": "Json",
      "Description": "The dedicated master node setting. If specified, dedicated master node will be created."
    },
    "Description": {
      "Type": "String",
      "Description": "The description of instance. It a string of 0 to 30 characters. It can contain numbers, letters, underscores, (_) and hyphens (-). It must start with a letter, a number or Chinese character.",
      "MaxLength": 30
    },
    "ResourceGroupId": {
      "Type": "String",
      "Description": "The ID of the resource group."
    },
    "PublicWhitelist": {
      "Type": "CommaDelimitedList",
      "Description": "Set the instance's IP whitelist in Internet. The AllocatePublicAddress should be true."
    },
    "InstanceChargeType": {
      "Type": "String",
      "Description": "Valid values are PrePaid, PostPaid, Default to PostPaid.",
      "AllowedValues": [
        "Subscription",
        "PrePaid",
        "PrePay",
        "Prepaid",
        "PayAsYouGo",
        "PostPaid",
        "PayOnDemand",
        "Postpaid"
      ],
      "Default": "PostPaid"
    },
    "VSwitchId": {
      "Type": "String",
      "Description": "The ID of VSwitch."
    },
    "Period": {
      "Type": "Number",
      "Description": "The duration that you will buy Elasticsearch instance (in month). It is valid when instance_charge_type is PrePaid. Valid values: [1~9], 12, 24, 36. Default to 1.",
      "AllowedValues": [
        1,
        2,
        3,
        4,
        5,
        6,
        7,
        8,
        9,
        12,
        24,
        36
      ],
      "Default": 1
    },
    "EnablePublic": {
      "Type": "Boolean",
      "Description": "Whether enable public access. If properties is true, will allocate public address.Default: false.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "PrivateWhitelist": {
      "Type": "CommaDelimitedList",
      "Description": "Set the instance's IP whitelist in VPC network."
    },
    "Version": {
      "Type": "String",
      "Description": "Elasticsearch version. Supported values: 5.5.3_with_X-Pack, 6.3_with_X-Pack, 6.7_with_X-Pack, 7.4_with_X-Pack, 6.8, 7.4, 7.7 and so on."
    },
    "DataNode": {
      "Type": "Json",
      "Description": "The Elasticsearch cluster's data node setting."
    },
    "KibanaWhitelist": {
      "Type": "CommaDelimitedList",
      "Description": "Set the Kibana's IP whitelist in internet network."
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to instance. Max support 20 tags to add during create instance. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
    },
    "Password": {
      "Type": "String",
      "Description": "The password of the instance. The password can be 8 to 32 characters in length and must contain three of the following conditions: uppercase letters, lowercase letters, numbers, and special characters (!@#$%&*()_+-=)."
    }
  },
  "Resources": {
    "Instance": {
      "Type": "ALIYUN::ElasticSearch::Instance",
      "Properties": {
        "MasterNode": {
          "Ref": "MasterNode"
        },
        "Description": {
          "Ref": "Description"
        },
        "ResourceGroupId": {
          "Ref": "ResourceGroupId"
        },
        "PublicWhitelist": {
          "Ref": "PublicWhitelist"
        },
        "InstanceChargeType": {
          "Ref": "InstanceChargeType"
        },
        "VSwitchId": {
          "Ref": "VSwitchId"
        },
        "Period": {
          "Ref": "Period"
        },
        "EnablePublic": {
          "Ref": "EnablePublic"
        },
        "PrivateWhitelist": {
          "Ref": "PrivateWhitelist"
        },
        "Version": {
          "Ref": "Version"
        },
        "DataNode": {
          "Ref": "DataNode"
        },
        "KibanaWhitelist": {
          "Ref": "KibanaWhitelist"
        },
        "Tags": {
          "Ref": "Tags"
        },
        "Password": {
          "Ref": "Password"
        }
      }
    }
  },
  "Outputs": {
    "Status": {
      "Description": "The Elasticsearch instance status. Includes active, activating, inactive. Some operations are denied when status is not active.",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "Status"
        ]
      }
    },
    "InstanceId": {
      "Description": "The ID of the Elasticsearch instance.",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "InstanceId"
        ]
      }
    },
    "Version": {
      "Description": "Elasticsearch version.",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "Version"
        ]
      }
    },
    "InstanceChargeType": {
      "Description": "Instance charge type.",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "InstanceChargeType"
        ]
      }
    },
    "KibanaPort": {
      "Description": "Kibana console port.",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "KibanaPort"
        ]
      }
    },
    "VSwitchId": {
      "Description": "The ID of VSwitch.",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "VSwitchId"
        ]
      }
    },
    "Port": {
      "Description": " Instance connection port.",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "Port"
        ]
      }
    },
    "Domain": {
      "Description": "Instance connection domain (only VPC network access supported).",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "Domain"
        ]
      }
    },
    "KibanaDomain": {
      "Description": "Kibana console domain (Internet access supported).",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "KibanaDomain"
        ]
      }
    },
    "PublicDomain": {
      "Description": "Instance public connection domain.",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "PublicDomain"
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
  DataNode:
    Description: The Elasticsearch cluster's data node setting.
    Type: Json
  Description:
    Description: The description of instance. It a string of 0 to 30 characters. It
      can contain numbers, letters, underscores, (_) and hyphens (-). It must start
      with a letter, a number or Chinese character.
    MaxLength: 30
    Type: String
  EnablePublic:
    AllowedValues:
    - 'True'
    - 'true'
    - 'False'
    - 'false'
    Description: 'Whether enable public access. If properties is true, will allocate
      public address.Default: false.'
    Type: Boolean
  InstanceChargeType:
    AllowedValues:
    - Subscription
    - PrePaid
    - PrePay
    - Prepaid
    - PayAsYouGo
    - PostPaid
    - PayOnDemand
    - Postpaid
    Default: PostPaid
    Description: Valid values are PrePaid, PostPaid, Default to PostPaid.
    Type: String
  KibanaWhitelist:
    Description: Set the Kibana's IP whitelist in internet network.
    Type: CommaDelimitedList
  MasterNode:
    Description: The dedicated master node setting. If specified, dedicated master
      node will be created.
    Type: Json
  Password:
    Description: 'The password of the instance. The password can be 8 to 32 characters
      in length and must contain three of the following conditions: uppercase letters,
      lowercase letters, numbers, and special characters (!@#$%&*()_+-=).'
    Type: String
  Period:
    AllowedValues:
    - 1
    - 2
    - 3
    - 4
    - 5
    - 6
    - 7
    - 8
    - 9
    - 12
    - 24
    - 36
    Default: 1
    Description: 'The duration that you will buy Elasticsearch instance (in month).
      It is valid when instance_charge_type is PrePaid. Valid values: [1~9], 12, 24,
      36. Default to 1.'
    Type: Number
  PrivateWhitelist:
    Description: Set the instance's IP whitelist in VPC network.
    Type: CommaDelimitedList
  PublicWhitelist:
    Description: Set the instance's IP whitelist in Internet. The AllocatePublicAddress
      should be true.
    Type: CommaDelimitedList
  ResourceGroupId:
    Description: The ID of the resource group.
    Type: String
  Tags:
    Description: Tags to attach to instance. Max support 20 tags to add during create
      instance. Each tag with two properties Key and Value, and Key is required.
    MaxLength: 20
    Type: Json
  VSwitchId:
    Description: The ID of VSwitch.
    Type: String
  Version:
    Description: 'Elasticsearch version. Supported values: 5.5.3_with_X-Pack, 6.3_with_X-Pack,
      6.7_with_X-Pack, 7.4_with_X-Pack, 6.8, 7.4, 7.7 and so on.'
    Type: String
Resources:
  Instance:
    Properties:
      DataNode:
        Ref: DataNode
      Description:
        Ref: Description
      EnablePublic:
        Ref: EnablePublic
      InstanceChargeType:
        Ref: InstanceChargeType
      KibanaWhitelist:
        Ref: KibanaWhitelist
      MasterNode:
        Ref: MasterNode
      Password:
        Ref: Password
      Period:
        Ref: Period
      PrivateWhitelist:
        Ref: PrivateWhitelist
      PublicWhitelist:
        Ref: PublicWhitelist
      ResourceGroupId:
        Ref: ResourceGroupId
      Tags:
        Ref: Tags
      VSwitchId:
        Ref: VSwitchId
      Version:
        Ref: Version
    Type: ALIYUN::ElasticSearch::Instance
Outputs:
  Domain:
    Description: Instance connection domain (only VPC network access supported).
    Value:
      Fn::GetAtt:
      - Instance
      - Domain
  InstanceChargeType:
    Description: Instance charge type.
    Value:
      Fn::GetAtt:
      - Instance
      - InstanceChargeType
  InstanceId:
    Description: The ID of the Elasticsearch instance.
    Value:
      Fn::GetAtt:
      - Instance
      - InstanceId
  KibanaDomain:
    Description: Kibana console domain (Internet access supported).
    Value:
      Fn::GetAtt:
      - Instance
      - KibanaDomain
  KibanaPort:
    Description: Kibana console port.
    Value:
      Fn::GetAtt:
      - Instance
      - KibanaPort
  Port:
    Description: ' Instance connection port.'
    Value:
      Fn::GetAtt:
      - Instance
      - Port
  PublicDomain:
    Description: Instance public connection domain.
    Value:
      Fn::GetAtt:
      - Instance
      - PublicDomain
  Status:
    Description: The Elasticsearch instance status. Includes active, activating, inactive.
      Some operations are denied when status is not active.
    Value:
      Fn::GetAtt:
      - Instance
      - Status
  VSwitchId:
    Description: The ID of VSwitch.
    Value:
      Fn::GetAtt:
      - Instance
      - VSwitchId
  Version:
    Description: Elasticsearch version.
    Value:
      Fn::GetAtt:
      - Instance
      - Version
```

For more examples, see [Instance.json](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ElasticSearch/JSON/Instance.json) and [Instance.yml](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ElasticSearch/YAML/Instance.yml).

