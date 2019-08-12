# ALIYUN::UIS::UisNode {#concept_12345_zh .concept}

ALIYUN::UIS::UisNode is used to add an access node to a created Ultimate Internet Service \(UIS\) instance.

## Syntax {#section_bnr_dxz_lfb .section}

``` {#codeblock_ts7_nzf_et0 .language-json}
{
  "Type": "ALIYUN::UIS::UisNode",
  "Properties": {
    "Name": String,
    "UisNodeAreaId": String,
    "IpAddrsNum": Integer,
    "UisId": String,
    "UisNodeBandwidth": Integer,
    "Description": String
  }
}
```

## Properties {#section_xwy_z5d_pg6 .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Name|String|No|Yes|The name of the access node to be added.|None|
|UisNodeAreaId|String|Yes|No|The region ID of the specified node. You can call the DescribeRegions operation to query supported regions.|None|
|IpAddrsNum|Integer|Yes|No|The number of IP addresses available for the access node. Valid values: 1 to 10. Default value: 2. If you need more IP addresses, submit a ticket.|None|
|UisId|String|Yes|No|The ID of the UIS instance to which the access node will belong.|None|
|UisNodeBandwidth|Integer|Yes|Yes|The Internet bandwidth of the access node. Unit: Mbit/s. Default value: 20.|Minimum value: 1|
|Description|String|No|Yes|The description of the access node.|None|

## Response parameters {#section_il5_9m6_2vd .section}

**Fn::GetAtt**

-   UisNodeId: the ID of the access node.
-   UisNodeIps: The list of IP addresses available for the access node.
-   UisNodeActiveIps: The list of active IP addresses available for the access node.

## Examples {#section_zhq_syz_lfb .section}

``` {#codeblock_3ap_5bd_ea1 .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "UisNode": {
      "Type": "ALIYUN::UIS::UisNode",
      "Properties": {
        "Description": {
          "Ref": "Description"
        },
        "UisNodeAreaId": {
          "Ref": "UisNodeAreaId"
        },
        "IpAddrsNum": {
          "Ref": "IpAddrsNum"
        },
        "UisId": {
          "Ref": "UisId"
        },
        "UisNodeBandwidth": {
          "Ref": "UisNodeBandwidth"
        },
        "Name": {
          "Ref": "Name"
        }
      }
    }
  },
  "Parameters": {
    "Description": {
      "Type": "String",
      "Description": "The description of the access node."
    },
    "UisNodeAreaId": {
      "Type": "String",
      "Description": "Specifies the region ID of the node. You can query the supported regions through the DescribeRegions operation."
    },
    "IpAddrsNum": {
      "Default": 2,
      "Type": "Number",
      "Description": "The number of IP addresses available for the access node. Valid values: 1 to 10. Default value: 2. If you need more IP addresses, submit a ticket.",
      "MinValue": 2
    },
    "UisId": {
      "Type": "String",
      "Description": "The ID of the UIS instance to which the access node will belong."
    },
    "UisNodeBandwidth": {
      "Default": 20,
      "Type": "Number",
      "Description": "The Internet bandwidth of the access node.\n If you do not specify a bandwidth, the default value is 20 Mbit/s.",
      "MinValue": 1
    },
    "Name": {
      "Type": "String",
      "Description": "The name of the access node."
    }
  },
  "Outputs": {
    "UisNodeId": {
      "Description": "The ID of the access node.",
      "Value": {
        "Fn::GetAtt": [
          "UisNode",
          "UisNodeId"
        ]
      }
    },
    "UisNodeIps": {
      "Description": "The list of IP addresses available for the access node.",
      "Value": {
        "Fn::GetAtt": [
          "UisNode",
          "UisNodeIps"
        ]
      }
    },
    "UisNodeActiveIps": {
      "Description": "The list of active IP addresses available for the access node.",
      "Value": {
        "Fn::GetAtt": [
          "UisNode",
          "UisNodeActiveIps"
        ]
      }
    }
  }
}
```

