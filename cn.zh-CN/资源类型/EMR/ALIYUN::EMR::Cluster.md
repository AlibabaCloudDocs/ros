# ALIYUN::EMR::Cluster {#concept_xsc_jmm_4fb .concept}

ALIYUN::EMR::Cluster类型用于创建一个E-MapReduce集群。

## 语法 {#section_bnr_dxz_lfb .section}

``` {#codeblock_z7v_btq_xlj .language-json}
{
  "Type": "ALIYUN::EMR::Cluster",
  "Properties": {
    "SshEnable": Boolean,
    "EasEnable": Boolean,
    "WhiteListType": String,
    "InitCustomHiveMetaDB": Boolean,
    "IoOptimized": Boolean,
    "HostGroup": List,
    "Config": List,
    "KeyPairName": String,
    "VpcId": String,
    "AutoRenew": Boolean,
    "RelatedClusterId": String,
    "BootstrapAction": List,
    "InstanceGeneration": String,
    "VSwitchId": String,
    "NetType": String,
    "UserDefinedEmrEcsRole": String,
    "Name": String,
    "ClusterType": String,
    "ZoneId": String,
    "IsOpenPublicIp": Boolean,
    "OptionSoftWareList": List,
    "Configurations": String,
    "MasterPwd": String,
    "MachineType": String,
    "EmrVer": String,
    "SecurityGroupName": String,
    "DepositType": String,
    "SecurityGroupId": String,
    "LogPath": String,
    "Period": Integer,
    "HighAvailabilityEnable": Boolean,
    "UseCustomHiveMetaDB": Boolean,
    "UserInfo": List,
    "ChargeType": String,
    "AuthorizeContent": String,
    "UseLocalMetaDb": Boolean
  }
}
```

## 属性 {#section_ydp_4z7_cl4 .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|SshEnable|Boolean|否|否|是否开启SSH|无|
|EasEnable|Boolean|否|否|是否高安全集群|无|
|WhiteListType|String|否|否|暂时无需填写|无|
|InitCustomHiveMetaDB|Boolean|否|否|保留字段，无需填写|无|
|IoOptimized|Boolean|否|否|是否开启IO优化|取值范围：true（默认值）、false|
|HostGroup|List|是|否|机器组|无|
|Config|List|否|否|自定义配置项|无|
|KeyPairName|String|否|否|密钥对|无|
|VpcId|String|否|否|VpcID|当NetType=vpc时，此参数为必填参数。|
|AutoRenew|Boolean|否|否|包年包月集群是否自动续费|无|
|RelatedClusterId|String|否|否|当前集群是gateway时，其关联的主集群ID|无|
|BootstrapAction|List|否|否|引导操作|无|
|InstanceGeneration|String|否|否|ECS实例分代|无|
|VSwitchId|String|否|否|交换机ID|当NetType=vpc时，此参数为必填参数。|
|NetType|String|是|否|网络类型|无|
|UserDefinedEmrEcsRole|String|否|否|用于ECS调用的EMR权限名|无|
|Name|String|是|是|集群名|只允许包含中文、字母、数字、-、\_，长度为1~64个字符。|
|ClusterType|String|是|否|集群类型|取值范围：HADOOP、KAFKA、DRUID、ZOOKEEPER、DATA\_SCIENCE、GATEWAY|
|ZoneId|String|是|否|可用区ID| -   华东1（杭州）支持：cn-hangzhou-b
-   华北2（北京）支持：cn-beijing-a、cn-beijing-b、cn-beijing-c

 |
|IsOpenPublicIp|Boolean|否|否|是否开启公网IP|若开启，则默认会带8MB的带宽。|
|OptionSoftWareList|List|否|否|可选软件列表|无|
|Configurations|String|否|否|无需填写|无|
|MasterPwd|String|否|否|Master节点SSH访问密码|需要满足ECS的密码规则：8~30个字符，且同时包含任意三项（大、小写字母，数字和特殊符号）。|
|MachineType|String|否|否|机器类型|无|
|EmrVer|String|是|否|EMR版本|无|
|SecurityGroupName|String|否|否|需要新建的安全组名称|如果不指定安全组ID，则将使用这个名字创建一个新的安全组。当集群创建完成后，可以在集群详情中看到创建的安全组ID。这个安全组将会带有默认的安全组策略：入只开放22端口，出开放所有端口。|
|DepositType|String|否|否|托管类型|无|
|SecurityGroupId|String|否|否|安全组ID，可在ECS中创建后使用。|若使用已有的安全组，会被增加上默认安全组策略：入只开放22端口，出开放所有端口。|
|LogPath|String|否|否|OSS日志路径|无|
|Period|Integer|否|否|包年包月时间| -   取值范围：1、2、3、4、5、6、7、8、9、12、24、36，单位：月
-   当ChargeType=PrePaid时，此参数为必填参数。

 |
|HighAvailabilityEnable|Boolean|否|否|是否开启高可用集群|若开启，则需要2台Master节点。|
|UseCustomHiveMetaDB|Boolean|否|否|保留字段，无需填写|无|
|UserInfo|List|否|否|用户信息|无|
|ChargeType|String|是|否|付费类型|取值范围：PostPaid（按量付费）、PrePaid（包年包月）|
|AuthorizeContent|String|否|否|暂时无需填写|无|
|UseLocalMetaDb|Boolean|是|否|是否使用本地Hive元数据库|无|

## HostGroup 语法 {#section_f06_zn9_foc .section}

``` {#codeblock_g10_x2o_wz1 .language-json}
"HostGroup": [
  {
    "Comment": String,
    "SysDiskType": String,
    "DiskCapacity": Integer,
    "NodeCount": Integer,
    "ClusterId": String,
    "DiskCount": Integer,
    "CreateType": String,
    "DiskType": String,
    "AutoRenew": Boolean,
    "HostGroupType": String,
    "SysDiskCapacity": Integer,
    "VSwitchId": String,
    "ChargeType": String,
    "Period": Integer,
    "HostKeyPairName": String,
    "HostPassword": String,
    "HostGroupId": String,
    "InstanceType": String,
    "GpuDriver": String,
    "HostGroupName": String
  }
]
```

## HostGroup 属性 {#section_r77_3ze_on1 .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Comment|String|否|否|保留字段，无需填写|无|
|SysDiskType|String|是|否|机器组的系统盘类型|无|
|DiskCapacity|Integer|是|否|机器组的数据盘容量|无|
|NodeCount|Integer|是|否|机器组节点数|无|
|ClusterId|String|否|否|保留字段，无需填写|无|
|DiskCount|Integer|是|否|机器组的数据盘数量|无|
|CreateType|String|否|否|保留字段，无需填写|无|
|DiskType|String|是|否|机器组的数据盘类型|取值范围： CLOUD、CLOUD\_EFFICIENCY、CLOUD\_SSD|
|AutoRenew|Boolean|否|否|包年包月集群是否自动续费|无|
|HostGroupType|String|是|否|机器组类型|取值范围：MASTER、CORE、TASK|
|SysDiskCapacity|Integer|是|否|机器组的系统盘容量|无|
|VSwitchId|String|否|否|交换机ID|当NetType=vpc时，此参数为必填参数。|
|ChargeType|String|是|否|付费类型|取值范围：PostPaid（按量付费）、PrePaid（包年包月）|
|Period|Integer|否|否|包年包月时间| -   取值范围：1、2、3、4、5、6、7、8、9、12、24、36，单位：月
-   当ChargeType=PrePaid时，此参数为必填参数。

 |
|HostKeyPairName|String|否|否|主机组的密钥对名称|目前只支持网关|
|HostPassword|String|否|否|主机的密码|目前只支持网关|
|HostGroupId|String|否|否|保留参数|无|
|InstanceType|String|是|否|机器组型号|无|
|GpuDriver|String|否|否|GPU驱动|无|
|HostGroupName|String|否|否|机器组名字|无|

## Config 语法 {#section_hnw_gcn_xnz .section}

``` {#codeblock_8b9_rt9_n7c .language-json}
"Config": [
  {
    "Encrypt": String,
    "ConfigKey": String,
    "FileName": String,
    "ServiceName": String,
    "Replace": String,
    "ConfigValue": String
  }
]
```

## Config 属性 {#section_75b_6yf_d0t .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Encrypt|String|否|否|保留字段|无|
|ConfigKey|String|否|否|自定义配置项的key|无|
|FileName|String|否|否|自定义配置项所属文件名|无|
|ServiceName|String|否|否|自定义配置项服务名（大写）|无|
|Replace|String|否|否|保留字段|无|
|ConfigValue|String|否|否|自定义配置项的值|无|

## BootstrapAction 语法 {#section_d53_78b_e4y .section}

``` {#codeblock_15f_694_vhe .language-json}
"BootstrapAction": [
  {
    "Path": String,
    "Name": String,
    "Arg": String
  }
]
```

## BootstrapAction 属性 {#section_w14_qkq_a98 .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Path|String|否|否|引导操作脚本路径|无|
|Name|String|否|否|引导操作名字|无|
|Arg|String|否|否|引导操作参数|无|

## UserInfo 语法 {#section_v1g_hgk_mcc .section}

``` {#codeblock_08q_2b5_pgj .language-json}
"UserInfo": [
  {
    "UserName": String,
    "Password": String,
    "UserId": String
  }
]
```

## UserInfo 属性 {#section_crb_efy_ska .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|UserName|String|否|否|knox账号用户名|无|
|Password|String|否|否|集群密码|无|
|UserId|String|否|否|knox账号的aliyun用户ID|无|

## 返回值 {#section_4jt_kuc_6pj .section}

Fn::GetAtt

-   ClusterId：集群ID

## 示例 {#section_zhq_syz_lfb .section}

``` {#codeblock_7zs_rk5_rat .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "Cluster": {
      "Type": "ALIYUN::EMR::Cluster",
      "Properties": {
        "SshEnable": {
          "Ref": "SshEnable"
        },
        "EasEnable": {
          "Ref": "EasEnable"
        },
        "WhiteListType": {
          "Ref": "WhiteListType"
        },
        "InitCustomHiveMetaDB": {
          "Ref": "InitCustomHiveMetaDB"
        },
        "IoOptimized": {
          "Ref": "IoOptimized"
        },
        "HighAvailabilityEnable": {
          "Ref": "HighAvailabilityEnable"
        },
        "Config": {
          "Ref": "Config"
        },
        "KeyPairName": {
          "Ref": "KeyPairName"
        },
        "VpcId": {
          "Ref": "VpcId"
        },
        "AutoRenew": {
          "Ref": "AutoRenew"
        },
        "RelatedClusterId": {
          "Ref": "RelatedClusterId"
        },
        "BootstrapAction": {
          "Ref": "BootstrapAction"
        },
        "InstanceGeneration": {
          "Ref": "InstanceGeneration"
        },
        "VSwitchId": {
          "Ref": "VSwitchId"
        },
        "NetType": {
          "Ref": "NetType"
        },
        "Name": {
          "Ref": "Name"
        },
        "ClusterType": {
          "Ref": "ClusterType"
        },
        "ZoneId": {
          "Ref": "ZoneId"
        },
        "IsOpenPublicIp": {
          "Ref": "IsOpenPublicIp"
        },
        "OptionSoftWareList": {
          "Ref": "OptionSoftWareList"
        },
        "Configurations": {
          "Ref": "Configurations"
        },
        "MasterPwd": {
          "Ref": "MasterPwd"
        },
        "MachineType": {
          "Ref": "MachineType"
        },
        "EmrVer": {
          "Ref": "EmrVer"
        },
        "SecurityGroupName": {
          "Ref": "SecurityGroupName"
        },
        "DepositType": {
          "Ref": "DepositType"
        },
        "HostGroup": {
          "Ref": "HostGroup"
        },
        "SecurityGroupId": {
          "Ref": "SecurityGroupId"
        },
        "LogPath": {
          "Ref": "LogPath"
        },
        "Period": {
          "Ref": "Period"
        },
        "UserDefinedEmrEcsRole": {
          "Ref": "UserDefinedEmrEcsRole"
        },
        "UseCustomHiveMetaDB": {
          "Ref": "UseCustomHiveMetaDB"
        },
        "UserInfo": {
          "Ref": "UserInfo"
        },
        "ChargeType": {
          "Ref": "ChargeType"
        },
        "AuthorizeContent": {
          "Ref": "AuthorizeContent"
        },
        "UseLocalMetaDb": {
          "Ref": "UseLocalMetaDb"
        }
      }
    }
  },
  "Parameters": {
    "SshEnable": {
      "Type": "Boolean",
      "Description": "Indicates whether SSH is enabled.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "EasEnable": {
      "Type": "Boolean",
      "Description": "Indicates whether the cluster is a high-security cluster.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "WhiteListType": {
      "Type": "String",
      "Description": "Not required."
    },
    "InitCustomHiveMetaDB": {
      "Type": "Boolean",
      "Description": "A reserved parameter. Not required.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "IoOptimized": {
      "Default": true,
      "Type": "Boolean",
      "Description": "Indicates wether I/O optimization is enabled. Default value: true.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "HighAvailabilityEnable": {
      "Type": "Boolean",
      "Description": "Indicates whether the cluster is a high-availability cluster. A value of true indicates\nthat two master nodes are required.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "Config": {
      "Type": "Json",
      "Description": ""
    },
    "KeyPairName": {
      "Type": "String",
      "Description": "The name of the key pair."
    },
    "VpcId": {
      "Type": "String",
      "Description": "The ID of the VPC. A value is required when NetType=vpc."
    },
    "AutoRenew": {
      "Type": "Boolean",
      "Description": "Indicates whether the subscription cluster is auto-renewed.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "RelatedClusterId": {
      "Type": "String",
      "Description": "The ID of the primary cluster (when the cluster that you create is a Gateway cluster)."
    },
    "BootstrapAction": {
      "Type": "Json",
      "Description": ""
    },
    "InstanceGeneration": {
      "Type": "String",
      "Description": "The generation of the ECS instances."
    },
    "VSwitchId": {
      "Type": "String",
      "Description": "The ID of the Vswitch. A value is required when NetType=vpc."
    },
    "NetType": {
      "Type": "String",
      "Description": "The type of the network."
    },
    "Name": {
      "Type": "String",
      "Description": "The name of the cluster. The name can be 1 to 64 characters in length and only contain\nChinese characters, letters, numbers, hyphens (-), and underscores (_)."
    },
    "ClusterType": {
      "Type": "String",
      "Description": "The type of the cluster. Allowd values: HADOOP, KAFKA, DRUID, ZOOKEEPER, DATA_SCIENCE, GATEWAY.",
      "AllowedValues": [
        "HADOOP",
        "KAFKA",
        "DRUID",
        "ZOOKEEPER",
        "DATA_SCIENCE",
        "GATEWAY"
      ]
    },
    "ZoneId": {
      "Type": "String",
      "Description": "The zone ID."
    },
    "IsOpenPublicIp": {
      "Type": "Boolean",
      "Description": "Indicates whether a public IP address is assigned. A value of true indicates that\na bandwidth of 8 MB is set by default.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "OptionSoftWareList": {
      "Type": "Json",
      "Description": "The list of optional services."
    },
    "Configurations": {
      "Type": "String",
      "Description": "Not required."
    },
    "MasterPwd": {
      "MinLength": 8,
      "Type": "String",
      "Description": "The SSH password for the master node. The password must meet the following requirements.\nLength constraints: Minimum length of 8 characters. Maximum length of 30 characters.\nIt must contain three types of characters (uppercase letters, lowercase letters, numbers,\nand special symbols).",
      "MaxLength": 30
    },
    "MachineType": {
      "Type": "String",
      "Description": "The type of the machine."
    },
    "EmrVer": {
      "Type": "String",
      "Description": "The version of EMR."
    },
    "SecurityGroupName": {
      "Type": "String",
      "Description": "The name of the security group to create. If the ID of the security group is not specified,\nthis name is used to create a new security group. After the cluster is created, you\ncan view the ID of the security group on the Cluster Management page. The default\nsecurity group policy is applied to this security group: Only port 22 is open at the\ninbound and all ports are open at the outbound. You need to specify either SecurityGroupId\nor SecurityGroupName."
    },
    "DepositType": {
      "Type": "String",
      "Description": "The hosting type."
    },
    "HostGroup": {
      "Type": "Json",
      "Description": ""
    },
    "SecurityGroupId": {
      "Type": "String",
      "Description": "The ID of the security group. You can create a security group in the ECS console and\nuse it. Note: If you use an existing security group, the default security group policy\nis applied to this security group: Only port 22 is open at the inbound and all ports\nare open at the outbound. You need to specify either SecurityGroupId or SecurityGroupName."
    },
    "LogPath": {
      "Type": "String",
      "Description": "The log path in OSS."
    },
    "Period": {
      "Type": "Number",
      "Description": "The length of the subscription. Unit: months. Valid values: 1, 2, 3, 4, 5, 6, 7, 8,\n9, 12, 24, and 36. A value is required when ChargeType=PrePaid.",
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
    "UserDefinedEmrEcsRole": {
      "Type": "String",
      "Description": "The role that is assigned to EMR for calling ECS resources."
    },
    "UseCustomHiveMetaDB": {
      "Type": "Boolean",
      "Description": "A reserved parameter. Not required.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    },
    "UserInfo": {
      "Type": "Json",
      "Description": ""
    },
    "ChargeType": {
      "Type": "String",
      "Description": "The billing method. Valid values: PostPaid and PrePaid. PostPaid: pay-as-you-go. PrePaid:\nsubscription.",
      "AllowedValues": [
        "PostPaid",
        "PrePaid"
      ]
    },
    "AuthorizeContent": {
      "Type": "String",
      "Description": "Not required."
    },
    "UseLocalMetaDb": {
      "Type": "Boolean",
      "Description": "Indicates whether the local Hive metadatabase is used.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    }
  },
  "Outputs": {
    "ClusterId": {
      "Description": "The ID of the cluster.",
      "Value": {
        "Fn::GetAtt": [
          "Cluster",
          "ClusterId"
        ]
      }
    }
  }
}
```

