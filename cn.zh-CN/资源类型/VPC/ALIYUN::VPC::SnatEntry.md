# ALIYUN::VPC::SnatEntry {#concept_228317 .concept}

ALIYUN::VPC::SnatEntry 类型用于在SNAT列表中添加SNAT条目。

## 语法 {#section_fzv_zle_qz3 .section}

``` {#codeblock_d5d_zcj_9h8 .language-json}
{
  "Type": "ALIYUN::VPC::SnatEntry",
  "Properties": {
    "SnatTableId": String,
    "SnatEntryName": String,
    "SourceVSwitchIds": List,
    "SnatIp": String
  }
}
```

## 属性 {#section_1nb_wqs_pe0 .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|SnatTableId|String|是|否|SNAT表ID。|无|
|SnatEntryName|String|否|是|SNAT规则的名称。|长度为2-128个字符，必须以字母或中文开头，但不能以http://或https://开头。|
|SourceVSwitchIds|List|否|否|需要公网访问的交换机的ID。|无|
|SnatIp|String|是|是|公网IP地址。|多个IP之间逗号隔开。|

## 返回值 {#section_lra_7il_dyt .section}

**Fn::GetAtt**

SnatEntryIds：SNAT条目ID。

## 示例 {#section_dps_886_kux .section}

``` {#codeblock_u1e_168_3aj .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "SnatEntry": {
      "Type": "ALIYUN::VPC::SnatEntry",
      "Properties": {
        "SnatTableId": {
          "Ref": "SnatTableId"
        },
        "SnatEntryName": {
          "Ref": "SnatEntryName"
        },
        "SourceVSwitchIds": {
          "Fn::Split": [
            ",",
            {
              "Ref": "SourceVSwitchIds"
            },
            {
              "Ref": "SourceVSwitchIds"
            }
          ]
        },
        "SnatIp": {
          "Ref": "SnatIp"
        }
      }
    }
  },
  "Parameters": {
    "SnatTableId": {
      "Type": "String",
      "Description": "The ID of the SNAT table."
    },
    "SnatEntryName": {
      "Type": "String",
      "Description": "he name of the SNAT rule is 2-128 characters long and must start with a letter or Chinese, but cannot begin with HTTP:// or https://."
    },
    "SourceVSwitchIds": {
      "Type": "CommaDelimitedList",
      "Description": "The ID of the VSwitch to access the Internet."
    },
    "SnatIp": {
      "Type": "String",
      "Description": "The public IP address. Separate multiple EIPs with commas."
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

