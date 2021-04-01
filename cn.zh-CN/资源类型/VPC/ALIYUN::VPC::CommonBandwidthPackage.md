# ALIYUN::VPC::CommonBandwidthPackage

ALIYUN::VPC::CommonBandwidthPackage类型用于创建共享带宽实例。

## 语法

```
{
  "Type": "ALIYUN::VPC::CommonBandwidthPackage",
  "Properties": {
    "Ratio": Integer,
    "Description": String,
    "Zone": String,
    "ISP": String,
    "ResourceGroupId": String,
    "Bandwidth": Integer,
    "InternetChargeType": String,
    "Name": String,
    "Tags": List
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Ratio|Integer|否|否|共享带宽的保底百分比。取值为20，即保底百分比的范围是20%。|当InternetChargeType取值为PayBy95时，需指定该参数。默认值：100。 |
|Description|String|否|是|共享带宽的描述信息。|长度为2~256个字符，必须以英文字母或汉字开头，但不能以`http://`或`https://`开头。|
|Zone|String|否|否|共享带宽的可用区。|不需要指定该参数。|
|ISP|String|否|否|EIP的线路类型。|取值：BGP（多线）。|
|ResourceGroupId|String|否|否|资源组ID。|无|
|Bandwidth|Integer|是|是|共享带宽的带宽峰值。|取值范围：2~5000。单位：Mbps。 |
|InternetChargeType|String|否|否|共享带宽的计费方式。|取值范围：-   PayByBandwidth（默认值）：按带宽计费。
-   PayBy95：按增强型95计费。 |
|Name|String|否|是|共享带宽的名称。|长度为2~128个字符。必须以英文字母或汉字开头，但不能以`http://`或`https://`开头。可包含英文字母、汉字、数字、半角句号（.）、下划线（\_）和短划线（-）。|
|Tags|List|否|是|标签。|最多支持添加20个标签。更多信息，请参见[Tags属性](#section_lkc_fkh_ji7)。 |

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

BandwidthPackageId：共享带宽实例的ID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Description": {
      "Type": "String",
      "Description": "The description of the Internet Shared Bandwidth instance.\nThe description must be 2 to 256 characters in length. It must start with a letter,\nand cannot start with http:// or https://.",
      "MinLength": 2,
      "MaxLength": 256
    },
    "ResourceGroupId": {
      "Type": "String",
      "Description": "The ID of the resource group."
    },
    "Zone": {
      "Type": "String",
      "Description": "Zone Id."
    },
    "ISP": {
      "Type": "String",
      "Description": "Line type of EIP, value: BGP (multi-line).",
      "Default": "BGP"
    },
    "Bandwidth": {
      "Type": "Number",
      "Description": "The peak bandwidth of the Internet Shared Bandwidth instance. Unit: Mbit/s.",
      "MinValue": 2
    },
    "Ratio": {
      "Type": "Number",
      "Description": "The minimum consumption ratio of the Internet Shared Bandwidth instance. Default to 100.\nNote This parameter is only supported on the China site.",
      "MinValue": 0,
      "MaxValue": 100,
      "Default": 100
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to instance. Max support 20 tags to add during create instance. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
    },
    "InternetChargeType": {
      "Type": "String",
      "Description": "The billing model of the Internet Shared Bandwidth instance. Allowed values:\nPayByBandwidth (default): Billed by bandwidth.\nPayBy95: Charged at Enhanced 95."
    },
    "Name": {
      "Type": "String",
      "Description": "The name of the Internet Shared Bandwidth instance.\nThe name must be 2 to 128 characters in length and can contain letters, numbers, periods\n(.), underscores (_), and hyphens (-). The name must start with a letter, and cannot\nstart with http:// or https://.",
      "MinLength": 2,
      "MaxLength": 128
    }
  },
  "Resources": {
    "CommonBandwidthPackage": {
      "Type": "ALIYUN::VPC::CommonBandwidthPackage",
      "Properties": {
        "Description": {
          "Ref": "Description"
        },
        "ResourceGroupId": {
          "Ref": "ResourceGroupId"
        },
        "Zone": {
          "Ref": "Zone"
        },
        "ISP": {
          "Ref": "ISP"
        },
        "Bandwidth": {
          "Ref": "Bandwidth"
        },
        "Ratio": {
          "Ref": "Ratio"
        },
        "Tags": {
          "Ref": "Tags"
        },
        "InternetChargeType": {
          "Ref": "InternetChargeType"
        },
        "Name": {
          "Ref": "Name"
        }
      }
    }
  },
  "Outputs": {
    "BandwidthPackageId": {
      "Description": "The ID of the Internet Shared Bandwidth instance.",
      "Value": {
        "Fn::GetAtt": [
          "CommonBandwidthPackage",
          "BandwidthPackageId"
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
  Bandwidth:
    Description: 'The peak bandwidth of the Internet Shared Bandwidth instance. Unit:
      Mbit/s.'
    MinValue: 2
    Type: Number
  Description:
    Description: 'The description of the Internet Shared Bandwidth instance.

      The description must be 2 to 256 characters in length. It must start with a
      letter,

      and cannot start with http:// or https://.'
    MaxLength: 256
    MinLength: 2
    Type: String
  ISP:
    Default: BGP
    Description: 'Line type of EIP, value: BGP (multi-line).'
    Type: String
  InternetChargeType:
    Description: 'The billing model of the Internet Shared Bandwidth instance. Allowed
      values:

      PayByBandwidth (default): Billed by bandwidth.

      PayBy95: Charged at Enhanced 95.'
    Type: String
  Name:
    Description: 'The name of the Internet Shared Bandwidth instance.

      The name must be 2 to 128 characters in length and can contain letters, numbers,
      periods

      (.), underscores (_), and hyphens (-). The name must start with a letter, and
      cannot

      start with http:// or https://.'
    MaxLength: 128
    MinLength: 2
    Type: String
  Ratio:
    Default: 100
    Description: 'The minimum consumption ratio of the Internet Shared Bandwidth instance.
      Default to 100.

      Note This parameter is only supported on the China site.'
    MaxValue: 100
    MinValue: 0
    Type: Number
  ResourceGroupId:
    Description: The ID of the resource group.
    Type: String
  Tags:
    Description: Tags to attach to instance. Max support 20 tags to add during create
      instance. Each tag with two properties Key and Value, and Key is required.
    MaxLength: 20
    Type: Json
  Zone:
    Description: Zone Id.
    Type: String
Resources:
  CommonBandwidthPackage:
    Properties:
      Bandwidth:
        Ref: Bandwidth
      Description:
        Ref: Description
      ISP:
        Ref: ISP
      InternetChargeType:
        Ref: InternetChargeType
      Name:
        Ref: Name
      Ratio:
        Ref: Ratio
      ResourceGroupId:
        Ref: ResourceGroupId
      Tags:
        Ref: Tags
      Zone:
        Ref: Zone
    Type: ALIYUN::VPC::CommonBandwidthPackage
Outputs:
  BandwidthPackageId:
    Description: The ID of the Internet Shared Bandwidth instance.
    Value:
      Fn::GetAtt:
      - CommonBandwidthPackage
      - BandwidthPackageId
```

更多示例，请参见创建专有网络、创建专有网络中的交换机、在SNAT列表中添加SNAT条目、创建共享带宽实例、添加EIP到共享带宽中、创建IPv6网关和为IPv6地址购买公网带宽的组合示例：[JSON示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/VPC/JSON/SnatEntry.json)和[YAML示例](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/VPC/YAML/SnatEntry.yml)。

