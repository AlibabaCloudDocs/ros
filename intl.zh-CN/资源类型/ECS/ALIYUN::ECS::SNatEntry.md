# ALIYUN::ECS::SNatEntry

ALIYUN::ECS::SNatEntry类型用于配置NAT网关中的源地址转换表。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|SNatTableId|String|是|是|源地址转换表ID。|无|
|SNatIp|String|是|是|用于源地址转换的公网IP。|必须是NAT网关中带宽包的IP。每个NAT网关上的公网IP，不能既存在于端口转发表中，也存在于SNAT表中。|
|SnatEntryName|String|否|是|SNAT条目的名称。|长度为2~128个字符，必须以英文字母或汉字开头，但不能以`http://`或`https://`开头。|
|SourceCIDR|String|否|否|交换机或ECS实例的网段。-   交换机粒度：指定交换机的网段（如192.168.1.0/24），当交换机下的ECS实例发起互联网访问请求时，NAT网关会为其提供SNAT服务（代理上网服务）。如果SnatIp仅指定了一个公网IP，ECS实例使用指定的公网IP访问互联网；如果SnatIp指定了多个公网IP，ECS实例随机使用SnatIp中的公网IP访问互联网。
-   ECS粒度：指定ECS实例的地址（如192.168.1.1/32），当ECS实例发起互联网访问请求时，NAT网关会为其提供SNAT服务（代理上网服务）。如果SnatIp仅指定了一个公网IP，ECS实例使用指定的公网IP访问互联网；如果SnatIp指定了多个公网IP，ECS实例随机使用SnatIp中的公网IP访问互联网。

|不能同时指定SourceCIDR和SourceVSwtichId，必须指定其中之一。|
|SourceVSwitchId|String|否|是|可通过NAT网关的SNAT功能访问互联网的ECS实例所在的VSwitch ID。|不能同时指定SourceCIDR和SourceVSwtichId，必须指定其中之一。|

## 返回值

Fn::GetAtt

SNatEntryId：源地址转换表中的表项ID。

## 示例

`JSON`格式

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

`YAML`格式

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

