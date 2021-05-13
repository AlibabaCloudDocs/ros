# ALIYUN::VPC::EIPSegment

ALIYUN::VPC::EIPSegment类型用于申请连续弹性公网IP（EIP）。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|EipMask|Integer|是|否|连续EIP的掩码。|取值：-   28：单次调用，系统将分配16个连续EIP。
-   27：单次调用，系统将分配32个连续EIP。
-   26：单次调用，系统将分配64个连续EIP。
-   25：单次调用，系统将分配128个连续EIP。
-   24：单次调用，系统将分配256个连续EIP。

**说明：** 由于IP地址保留，实际申请到的连续EIP可能缺少1个、3个或者4个EIP。 |
|ResourceGroupId|String|否|否|资源组ID。|无|
|Netmode|String|否|否|网络类型。|取值：-   public（默认）：公网。连续EIP和云资源绑定后，云资源可以通过EIP与公网通信。
-   hybrid：混合云。连续EIP和云资源绑定后，云资源可以通过EIP进行混合云通信。

**说明：** 仅具有混合云白名单的用户支持选择混合云类型，如需使用，请联系您的客户经理。 |
|Bandwidth|Integer|否|否|EIP的带宽峰值。|默认值：5。单位：Mbps。 |
|InternetChargeType|String|否|否|连续EIP的计费方式。|取值：-   PayByBandwidth（默认值）：按带宽计费。
-   PayByTraffic：按流量计费。

**说明：** 当Netmode取值为hybrid时，InternetChargeType仅支持按带宽计费（PayByBandwidth）。 |

## 返回值

Fn::GetAtt

-   EipSegmentInstanceId：连续EIP的实例ID。
-   EipAddresses：EIP实例地址。

## 示例

`JSON`格式

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

`YAML`格式

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

