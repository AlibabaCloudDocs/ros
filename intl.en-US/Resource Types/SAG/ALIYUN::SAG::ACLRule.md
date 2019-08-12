# ALIYUN::SAG::ACLRule {#concept_264670 .concept}

ALIYUN::SAG::ACLRule is used to add an access control list \(ACL\) rule.

## Syntax {#section_6yd_ywb_5ei .section}

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

## Properties {#section_wqi_d6o_36k .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Direction|String|Yes|Yes|The direction of traffic to match in the ACL rule.|Valid values: in and out|
|Description|String|No|Yes|The description of the ACL rule.|The description must be 1 to 512 characters in length.|
|AclId|String|Yes|No|The ID of the ACL.|None|
|SourceCidr|String|Yes|Yes|The source IP address range specified in the ACL rule. CIDR blocks and IPv4 addresses are supported.|None|
|DestCidr|String|Yes|Yes|The destination IP address range specified in the ACL rule. CIDR blocks and IPv4 addresses are supported.|None|
|Priority|Integer|No|Yes|The priority of the ACL rule.| Valid values: 1 to 100

 Default value: 1

 |
|DestPortRange|String|Yes|Yes|The destination port range of the transport layer.|None|
|Policy|String|Yes|Yes|The access control policy.|Valid values: accept and drop|
|IpProtocol|String|Yes|Yes|The transport layer protocol. This parameter is not case-sensitive.|None|
|SourcePortRange|String|Yes|Yes|The source port range of the transport layer.|None|

## Response parameters {#section_lbf_s6j_ht3 .section}

 **Fn::GetAtt** 

AcrId: the ID of the ACL rule.

## Examples {#section_93m_1el_l07 .section}

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
      "Description": "Rule description, which must be 1 to 512 characters in length.",
      "MaxLength": 512
    },
    "AclId": {
      "Type": "String",
      "Description": "Access control list ID."
    },
    "SourceCidr": {
      "Type": "String",
      "Description": "Source IP address range. CIDR format and IP address range in IPv4 format are supported."
    },
    "DestCidr": {
      "Type": "String",
      "Description": "Destination IP address range. CIDR format and IP address range in IPv4 format are supported."
    },
    "Priority": {
      "Default": 1,
      "Type": "Number",
      "Description": "Priority, ranging from 1 to 100.\nDefault value: 1",
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

