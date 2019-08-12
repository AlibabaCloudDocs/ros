# ALIYUN::SLB::AccessControl {#concept_yd3_rw2_2hb .concept}

ALIYUN::SLB::AccessControl 用于创建访问控制策略组。

## 语法 {#section_ey2_ycz_lfb .section}

``` {#codeblock_lzd_p7y_sbk .language-json}
{
  "Type": "ALIYUN::SLB::AccessControl",
  "Properties": {
    "AddressIPVersion": String,
    "AclName": String,
    "AclEntrys": List
  }
}
```

## 属性 {#section_n13_22z_lfb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|AddressIPVersion|String|否|否|IP版本，可以设置为ipv4或者ipv6。|可用值：ipv4、ipv6。|
|AclName|String|是|是|访问控制策略组名称。|无。|
|AclEntrys|List|否|否|访问控制策略组的信息列表。|最多50个。|

## AclEntrys语法 {#section_vwl_vw2_2hb .section}

``` {#codeblock_mfy_apo_181}
"AclEntrys": [
  {
    "Comment": String,
    "Entry": String
  }
]
```

## AclEntrys属性 {#section_wwl_vw2_2hb .section}

|名称|类型|必须|允许更新|描述|约束|
|--|--|--|----|--|--|
|Comment|String|否|否|访问控制条目备注。|无。|
|Entry|String|是|否|IP地址或CIDR网段。|无。|

## 返回值 {#section_wfc_q2z_lfb .section}

**Fn::GetAtt**

AclId：访问控制策略组ID。

## 示例 {#section_lcd_s2z_lfb .section}

该资源使用示例

``` {#codeblock_wvp_rm9_ao8 .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "AccessControl": {
      "Type": "ALIYUN::SLB::AccessControl",
      "Properties": {
        "AddressIPVersion": {
          "Ref": "AddressIPVersion"
        },
        "AclName": {
          "Ref": "AclName"
        },
        "AclEntrys": {
          "Fn::Split": [",", {
            "Ref": "AclEntrys"
          }, {
            "Ref": "AclEntrys"
          }]
        }
      }
    }
  },
  "Parameters": {
    "AddressIPVersion": {
      "Type": "String",
      "Description": "IP version. Could be \"ipv4\" or \"ipv6\".",
      "AllowedValues": ["ipv4", "ipv6"]
    },
    "AclName": {
      "Type": "String",
      "Description": "The name of the access control list."
    },
    "AclEntrys": {
      "Type": "CommaDelimitedList",
      "Description": "A list of acl entrys. Each entry can be IP addresses or CIDR blocks. Max length: 50.",
      "MaxLength": 50
    }
  },
  "Outputs": {
    "AclId": {
      "Description": "The ID of the access control list.",
      "Value": {
        "Fn::GetAtt": ["AccessControl", "AclId"]
      }
    }
  }
}
```

SLB相关资源结合使用示例

``` {#codeblock_wvp_rm9_ao8 .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "LoadBalancer": {
      "Type": "ALIYUN::SLB::LoadBalancer",
      "Properties": {
        "LoadBalancerName": "slb-with-listener-and-acl",
        "AddressType": "internet",
        "InternetChargeType": "paybybandwidth",
        "Bandwidth": 10,
        "VpcId": "vpc-xxxxxxxxxxxxxxxxxxxx",
        "VSwitchId": "vsw-xxxxxxxxxxxxxxxxxxxx"
      }
    },
    "ACL": {
      "Type": "ALIYUN::SLB::AccessControl",
      "Properties": {
        "AclName": "acl-for-listener",
        "AddressIPVersion": "ipv4",
        "AclEntrys": [
          {
            "entry": "192.168.x.x"
          },
          {
            "entry": "10.0.x.x/24",
            "comment": "just comment"
          }
        ]
      }
    },
    "CreateListener": {
      "Type": "ALIYUN::SLB::Listener",
      "Properties": {
        "LoadBalancerId": {
          "Ref": "LoadBalancer"
        },
        "ListenerPort": "80",
        "BackendServerPort": 8080,
        "Bandwidth": 1,
        "Protocol": "http",
        "HealthCheck": {
          "HealthyThreshold": 3,
          "UnhealthyThreshold": 3,
          "Interval": 2,
          "Timeout": 5
        },
        "Scheduler": "wrr",
        "RequestTimeout": 179,
        "IdleTimeout": 59,
        "AclId": {
          "Ref": "ACL"
        },
        "AclStatus": "on",
        "AclType": "white"
      }
    }
  },
  "Outputs": {
    "LoadBalanceDetails": {
      "Value": {
        "Fn::GetAtt": [
          "LoadBalancerId",
          "Listeners"
        ]
      }
    }
  }
}
```

