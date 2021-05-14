# ALIYUN::VPC::CommonBandwidthPackage

ALIYUN::VPC::CommonBandwidthPackage is used to create an elastic IP \(EIP\) bandwidth plan.

## Syntax

```
{
  "Type": "ALIYUN::VPC::CommonBandwidthPackage",
  "Properties": {
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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Description|String|No|Yes|The description of the EIP bandwidth plan.|The description must be 2 to 256 characters in length. It must start with a letter and cannot start with `http://` or `https://`.|
|Zone|String|No|No|The zone where you want to create the EIP bandwidth plan.|You do not need to specify this parameter.|
|ISP|String|No|No|The line type of the EIP.|Set the value to BGP \(Multi-ISP\).|
|ResourceGroupId|String|No|No|The ID of the resource group.|None|
|Bandwidth|Integer|Yes|Yes|The maximum bandwidth of the EIP bandwidth plan.|Valid values: 2 to 5000. Unit: Mbit/s. |
|InternetChargeType|String|No|No|The billing method of the EIP bandwidth plan.|Default value: PayByBandwidth. Valid values:-   PayByBandwidth: You are charged for the EIP bandwidth plan based on the bandwidth.
-   PayBy95: You are charged for the EIP bandwidth plan by the enhanced 95th percentile billing method. |
|Name|String|No|Yes|The name of the EIP bandwidth plan.|The name must be 2 to 128 characters in length and can contain letters, digits, periods \(.\), underscores \(\_\), and hyphens \(-\). It must start with a letter but cannot start with `http://` or `https://`.|
|Tags|List|No|Yes|The tags of the EIP bandwidth plan.|A maximum of 20 tags can be specified. For more information, see the [Tags properties](#section_lkc_fkh_ji7) section in this topic. |

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

BandwidthPackageId: the ID of the EIP bandwidth plan.

## Examples

`JSON` format

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

`YAML` format

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

For more examples, visit [SnatEntry.json](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/VPC/JSON/SnatEntry.json) and [SnatEntry.yml](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/VPC/YAML/SnatEntry.yml). In the examples, the ALIYUN::ECS::VPC, ALIYUN::ECS::VSwitch, ALIYUN::VPC::SnatEntry, ALIYUN::VPC::CommonBandwidthPackage, ALIYUN::VPC::CommonBandwidthPackageIp, ALIYUN::VPC::Ipv6Gateway, and ALIYUN::VPC::Ipv6InternetBandwidth resource types are involved.

