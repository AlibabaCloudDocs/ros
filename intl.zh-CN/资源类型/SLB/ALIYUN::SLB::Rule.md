# ALIYUN::SLB::Rule {#concept_ett_qbf_2hb .concept}

ALIYUN::SLB::Rule 用于指定的HTTP或HTTPS监听添加转发规则。

## 语法 {#section_ey2_ycz_lfb .section}

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

## 属性 {#section_n13_22z_lfb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ListenerPort|Integer|是|否|负载均衡实例前端使用的监听端口。|取值范围：1~65535。|
|RuleList|List|是|否|要添加的转发规则。| 一次请求中，最多可添加10条转发规则。

 每条转发规则包含以下参数：RuleName、Domain、Url、VServerGroupId。

 Domain和Url两者必须指定一个，也可以同时指定。

 Domain和Url的组合在同一个监听内必须唯一。

 |
|LoadBalancerId|String|是|否|负载均衡实例ID。|无。|

## RuleList语法 {#section_vwl_vw2_2hb .section}

```
"RuleList": [
  {
    "Url": String,
    "Domain": String,
    "VServerGroupId": String,
    "RuleName": String
  }
]
```

## RuleList属性 {#section_wwl_vw2_2hb .section}

|名称|类型|必须|允许更新|描述|约束|
|--|--|--|----|--|--|
|Url|String|否|否|访问路径。|长度限制为1~80，只能使用字母、数字和-/.%?\#&这些字符。|
|Domain|String|否|否|转发规则关联的请求域名。|无。|
|VServerGroupId|String|是|否|该转发规则的目标虚拟服务器组ID。|无。|
|RuleName|String|是|否|转发规则名称。|长度限制为1~40，只能使用字母、数字和-/.\_这些字符。同一个监听内不同规则的名称必须唯一。|

## 返回值 {#section_wfc_q2z_lfb .section}

**Fn::GetAtt**

Rules：转发规则列表。

## 示例 {#section_lcd_s2z_lfb .section}

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
      "Description": "The front-end HTTPS listener port of the Server Load Balancer instance. Valid value:\n1-65535",
      "MaxValue": 65535,
      "MinValue": 1
    },
    "RuleList": {
      "MinLength": 1,
      "Type": "CommaDelimitedList",
      "Description": "The forwarding rules to add.",
      "MaxLength": 10
    },
    "LoadBalancerId": {
      "Type": "String",
      "Description": "The ID of Server Load Balancer instance."
    }
  },
  "Outputs": {
    "Rules": {
      "Description": "A list of forwarding rules. Each element of rules contains \"RuleId\".",
      "Value": {
        "Fn::GetAtt": ["Rule", "Rules"]
      }
    }
  }
}
```

