# ALIYUN::ECS::SNatEntry

ALIYUN::ECS::SNatEntry is used to configure the Source Network Address Translation \(SNAT\) table of a NAT gateway.

## Syntax

```
{
  "Type": "ALIYUN::ECS::SNatEntry",
  "Properties": {
    "SNatTableId": String,
    "SNatIp": String,
    "SnatEntryName": String,
    "SourceCIDR": String,
    "SourceVSwitchId": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|SNatTableId|String|Yes|Yes|The ID of the SNAT table.|None|
|SNatIp|String|Yes|Yes|The public IP address to be translated.|The public IP address must be included in the NAT service plan. It cannot exist in both the forwarding table and the SNAT table.|
|SnatEntryName|String|No|Yes|The name of the SNAT entry.|The name must be 2 to 128 characters in length. It must start with a letter and cannot start with `http://` or `https://`.|
|SourceCIDR|String|No|No|The CIDR block of the vSwitch or the IP address of the ECS instance.-   vSwitch granularity: specifies the CIDR block of the vSwitch such as 192.168.1.0/24. When an ECS instance attached to the vSwitch requires Internet access, the NAT gateway provides the SNAT service \(Internet proxy service\) for the ECS instance. If you specify only one public IP address for the SnatIp parameter, the ECS instance uses the specified public IP address to access the Internet. If you specify multiple public IP addresses for the SnatIp parameter, the ECS instance randomly selects a public IP address from SnatIp to access the Internet.
-   ECS granularity: specifies the IP address of the ECS instance such as 192.168.1.1/32. When the ECS instance requires Internet access, the NAT gateway provides the SNAT service \(Internet proxy service\) for the ECS instance. If you specify only one public IP address for the SnatIp parameter, the ECS instance uses the specified public IP address to access the Internet. If you specify multiple public IP addresses for the SnatIp parameter, the ECS instance randomly selects a public IP address from SnatIp to access the Internet.

|You must specify one of the SourceCIDR and SourceVSwtichId parameters, but you cannot specify both of them.|
|SourceVSwitchId|String|No|Yes|The vSwitch ID of the ECS instance that accesses the Internet by using the SNAT feature.|You must specify one of the SourceCIDR and SourceVSwtichId parameters, but you cannot specify both of them.|

## Response parameters

Fn::GetAtt

SNatEntryId: the ID of each entry in the SNAT table.

## Example

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "SourceVSwitchId": {
      "Type": "String",
      "Description": "Allow which switch can access internet."
    },
    "SnatEntryName": {
      "Type": "String",
      "Description": "he name of the SNAT rule is 2-128 characters long and must start with a letter or Chinese, but cannot begin with HTTP:// or https://."
    },
    "SourceCIDR": {
      "Type": "String",
      "Description": "Specifies the network segment of the switch. For example, 10.0.0.1/24. This parameter and the SourceVSwtichId parameter are mutually exclusive and cannot appear at the same time."
    },
    "SNatTableId": {
      "Type": "String",
      "Description": "Create SNAT entry in specified SNAT table."
    },
    "SNatIp": {
      "Type": "String",
      "Description": "Source IP, must belongs to bandwidth package internet IP"
    }
  },
  "Resources": {
    "SNatTableEntry": {
      "Type": "ALIYUN::ECS::SNatEntry",
      "Properties": {
        "SourceVSwitchId": {
          "Ref": "SourceVSwitchId"
        },
        "SnatEntryName": {
          "Ref": "SnatEntryName"
        },
        "SourceCIDR": {
          "Ref": "SourceCIDR"
        },
        "SNatTableId": {
          "Ref": "SNatTableId"
        },
        "SNatIp": {
          "Ref": "SNatIp"
        }
      }
    }
  },
  "Outputs": {
    "SNatEntryId": {
      "Description": "The id of created SNAT entry.",
      "Value": {
        "Fn::GetAtt": [
          "SNatTableEntry",
          "SNatEntryId"
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
  SourceVSwitchId:
    Type: String
    Description: Allow which switch can access internet.
  SnatEntryName:
    Type: String
    Description: >-
      he name of the SNAT rule is 2-128 characters long and must start with a
      letter or Chinese, but cannot begin with HTTP:// or https://.
  SourceCIDR:
    Type: String
    Description: >-
      Specifies the network segment of the switch. For example, 10.0.0.1/24.
      This parameter and the SourceVSwtichId parameter are mutually exclusive
      and cannot appear at the same time.
  SNatTableId:
    Type: String
    Description: Create SNAT entry in specified SNAT table.
  SNatIp:
    Type: String
    Description: 'Source IP, must belongs to bandwidth package internet IP'
Resources:
  SNatTableEntry:
    Type: 'ALIYUN::ECS::SNatEntry'
    Properties:
      SourceVSwitchId:
        Ref: SourceVSwitchId
      SnatEntryName:
        Ref: SnatEntryName
      SourceCIDR:
        Ref: SourceCIDR
      SNatTableId:
        Ref: SNatTableId
      SNatIp:
        Ref: SNatIp
Outputs:
  SNatEntryId:
    Description: The id of created SNAT entry.
    Value:
      'Fn::GetAtt':
        - SNatTableEntry
        - SNatEntryId
```

