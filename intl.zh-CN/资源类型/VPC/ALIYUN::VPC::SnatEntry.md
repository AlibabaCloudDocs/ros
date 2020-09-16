# ALIYUN::VPC::SnatEntry

ALIYUN::VPC::SnatEntry类型用于在SNAT列表中添加SNAT条目。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|SnatTableId|String|是|否|SNAT表ID。|无|
|SnatEntryName|String|否|是|SNAT规则的名称。|长度为2~128个字符，必须以英文字母或汉字开头，但不能以`http://`或`https://`开头。|
|SourceVSwitchIds|List|否|否|需要公网访问的交换机的ID。|无|
|SourceCIDR|String|否|否|交换机或ECS实例的网段。|不能同时指定SourceCIDR和SourceVSwitchIds。|
|SnatIp|String|是|是|公网IP地址。|多个IP之间用半角逗号（,）间隔。|

## 返回值

Fn::GetAtt

SnatEntryIds：SNAT条目ID。

## 示例

`JSON`格式

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

`YAML`格式

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

