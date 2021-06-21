# ALIYUN::VPC::EIPSegment

ALIYUN::VPC::EIP is used to apply for contiguous elastic IP addresses \(EIPs\).

## Syntax

```
{
  "Type": "ALIYUN::VPC::EIPSegment",
  "Properties": {
    "EipMask": Integer,
    "ResourceGroupId": String,
    "Netmode": String,
    "Bandwidth": Integer,
    "InternetChargeType": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|EipMask|Integer|Yes|No|The subnet mask length for the contiguous EIPs.|Valid values:-   28: 16 contiguous EIPs are allocated for one call.
-   27: 32 contiguous EIPs are allocated for one call.
-   26: 64 contiguous EIPs are allocated for one call.
-   25: 128 contiguous EIPs are allocated for one call.
-   24: 256 contiguous EIPs are allocated for one call.

**Note:** The actual number of requested EIPs may be less than the expected number because one, three, or four EIPs may be reserved. |
|ResourceGroupId|String|No|No|The ID of the resource group.|None|
|Netmode|String|No|No|The network type of the EIPs.|Default value: public. Valid values:-   public: the Internet. After contiguous EIPs are associated with cloud resources, the cloud resources can access the Internet by using the EIPs.
-   hybrid: a hybrid cloud. After contiguous EIPs are associated with cloud resources, the cloud resources can access the hybrid cloud by using the EIPs.

**Note:** This network type is available only to users who are included in the whitelist. To use this network type, contact your sales account manager. |
|Bandwidth|Integer|No|No|The maximum bandwidth of the EIPs.|Default value: 5. Unit: Mbit/s. |
|InternetChargeType|String|No|No|The billing method of the contiguous EIPs.|Default value: PayByBandwidth. Valid values:-   PayByBandwidth
-   PayByTraffic

**Note:** When the Netmode parameter is set to hybrid, the InternetChangeType parameter can be set only to PayByBandwidth. |

## Response parameters

Fn::GetAtt

-   EipSegmentInstanceId: the ID of the contiguous EIP group.
-   EipAddresses: the EIPs.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "EipMask": {
      "Type": "Number",
      "Description": "The mask of the contiguous EIP group. Valid values:\n28: 16 contiguous EIPs are allocated for one call.\n27: 32 contiguous EIPs are allocated for one call.\n26: 64 contiguous EIPs are allocated for one call.\n25: 128 contiguous EIPs are allocated for one call.\n24: 256 contiguous EIPs are allocated for one call.\nNote The actual number of assigned EIPs may be less than the expected number because one,\nthree, or four EIPs may be reserved.",
      "AllowedValues": [
        28,
        27,
        26,
        25,
        24
      ]
    },
    "ResourceGroupId": {
      "Type": "String",
      "Description": "The ID of the resource group to which the EIPs belong."
    },
    "Netmode": {
      "Type": "String",
      "Description": "The network type. Valid values:\npublic: the Internet. This is the default value. After contiguous EIPs are associated with\ncloud resources, the cloud resources can access the Internet by using the EIPs.\nhybrid: the hybrid cloud. After contiguous EIPs are associated with cloud resources, the\ncloud resources can access the hybrid cloud by using the EIPs.\nNote This network type is available only to users who are added to the whitelist. To use\nthis network type, contact your customer manager.",
      "AllowedValues": [
        "public",
        "hybrid"
      ]
    },
    "Bandwidth": {
      "Type": "Number",
      "Description": "The maximum bandwidth of the contiguous EIPs. Unit: Mbit/s. Default value: 5."
    },
    "InternetChargeType": {
      "Type": "String",
      "Description": "The metering method of the contiguous EIPs. Valid values:\nPayByBandwidth: Fees are charged based on bandwidth usage. This is the default value.\nPayByTraffic: Fees are charged based on data transfer.\nNote If the Netmode parameter is set to hybrid, InternetChargeType is set to PayByBandwidth.",
      "AllowedValues": [
        "PayByBandwidth",
        "PayByTraffic"
      ]
    }
  },
  "Resources": {
    "EIPSegment": {
      "Type": "ALIYUN::VPC::EIPSegment",
      "Properties": {
        "EipMask": {
          "Ref": "EipMask"
        },
        "ResourceGroupId": {
          "Ref": "ResourceGroupId"
        },
        "Netmode": {
          "Ref": "Netmode"
        },
        "Bandwidth": {
          "Ref": "Bandwidth"
        },
        "InternetChargeType": {
          "Ref": "InternetChargeType"
        }
      }
    }
  },
  "Outputs": {
    "EipSegmentInstanceId": {
      "Description": "The ID of the contiguous EIP group.",
      "Value": {
        "Fn::GetAtt": [
          "EIPSegment",
          "EipSegmentInstanceId"
        ]
      }
    },
    "EipAddresses": {
      "Description": "List of EIP addresses. like [{\"AllocationId\": \"eip-xxx\", \"IpAddress\": \"xx.xx.xx.xx\"}]",
      "Value": {
        "Fn::GetAtt": [
          "EIPSegment",
          "EipAddresses"
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
    Description: 'The maximum bandwidth of the contiguous EIPs. Unit: Mbit/s. Default
      value: 5.'
    Type: Number
  EipMask:
    AllowedValues:
    - 28
    - 27
    - 26
    - 25
    - 24
    Description: 'The mask of the contiguous EIP group. Valid values:

      28: 16 contiguous EIPs are allocated for one call.

      27: 32 contiguous EIPs are allocated for one call.

      26: 64 contiguous EIPs are allocated for one call.

      25: 128 contiguous EIPs are allocated for one call.

      24: 256 contiguous EIPs are allocated for one call.

      Note The actual number of assigned EIPs may be less than the expected number
      because one,

      three, or four EIPs may be reserved.'
    Type: Number
  InternetChargeType:
    AllowedValues:
    - PayByBandwidth
    - PayByTraffic
    Description: 'The metering method of the contiguous EIPs. Valid values:

      PayByBandwidth: Fees are charged based on bandwidth usage. This is the default
      value.

      PayByTraffic: Fees are charged based on data transfer.

      Note If the Netmode parameter is set to hybrid, InternetChargeType is set to
      PayByBandwidth.'
    Type: String
  Netmode:
    AllowedValues:
    - public
    - hybrid
    Description: 'The network type. Valid values:

      public: the Internet. This is the default value. After contiguous EIPs are associated
      with

      cloud resources, the cloud resources can access the Internet by using the EIPs.

      hybrid: the hybrid cloud. After contiguous EIPs are associated with cloud resources,
      the

      cloud resources can access the hybrid cloud by using the EIPs.

      Note This network type is available only to users who are added to the whitelist.
      To use

      this network type, contact your customer manager.'
    Type: String
  ResourceGroupId:
    Description: The ID of the resource group to which the EIPs belong.
    Type: String
Resources:
  EIPSegment:
    Properties:
      Bandwidth:
        Ref: Bandwidth
      EipMask:
        Ref: EipMask
      InternetChargeType:
        Ref: InternetChargeType
      Netmode:
        Ref: Netmode
      ResourceGroupId:
        Ref: ResourceGroupId
    Type: ALIYUN::VPC::EIPSegment
Outputs:
  EipAddresses:
    Description: 'List of EIP addresses. like [{"AllocationId": "eip-xxx", "IpAddress":
      "xx.xx.xx.xx"}]'
    Value:
      Fn::GetAtt:
      - EIPSegment
      - EipAddresses
  EipSegmentInstanceId:
    Description: The ID of the contiguous EIP group.
    Value:
      Fn::GetAtt:
      - EIPSegment
      - EipSegmentInstanceId
```

