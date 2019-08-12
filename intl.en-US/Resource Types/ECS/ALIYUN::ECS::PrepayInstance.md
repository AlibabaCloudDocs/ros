# ALIYUN::ECS::PrepayInstance {#concept_n23_ryt_qgb .concept}

Creates ECS instances that are billed using the subscription method.

## Syntax {#section_xyg_tn2_lfb .section}

``` {#codeblock_a4p_eb4_3h6 .language-json}
{
  "Type": "ALIYUN::ECS::PrepayInstance",
  "Properties": {
    "PeriodType": String,
    "DedicatedHostId": String,
    "RamRoleName": String,
    "IoOptimized": Boolean,
    "InternetChargeType": String,
    "PrivateIpAddress": String,
    "KeyPairName": String,
    "SystemDiskDiskName": String,
    "PeriodUnit": String,
    "Description": String,
    "Tags": List,
    "MinAmount": Integer,
    "HostName": String,
    "AutoRenewPeriod": Number,
    "ImageId": String,
    "AutoRenew": Boolean,
    "InstanceChargeType": String,
    "VSwitchId": String,
    "Password": String,
    "InstanceType": String,
    "MaxAmount": Integer,
    "SystemDiskCategory": String,
    "SystemDiskSize": Number,
    "ZoneId": String,
    "InternetMaxBandwidthOut": Integer,
    "VpcId": String,
    "InstanceName": String,
    "InternetMaxBandwidthIn": Integer,
    "UserData": String,
    "SecurityGroupId": String,
    "Period": Number,
    "AllocatePublicIP": Boolean,
    "SystemDiskDescription": String,
    "DiskMappings": List
  }
}
```

## Properties {#section_cgd_53n_4fb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|PeriodType|String|Yes|No|The billing cycle.|Valid values: Monthly | Yearly|
|DedicatedHostId|String|No|No|Specifies whether to create ECS instances that run on a dedicated host \(DDH\). If yes, specify the ID of the DDH where the ECS instances are to be created.|N/A|
|RamRoleName|String|No|No|The RAM role of an instance. You can query the RAM role of an instance by calling the ListRoles API. See [CreateRole](https://partners-intl.aliyun.com/help/doc-detail/28710.htm) and [ListRoles](https://partners-intl.aliyun.com/help/doc-detail/28713.htm).|N/A|
|IoOptimized|Boolean|No|No| Whether an instance is I/O-optimized.

 For [retired instance types](https://partners-intl.aliyun.com/help/faq-detail/55263.htm), the default value is none.

 For other instance types, the default value is optimized.

 |Valid values: -   none: indicates that the instance is not I/O-optimized.
-   optimized: indicates that the instance is I/O-optimized.

 |
|InternetChargeType|String|No|No| The network billing method.

 Default value: PayByBandwidth.

 |Valid values: -   PayByBandwidth: The network service is billed by fixed bandwidth.
-   PayByTraffic: The network service is billed by network traffic.

 |
|PrivateIpAddress|String|No|No|The private IP address of an ECS instance. The private IP address must be a subnet of the CIDR block of the `VSwitchId`and cannot be specified separately.|N/A|
|KeyPairName|String|No|No|The name of the key pair associated with an ECS instance. -   This parameter is unspecified by default. For Windows instances, the KeyPairName parameter is inapplicable. Even if you specify the KeyPairName parameter, you still need to specify the `Password` parameter to log on to an instance.
-   For Linux instances, the KeyPairName is a primary logon method. If you specify the KeyPairName parameter, you cannot log on to an instance using the username and password.

 |N/A|
|SystemDiskDiskName|String|No|No|The system disk name.|N/A|
|PeriodUnit|String|No|No|The subscription period. When the `PeriodUnit` parameter is set to `Week`:

 -   Valid values for Period: 1 | 2 | 3 | 4.
-   Valid values for AutoRenewPeriod: 1 | 2 | 3.

 When the `PeriodUnit` parameter is set to `Month`: -   Valid values for Period: 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 12 | 24 | 36 | 48 | 60.
-   Valid values for AutoRenewPeriod: 1 | 2 | 3 | 6 | 12.

 Default value: Month.|Valid values: Week | Month.|
|Description|String|No|No| The instance description.

 The description must be 2 to 256 characters in length. This parameter is unspecified by default.

 |N/A|
|Tags|List|No|No|The custom tags.|You can define up to 20 tags.|
|MinAmount|Integer|Yes|No| The minimum number of instances to be created.

 Default value: 1.

 |Value range: 1 to 100.|
|HostName|String|No|No|The hostname of an ECS instance. -   The name cannot start or end with a period \(.\) or a hyphen \(-\) and cannot contain consecutive periods \(.\) or hyphens \(-\).
-   For Windows instances, the hostname must be 2 to 15 characters in length, including uppercase or lowercase letters, digits, and hyphens \(-\), and excluding periods \(.\). A hostname must follow the predefined format \(only using numbers is invalid\).
-   For Linux instances and other instances, the hostname must be 2 to 64 characters in length, including uppercase or lowercase letters, digits, and hyphens \(-\). You can use periods to split a name into multiple segments.

 |N/A|
|AutoRenewPeriod|Number|No|No|The automatic renewal period you select to extend your subscription. This parameter is mandatory if the `AutoRenew` parameter is set to `True`.|Valid values: 1 | 2 | 3 | 6 | 12.|
|ImageId|String|Yes|Yes| The ID of the image used to launch the instance.

 You can check the available images by calling the [DescribeImages](https://partners-intl.aliyun.com/help/doc-detail/25534.htm) function.

 If you need to use images from the Marketplace, you can view ImageId at the project landing page.

 |N/A|
|AutoRenew|Boolean|No|No|Specifies whether the automatic renewal feature is enabled for an instance. The automatic renewal feature is enabled only when the `InstanceChargeType` parameter is set to `Prepaid`. Valid values: -   True: indicates that the automatic renewal feature is enabled.
-   False: indicates that the automatic renewal feature is disabled.

 Default value: False.|N/A|
|InstanceChargeType|String|No|No|The billing method of an instance.|Valid values: -   PrePaid: indicates the subscription billing method. In this case, the service is billed on a yearly or monthly basis. You must ensure the balance of your account or credit balance can cover the cost of the subscription. Otherwise, you will receive an `InvalidPayMethod` error code.
-   PostPaid: indicates the Pay-As-You-Go billing method. In this case, the service is billed by the amount of resources you actually use.

 |
|VSwitchId|String|No|No|The VSwitch ID must be specified when you create a VPC-connected instance.|N/A|
|Password|String|No|No|The password used to log on to an instance. The password must be 8 to 30 characters in length and contain at least an uppercase letter, lowercase letter, digit, and special character. The password can contain any of the following characters: \(\)\` ~!@\#$%^&amp;\*-+=|\{\}\[\]:;‘&lt;\>,.? /. The password for Windows instances cannot start with a slash \(/\).|N/A|
|InstanceType|String|Yes|No|The instance type. For more information, see [ECS instance type families](https://partners-intl.aliyun.com/help/doc-detail/25378.htm). You can also view details about the latest instance types by calling the [DescribeInstanceTypes](https://partners-intl.aliyun.com/help/doc-detail/25620.htm) API.|N/A|
|MaxAmount|Integer|Yes|No|The maximum number of instances to be created.|Value range: 1 to 100.|
|SystemDiskCategory|String|No|No| The system disk type.

 For phased-out instances which are I/O optimized, the default value is cloud.

 For more instances, the default value is cloud\_efficiency.

 |Valid values: -   cloud: indicates basic cloud disks.
-   cloud\_efficiency: indicates ultra cloud disks.
-   cloud\_ssd: indicates SSD disks.
-   ephemeral\_ssd: indicates local SSD disks.

 |
|SystemDiskSize|Number|Yes|No|The system disk size, measured in GB. This parameter must be set to a value smaller than or equal to max\{20, ImageSize\}.

 Default value: max\{40, ImageSize\}.

 |Value range: 20 to 500.|
|ZoneId|String|No|No|The ID of a zone to which an instance is assigned. See [DescribeZones](https://partners-intl.aliyun.com/help/doc-detail/25610.htm) for the list of available zones. This parameter is unspecified by default, indicating that the zone is allocated by the system.

 |N/A|
|InternetMaxBandwidthOut|Integer|No|No|The maximum outbound bandwidth of the public network, measured in Mbit/s.| For instances billed by fixed bandwidth, the value of this parameter ranges from 0 to 200. The default value is 0.

 For instances billed by network traffic, the value of this parameter ranges from 1 to 200. This parameter must be specified.

 |
|VpcId|String|No|No|The VPC ID.|N/A|
|InstanceName|String|No|No|The instance name.|The name must be 128 characters in length, including letters, Chinese characters, digits, underscores\(\_\), periods \(.\) and hyphens \(-\).|
|InternetMaxBandwidthIn|Integer|No|No|The maximum inbound bandwidth of the public network, measured in Mbit/s. Default value: 200.|Value range: 1 to 200.|
|UserData|String|No|No|The user data you need to enter when you create an ECS instance.|The user data is limited to 16 KB and needs to be converted into Base64-encoded strings. If the data contains special characters, put a backslash \(\\\) immediate before each special character for these characters to be translated into regular texts.|
|SecurityGroupId|String|No|No|The ID of the security group associated with the instances to be created. Instances associated with the same security group are permitted to access each other.|N/A|
|Period|Number|Yes|No|The subscription period of an instance, measured in months. This parameter is valid and mandatory only when `InstanceChargeType` is set to `PrePaid`. If DedicatedHostId is specified, the subscription period of the instance must be shorter than the subscription period of DDH.|Valid values: -   Valid values for the Period parameter when `PeriodUnit=Week`: 1 | 2 | 3 | 4.
-   Valid values for the Period parameter when `PeriodUnit=Month`: 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 12 | 24 | 36 | 48 | 60.

 |
|AllocatePublicIP|Boolean|No|No|Specifies whether a public IP address is allocated to an instance. If `InternetMaxBandwidthOut` is set to 0, no public IP address is allocated to an instance. Default value: True.|N/A|
|SystemDiskDescription|String|No|No|The system disk description.|N/A|
|DiskMappings|List|No|No|Specifies the disks to be attached to an instance.|A maximum of 16 disks can be attached to an instance.|

## Tags syntax {#section_58f_3ko_84e .section}

``` {#codeblock_kog_noe_4r3}
"Tags": [
  {
    "Key": String,
    "Value": String
  }
]
```

## Tags properties {#section_mn2_xaa_8c4 .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Key|String|Yes|No|None|N/A|
|Value|String|No|No|None|N/A|

## DiskMappings syntax {#section_6uz_rt1_wbr .section}

``` {#codeblock_ig6_0we_0qo}
"DiskMappings": [
  {
    "Category" : String,
    "DiskName" : String,
    "Description": String,
    "Device" : String,
    "SnapshotId" : String,
    "Size" : String
  }
]
```

## DiskMappings properties {#section_vmt_ehe_ulg .section}

|**Name**|**Type**|**Required**|**Editable**|**Description**|**Validity**|
|--------|--------|------------|------------|---------------|------------|
|Category|String|No|No|The data disk type.| Valid values: cloud | cloud\_efficiency | cloud\_ssd | ephemeral\_ssd.

 Default value: cloud\_efficiency.

 |
|DiskName|String|No|No|The data disk name.|The name can contain up to 128 characters, including letters, Chinese characters, digits, underscores \(\_\), periods \(.\), and hyphens \(-\).|
|Description|String|No|No|The description of a data disk.|Value range: 2 to 256. This parameter is unspecified by default.|
|Device|String|No|No|Specifies the device name of a data disk.|If this parameter is unspecified, the system automatically allocates a device name according to the default order from /dev/xvdb to /dev/xvdz.|
|Snapshotid|String|No|No|The snapshot used to create a data disk.|N/A|
|Size|String|Yes|No|The data disk size, measured in GB.|N/A|

## Response elements {#section_fsg_t4n_4fb .section}

**FN::GetAtt**

-   OrderId: indicates the ID of the order.
-   InnerIps: indicates the list of private IP addresses for instances connected to the classic network. This parameter is only applicable when the `NetworkType` parameter is set to Classic.
-   PrivateIps: indicates the list of private IP addresses for VPC-connected instances. This parameter is only applicable when the `NetworkType` parameter is set to VPC.
-   ZoneIds: indicates the list of available zone IDs.
-   PublicIps: indicates the public IP addresses for instances connected to the classic network. This parameter is only applicable when the `NetworkType` parameter is set to Classic.
-   HostNames: indicates the list of hostnames. RelatedOrderIds: indicates the list of relevant order IDs.
-   InstanceIds: indicates the list of instance IDs. It is a globally unique identifier \(GUID\) generated by the system for an instance.


## Example {#section_klp_54n_4fb .section}

``` {#codeblock_86u_oe7_anh}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "PeriodType": {
      "Type": "String",
      "Description": "Charge period for created instances.",
      "AllowedValues": [
        "Monthly",
        "Yearly"
      ]
    },
    "DedicatedHostId": {
      "Type": "String",
      "Description": "which dedicated host will be deployed"
    },
    "PrivateIpAddress": {
      "Type": "String",
      "Description": "Private IP for the instance created. Only works for VPC instance and cannot duplicated with existing instance."
    },
    "Description": {
      "Type": "String",
      "Description": "Description of the instance, [2, 256] characters. Do not fill or empty, the default is empty."
    },
    "DiskMappings": {
      "Type": "CommaDelimitedList",
      "Description": "Disk mappings to attach to instance. Max support 16 disks.\nIf the image contains a data disk, you can specify other parameters of the data disk via the same value of parameter \"Device\". If parameter \"Category\" is not specified, it will be cloud_efficiency instead of \"Category\" of data disk in the image.",
      "MaxLength": 16
    },
    "SystemDiskSize": {
      "Type": "Number",
      "Description": "Disk size of the system disk, range from 20 to 500 GB. If you specify with your own image, make sure the system disk size bigger than image size. ",
      "MinValue": 20,
      "MaxValue": 500
    },
    "UserData": {
      "Type": "String",
      "Description": "User data to pass to instance. [1, 16KB] characters.User data should not be base64 encoded. If you want to pass base64 encoded string to the property, use function Fn::Base64Decode to decode the base64 string first."
    },
    "SystemDiskDescription": {
      "Type": "String",
      "Description": "Description of created system disk."
    },
    "InstanceChargeType": {
      "Type": "String",
      "Description": "Instance Charge type, allowed value: Prepaid and Postpaid. If specified Prepaid, please ensure you have sufficient balance in your account. Or instance creation will be failure. Default value is Postpaid.",
      "AllowedValues": [
        "PrePaid",
        "PostPaid"
      ],
      "Default": "PostPaid"
    },
    "AutoRenew": {
      "Type": "Boolean",
      "Description": "Auto renew the prepay instance. If the period type is by year, it will renew by year, else it will renew by month.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ],
      "Default": false
    },
    "MaxAmount": {
      "Type": "Number",
      "Description": "Max number of instances to create, should be smaller than 'MaxAmount' and smaller than 100.",
      "MinValue": 1,
      "MaxValue": 100
    },
    "RamRoleName": {
      "Type": "String",
      "Description": "Instance RAM role name. The name is provided and maintained by Resource Access Management (RAM) and can be queried using ListRoles. For more information, see RAM API CreateRole and ListRoles."
    },
    "MinAmount": {
      "Type": "Number",
      "Description": "Max number of instances to create, should be bigger than 'MinAmount' and smaller than 100.",
      "MinValue": 1,
      "MaxValue": 100,
      "Default": 1
    },
    "ImageId": {
      "Type": "String",
      "Description": "Image ID to create ecs instance."
    },
    "SystemDiskDiskName": {
      "Type": "String",
      "Description": "Name of created system disk."
    },
    "InstanceType": {
      "Type": "String",
      "Description": "Ecs instance supported instance type, make sure it should be correct."
    },
    "AllocatePublicIP": {
      "Type": "Boolean",
      "Description": "The public ip for ecs instance, if properties is true, will allocate public ip. If property InternetMaxBandwidthOut set to 0, it will not assign public ip.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ],
      "Default": true
    },
    "Tags": {
      "Type": "CommaDelimitedList",
      "Description": "Tags to attach to instance. Max support 20 tags to add during create instance. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
    },
    "HostName": {
      "Type": "String",
      "Description": "Host name of created ecs instance. at least 2 characters, and '.' '-' Is not the first and last characters as hostname, not continuous use. Windows platform can be up to 15 characters, allowing letters (without limiting case), numbers and '-', and does not support the number of points, not all is digital ('.'). Other (Linux, etc.) platform up to 30 characters, allowing support number multiple points for the period between the points, each permit letters (without limiting case), numbers and '-' components."
    },
    "Password": {
      "Type": "String",
      "Description": "Password of created ecs instance. Must contain at least 3 types of special character, lower character, upper character, number."
    },
    "AutoRenewPeriod": {
      "Type": "Number",
      "Description": "The time period of auto renew. When the parameter InstanceChargeType is PrePaid, it will take effect. It could be 1, 2, 3, 6, 12. Default value is 1.",
      "AllowedValues": [
        1,
        2,
        3,
        6,
        12
      ],
      "Default": 1
    },
    "KeyPairName": {
      "Type": "String",
      "Description": "SSH key pair name."
    },
    "IoOptimized": {
      "Type": "Boolean",
      "Description": "The 'optimized' instance can provide better IO performance. Support true or false, Default is true. ",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ],
      "Default": true
    },
    "ZoneId": {
      "Type": "String",
      "Description": "current zone to create the instance."
    },
    "VSwitchId": {
      "Type": "String",
      "Description": "The vSwitch Id to create ecs instance."
    },
    "SecurityGroupId": {
      "Type": "String",
      "Description": "Security group to create ecs instance. For classic instance need the security group not belong to VPC, for VPC instance, please make sure the security group belong to specified VPC."
    },
    "Period": {
      "Type": "Number",
      "Description": "Prepaid time period. While choose by pay by month, it could be from 1 to 9. While choose pay by year, it could be from 1 to 3.",
      "MinValue": 1,
      "MaxValue": 9,
      "Default": 1
    },
    "InternetChargeType": {
      "Type": "String",
      "Description": "Instance internet access charge type.Support 'PayByBandwidth' and 'PayByTraffic' only. For AfterPay instance, default is 'PayByBandwidth'.",
      "AllowedValues": [
        "PayByBandwidth",
        "PayByTraffic"
      ],
      "Default": "PayByBandwidth"
    },
    "SystemDiskCategory": {
      "Type": "String",
      "Description": "Category of system disk. Default is cloud_efficiency. support cloud|cloud_efficiency|cloud_ssd|ephemeral_ssd",
      "AllowedValues": [
        "cloud",
        "cloud_efficiency",
        "cloud_ssd",
        "ephemeral_ssd"
      ],
      "Default": "cloud_efficiency"
    },
    "InstanceName": {
      "Type": "String",
      "Description": "Display name of the instance, [2, 128] English or Chinese characters, must start with a letter or Chinese in size, can contain numbers, '_' or '.', '-'"
    },
    "InternetMaxBandwidthOut": {
      "Type": "Number",
      "Description": "Set internet output bandwidth of instance. Unit is Mbps(Mega bit per second). Range is [0,200]. Default is 1. While the property is not 0, public ip will be assigned for instance.",
      "MinValue": 0,
      "MaxValue": 200,
      "Default": 1
    },
    "VpcId": {
      "Type": "String",
      "Description": "The VPC id to create ecs instance."
    },
    "InternetMaxBandwidthIn": {
      "Type": "Number",
      "Description": "Max internet out band width setting, unit in Mbps(Mega bit per second). The range is [1,200], default is 200 Mbps.",
      "MinValue": 1,
      "MaxValue": 200,
      "Default": 200
    },
    "PeriodUnit": {
      "Type": "String",
      "Description": "Unit of prepaid time period, it could be Week/Month. Default value is Month.",
      "AllowedValues": [
        "Week",
        "Month"
      ],
      "Default": "Month"
    }
  },
  "Resources": {
    "PrepayInstance": {
      "Type": "ALIYUN::ECS::PrepayInstance",
      "Properties": {
        "PeriodType": {
          "Ref": "PeriodType"
        },
        "DedicatedHostId": {
          "Ref": "DedicatedHostId"
        },
        "PrivateIpAddress": {
          "Ref": "PrivateIpAddress"
        },
        "Description": {
          "Ref": "Description"
        },
        "DiskMappings": {
          "Fn::Split": [
            ",",
            {
              "Ref": "DiskMappings"
            },
            {
              "Ref": "DiskMappings"
            }
          ]
        },
        "SystemDiskSize": {
          "Ref": "SystemDiskSize"
        },
        "UserData": {
          "Ref": "UserData"
        },
        "SystemDiskDescription": {
          "Ref": "SystemDiskDescription"
        },
        "InstanceChargeType": {
          "Ref": "InstanceChargeType"
        },
        "AutoRenew": {
          "Ref": "AutoRenew"
        },
        "MaxAmount": {
          "Ref": "MaxAmount"
        },
        "RamRoleName": {
          "Ref": "RamRoleName"
        },
        "MinAmount": {
          "Ref": "MinAmount"
        },
        "ImageId": {
          "Ref": "ImageId"
        },
        "SystemDiskDiskName": {
          "Ref": "SystemDiskDiskName"
        },
        "InstanceType": {
          "Ref": "InstanceType"
        },
        "AllocatePublicIP": {
          "Ref": "AllocatePublicIP"
        },
        "Tags": {
          "Fn::Split": [
            ",",
            {
              "Ref": "Tags"
            },
            {
              "Ref": "Tags"
            }
          ]
        },
        "HostName": {
          "Ref": "HostName"
        },
        "Password": {
          "Ref": "Password"
        },
        "AutoRenewPeriod": {
          "Ref": "AutoRenewPeriod"
        },
        "KeyPairName": {
          "Ref": "KeyPairName"
        },
        "IoOptimized": {
          "Ref": "IoOptimized"
        },
        "ZoneId": {
          "Ref": "ZoneId"
        },
        "VSwitchId": {
          "Ref" : "VSwitchId"
        },
        "SecurityGroupId": {
          "Ref": "SecurityGroupId"
        },
        "Period": {
          "Ref": "Period"
        },
        "InternetChargeType": {
          "Ref": "InternetChargeType"
        },
        "SystemDiskCategory": {
          "Ref": "SystemDiskCategory"
        },
        "InstanceName": {
          "Ref": "InstanceName"
        },
        "InternetMaxBandwidthOut": {
          "Ref": "InternetMaxBandwidthOut"
        },
        "VpcId": {
          "Ref": "VpcId"
        },
        "InternetMaxBandwidthIn": {
          "Ref": "InternetMaxBandwidthIn"
        },
        "PeriodUnit": {
          "Ref": "PeriodUnit"
        }
      }
    }
  },
  "Outputs": {
    "PublicIps": {
      "Description": "Public IP address list of created ecs instance.",
      "Value": {
        "Fn::GetAtt": [
          "PrepayInstance",
          "PublicIps"
        ]
      }
    },
    "RelatedOrderIds": {
      "Description": "The related order id list of created ecs instances",
      "Value": {
        "Fn::GetAtt": [
          "PrepayInstance",
          "RelatedOrderIds"
        ]
      }
    },
    "PrivateIps": {
      "Description": "Private IP address list of created ecs instance. Only for VPC instance.",
      "Value": {
        "Fn::GetAtt": [
          "PrepayInstance",
          "PrivateIps"
        ]
      }
    },
    "HostNames": {
      "Description": "Host names of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "PrepayInstance",
          "HostNames"
        ]
      }
    },
    "InnerIps": {
      "Description": "Inner IP address list of the specified instance. Only for classical instance.",
      "Value": {
        "Fn::GetAtt": [
          "PrepayInstance",
          "InnerIps"
        ]
      }
    },
    "ZoneIds": {
      "Description": "Zone id of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "PrepayInstance",
          "ZoneIds"
        ]
      }
    },
    "OrderId": {
      "Description": "The order id list of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "PrepayInstance",
          "OrderId"
        ]
      }
    },
    "InstanceIds": {
      "Description": "The instance id list of created ecs instance",
      "Value": {
        "Fn::GetAtt": [
          "PrepayInstance",
          "InstanceIds"
        ]
      }
    }
  }
}
```

