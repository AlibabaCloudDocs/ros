# ALIYUN::SLB::AccessControl {#concept_yd3_rw2_2hb .concept}

ALIYUN::SLB::AccessControl is used to create an access control list \(ACL\).

## Syntax {#section_ey2_ycz_lfb .section}

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

## Properties {#section_n13_22z_lfb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|AddressIPVersion|String|No|No|The Internet Protocol \(IP\) version for the ACL to be created.|Valid values: ipv4 and ipv6|
|AclName|String|Yes|Yes|The name of the ACL.|None|
|AclEntrys|List|No|No|The list of ACL entries.|A list can contain up to 50 ACL entries.|

## AclEntrys syntax {#section_vwl_vw2_2hb .section}

``` {#codeblock_mfy_apo_181}
"AclEntrys": [
  {
    "Comment": String,
    "Entry": String
  }
]
```

## AclEntrys properties {#section_wwl_vw2_2hb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Comment|String|No|No|The comments on ACL entries.|None|
|Entry|String|Yes|No|The authorized IP addresses or CIDR blocks.|None|

## Response parameters {#section_wfc_q2z_lfb .section}

**Fn::GetAtt**

AclId: the ID of the ACL.

## Examples {#section_lcd_s2z_lfb .section}

Resource usage example

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
      "Description": "A list of ACL entries. Each entry can be IP addresses or CIDR blocks. Max length: 50.",
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

Example of combined use of SLB-related resources

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

