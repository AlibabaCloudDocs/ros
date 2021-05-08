# ALIYUN::PrivateLink::VpcEndpoint

ALIYUN::PrivateLink::VpcEndpoint类型用于创建终端节点。

## 语法

```
{
  "Type": "ALIYUN::PrivateLink::VpcEndpoint",
  "Properties": {
    "VpcId": String,
    "EndpointName": String,
    "ServiceName": String,
    "Zone": List,
    "SecurityGroupId": List,
    "EndpointDescription": String,
    "ServiceId": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|VpcId|String|是|否|终端节点所属的专有网络ID。|无|
|EndpointName|String|否|是|终端节点名称。|长度为2~128个字符，以英文字母或汉字开头。可包含英文字母、汉字、数字、短划线（-）和下划线（\_）。|
|ServiceName|String|否|否|终端节点关联的终端节点服务名称。|无|
|Zone|List|否|是|可用区。|最多支持10个可用区。更多信息，请参见[Zone属性](#section_kxm_hm7_qju)。 |
|SecurityGroupId|List|是|是|终端节点网卡关联的安全组ID，安全组可以管控专有网络到终端节点网卡的数据通信。|最多支持关联10个安全组。|
|EndpointDescription|String|否|是|终端节点描述。|长度为2~256个字符，不能以`http://`或`https://`开头。|
|ServiceId|String|否|否|终端节点关联的终端节点服务ID。|无|

## Zone语法

```
"Zone": [
  {
    "ZoneId": String,
    "VSwitchId": String
  }
]
```

## Zone属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ZoneId|String|是|否|终端节点服务对应的可用区ID。|无|
|VSwitchId|String|是|否|在可用区内，需要创建终端节点网卡的交换机ID。|无|

## 返回值

Fn::GetAtt

-   EndpointDomain：终端节点域名。
-   Bandwidth：终端节点的连接带宽。
-   EndpointId：终端节点ID。
-   EndpointName：终端节点名称。
-   VpcId：终端节点所属的专有网络ID。
-   ServiceName：终端节点关联的终端节点服务名称。
-   ServiceId：终端节点关联的终端节点服务ID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "VpcId": {
      "Type": "String",
      "Description": "The VPC to which the endpoint belongs."
    },
    "EndpointName": {
      "Type": "String",
      "Description": "The name of the endpoint.\nThe name must be 2 to 128 characters in length and can contain digits, underscores\n(_), and hyphens (-). The name must start with a letter.",
      "MinLength": 2,
      "MaxLength": 128
    },
    "ServiceName": {
      "Type": "String",
      "Description": "The name of the endpoint service that is associated with the endpoint. One of ServiceId and ServiceName is required."
    },
    "Zone": {
      "Type": "Json",
      "Description": "",
      "MinLength": 1,
      "MaxLength": 10
    },
    "SecurityGroupId": {
      "Type": "Json",
      "Description": "The security group associated with the endpoint network interface. The security group can control the data communication from the VPC to the endpoint network interface.",
      "MinLength": 1,
      "MaxLength": 10
    },
    "EndpointDescription": {
      "Type": "String",
      "Description": "The description of the endpoint.\nThe description must be 2 to 256 characters in length and cannot start with http:// or https://.",
      "MinLength": 2,
      "MaxLength": 256
    },
    "ServiceId": {
      "Type": "String",
      "Description": "The endpoint service that is associated with the endpoint. One of ServiceId and ServiceName is required."
    }
  },
  "Resources": {
    "VpcEndpoint": {
      "Type": "ALIYUN::PrivateLink::VpcEndpoint",
      "Properties": {
        "VpcId": {
          "Ref": "VpcId"
        },
        "EndpointName": {
          "Ref": "EndpointName"
        },
        "ServiceName": {
          "Ref": "ServiceName"
        },
        "Zone": {
          "Ref": "Zone"
        },
        "SecurityGroupId": {
          "Ref": "SecurityGroupId"
        },
        "EndpointDescription": {
          "Ref": "EndpointDescription"
        },
        "ServiceId": {
          "Ref": "ServiceId"
        }
      }
    }
  },
  "Outputs": {
    "VpcId": {
      "Description": "The vpc ID of endpoint.",
      "Value": {
        "Fn::GetAtt": [
          "VpcEndpoint",
          "VpcId"
        ]
      }
    },
    "EndpointDomain": {
      "Description": "The domain name of the endpoint.",
      "Value": {
        "Fn::GetAtt": [
          "VpcEndpoint",
          "EndpointDomain"
        ]
      }
    },
    "EndpointName": {
      "Description": "The name of the endpoint.",
      "Value": {
        "Fn::GetAtt": [
          "VpcEndpoint",
          "EndpointName"
        ]
      }
    },
    "ServiceName": {
      "Description": "The name of endpoint service that is associated with the endpoint.",
      "Value": {
        "Fn::GetAtt": [
          "VpcEndpoint",
          "ServiceName"
        ]
      }
    },
    "Bandwidth": {
      "Description": "The bandwidth of the endpoint.",
      "Value": {
        "Fn::GetAtt": [
          "VpcEndpoint",
          "Bandwidth"
        ]
      }
    },
    "EndpointId": {
      "Description": "The ID of the endpoint.",
      "Value": {
        "Fn::GetAtt": [
          "VpcEndpoint",
          "EndpointId"
        ]
      }
    },
    "ServiceId": {
      "Description": "The ID of endpoint service that is associated with the endpoint.",
      "Value": {
        "Fn::GetAtt": [
          "VpcEndpoint",
          "ServiceId"
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
  EndpointDescription:
    Description: 'The description of the endpoint.

      The description must be 2 to 256 characters in length and cannot start with
      http:// or https://.'
    MaxLength: 256
    MinLength: 2
    Type: String
  EndpointName:
    Description: 'The name of the endpoint.

      The name must be 2 to 128 characters in length and can contain digits, underscores

      (_), and hyphens (-). The name must start with a letter.'
    MaxLength: 128
    MinLength: 2
    Type: String
  SecurityGroupId:
    Description: The security group associated with the endpoint network interface.
      The security group can control the data communication from the VPC to the endpoint
      network interface.
    MaxLength: 10
    MinLength: 1
    Type: Json
  ServiceId:
    Description: The endpoint service that is associated with the endpoint. One of
      ServiceId and ServiceName is required.
    Type: String
  ServiceName:
    Description: The name of the endpoint service that is associated with the endpoint.
      One of ServiceId and ServiceName is required.
    Type: String
  VpcId:
    Description: The VPC to which the endpoint belongs.
    Type: String
  Zone:
    Description: ''
    MaxLength: 10
    MinLength: 1
    Type: Json
Resources:
  VpcEndpoint:
    Properties:
      EndpointDescription:
        Ref: EndpointDescription
      EndpointName:
        Ref: EndpointName
      SecurityGroupId:
        Ref: SecurityGroupId
      ServiceId:
        Ref: ServiceId
      ServiceName:
        Ref: ServiceName
      VpcId:
        Ref: VpcId
      Zone:
        Ref: Zone
    Type: ALIYUN::PrivateLink::VpcEndpoint
Outputs:
  Bandwidth:
    Description: The bandwidth of the endpoint.
    Value:
      Fn::GetAtt:
      - VpcEndpoint
      - Bandwidth
  EndpointDomain:
    Description: The domain name of the endpoint.
    Value:
      Fn::GetAtt:
      - VpcEndpoint
      - EndpointDomain
  EndpointId:
    Description: The ID of the endpoint.
    Value:
      Fn::GetAtt:
      - VpcEndpoint
      - EndpointId
  EndpointName:
    Description: The name of the endpoint.
    Value:
      Fn::GetAtt:
      - VpcEndpoint
      - EndpointName
  ServiceId:
    Description: The ID of endpoint service that is associated with the endpoint.
    Value:
      Fn::GetAtt:
      - VpcEndpoint
      - ServiceId
  ServiceName:
    Description: The name of endpoint service that is associated with the endpoint.
    Value:
      Fn::GetAtt:
      - VpcEndpoint
      - ServiceName
  VpcId:
    Description: The vpc ID of endpoint.
    Value:
      Fn::GetAtt:
      - VpcEndpoint
      - VpcId
```

