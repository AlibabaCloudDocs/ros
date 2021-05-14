# ALIYUN::ECS::NetworkInterface

ALIYUN::ECS::NetworkInterface is used to create an elastic network interface \(ENI\).

## Syntax

```
{
  "Type": "ALIYUN::ECS::NetworkInterface",
  "Properties": {
    "Description": String,
    "SecurityGroupId": String,
    "PrimaryIpAddress": String,
    "ResourceGroupId": String,
    "VSwitchId": String,
    "NetworkInterfaceName": String,
    "Tags": List,
    "SecurityGroupIds": List,
    "PrivateIpAddresses": List
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ResourceGroupId|String|No|No|The ID of the resource group to which the ECS instance belongs.|None|
|SecurityGroupId|String|No|Yes|The ID of the security group.|The security group and the ENI must belong to the same VPC.|
|VSwitchId|String|Yes|No|The ID of the vSwitch.|None|
|Description|String|No|Yes|The description of the ENI.|The description must be 2 to 256 characters in length and cannot start with `http://` or `https://`. |
|NetworkInterfaceName|String|No|Yes|The name of the ENI.|The name must be 2 to 128 characters in length and can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). It must start with a letter and cannot start with `http://` or `https://`. |
|PrimaryIpAddress|String|No|No|The primary private IP address of the ENI.|The specified IP address must be available within the CIDR block of the vSwitch. If this parameter is not specified, an available IP address in the vSwitch CIDR block is selected at random.|
|Tags|List|No|Yes|The tags of the ENI.|A maximum of 20 tags can be specified. For more information, see the [Tags properties](#section_tpw_if9_xq8) section in this topic. |
|SecurityGroupIds|List|No|Yes|One or more security groups to which the ENI belongs|The security groups and the ENI must belong to the same VPC. **Note:** You cannot specify both the SecurityGroupId and SecurityGroupIds parameters. |
|PrivateIpAddresses|List|No|No|One or more secondary private IP addresses selected from the CIDR block of the vSwitch that hosts the ENI.|Valid values of the number of IP addresses that can be assigned to the ENI:-   When the ENI is in the Available state, the valid values are 1 to 10.
-   When the ENI is in the InUse state, the valid values depend on the instance type. For more information, see [Instance families](/intl.en-US/Instance/Instance families.md). |

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

-   NetworkInterfaceId: the ID of the ENI.
-   MacAddress: the MAC address of the ENI.
-   PrivateIpAddresses: the primary private IP addresses assigned to the ENI.
-   SecondaryPrivateIpAddresses: all secondary private IP addresses assigned to the ENI.

## Examples

`JSON` format

```
{
"ROSTemplateFormatVersion": "2015-09-01",
  "Parameters":
{
    "Description": {
      "Type":
"String",
      "Description": "Description of your ENI.
It is a string of [2, 256] English or Chinese characters." },
    "PrivateIpAddresses":
{
      "Type": "Json",
      "Description": "Specifies secondary private IP addresses of the ENI.
This IP address must be an available IP address in the CIDR block of the VSwitch to which the ENI belongs.",
"MaxLength": 10
    },
    "ResourceGroupId":
{
      "Type": "String",
      "Description":
"Resource group id." },
    "SecurityGroupId": {
      "Type":
"String",
      "Description": "The ID of the security group that the ENI joins.
The security group and the ENI must be in a same VPC."
},
    "VSwitchId": {
      "Type":
"String",
      "Description": "VSwitch ID of the specified VPC.
Specifies the switch ID for the VPC." },
    "NetworkInterfaceName":
{
      "Type":
"String",
      "Description": "Name of your ENI.
It is a string of [2, 128]  Chinese or English characters. It must begin with a letter and can contain numbers, underscores (_), colons (:), or hyphens (-)."
    },
    "PrimaryIpAddress":
{
      "Type": "String",
      "Description": "The primary private IP address of the ENI.
The specified IP address must have the same Host ID as the VSwitch.
If no IP addresses are specified, a random network ID is assigned for the ENI." },
    "SecurityGroupIds":
{
      "Type": "Json",
      "Description":
"The IDs of the security groups that the ENI joins. The security groups and the ENI must belong to the same VPC.", "MaxLength":
16
    },
    "Tags":
{
      "Type": "Json",
      "Description":
"Tags to attach to instance. Max support 20 tags to add during create instance.
Each tag with two properties Key and Value, and Key is required.", "MaxLength": 20
    }
  },
  "Resources": {
    "EniInstance":
{
      "Type":
"ALIYUN::ECS::NetworkInterface",
      "Properties": {
        "Description":
{
          "Ref": "Description"
        },
        "PrivateIpAddresses":
{
          "Ref": "PrivateIpAddresses"
        },
        "ResourceGroupId":  "ResourceGroupId"
        },
        "SecurityGroupId": {
          "Ref":
"SecurityGroupId"
        },
        "VSwitchId":
{
          "Ref": "VSwitchId"
        },
        "NetworkInterfaceName":
{
          "Ref": "NetworkInterfaceName"
        },
        "PrimaryIpAddress":
{
          "Ref": "PrimaryIpAddress"
        },
        "SecurityGroupIds": {
          "Ref":
"SecurityGroupIds"
        },
        "Tags": {
          "Ref":
"Tags"
        }
      }
    }
  },
  "Outputs":
{
    "PrivateIpAddress": {
      "Description":
"The primary private ip address of your Network Interface.", "Value":
{
        "Fn::GetAtt": [
          "EniInstance",
          "PrivateIpAddress"
        ]
      }
    },
    "SecondaryPrivateIpAddresses": {
      "Description": "The secondary private IP addresses of your Network Interface.",
"Value": {
        "Fn::GetAtt":
[
          "EniInstance",
          "SecondaryPrivateIpAddresses"
        ]
      }
    },
    "MacAddress":
{
      "Description":
"The MAC address of your Network Interface.", "Value":
{
        "Fn::GetAtt": [
          "EniInstance",
          "MacAddress"
        ]
      }
    },
    "NetworkInterfaceId":
{
      "Description": "ID of your Network Interface.",
"Value": {
        "Fn::GetAtt":
[
          "EniInstance",
          "NetworkInterfaceId"
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
    Description: Description of your ENI. It is a string of [2, 256] English or Chinese
      characters.
      Type:
    String
  NetworkInterfaceName: Description:
  Name of your ENI.
    It is a string of [2, 128]  Chinese or English
      characters. It must begin with a letter and can contain numbers, underscores
      (_), colons (:), or hyphens (-).
    Type: String
  PrimaryIpAddress:
      Description: The primary private IP address of the ENI.
      The specified IP address
      must have the same Host ID as the VSwitch.
    If no IP addresses are specified,
      a random network ID is assigned for the ENI. Type:
  String
  PrivateIpAddresses:
    Description: Specifies secondary private IP addresses of the ENI.  This IP address
      must be an available IP address in the CIDR block of the VSwitch to which the
      ENI belongs.
      MaxLength: 10
    Type:
      Json
  ResourceGroupId:
    Description: Resource group id.
  Type:
    String
  SecurityGroupId: Description: The ID of the security group that the ENI joins.
      The security group
      and the ENI must be in a same VPC.
      Type:
    String
  SecurityGroupIds: Description:
    The IDs of the security groups that the ENI joins. The security groups
      and the ENI must belong to the same VPC.
  MaxLength:
    16
    Type: Json
  Tags:
    Description: Tags to attach to instance.
  Max support 20 tags to add during create
      instance.
    Each tag with two properties Key and Value, and Key is required. MaxLength: 20
    Type:
      Json
  VSwitchId:
    Description: VSwitch ID of the specified VPC.
  Specifies the switch ID for the
      VPC.
    Type: String
Resources: EniInstance:
      Properties:
    Description: Ref:
    Description
      NetworkInterfaceName: Ref:
  NetworkInterfaceName
      PrimaryIpAddress:
    Ref: PrimaryIpAddress
      PrivateIpAddresses: Ref:
      PrivateIpAddresses
      ResourceGroupId: Ref:
    ResourceGroupId
      SecurityGroupId: Ref:
    SecurityGroupId
      SecurityGroupIds: Ref:
  SecurityGroupIds
      Tags:
    Ref: Tags
      VSwitchId: Ref:
      VSwitchId
    Type:
    ALIYUN::ECS::NetworkInterface
Outputs: MacAddress:
Description:
  The MAC address of your Network Interface.
    Value:
      Fn::GetAtt:
        - EniInstance
      - MacAddress
  NetworkInterfaceId: Description:
      ID of your Network Interface.
        Value: Fn::GetAtt:
      - EniInstance
      - NetworkInterfaceId
  PrivateIpAddress:
        Description: The primary private ip address of your Network Interface.
      Value:
        Fn::GetAtt: - EniInstance
      - PrivateIpAddress
  SecondaryPrivateIpAddresses:
      Description:
        The secondary private IP addresses of your Network Interface. Value:
      Fn::GetAtt:
        - EniInstance
      - SecondaryPrivateIpAddresses  
```

For more examples, visit [NetworkInterfaceAttachment.json](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ECS/JSON/NetworkInterfaceAttachment.json) and [NetworkInterfaceAttachment.yml](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/ECS/YAML/NetworkInterfaceAttachment.yml). In the examples, the ALIYUN::ECS::NetworkInterface, ALIYUN::ECS::NetworkInterfaceAttachment, and ALIYUN::ECS::NetworkInterfacePermission resource types are involved.

