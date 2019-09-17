# ALIYUN::ECS::SecurityGroupClone {#concept_54355_zh .concept}

ALIYUN::ECS::SecurityGroupClone 类型用于克隆安全组。

## 语法 {#section_xyd_mz2_lfb .section}

``` {#codeblock_yv5_li7_qrp .language-json}
{
  "Type": "ALIYUN::ECS::SecurityGroupClone",
  "Properties": {
    "DestinationRegionId": String,
    "VpcId": String,
    "Description": String,
    "SecurityGroupName": String,
    "SourceSecurityGroupId": String,
    "ResourceGroupId": String,
    "NetworkType": String,
    "SecurityGroupType": String
  }
}
```

## 属性 {#section_ak4_iko_c1h .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ResourceGroupId|String|否|否|实例所在的资源组ID。|无。|
|SourceSecurityGroupId|string|是|否|用于克隆的原始安全组 ID。|根据新安全组的网络类型，克隆合适的安全组规则。|
|NetworkType|string|否|否|克隆的新安全组网络类型为经典网络。|允许值：Classic。|
|VpcId|string|否|否|克隆的新安全组所属的 VPC ID。|同时指定 VpcId 和 NetworkType 时，则忽略 NetworkType。|
|Description|string|否|否|安全组描述信息。|长度为 \[2, 256\] 个字符。不能以 http:// 和 https:// 开头。|
|SecurityGroupName|string|否|否|安全组名称。|默认值为空。长度为 \[2, 128\] 字符，必须以大小字母或中文开头，可包含字母、汉字、数字、点号（.）、下划线（\_）和连字符（-）。不能以 http:// 和 https:// 开头。|
|DestinationRegionId|String|否|否|将安全组克隆到指定区域。|默认值：CURRENT。|
|SecurityGroupType|String|否|否|安全组的类型。有效值：normal：基本安全组，enterprise：高级安全组。|可用值: normal, enterprise。|

## 返回值 {#section_ggb_hbi_6re .section}

**Fn::GetAtt**

SecurityGroupId：安全组 ID。

## 示例 {#section_8gi_jy8_w0p .section}

``` {#codeblock_3ck_4uz_q27 .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "SecurityGroupClone": {
      "Type": "ALIYUN::ECS::SecurityGroupClone",
      "Properties": {
        "SourceSecurityGroupId": {
          "Ref": "SourceSecurityGroupId"
        },
        "VpcId": {
          "Ref": "VpcId"
        },
        "Description": {
          "Ref": "Description"
        },
        "SecurityGroupName": {
          "Ref": "SecurityGroupName"
        },
        "DestinationRegionId": {
          "Ref": "DestinationRegionId"
        },
        "NetworkType": {
          "Ref": "NetworkType"
        }
      }
    }
  },
  "Parameters": {
    "SourceSecurityGroupId": {
      "Type": "String",
      "Description": "Source security group ID is used to copy properties to clone new security group. If the NetworkType and VpcId is not specified, the same security group will be cloned. If NetworkType or VpcId is specified, only proper security group rules will be cloned."
    },
    "VpcId": {
      "Type": "String",
      "Description": "Physical ID of the VPC."
    },
    "Description": {
      "Type": "String",
      "Description": "Description of the security group, [2, 256] characters. Do not fill or empty, the default is empty."
    },
    "SecurityGroupName": {
      "Type": "String",
      "Description": "Display name of the security group, [2, 128] English or Chinese characters, must start with a letter or Chinese in size, can contain numbers, '_' or '.', '-'"
    },
    "DestinationRegionId": {
      "Default": "CURRENT",
      "Type": "String",
      "Description": "Clone security group to the specified region. Default to current region."
    },
    "NetworkType": {
      "Type": "String",
      "Description": "Clone new security group as classic network type. If the VpcId is specified, the value will be ignored.",
      "AllowedValues": [
        "Classic"
      ]
    }
  },
  "Outputs": {
    "SecurityGroupId": {
      "Description": "Generated security group id of new security group.",
      "Value": {
        "Fn::GetAtt": [
          "SecurityGroupClone",
          "SecurityGroupId"
        ]
      }
    }
  }
}
```

