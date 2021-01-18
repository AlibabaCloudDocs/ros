# ALIYUN::ElasticSearch::Instance

ALIYUN::ElasticSearch::Instance is used to create an Elasticsearch cluster.

**Note:** It takes nearly 1 hour to create an ElasticSearch cluster, and 0.5 to 3 hours to update an ElasticSearch cluster. We recommend that you set the timeout period to 300 minutes for the stack creation request.

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
    "Password": String,
    "MasterNode": Map,
    "Description": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|KibanaWhitelist|List|No|Yes|The whitelist of IP addresses that can access Kibana.|None|
|PublicWhitelist|List|No|Yes|The whitelist of public IP addresses that can access the Elasticsearch cluster.|None|
|VSwitchId|String|Yes|No|The ID of the vSwitch.|None|
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
|Version|String|Yes|No|The version of the Elasticsearch cluster.|Valid values: -   5.5.3\_with\_X-Pack
-   6.3\_with\_X-Pack
-   6.7\_with\_X-Pack |
|DataNode|Map|Yes|Yes|The data node configurations of the Elasticsearch cluster.|For more information, see [DataNode properties](#section_427_fa1_6fy).|
|PrivateWhitelist|List|No|Yes|The whitelist of IP addresses that can access the Elasticsearch cluster in a VPC.|None|
|Password|String|Yes|Yes|The password of the Elasticsearch cluster.|The password must be 8 to 32 characters in length and must contain at least three of the following character types: uppercase letters, lowercase letters, digits, and special characters. Special characters include `! @ # $ % & * ( ) _ + - =`|
|MasterNode|Map|No|Yes|The primary node configurations of the Elasticsearch cluster.|If this parameter is specified, one or more dedicated primary nodes are created.For more information, see [MasterNode properties](#section_hk7_njb_52o). |
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
|DiskSize|Integer|Yes|Yes|The disk size of the data node.|Valid values: -   Maximum value when DiskType is set to cloud\_ssd: 2048. This value is equivalent to 2 TB.
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
|Amount|Integer|No|Yes|The number of dedicated primary nodes.|Default value: 3.|
|DiskSize|Integer|No|No|The disk size of the dedicated primary node.|Default value: 20.|
|Spec|String|Yes|No|The specifications of the dedicated primary node.|None|
|DiskType|String|No|No|The disk type of the dedicated primary node.|None|

## Response parameters

Fn::GetAtt

-   Status: the status of the Elasticsearch cluster, which can be active, activating, or inactive. Some requests may be denied if the Elasticsearch cluster is in the inactive state.
-   KibanaDomain: the domain name of the Kibana console. Access from the Internet is supported.
-   Domain: the domain name that is used to connect to the Elasticsearch cluster. Only access from VPCs is supported.
-   InstanceId: the ID of the Elasticsearch cluster.
-   KibanaPort: the port that is used to connect to the Kibana console.
-   Port: the port that is used to connect to the Elasticsearch cluster.

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
    "PrivateWhitelist": {
      "Type": "CommaDelimitedList",
      "Description": "Set the instance's IP whitelist in VPC network."
    },
    "PublicWhitelist": {
      "Type": "CommaDelimitedList",
      "Description": "Set the instance's IP whitelist in Internet."
    },
    "Version": {
      "Type": "String",
      "Description": "Elasticsearch version. Supported values: 5.5.3_with_X-Pack, 6.3_with_X-Pack, 6.7_with_X-Pack, 7.4_with_X-Pack, 6.8, 7.4, 7.7 and so on."
    },
    "InstanceChargeType": {
      "Type": "String",
      "Description": "Valid values are PrePaid, PostPaid, Default to PostPaid.",
      "AllowedValues": [
        "PrePaid",
        "PostPaid"
      ],
      "Default": "PostPaid"
    },
    "DataNode": {
      "Type": "Json",
      "Description": "The Elasticsearch cluster's data node setting."
    },
    "VSwitchId": {
      "Type": "String",
      "Description": "The ID of VSwitch."
    },
    "KibanaWhitelist": {
      "Type": "CommaDelimitedList",
      "Description": "Set the Kibana's IP whitelist in internet network."
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
    "Password": {
      "Type": "String",
      "Description": "The password of the instance. The password can be 8 to 32 characters in length and must contain three of the following conditions: uppercase letters, lowercase letters, numbers, and special characters (! @#$%&*()_+-=)."
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
        "PrivateWhitelist": {
          "Ref": "PrivateWhitelist"
        },
        "PublicWhitelist": {
          "Ref": "PublicWhitelist"
        },
        "Version": {
          "Ref": "Version"
        },
        "InstanceChargeType": {
          "Ref": "InstanceChargeType"
        },
        "DataNode": {
          "Ref": "DataNode"
        },
        "VSwitchId": {
          "Ref": "VSwitchId"
        },
        "KibanaWhitelist": {
          "Ref": "KibanaWhitelist"
        },
        "Period": {
          "Ref": "Period"
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
    "KibanaPort": {
      "Description": "Kibana console port.",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "KibanaPort"
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
    }
  }
}
```

`YAML` format

```
ROSTemplateFormatVersion: '2015-09-01'
Parameters:
  MasterNode:
    Type: Json
    Description: >-
      The dedicated master node setting. If specified, dedicated master node
      will be created.
  Description:
    Type: String
    Description: >-
      The description of instance. It a string of 0 to 30 characters. It can
      contain numbers, letters, underscores, (_) and hyphens (-). It must start
      with a letter, a number or Chinese character.
    MaxLength: 30
  PrivateWhitelist:
    Type: CommaDelimitedList
    Description: Set the instance's IP whitelist in VPC network.
  PublicWhitelist:
    Type: CommaDelimitedList
    Description: Set the instance's IP whitelist in Internet.
  Version:
    Type: String
    Description: >-
      Elasticsearch version. Supported values: 5.5.3_with_X-Pack,
      6.3_with_X-Pack, 6.7_with_X-Pack, 7.4_with_X-Pack, 6.8, 7.4, 7.7 and so
      on.
  InstanceChargeType:
    Type: String
    Description: 'Valid values are PrePaid, PostPaid, Default to PostPaid.'
    AllowedValues:
      - PrePaid
      - PostPaid
    Default: PostPaid
  DataNode:
    Type: Json
    Description: The Elasticsearch cluster's data node setting.
  VSwitchId:
    Type: String
    Description: The ID of VSwitch.
  KibanaWhitelist:
    Type: CommaDelimitedList
    Description: Set the Kibana's IP whitelist in internet network.
  Period:
    Type: Number
    Description: >-
      The duration that you will buy Elasticsearch instance (in month). It is
      valid when instance_charge_type is PrePaid. Valid values: [1~9], 12, 24,
      36. Default to 1.
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
  Password:
    Type: String
    Description: >-
      The password of the instance. The password can be 8 to 32 characters in
      length and must contain three of the following conditions: uppercase
      letters, lowercase letters, numbers, and special characters
      (! @#$%&*()_+-=).
Resources:
  Instance:
    Type: 'ALIYUN::ElasticSearch::Instance'
    Properties:
      MasterNode:
        Ref: MasterNode
      Description:
        Ref: Description
      PrivateWhitelist:
        Ref: PrivateWhitelist
      PublicWhitelist:
        Ref: PublicWhitelist
      Version:
        Ref: Version
      InstanceChargeType:
        Ref: InstanceChargeType
      DataNode:
        Ref: DataNode
      VSwitchId:
        Ref: VSwitchId
      KibanaWhitelist:
        Ref: KibanaWhitelist
      Period:
        Ref: Period
      Password:
        Ref: Password
Outputs:
  Status:
    Description: >-
      The Elasticsearch instance status. Includes active, activating, inactive.
      Some operations are denied when status is not active.
    Value:
      'Fn::GetAtt':
        - Instance
        - Status
  InstanceId:
    Description: The ID of the Elasticsearch instance.
    Value:
      'Fn::GetAtt':
        - Instance
        - InstanceId
  KibanaPort:
    Description: Kibana console port.
    Value:
      'Fn::GetAtt':
        - Instance
        - KibanaPort
  Port:
    Description: ' Instance connection port.'
    Value:
      'Fn::GetAtt':
        - Instance
        - Port
  Domain:
    Description: Instance connection domain (only VPC network access supported).
    Value:
      'Fn::GetAtt':
        - Instance
        - Domain
  KibanaDomain:
    Description: Kibana console domain (Internet access supported).
    Value:
      'Fn::GetAtt':
        - Instance
        - KibanaDomain
            
```

