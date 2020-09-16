# ALIYUN::VPC::SnatEntry

ALIYUN::VPC::SnatEntry is used to add a Source Network Address Translation \(SNAT\) entry to an SNAT table.

## Syntax

```
{
  "Type": "ALIYUN::VPC::SnatEntry",
  "Properties": {
    "SnatTableId": String,
    "SnatEntryName": String,
    "SourceVSwitchIds": List,
    "SourceCIDR": String,
    "SnatIp": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|SnatTableId|String|Yes|No|The ID of the SNAT table.|None|
|SnatEntryName|String|No|Yes|The name of the SNAT entry to be added to the SNAT table.|The name must be 2 to 128 characters in length. It must start with a letter but cannot start with `http://` or `https://`.|
|SourceVSwitchIds|List|No|No|The IDs of VSwitches used to access the Internet.|None|
|SourceCIDR|String|No|No|The CIDR block of the VSwitch or ECS instance.|You cannot specify both the SourceCIDR and SourceVSwitchIds parameters.|
|SnatIp|String|Yes|Yes|The public IP address.|Separate multiple IP addresses with commas \(,\).|

## Response parameters

Fn::GetAtt

SnatEntryIds: the IDs of SNAT entries in the table.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "SnatEntryName": {
      "Type": "String",
      "Description": "he name of the SNAT rule is 2-128 characters long and must start with a letter or Chinese, but cannot begin with HTTP:// or https://."
    },
    "SourceVSwitchIds": {
      "Type": "CommaDelimitedList",
      "Description": "The ID of the VSwitch to access the Internet."
    },
    "SourceCIDR": {
      "Type": "String",
      "Description": "Specifies the network segment of the switch. For example, 10.0.XX.XX/24. This parameter and the SourceVSwtichId parameter are mutually exclusive and cannot appear at the same time."
    },
    "SnatIp": {
      "Type": "String",
      "Description": "The public IP address. Separate multiple EIPs with commas."
    },
    "SnatTableId": {
      "Type": "String",
      "Description": "The ID of the SNAT table."
    }
  },
  "Resources": {
    "SnatEntry": {
      "Type": "ALIYUN::VPC::SnatEntry",
      "Properties": {
        "SnatEntryName": {
          "Ref": "SnatEntryName"
        },
        "SourceVSwitchIds": {
          "Ref": "SourceVSwitchIds"
        },
        "SourceCIDR": {
          "Ref": "SourceCIDR"
        },
        "SnatIp": {
          "Ref": "SnatIp"
        },
        "SnatTableId": {
          "Ref": "SnatTableId"
        }
      }
    }
  },
  "Outputs": {
    "SnatEntryIds": {
      "Description": "The IDS of the SNAT entry.",
      "Value": {
        "Fn::GetAtt": [
          "SnatEntry",
          "SnatEntryIds"
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
  SnatEntryName:
    Type: String
    Description: >-
      he name of the SNAT rule is 2-128 characters long and must start with a
      letter or Chinese, but cannot begin with HTTP:// or https://.
  SourceVSwitchIds:
    Type: CommaDelimitedList
    Description: The ID of the VSwitch to access the Internet.
  SourceCIDR:
    Type: String
    Description: >-
      Specifies the network segment of the switch. For example, 10.0.XX.XX/24.
      This parameter and the SourceVSwtichId parameter are mutually exclusive
      and cannot appear at the same time.
  SnatIp:
    Type: String
    Description: The public IP address. Separate multiple EIPs with commas.
  SnatTableId:
    Type: String
    Description: The ID of the SNAT table.
Resources:
  SnatEntry:
    Type: 'ALIYUN::VPC::SnatEntry'
    Properties:
      SnatEntryName:
        Ref: SnatEntryName
      SourceVSwitchIds:
        Ref: SourceVSwitchIds
      SourceCIDR:
        Ref: SourceCIDR
      SnatIp:
        Ref: SnatIp
      SnatTableId:
        Ref: SnatTableId
Outputs:
  SnatEntryIds:
    Description: The IDS of the SNAT entry.
    Value:
      'Fn::GetAtt':
        - SnatEntry
        - SnatEntryIds
```

