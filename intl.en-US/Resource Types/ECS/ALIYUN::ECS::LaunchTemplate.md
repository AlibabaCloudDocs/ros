# ALIYUN::ECS::LaunchTemplate {#concept_xsc_jmm_4fb .concept}

Creates a template to launch ECS instances.

## Syntax {#section_xyg_tn2_lfb .section}

```language-json
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

## Properties {#section_cgd_53n_4fb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|LaunchTemplateName|String|Yes|No|The name of the launch template for ECS instances.|The name must be 2 to 128 characters in length, including digits, colons \(:\), underscores \(\_\), and hyphens \(-\). It must start with an uppercase letter, lowercase letter, or a Chinese character, and must not start with http:// or https://.|
|VersionDescription|String|No|No|The description for the first version of the template to launch ECS instances.|The description must be 2 to 256 characters in length and must not start with http:// or https://.|
|ImageId|String|No|No|The ID of an image used to boot the instance.|N/A|
|InstanceType|String|No|No|The type of an instance.|N/A|
|SecurityGroupId|String|No|No|The ID of a security group.|N/A|
|NetworkType|String|No|No|The network type of an instance.| Valid values:

 classic: indicates classic networks.

 vpc: indicates VPCs.

 |
|VSwitchId|String|No|No|The ID of the VSwitch that is specified when you create a VPC instance.|N/A|
|InstanceName|String|No|No|The name of an instance.|The name must be 2 to 128 characters in length, including digits, colons \(:\), underscores \(\_\), and hyphens \(-\). It must start with an uppercase letter, lowercase letter, or a Chinese character, and must not start with http:// or https://.|
|Description|String|No|No|The description of an instance.|The description must be 2 to 256 characters in length and must not start with http:// or https://.|
|InternetMaxBandwidthIn|Integer|No|No|The maximum inbound bandwidth of the public network, measured in Mbit/s.|Value range: 1 to 200.|
|InternetMaxBandwidthOut|Integer|No|No|The maximum outbound bandwidth of the public network, measured in Mbit/s.|Value range: 0 to 100.|
|HostName|String|No|No|The host name of an instance.| The name must not start or end with a period \(.\) or a hyphen \(-\) and must not contain consecutive periods \(.\) or hyphens \(-\).

 Windows instances:

 The host name must be 2 to 15 characters in length, including uppercase or lowercase letters, digits, and hyphens \(-\) and excluding periods \(.\). A host name must follow the predefined format \(only using numbers is invalid\).

 Linux instances and other instances:

 The host name must be 2 to 64 characters in length, including uppercase or lowercase letters, digits, hyphens \(-\), and periods \(.\). You can use periods \(.\) to split a name into multiple segments.

 |
|ZoneId|String|No|No|The ID of the zone where the instance is located.|N/A|
|SystemDiskCategory|String|No|No|The type of a system disk.|Valid values:cloud: indicates basic cloud disks.

cloud\_efficiency: indicates ultra cloud disks.cloud\_ssd: Indiates SSD disks.

ephemeral\_ssd: indicates local SSD disks.

|
|SystemDiskSize|Number|No|No|The capacity of a system disk, measured in GBs.|Value range: 20 to 500.|
|SystemDiskDiskName|String|No|No|The name of a system disk.|The name must be 2 to 128 characters in length, including digits, colons \(:\), underscores \(\_\), and hyphens \(-\). It must start with an uppercase letter, lowercase letter, or a Chinese character, and must not start with http:// or https://.|
|SystemDiskDescription|String|No|No|The description of a system disk.|The description must be 2 to 256 characters in length and must not start with http:// or https://.|
|IoOptimized|String|No|No|Specifies whether an instance is I/O optimized.| Valid values:

 none: indicates that the instance is I/O optimized.

 optimized: indicates that instance is not I/O optimized.

 |
|InternetChargeType|String|No|No|The network billing method.| Valid values:

 PayByBandwidth: indicates that the network is billed by bandwidth.

 PayByTraffic: indicates that the network is billed by traffic.

 |
|UserData|String|No|No|The custom data of an instance.|The data must be Base64-encoded. The upper limit of the raw data size is 16 KB.|
|KeyPairName|String|No|No|The name of a key pair.|For Windows instances, keep the default value of this parameter. This parameter is unspecified by default. Only your password is used to log on to your instance even if you have specified the KeyPairName parameter. If you specify this parameter for Linux instances, you cannot log on to the instances using the username and password.|
|RamRoleName|String|No|No|The RAM role of an instance.|N/A|
|AutoReleaseTime|String|No|No|The time scheduled for an instance to be automatically released.|The time format is yyyy-MM-ddTHH:mm:ssZ, which must use UTC and follow ISO 8601 standard.|
|SpotStrategy|String|No|No|The preemptive policy of a Pay-As-You-Go instance.| This policy only takes effect when the InstanceChargeType parameter of the API for creating an instance is set to PostPaid.

 Valid values:

 NoSpot: indicates a Pay-As-You-Go instance.

 SpotWithPriceLimit: indicates a preemptible instance with a preset upper price limit.

 SpotAsPriceGo: indicates an instance with the highest system-generated Pay-As-You-Go price.

 |
|SpotPriceLimit|String|No|No|The maximum price per hour of an instance.|The price is limited to 3 decimal places.|
|SecurityEnhancementStrategy|String|No|No|Specifies whether to enable the security enhancement feature.| Valid values:

 Active: indicates enabling the security enhancement feature.

 Deactive: indicates disabling the security enhancement feature.

 |
|DiskMappings|List|No|No|The list of data disks.|A list includes up to 16 data disks.|
|NetworkInterfaces|List|No|No|The list of elastic network interfaces \(ENIs\).|A list includes up to eight ENIs.|
|Tags|List|No|No|The list of tags for instances, security groups, disks, and ENIs.|A list includes up to 20 tags.|
|TemplateTags|List|No|No|The list of tags contained in an instance launch template.|A list can describe up to 20 tags.|

## DiskMappings syntax {#section_ztl_jmn_4fb .section}

```
"DiskMappings": [
  {
    "Category": String,
    "DiskName" : String,
    "Description": String,
    "SnapshotId" : String,
    "Size" : String
    "Encrypted" : String,
    "DeleteWithInstance" : String,
  }
]
```

## DiskMappings properties {#section_p35_rmn_4fb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Category|String|No|No|The type of a data disk.| Valid values:

 cloud: indicates basic cloud disks.

 cloud\_efficiency: indicates ultra cloud disks.

 cloud\_ssd: indicates SSD disks.

 ephemeral\_ssd: indicates local SSD disks.

 |
|DiskName|String|No|No|The name of a data disk.|The name must be 2 to 128 characters in length, including digits, colons \(:\), underscores \(\_\), and hyphens \(-\). It must start with an uppercase letter, lowercase letter, or a Chinese character, and must not start with http:// or https://.|
|Description|String|No|No|The description of a data disk.|The description must be 2 to 256 characters in length and must not start with http:// or https://.|
|SnapshotId|String|No|No|The snapshot used for creating a data disk.|N/A|
|Size|String|No|No|The capacity of a system disk, measured in GBs.| Valid values:

 cloud: 5 to 2000.

 cloud\_efficiency: 20 to 32768.

 cloud\_ssd: 20 to 32768.

 ephemeral\_ssd: 5 to 800.

 |
|Encrypted|Boolean|No|No|Specifies whether to encrypt a data disk.|N/A|
|DeleteWithInstance|Boolean|No|No|Specifies whether a data disk is released at the same time the instance is released.|N/A|

## NetworkInterfaces syntax {#section_uq1_ymn_4fb .section}

```
"NetworkInterfaces": [
  {
    "PrimaryIpAddress": String,
    "VSwitchId": String,
    "SecurityGroupId": String,
    "NetworkInterfaceName": String,
    "Description": String }
]
```

## NetworkInterface properties {#section_bs3_2nn_4fb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|PrimaryIpAddress|String|No|No|The primary private IP address of an ENI.|N/A|
|VSwitchId|String|No|No|The ID of the VSwitch associated with the ENI.|N/A|
|SecurityGroupId|String|No|No|The ID of the security group associated with the ENI.|N/A|
|NetworkInterfaceName|String|No|No|The name of the ENI.|N/A|
|Description|String|No|No|The description of the ENI.|The description must be 2 to 256 characters in length and must not start with http:// or https://.|

## Tags syntax {#section_g5w_jnn_4fb .section}

```
"Tags": [
  {
    "Value" : String,
    "Key" : String
  }
]
```

## Tag properties {#section_e2f_vnn_4fb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Key|String|Yes|No|None|N/A|
|Value|String|No|No|None|N/A|

## TemplateTag syntax {#section_oph_24n_4fb .section}

```
"TemplateTags": [
  {
    "Value" : String,
    "Key": String
  }
]
```

## TemplateTag properties {#section_fcq_n4n_4fb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Key|String|Yes|No|None|N/A|
|Value|String|No|No|None|N/A|

## Response elements {#section_fsg_t4n_4fb .section}

**Fn::GetAtt**

-   LaunchTemplateId: indicates the ID of the template for launching ECS instances.
-   LaunchTemplateName: indicates the name of the template for launching ECS instances.
-   DefaultVersionNumber: indicates the default version of the template for launching ECS instances.
-   LatestVersionNumber: indicates the latest version of template for launching ECS instances.

## Example {#section_klp_54n_4fb .section}

```
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

