# ALIYUN::VPC::Ipv6Gateway

ALIYUN::VPC::Ipv6Gateway类型用于创建IPv6网关。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Description|String|否|是|IPv6网关的描述信息。|长度为2~256个字符。必须以英文字母或汉字开头，不能以`http://`或`https://`开头。可包含英文字母、汉字、数字、半角句号（.）、下划线（\_）和短划线（-）。|
|VpcId|String|是|否|要开通IPv6网关的专有网络ID。|无|
|Spec|String|否|是|IPv6网关的规格。|取值： -   Small（默认值）：免费版。
-   Medium：企业版。
-   Large：企业增强版。 |
|Name|String|否|是|IPv6网关的名称。|长度为2~256个字符。必须以英文字母或汉字开头，不能以`http://`或`https://`开头。可包含英文字母、汉字、数字、半角句号（.）、下划线（\_）和短划线（-）。|
|Tags|List|否|是|标签。|最多支持添加20个标签。更多信息，请参见[Tags属性](#section_og8_l1v_z8f)。 |

## Tags语法

```
"Tags": [
  {
    "Key": String,
    "Value": String
  }
]  
```

## Tags属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Key|String|是|否|标签键。|长度为1~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或者`https://` 。|
|Value|String|否|否|标签值。|长度为0~128个字符，不能以`aliyun`和`acs:`开头，不能包含`http://`或者`https://` 。|

## 返回值

Fn::GetAtt

Ipv6GatewayId：IPv6网关的ID。

## 示例

`JSON`格式

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

`YAML`格式

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

更多示例，请参见创建专有网络、创建专有网络中的交换机、在SNAT列表中添加SNAT条目、创建共享带宽实例、添加EIP到共享带宽中、创建IPv6网关和为IPv6地址购买公网带宽的组合示例：[JSON示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/VPC/JSON/SnatEntry.json)和[YAML示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/VPC/YAML/SnatEntry.yml)。

