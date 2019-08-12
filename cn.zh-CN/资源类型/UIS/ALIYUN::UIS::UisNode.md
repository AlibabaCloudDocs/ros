# ALIYUN::UIS::UisNode {#concept_12345_zh .concept}

ALIYUN::UIS::UisNode类型为已创建的实例添加上车点实例。

## 语法 {#section_bnr_dxz_lfb .section}

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

## 属性 {#section_xwy_z5d_pg6 .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Name|String|否|是|上车点实例的名称。|无。|
|UisNodeAreaId|String|是|否|指定节点的地域ID。您可通过DescribeRegions接口查询支持的地域。|无。|
|IpAddrsNum|Integer|是|否|该上车点可用的IP数量。默认值为2，最大10个数，您如果需要更多配额，请提交工单。|无。|
|UisId|String|是|否|上车点所属的实例ID。|无。|
|UisNodeBandwidth|Integer|是|是|指定此上车点的带宽带宽值，即互联网带宽。如果不指定带宽，默认值20Mbps。|最小为1。|
|Description|String|否|是|上车点实例的描述。|无。|

## 返回值 {#section_il5_9m6_2vd .section}

**Fn::GetAtt**

-   UisNodeId: 实例的节点ID。
-   UisNodeIps: 节点IP列表。
-   UisNodeActiveIps: 节点活动IP列表。

## 示例 {#section_zhq_syz_lfb .section}

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
      "Description": "Description of the instance of the boarding point."
    },
    "UisNodeAreaId": {
      "Type": "String",
      "Description": "Specifies the territory ID of the node. You can query the supported territories through the DescribeRegions interface."
    },
    "IpAddrsNum": {
      "Default": 2,
      "Type": "Number",
      "Description": "The number of IPs available at the boarding point. The default is 2, the maximum is 10, if you need more quota, please submit the work order.",
      "MinValue": 2
    },
    "UisId": {
      "Type": "String",
      "Description": "The instance ID to which the boarding point belongs."
    },
    "UisNodeBandwidth": {
      "Default": 20,
      "Type": "Number",
      "Description": "Specify the bandwidth bandwidth value for this pick-up point, even if the Internet bandwidth.\nIf you do not specify a bandwidth, the default value is 20Mbps.",
      "MinValue": 1
    },
    "Name": {
      "Type": "String",
      "Description": "The name of the instance of the boarding point."
    }
  },
  "Outputs": {
    "UisNodeId": {
      "Description": "The node ID of the instance.",
      "Value": {
        "Fn::GetAtt": [
          "UisNode",
          "UisNodeId"
        ]
      }
    },
    "UisNodeIps": {
      "Description": "The node IP list.",
      "Value": {
        "Fn::GetAtt": [
          "UisNode",
          "UisNodeIps"
        ]
      }
    },
    "UisNodeActiveIps": {
      "Description": "The node active IP list.",
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

