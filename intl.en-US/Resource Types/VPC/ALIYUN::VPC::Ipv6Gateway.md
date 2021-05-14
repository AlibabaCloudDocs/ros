# ALIYUN::VPC::Ipv6Gateway

ALIYUN::VPC::Ipv6Gateway is used to create an IPv6 gateway.

## Syntax

```
{
  "Type": "ALIYUN::VPC::Ipv6Gateway",
  "Properties": {
    "Description": String,
    "VpcId": String,
    "Spec": String,
    "Name": String,
    "Tags": List
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Description|String|No|Yes|The description of the IPv6 gateway.|The description must be 2 to 256 characters in length and can contain letters, digits, periods \(.\), underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with `http://` or `https://`.|
|VpcId|String|Yes|No|The ID of the virtual private cloud \(VPC\) for which you want to create the IPv6 gateway.|None|
|Spec|String|No|Yes|The specification of the IPv6 gateway.|Default value: Small. Valid values: -   Small: Free Edition
-   Medium: Enterprise Edition
-   Large: Enhanced Enterprise Edition |
|Name|String|No|Yes|The name of the IPv6 gateway.|The name must be 2 to 256 characters in length and can contain letters, digits, periods \(.\), underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with `http://` or `https://`.|
|Tags|List|No|Yes|The tags of the IPv6 gateway.|A maximum of 20 tags can be specified. For more information, see the [Tags properties](#section_og8_l1v_z8f) section in this topic. |

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

## Response parameters

Fn::GetAtt

Ipv6GatewayId: the ID of the IPv6 gateway.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Description": {
      "Type": "String",
      "Description": "Description of IPv6 gateway.\nLength of 2 to 256 characters, must begin with a letter or Chinese, may contain numbers, numbers, underscore (_) and dot dash (-), but not at the http (.): // or https: // at the beginning ."
    },
    "VpcId": {
      "Type": "String",
      "Description": "To open VPC ID IPv6 gateway."
    },
    "Spec": {
      "Type": "String",
      "Description": "Specifications IPv6 gateway, the value:\nSmall (default): Free.\nMedium: Enterprise Edition.\nLarge: Enterprise Enhanced Edition.\nDifferent specifications of the IPv6 forwarding capability of the gateway is different. For more information, see IPv6 gateway specification."
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to instance. Max support 20 tags to add during create instance. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
    },
    "Name": {
      "Type": "String",
      "Description": "Name of the IPv6 gateway.\nLength of 2 to 128 characters, beginning with a letter or Chinese, can contain numbers, dot, underscore (_) and dash (-), but not at http (.): // or with https: // ."
    }
  },
  "Resources": {
    "Ipv6Gateway": {
      "Type": "ALIYUN::VPC::Ipv6Gateway",
      "Properties": {
        "Description": {
          "Ref": "Description"
        },
        "VpcId": {
          "Ref": "VpcId"
        },
        "Spec": {
          "Ref": "Spec"
        },
        "Tags": {
          "Ref": "Tags"
        },
        "Name": {
          "Ref": "Name"
        }
      }
    }
  },
  "Outputs": {
    "Ipv6GatewayId": {
      "Description": "ID IPv6 gateway.",
      "Value": {
        "Fn::GetAtt": [
          "Ipv6Gateway",
          "Ipv6GatewayId"
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
  Description:
    Description: 'Description of IPv6 gateway.

      Length of 2 to 256 characters, must begin with a letter or Chinese, may contain
      numbers, numbers, underscore (_) and dot dash (-), but not at the http (.):
      // or https: // at the beginning .'
    Type: String
  Name:
    Description: 'Name of the IPv6 gateway.

      Length of 2 to 128 characters, beginning with a letter or Chinese, can contain
      numbers, dot, underscore (_) and dash (-), but not at http (.): // or with https:
      // .'
    Type: String
  Spec:
    Description: 'Specifications IPv6 gateway, the value:

      Small (default): Free.

      Medium: Enterprise Edition.

      Large: Enterprise Enhanced Edition.

      Different specifications of the IPv6 forwarding capability of the gateway is
      different. For more information, see IPv6 gateway specification.'
    Type: String
  Tags:
    Description: Tags to attach to instance. Max support 20 tags to add during create
      instance. Each tag with two properties Key and Value, and Key is required.
    MaxLength: 20
    Type: Json
  VpcId:
    Description: To open VPC ID IPv6 gateway.
    Type: String
Resources:
  Ipv6Gateway:
    Properties:
      Description:
        Ref: Description
      Name:
        Ref: Name
      Spec:
        Ref: Spec
      Tags:
        Ref: Tags
      VpcId:
        Ref: VpcId
    Type: ALIYUN::VPC::Ipv6Gateway
Outputs:
  Ipv6GatewayId:
    Description: ID IPv6 gateway.
    Value:
      Fn::GetAtt:
      - Ipv6Gateway
      - Ipv6GatewayId
```

For more examples, visit [SnatEntry.json](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/VPC/JSON/SnatEntry.json) and [SnatEntry.yml](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/VPC/YAML/SnatEntry.yml). In the examples, the ALIYUN::ECS::VPC, ALIYUN::ECS::VSwitch, ALIYUN::VPC::SnatEntry, ALIYUN::VPC::CommonBandwidthPackage, ALIYUN::VPC::CommonBandwidthPackageIp, ALIYUN::VPC::Ipv6Gateway, and ALIYUN::VPC::Ipv6InternetBandwidth resource types are involved.

