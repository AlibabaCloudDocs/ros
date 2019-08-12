# ALIYUN::ECS::LaunchTemplate {#concept_xsc_jmm_4fb .concept}

ALIYUN::ECS::LaunchTemplate类型可用于创建ECS实例启动模板。

## 语法 {#section_xyg_tn2_lfb .section}

``` {#codeblock_2sd_iv8_2q4 .language-json}
{
  "Type": "ALIYUN::ECS::LaunchTemplate",
  "Properties": {
    "LaunchTemplateName": String,
    "VersionDescription": String,
    "ImageId": String,
    "InstanceType": String,
    "SecurityGroupId": String,
    "NetworkType": String,
    "VSwitchId": String,
    "InstanceName": String,
    "Description": String,
    "InternetMaxBandwidthIn": Integer,
    "InternetMaxBandwidthOut": Integer,
    "HostName": String,
    "ZoneId": String,
    "SystemDiskCategory": String,
    "SystemDiskSize": Number,
    "SystemDiskDiskName": String,
    "SystemDiskDescription": String,
    "IoOptimized": String,
    "InternetChargeType": String,
    "UserData": String,
    "KeyPairName": String,
    "RamRoleName": String,
    "AutoReleaseTime": String,
    "SpotStrategy": String,
    "SpotPriceLimit": String,
    "SecurityEnhancementStrategy": String,
    "DiskMappings": List,
    "NetworkInterfaces": List,
    "Tags": List,
    "TemplateTags": List
  }
}
```

## 属性 {#section_cgd_53n_4fb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|LaunchTemplateName|String|是|否|实例启动模板名称。|长度为\[2, 128\]个英文或中文字符。必须以大小字母或中文开头，不能以http://和https://开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。|
|VersionDescription|String|否|否|实例启动模板版本1描述。|长度为\[2, 256\]个英文或中文字符，不能以http://和https://开头。|
|ImageId|String|否|否|镜像ID。|无|
|InstanceType|String|否|否|实例类型。|无|
|SecurityGroupId|String|否|否|安全组ID。|无|
|NetworkType|String|否|否|实例网络类型。| 取值范围：

 classic：经典网络。

 vpc：VPC网络。

 |
|VSwitchId|String|否|否|创建VPC类型实例时需要指定虚拟交换机ID。|无|
|InstanceName|String|否|否|实例名称。|长度为\[2, 128\]个英文或中文字符。必须以大小字母或中文开头，不能以http://和https://开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。|
|Description|String|否|否|实例描述。|长度为\[2, 256\]个英文或中文字符，不能以http://和https://开头。|
|InternetMaxBandwidthIn|Integer|否|否|公网入带宽最大值，单位为Mbit/s。|取值范围：\[1,200\]。|
|InternetMaxBandwidthOut|Integer|否|否|公网出带宽最大值，单位为Mbit/s。|取值范围：\[0, 100\]。|
|HostName|String|否|否|实例主机名。| 点号（.）和短横线（-）不能作为首尾字符，更不能连续使用。

 Windows实例：

 字符长度为\[2, 15\]，不支持点号（.），不能全是数字。允许大小写英文字母、数字和短横线（-）。

 其他类型实例（Linux等）：

 字符长度为\[2, 64\]，支持多个点号（.），点之间为一段，每段允许大小写英文字母、数字和短横线（-）。

 |
|ZoneId|String|否|否|实例所属的可用区ID。|无|
|SystemDiskCategory|String|否|否|系统盘的磁盘种类。|取值范围： cloud：普通云盘。

 cloud\_efficiency：高效云盘。 cloud\_ssd：SSD云盘。

 ephemeral\_ssd：本地SSD盘。

 |
|SystemDiskSize|Number|否|否|系统盘大小，单位为GiB。|取值范围：\[20, 500\]|
|SystemDiskDiskName|String|否|否|系统盘名称。|长度为\[2, 128\]个英文或中文字符。必须以大小字母或中文开头，不能以http://和https://开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。|
|SystemDiskDescription|String|否|否|系统盘描述。|长度为\[2, 256\]个英文或中文字符，不能以http://和https://开头。|
|IoOptimized|String|否|否|是否为I/O优化实例。| 取值范围：

 none：非I/O优化。

 optimized：I/O优化。

 |
|InternetChargeType|String|否|否|网络付费类型。| 取值范围：

 PayByBandwidth：按带宽计费。

 PayByTraffic：按流量计费。

 |
|UserData|String|否|否|实例自定义数据。|需要以Base64方式编码，原始数据最多为16 KB。|
|KeyPairName|String|否|否|密钥对名称。|Windows实例，忽略该参数。默认为空。即使填写了该参数，仍旧只执行Password的内容。Linux实例的密码登录方式会被初始化成禁止。|
|RamRoleName|String|否|否|实例RAM角色名称。|无|
|AutoReleaseTime|String|否|否|实例自动释放时间。|按照ISO8601标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。|
|SpotStrategy|String|否|否|后付费实例的抢占策略。| 当创建实例接口中的InstanceChargeType参数取值为PostPaid时为生效。

 取值范围：

 NoSpot：正常按量付费实例。

 SpotWithPriceLimit：设置上限价格的抢占式实例。

 SpotAsPriceGo：系统自动出价，最高按量付费价格。

 |
|SpotPriceLimit|String|否|否|设置实例的每小时最高价格。|支持最多3位小数。|
|SecurityEnhancementStrategy|String|否|否|是否开启安全加固。| 取值范围：

 Active：启用。

 Deactive：不启用。

 |
|DiskMappings|List|否|否|数据盘列表。|最多16个。|
|NetworkInterfaces|List|否|否|弹性网卡列表。|最多8个。|
|Tags|List|否|否|实例、安全组、磁盘和网卡的标签列表|最多20个|
|TemplateTags|List|否|否|启动模板的标签列表。|最多20个。|

## DiskMappings语法 {#section_ztl_jmn_4fb .section}

``` {#codeblock_efk_3ih_jx9 .language-json}
"DiskMappings": [
  {
    "Category": String,
    "DiskName": String,
    "Description": String,
    "SnapshotId": String,
    "Size": String,
    "Encrypted": String,
    "DeleteWithInstance": String
  }
]
```

## DiskMappings属性 {#section_p35_rmn_4fb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Category|String|否|否|数据盘的磁盘种类。| 取值范围：

 cloud：普通云盘。

 cloud\_efficiency：高效云盘。

 cloud\_ssd：SSD云盘。

 ephemeral\_ssd：本地SSD盘。

 |
|DiskName|String|否|否|数据盘名称。|长度为\[2, 128\]个英文或中文字符。必须以大小字母或中文开头，不能以http://和https://开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。|
|Description|String|否|否|数据盘描述。|长度为\[2, 256\]个英文或中文字符，不能以http://和https://开头。|
|SnapshotId|String|否|否|创建数据盘使用的快照。|无|
|Size|String|否|否|系统盘大小，单位为GiB。| 取值范围：

 cloud：\[5, 2000\]。

 cloud\_efficiency：\[20, 32768\]。

 cloud\_ssd：\[20, 32768\]。

 ephemeral\_ssd：\[5, 800\]。

 |
|Encrypted|Boolean|否|否|是否加密数据盘。|无|
|DeleteWithInstance|Boolean|否|否|数据盘是否随实例释放而释放。|无|

## NetworkInterfaces语法 {#section_uq1_ymn_4fb .section}

``` {#codeblock_1mp_sd4_i0g .language-json}
"NetworkInterfaces": [
  {
    "PrimaryIpAddress": String,
    "VSwitchId": String,
    "SecurityGroupId": String,
    "NetworkInterfaceName": String,
    "Description": String
  }
]
```

## NetworkInterfaces属性 {#section_bs3_2nn_4fb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|PrimaryIpAddress|String|否|否|弹性网卡的主私有IP地址。|无|
|VSwitchId|String|否|否|弹性网卡所属的虚拟交换机ID。|无|
|SecurityGroupId|String|否|否|弹性网卡所属的安全组ID。|无|
|NetworkInterfaceName|String|否|否|弹性网卡名称。|无|
|Description|String|否|否|弹性网卡描述信息。|长度为\[2, 256\]个英文或中文字符，不能以http://和https://开头。|

## Tags语法 {#section_g5w_jnn_4fb .section}

``` {#codeblock_adv_z3y_ysm .language-json}
"Tags": [
  {
    "Value": String,
    "Key": String
  }
]
```

## Tags属性 {#section_e2f_vnn_4fb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|key|String|是|否|无|无|
|value|String|否|否|无|无|

## TemplateTags语法 {#section_oph_24n_4fb .section}

``` {#codeblock_55g_enf_2bq .language-json}
"TemplateTags": [
  {
    "Value": String,
    "Key": String
  }
]
```

## TemplateTags属性 {#section_fcq_n4n_4fb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|key|String|是|否|无|无|
|value|String|否|否|无|无|

## 返回值 {#section_fsg_t4n_4fb .section}

 **Fn::GetAtt** 

-   LaunchTemplateId： 实例启动模板ID。
-   LaunchTemplateName：实例启动模板名称。
-   DefaultVersionNumber：实例启动模板默认版本号。
-   LatestVersionNumber：实例启动模板最新版本号。

## 示例 {#section_klp_54n_4fb .section}

``` {#codeblock_iuh_fde_2yc}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "Template1": {
      "Type": "ALIYUN::ECS::LaunchTemplate",
      "Properties": {
        "LaunchTemplateName": "MyTemplate",
        "VersionDescription": "Launch template with all properties set",
        "ImageId": "m-2ze9uqi7wo61hwep5q52",
        "InstanceType": "ecs.n4.small",
        "SecurityGroupId": "sg-2ze8yxgempcdsq3iucsi",
        "NetworkType": "vpc",
        "VSwitchId": "vsw-2zei67xd9nhcqxzec7qt7",
        "InstanceName": "InstanceName",
        "Description": "Description of template",
        "InternetMaxBandwidthIn": 100,
        "InternetMaxBandwidthOut": 200,
        "HostName": "tttinfo",
        "ZoneId": "cn-beijing-a",
        "SystemDiskCategory": "cloud_ssd",
        "SystemDiskSize": "40",
        "SystemDiskDiskName": "TheSystemDiskName",
        "SystemDiskDescription": "The system disk description",
        "IoOptimized": "optimized",
        "InternetChargeType": "PayByBandwidth",
        "UserData": "dGhpcyBpcyBhIHVzZXIgZGF0YSBleG1hcGxl",
        "KeyPairName": "ThisIsKeyPair",
        "RamRoleName": "ThisIsRamRole",
        "AutoReleaseTime": "2050-10-01T00:00:00Z",
        "SpotStrategy": "SpotWithPriceLimit",
        "SpotPriceLimit": "100.001",
        "SecurityEnhancementStrategy": "Active",
        "DiskMappings": [
          {
            "Category": "cloud_ssd",
            "Size": 40,
            "SnapshotId": "s-2ze1fr2bipove27bn9mz",
            "Encrypted": true,
            "DiskName": "dataDisk1",
            "Description": "I am data disk 1",
            "DeleteWithInstance": true
      },
      {
            "Category": "cloud_efficiency",
            "Size": 20,
            "SnapshotId": "s-2ze4k0w8b33mlsqu4tl6",
            "Encrypted": false,
            "DiskName": "dataDisk2",
            "Description": "I am data disk 2",
            "DeleteWithInstance": true
       }
     ],
     "NetworkInterfaces": [
       {
            "PrimaryIpAddress": "10.10.1.1",
            "VSwitchId": "vsw-2zetgeiqlemyok9z5j2em",
            "SecurityGroupId": "sg-2ze8yxgempcdsq3iucsi",
            "NetworkInterfaceName": "my-eni1",
            "Description": "My eni 1"
        },
     ],
     "Tags": [
          {
            "Key": "key1",
            "Value": "value1"
          },
          {
            "Key": "key2",
            "Value": "value2"
          }
         ],
     "TemplateTags": [
       {
            "Key": "templateKey1",
            "Value": "templateValue1"
             },
           {
            "Key": "templateKey2",
            "Value": "templateValue2"
           }
       ]
       }
     }
  },
  "Outputs": {
      "LaunchTemplateId": {
          "Value": {"Fn::GetAtt": ["Template1","LaunchTemplateId"]}
    },
   "LaunchTemplateName": {
        "Value": {"Fn::GetAtt": ["Template1","LaunchTemplateName"]}
    },
   "DefaultVersionNumber": {
          "Value": {"Fn::GetAtt": ["Template1","DefaultVersionNumber"]}
    },
   "LatestVersionNumber": {
          "Value": {"Fn::GetAtt": ["Template1","LatestVersionNumber"]}
    }
  }
}
```

