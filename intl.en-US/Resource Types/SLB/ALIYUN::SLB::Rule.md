# ALIYUN::SLB::Rule {#concept_ett_qbf_2hb .concept}

ALIYUN::SLB::Rule is used to add forwarding rules for the specified HTTP or HTTPS listener.

## Syntax {#section_ey2_ycz_lfb .section}

```language-json
{
  "Type": "ALIYUN::SLB::Rule",
  "Properties": {
    "ListenerPort": Integer,
    "RuleList": List,
    "LoadBalancerId": String
  }
}
```

## Properties {#section_n13_22z_lfb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|ListenerPort|Integer|Yes|No|The front-end listener port number used by a Server Load Balancer \(SLB\) instance.|Valid values: 1 to 65,535.|
|RuleList|List|Yes|No|The list of forwarding rules to be added.| A maximum of 10 forwarding rules can be added at a time.

 Each forwarding rule contains the following parameters: RuleName, Domain, Url, and VServerGroupId.

 You must set at least one of the following parameters: Domain and Url.

 The combination of Domain and Url must be unique in a listener.

 |
|LoadBalancerId|String|Yes|No|The ID of the SLB instance.|None|

## RuleList syntax {#section_vwl_vw2_2hb .section}

```
"RuleList":[
  {
    "Url": String,
    "Domain": String,
    "VServerGroupId": String,
    "RuleName": String
  }
]
```

## RuleList properties {#section_wwl_vw2_2hb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Url|String|No|No|The request URL.|The URL must be 1 to 80 characters in length. It can only contain letters, digits, hyphens \(-\), forward slashes \(/\), periods \(.\), percent signs \(%\), question marks \(?\), number signs \(\#\), and ampersands \(&\).|
|Domain|String|No|No|The request domain name associated with a forwarding rule.|None|
|VServerGroupId|String|Yes|No|The ID of the destination VServer group specified in the forwarding rule.|None|
|RuleName|String|Yes|No|The name of the forwarding rule.|The name must be 1 to 40 characters in length. It can only contain letters, digits, hyphens \(-\), forward slashes \(/\), periods \(.\), and underscores \(\_\). Forwarding rule names must be unique within each listener.|

## Response parameters {#section_wfc_q2z_lfb .section}

**Fn::GetAtt**

Rules: a list of forwarding rules. Each rule has a rule ID.

## Examples {#section_lcd_s2z_lfb .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "Rule": {
      "Type": "ALIYUN::SLB::Rule",
      "Properties": {
        "ListenerPort": {
          "Ref": "ListenerPort"
        },
        "RuleList": {
          "Fn::Split": [",", {
            "Ref": "RuleList"
          }, {
            "Ref": "RuleList"
          }]
        },
        "LoadBalancerId": {
          "Ref": "LoadBalancerId"
        }
      }
    }
  },
  "Parameters": {
    "ListenerPort": {
      "Type": "Number",
      "Description": "The front-end HTTPS listener port of the Server Load Balancer instance. Valid values:\n 1 to 65,535.",
      "MaxValue": 65535,
      "MinValue": 1
    },
    "RuleList": {
      "MinLength": 1,
      "Type": "CommaDelimitedList",
      "Description": "The forwarding rules to add.",
      "MaxLength": "100",
    },
    "LoadBalancerId": {
      "Type": "String",
      "Description": "The ID of Server Load Balancer instance."
    }
  },
  "Outputs": {
    "Rules": {
      "Description": "A list of forwarding rules. Each element of rules contains \ "RuleId \".",
      "Value": {
        "Fn::GetAtt": ["Rule", "Rules"]
      }
    }
  }
}
```

