# ALIYUN::EMR::Cluster {#concept_xsc_jmm_4fb .concept}

ALIYUN::EMR::Cluster is used to create an E-MapReduce cluster.

## Syntax {#section_bnr_dxz_lfb .section}

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

## Properties {#section_ydp_4z7_cl4 .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|SshEnable|Boolean|No|No|Specifies whether to enable SSH.|None|
|EasEnable|Boolean|No|No|Specifies whether the cluster is a high-security cluster.|None|
|WhiteListType|String|No|No|Not required.|None|
|InitCustomHiveMetaDB|Boolean|No|No|A reserved parameter. Not required.|None|
|IoOptimized|Boolean|No|No|Specifies whether to enable I/O optimization.|Valid values: true and false. Default value: true.|
|HostGroup|List|Yes|No|The list of instances in the host group.|None|
|Config|List|No|No|The list of custom configuration items.|None|
|KeyPairName|String|No|No|The name of the key pair.|None|
|VpcId|String|No|No|VpcID|This parameter is required when the NetType parameter is set to vpc.|
|AutoRenew|Boolean|No|No|Specifies whether to automatically renew the subscription cluster.|None|
|RelatedClusterId|String|No|No|The ID of the primary cluster when the cluster that you create is a gateway cluster.|None|
|BootstrapAction|List|No|No|The list of bootstrap actions.|None|
|InstanceGeneration|String|No|No|The generation of ECS instances in the cluster.|None|
|VSwitchId|String|No|No|The ID of the VSwitch.|This parameter is required when the NetType parameter is set to vpc.|
|NetType|String|Yes|No|The network type.|None|
|UserDefinedEmrEcsRole|String|No|No|The role that is assigned to EMR to call ECS resources.|None|
|Name|String|Yes|Yes|The name of the cluster.|The name must be 1 to 64 characters in length and can only contain letters, digits, hyphens \(-\), and underscores \(\_\).|
|ClusterType|String|Yes|No|The type of the cluster.|Valid values: HADOOP, KAFKA, DRUID, ZOOKEEPER, DATA\_SCIENCE, and GATEWAY.|
|ZoneId|String|Yes|No|The ID of the zone where the cluster resides.| -   Valid value for the China \(Hangzhou\) region: cn-hangzhou-b.
-   Valid values for the China \(Beijing\) region: cn-beijing-a, cn-beijing-b, and cn-beijing-c.

 |
|IsOpenPublicIp|Boolean|No|No|Specifies whether to assign a public IP address.|If you specify this parameter as true, a public IP address with a bandwidth of 8 Mbit/s is assigned.|
|OptionSoftWareList|List|No|No|The list of optional services.|None|
|Configurations|String|No|No|Not required.|None|
|MasterPwd|String|No|No|The SSH password used to connect to the master node.|The password must be 8 to 30 characters in length and must contain at least three types of the following characters: uppercase letters, lowercase letters, digits, and special characters.|
|MachineType|String|No|No|The type of instances in the cluster.|None|
|EmrVer|String|Yes|No|The version of EMR.|None|
|SecurityGroupName|String|No|No|The name of the security group to create.|When creating a security group, you must specify the name of the security group if you do not specify the ID of the security group. After the cluster is created, you can view the ID of the created security group on the Cluster Management page. The default security group policy is applied to this security group. The default policy only allows inbound traffic through port 22 but allows outbound traffic through all ports.|
|DepositType|String|No|No|The hosting type.|None|
|SecurityGroupId|String|No|No|The ID of the security group. You can create a security group in the ECS console and use the ID of this security group.|If you are using an existing security group, the default security group policy is applied to this security group. The default policy only allows inbound traffic through port 22 but allows outbound traffic through all ports.|
|LogPath|String|No|No|The log path in OSS.|None|
|Period|Integer|No|No|The subscription period.| -   Valid values: 1, 2, 3, 4, 5, 6, 7, 8, 9, 12, 24, and 36. Unit: months.
-   This parameter is required when the ChargeType parameter is set to PrePaid.

 |
|HighAvailabilityEnable|Boolean|No|No|Specifies whether the cluster is a high-availability cluster.|If high availability is enabled, a minimum of two master nodes are required.|
|UseCustomHiveMetaDB|Boolean|No|No|A reserved parameter. Not required.|None|
|UserInfo|List|No|No|The information you provide when creating the cluster.|None|
|ChargeType|String|Yes|No|The billing method.|Valid values: PostPaid and PrePaid.|
|AuthorizeContent|String|No|No|Not required.|None|
|UseLocalMetaDb|Boolean|Yes|No|Specifies whether to use the local Hive metadatabase.|None|

## HostGroup syntax {#section_f06_zn9_foc .section}

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

## HostGroup properties {#section_r77_3ze_on1 .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Comment|String|No|No|A reserved parameter. Not required.|None|
|SysDiskType|String|Yes|No|The system disk type of the host group.|None|
|DiskCapacity|Integer|Yes|No|The data disk capacity of the host group.|None|
|NodeCount|Integer|Yes|No|The number of nodes in the host group.|None|
|ClusterId|String|No|No|A reserved parameter. Not required.|None|
|DiskCount|Integer|Yes|No|The number of data disks in the host group.|None|
|CreateType|String|No|No|A reserved parameter. Not required.|None|
|DiskType|String|Yes|No|The data disk type of the host group.|Valid values: CLOUD, CLOUD\_EFFICIENCY, and CLOUD\_SSD.|
|AutoRenew|Boolean|No|No|Specifies whether to automatically renew the subscription cluster.|None|
|HostGroupType|String|Yes|No|The type of the host group.|Valid values: MASTER, CORE, and TASK.|
|SysDiskCapacity|Integer|Yes|No|The system disk capacity of the host group.|None|
|VSwitchId|String|No|No|The ID of the VSwitch.|This parameter is required when the NetType parameter is set to vpc.|
|ChargeType|String|Yes|No|The billing method.|Valid values: PostPaid and PrePaid.|
|Period|Integer|No|No|The subscription period.| -   Valid values: 1, 2, 3, 4, 5, 6, 7, 8, 9, 12, 24, and 36. Unit: months.
-   This parameter is required when the ChargeType parameter is set to PrePaid.

 |
|HostKeyPairName|String|No|No|The key pair name of the host group.|This parameter only applies to gateway clusters.|
|HostPassword|String|No|No|The password of the host.|This parameter only applies to gateway clusters.|
|HostGroupId|String|No|No|A reserved parameter.|None|
|InstanceType|String|Yes|No|The instance type of the host group.|None|
|GpuDriver|String|No|No|The GPU driver.|None|
|HostGroupName|String|No|No|The name of the host group.|None|

## Config syntax {#section_hnw_gcn_xnz .section}

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

## Config properties {#section_75b_6yf_d0t .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Encrypt|String|No|No|A reserved parameter.|None|
|ConfigKey|String|No|No|The key of the custom configuration item.|None|
|FileName|String|No|No|The name of the file that contains the custom configuration item.|None|
|ServiceName|String|No|No|The service name that is configured by using the custom configuration item. Specify the entire name in uppercase.|None|
|Replace|String|No|No|A reserved parameter.|None|
|ConfigValue|String|No|No|The value of the custom configuration item.|None|

## BootstrapAction syntax {#section_d53_78b_e4y .section}

``` {#codeblock_15f_694_vhe .language-json}
"BootstrapAction": [
  {
    "Path": String,
    "Name": String,
    "Arg": String
  }
]
```

## BootstrapAction properties {#section_w14_qkq_a98 .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Path|String|No|No|The path where the bootstrap action script is stored.|None|
|Name|String|No|No|The name of the bootstrap action.|None|
|Arg|String|No|No|The argument that you pass into the bootstrap action.|None|

## UserInfo syntax {#section_v1g_hgk_mcc .section}

``` {#codeblock_08q_2b5_pgj .language-json}
"UserInfo": [
  {
    "UserName": String,
    "Password": String,
    "UserId": String
  }
]
```

## UserInfo properties {#section_crb_efy_ska .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|UserName|String|No|No|The username for Knox.|None|
|Password|String|No|No|The password that is used to log on to the cluster.|None|
|UserId|String|No|No|The ID of the Alibaba Cloud account for Knox.|None|

## Response parameters {#section_4jt_kuc_6pj .section}

Fn::GetAtt

-   ClusterId: the ID of the cluster.

## Examples {#section_zhq_syz_lfb .section}

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
      "Description": "Indicates weather I/O optimization is enabled. Default value: true.",
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
      "Description": "The type of the cluster. Allowed values: HADOOP, KAFKA, DRUID, ZOOKEEPER, DATA_SCIENCE, GATEWAY.",
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

