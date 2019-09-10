# ALIYUN::ElasticSearch::Instance {#concept_xsc_jmm_4fb .concept}

ALIYUN::ElasticSearch::Instance类型用于创建ElasticSearch实例。

## 语法 {#section_bnr_dxz_lfb .section}

``` {#codeblock_8m6_63v_fto .language-json}
{
  "Type": "ALIYUN::ElasticSearch::Instance",
  "Properties": {
    "KibanaWhitelist": List,
    "PublicWhitelist": List,
    "VSwitchId": String,
    "InstanceChargeType": String,
    "Period": Integer,
    "Version": String,
    "DataNode": Map,
    "PrivateWhitelist": List,
    "Password": String,
    "MasterNode": Map,
    "Description": String
  }
}
```

## 属性 {#section_bnx_j8u_y94 .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|KibanaWhitelist|List|否|是|设置Kibana的IP白名单。|无。|
|PublicWhitelist|List|否|是|设置实例的公网IP白名单。|无。|
|VSwitchId|String|是|否|虚拟交换机id。|无。|
|InstanceChargeType|String|否|否|实例付费类型。|可用值: PrePaid, PostPaid。|
|Period|Integer|否|否|购买Elasticsearch实例的持续时间\(以月为单位\)。当为InstanceChargeType时，有效值:\[1~9\]，12,24,36。默认为1。|可用值: 1, 2, 3, 4, 5, 6, 7, 8, 9, 12, 24, 36。|
|Version|String|是|否|Elasticsearch版本。|可用值: 5.5.3\_with\_X-Pack, 6.3\_with\_X-Pack, 6.7\_with\_X-Pack|
|DataNode|Map|是|是|Elasticsearch集群的数据节点设置。|无。|
|PrivateWhitelist|List|否|是|在VPC网络中设置实例的IP白名单。|无。|
|Password|String|是|是|实例的密码。密码长度可以是8到32个字符，并且必须同时包含三项大写、小写字母、数字和特殊字符\(!@\#$%&\*\(\)\_+-=\)。|无。|
|MasterNode|Map|否|是|主节点设置。如果指定，将创建专用主节点。|无。|
|Description|String|否|是|实例的描述。0-30个字符组成的字符串。它可以包含数字、字母、下划线、\(\_\)和连字符\(-\)。它必须以字母、数字或汉字开头。|无。|

## DataNode 语法 {#section_xwa_bbe_xpe .section}

``` {#codeblock_lf5_0eb_ae1 .language-json}
"DataNode": {
  "Amount": Integer,
  "DiskSize": Integer,
  "Spec": String,
  "DiskType": String
}
```

## DataNode 属性 {#section_427_fa1_6fy .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Amount|Integer|是|是|Elasticsearch集群的数据节点数量在2-50范围内。|无。|
|DiskSize|Integer|是|是|单数据节点存储空间。cloud\_ssd: 最多支持2048 GiB \(2 TB\)。cloud\_efficiency:最多支持5120 GiB \(5 TB\)。如果要存储的数据大于2048 GiB，cloud\_efficiency只能支持以下数据大小\(GiB\):\[2560、3072、3584、4096、4608、5120\]。|无。|
|Spec|String|是|是|Elasticsearch实例的数据节点规格。|无。|
|DiskType|String|是|是|数据节点磁盘类型。支持的值:cloud\_ssd、cloud\_efficiency。|可用值: cloud\_ssd, cloud\_efficiency。|

## MasterNode 语法 {#section_wg3_w5s_qsd .section}

``` {#codeblock_3fe_mmh_k6r .language-json}
"MasterNode": {
  "Amount": Integer,
  "DiskSize": Integer,
  "Spec": String,
  "DiskType": String
}
```

## MasterNode 属性 {#section_hk7_njb_52o .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Amount|Integer|否|是|主节点数量。默认为3。|无。|
|DiskSize|Integer|否|否|主节点存储空间。默认为20。|无。|
|Spec|String|是|否|主节点规格。|无。|
|DiskType|String|否|否|主节点磁盘类型。|无。|

## 返回值 {#section_mvy_7tq_zfe .section}

Fn::GetAtt

-   Status：Elasticsearch实例状态。包括active、activating、inactive。有些操作在状态不活跃时被拒绝。
-   KibanaDomain：Kibana控制台域名（支持Internet访问）。
-   Domain：实例连接域名（仅支持VPC网络访问）。
-   InstanceId：Elasticsearch实例的ID。
-   KibanaPort：Kibana控制端口。
-   Port：实例连接端口。

## 示例 {#section_zhq_syz_lfb .section}

``` {#codeblock_0ns_thh_xdx .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "Instance": {
      "Type": "ALIYUN::ElasticSearch::Instance",
      "Properties": {
        "PrivateWhitelist": {
          "Fn::Split": [
            ",",
            {
              "Ref": "PrivateWhitelist"
            }
          ]
        },
        "DataNode": {
          "Ref": "DataNode"
        },
        "PublicWhitelist": {
          "Fn::Split": [
            ",",
            {
              "Ref": "PublicWhitelist"
            }
          ]
        },
        "InstanceChargeType": {
          "Ref": "InstanceChargeType"
        },
        "Period": {
          "Ref": "Period"
        },
        "Version": {
          "Ref": "Version"
        },
        "VSwitchId": {
          "Ref": "VSwitchId"
        },
        "KibanaWhitelist": {
          "Fn::Split": [
            ",",
            {
              "Ref": "KibanaWhitelist"
            }
          ]
        },
        "Password": {
          "Ref": "Password"
        },
        "MasterNode": {
          "Ref": "MasterNode"
        },
        "Description": {
          "Ref": "Description"
        }
      }
    }
  },
  "Parameters": {
    "PrivateWhitelist": {
      "Type": "CommaDelimitedList",
      "Description": "Set the instance's IP whitelist in VPC network."
    },
    "DataNode": {
      "Type": "Json",
      "Description": "The Elasticsearch cluster's data node setting."
    },
    "PublicWhitelist": {
      "Type": "CommaDelimitedList",
      "Description": "Set the instance's IP whitelist in Internet."
    },
    "InstanceChargeType": {
      "Default": "PostPaid",
      "Type": "String",
      "Description": "Valid values are PrePaid, PostPaid, Default to PostPaid.",
      "AllowedValues": [
        "PrePaid",
        "PostPaid"
      ]
    },
    "Period": {
      "Default": 1,
      "Type": "Number",
      "Description": "The duration that you will buy Elasticsearch instance (in month). It is valid when instance_charge_type is PrePaid. Valid values: [1~9], 12, 24, 36. Default to 1.",
      "AllowedValues": [
        1,
        2,
        3,
        4,
        5,
        6,
        7,
        8,
        9,
        12,
        24,
        36
      ]
    },
    "Version": {
      "Type": "String",
      "Description": "Elasticsearch version. Supported values: 5.5.3_with_X-Pack, 6.3_with_X-Pack and 6.7_with_X-Pack.",
      "AllowedValues": [
        "5.5.3_with_X-Pack",
        "6.3_with_X-Pack",
        "6.7_with_X-Pack"
      ]
    },
    "VSwitchId": {
      "Type": "String",
      "Description": "The ID of VSwitch."
    },
    "KibanaWhitelist": {
      "Type": "CommaDelimitedList",
      "Description": "Set the Kibana's IP whitelist in internet network."
    },
    "Password": {
      "Type": "String",
      "Description": "The password of the instance. The password can be 8 to 32 characters in length and must contain three of the following conditions: uppercase letters, lowercase letters, numbers, and special characters (!@#$%&*()_+-=)."
    },
    "MasterNode": {
      "Type": "Json",
      "Description": "The dedicated master node setting. If specified, dedicated master node will be created."
    },
    "Description": {
      "Type": "String",
      "Description": "The description of instance. It a string of 0 to 30 characters. It can contain numbers, letters, underscores, (_) and hyphens (-). It must start with a letter, a number or Chinese character.",
      "MaxLength": 30
    }
  },
  "Outputs": {
    "Status": {
      "Description": "The Elasticsearch instance status. Includes active, activating, inactive. Some operations are denied when status is not active.",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "Status"
        ]
      }
    },
    "KibanaDomain": {
      "Description": "Kibana console domain (Internet access supported).",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "KibanaDomain"
        ]
      }
    },
    "Domain": {
      "Description": "Instance connection domain (only VPC network access supported).",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "Domain"
        ]
      }
    },
    "InstanceId": {
      "Description": "The ID of the Elasticsearch instance.",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "InstanceId"
        ]
      }
    },
    "KibanaPort": {
      "Description": "Kibana console port.",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "KibanaPort"
        ]
      }
    },
    "Port": {
      "Description": " Instance connection port.",
      "Value": {
        "Fn::GetAtt": [
          "Instance",
          "Port"
        ]
      }
    }
  }
}
```

