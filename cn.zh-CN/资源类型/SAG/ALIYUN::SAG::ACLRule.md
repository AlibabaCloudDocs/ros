# ALIYUN::SAG::ACLRule {#concept_264670 .concept}

ALIYUN::SAG::ACLRule类型用于添加访问控制规则。

## 语法 {#section_6yd_ywb_5ei .section}

``` {#codeblock_adk_kjj_w8w .language-json}
{
  "Type": "ALIYUN::SAG::ACLRule",
  "Properties": {
    "Direction": String,
    "Description": String,
    "AclId": String,
    "SourceCidr": String,
    "DestCidr": String,
    "Priority": Integer,
    "DestPortRange": String,
    "Policy": String,
    "IpProtocol": String,
    "SourcePortRange": String
  }
}
```

## 属性 {#section_wqi_d6o_36k .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Direction|String|是|是|规则方向。|取值：in|out。|
|Description|String|否|是|规则描述信息。|长度为1~512个字符|
|AclId|String|是|否|访问控制ID。|无。|
|SourceCidr|String|是|是|源地址，CIDR 格式和IPv4格式的IP地址范围。|无。|
|DestCidr|String|是|是|目的地址，CIDR 格式和 IPv4 格式的IP地址范围。|无。|
|Priority|Integer|否|是|优先级。| 取值范围：1~100。

 默认值：1

 |
|DestPortRange|String|是|是|目的端口范围。|无。|
|Policy|String|是|是|访问权限。|取值：accept|drop。|
|IpProtocol|String|是|是|协议，不区分大小写。|无。|
|SourcePortRange|String|是|是|源端口范围。|无。|

## 返回值 {#section_lbf_s6j_ht3 .section}

**Fn::GetAtt**

AcrId: 访问控制规则ID。

## 示例 {#section_93m_1el_l07 .section}

``` {#codeblock_wvr_w39_sc1 .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "ACLRule": {
      "Type": "ALIYUN::SAG::ACLRule",
      "Properties": {
        "Direction": {
          "Ref": "Direction"
        },
        "Description": {
          "Ref": "Description"
        },
        "AclId": {
          "Ref": "AclId"
        },
        "SourceCidr": {
          "Ref": "SourceCidr"
        },
        "DestCidr": {
          "Ref": "DestCidr"
        },
        "Priority": {
          "Ref": "Priority"
        },
        "DestPortRange": {
          "Ref": "DestPortRange"
        },
        "Policy": {
          "Ref": "Policy"
        },
        "IpProtocol": {
          "Ref": "IpProtocol"
        },
        "SourcePortRange": {
          "Ref": "SourcePortRange"
        }
      }
    }
  },
  "Parameters": {
    "Direction": {
      "Type": "String",
      "Description": "Regular direction.\nValue: in|out",
      "AllowedValues": [
        "in",
        "out"
      ]
    },
    "Description": {
      "MinLength": 1,
      "Type": "String",
      "Description": "Rule description information, ranging from 1 to 512 characters.",
      "MaxLength": 512
    },
    "AclId": {
      "Type": "String",
      "Description": "Access control ID."
    },
    "SourceCidr": {
      "Type": "String",
      "Description": "Source address, CIDR format and IP address range in IPv4 format."
    },
    "DestCidr": {
      "Type": "String",
      "Description": "Destination address, CIDR format and IP address range in IPv4 format."
    },
    "Priority": {
      "Default": 1,
      "Type": "Number",
      "Description": "Priority, ranging from 1 to 100.\nDefault: 1",
      "MaxValue": 100,
      "MinValue": 1
    },
    "DestPortRange": {
      "Type": "String",
      "Description": "Destination port range, 80/80."
    },
    "Policy": {
      "Type": "String",
      "Description": "Access: accept|drop",
      "AllowedValues": [
        "accept",
        "drop"
      ]
    },
    "IpProtocol": {
      "Type": "String",
      "Description": "Protocol, not case sensitive."
    },
    "SourcePortRange": {
      "Type": "String",
      "Description": "Source port range, 80/80."
    }
  },
  "Outputs": {
    "AcrId": {
      "Description": "Access control rule ID.",
      "Value": {
        "Fn::GetAtt": [
          "ACLRule",
          "AcrId"
        ]
      }
    }
  }
}
```

