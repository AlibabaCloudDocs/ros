# ALIYUN::ElasticSearch::Instance

ALIYUN::ElasticSearch::Instance类型用于创建ElasticSearch实例。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|KibanaWhitelist|List|否|是|设置Kibana的IP白名单。|无|
|PublicWhitelist|List|否|是|设置实例的公网IP白名单。|无|
|VSwitchId|String|是|否|虚拟交换机ID。|无|
|InstanceChargeType|String|否|否|实例付费类型。|取值： -   PrePaid：预付费。
-   PostPaid：后付费。 |
|Period|Integer|否|否|购买Elasticsearch实例的持续时间。|取值：-   1（默认值）
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

单位：月。 |
|Version|String|是|否|Elasticsearch版本。|取值： -   5.5.3\_with\_X-Pack
-   6.3\_with\_X-Pack
-   6.7\_with\_X-Pack |
|DataNode|Map|是|是|Elasticsearch集群的数据节点设置。|详情请参见[DataNode属性](#section_427_fa1_6fy)。|
|PrivateWhitelist|List|否|是|在专有网络中设置实例的IP白名单。|无|
|Password|String|是|是|实例的密码。|长度为8~32个字符，必须同时包含大写英文字母、小写英文字母、数字和特殊字符中的三项。 支持的特殊字符如下：```
!@#$%&*()_+-=
``` |
|MasterNode|Map|否|是|主节点设置。|如果指定该参数，将创建专用主节点。详情请参见[MasterNode属性](#section_hk7_njb_52o)。 |
|Description|String|否|是|实例的描述。|长度为0~30个字符，必须以英文字母、数字或汉字开头，可包含英文字母、数字、汉字、下划线（\_）和短划线（-）。|

## DataNode语法

```
"DataNode": {
  "Amount": Integer,
  "DiskSize": Integer,
  "Spec": String,
  "DiskType": String
}
```

## DataNode属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Amount|Integer|是|是|Elasticsearch集群的数据节点数量。|取值范围：2~50。|
|DiskSize|Integer|是|是|单数据节点存储空间。|取值： -   cloud\_ssd：最多支持2048GiB（2TB）。
-   cloud\_efficiency：最多支持5120GiB（5TB）。如果要存储的数据大于2048GiB，cloud\_efficiency只能支持以下数据大小：
    -   2560GiB
    -   3072GiB
    -   3584GiB
    -   4096GiB
    -   4608GiB
    -   5120GiB

单位：GiB。 |
|Spec|String|是|是|Elasticsearch实例的数据节点规格。|无|
|DiskType|String|是|是|数据节点磁盘类型。|取值： -   cloud\_ssd
-   cloud\_efficiency |

## MasterNode语法

```
"MasterNode": {
  "Amount": Integer,
  "DiskSize": Integer,
  "Spec": String,
  "DiskType": String
}
```

## MasterNode属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Amount|Integer|否|是|主节点数量|默认值：3。|
|DiskSize|Integer|否|否|主节点存储空间|默认值：20。|
|Spec|String|是|否|主节点规格|无|
|DiskType|String|否|否|主节点磁盘类型|无|

## 返回值

Fn::GetAtt

-   Status：Elasticsearch实例状态。包括active、activating、inactive。有些操作在状态不活跃时会被拒绝。
-   KibanaDomain：Kibana控制台域名（支持Internet访问）。
-   Domain：实例连接域名（仅支持专有网络访问）。
-   InstanceId：Elasticsearch实例的ID。
-   KibanaPort：Kibana控制端口。
-   Port：实例连接端口。

## 示例

`JSON`格式

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

`YAML`格式

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
      (!@#$%&*()_+-=).
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

