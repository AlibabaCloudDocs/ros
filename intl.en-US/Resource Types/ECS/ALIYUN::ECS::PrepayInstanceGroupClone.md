# ALIYUN::ECS::PrepayInstanceGroupClone {#concept_fz2_pm5_qgb .concept}

Clones a group of ECS instances that use the subscription billing method.

## Syntax {#section_xyg_tn2_lfb .section}

```language-json
{
  "Type": "ALIYUN::ECS::PrepayInstanceGroupClone",
  "Properties": {
    "PeriodType": String,
    "SystemDiskCategory": String,
    "RamRoleName": String,
    "KeyPairName": String,
    "SystemDiskDiskName": String,
    "PeriodUnit": String,
    "Description": String,
    "Tags": List,
    "MinAmount": Integer,
    "AutoRenewPeriod": Number,
    "ImageId": String,
    "AutoRenew": String,
    "SourceInstanceId": String,
    "EniMappings": List,
    "Password": String,
    "MaxAmount": Integer,
    "DiskMappings": List,
    "LaunchTemplateName": String,
    "LaunchTemplateVersion": String,
    "ZoneId": String,
    "InternetMaxBandwidthOut": String,
    "InstanceName": String,
    "InternetMaxBandwidthIn": Integer,
    "SecurityGroupId": String,
    "LaunchTemplateId": String,
    "Period": Number,
    "SystemDiskDescription": String
  }
}
```

## Properties {#section_cgd_53n_4fb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|PeriodType|String|Yes|No|The subscription cycle.|Valid values: Monthly | Yearly.|
|SystemDiskCategory|String|No|Yes|The system disk type.| Valid values: cloud | cloud\_efficiency | cloud\_ssd | ephemeral\_ssd.

 Default value: cloud\_efficiency.

 |
|RamRoleName|String|No|No|The RAM role of an instance.|You can view the RAM role of an instance by calling the ListRoles API. For more information, see [CreateRole](https://partners-intl.aliyun.com/help/doc-detail/28710.htm) and [ListRoles](https://partners-intl.aliyun.com/help/doc-detail/28713.htm).|
|KeyPairName|String|No|Yes|The name of the key pair associated with an ECS instance. Default value: empty. For Windows instances, the KeyPairName parameter is inapplicable. Even if you specify the KeyPairName parameter, you are still required to specify the Password parameter to log on to an instance. For Linux instances, the KeyPairName is a primary logon method. If you specify the KeyPairName parameter, you cannot log on to an instance using the username and password.|N/A|
|SystemDiskDiskName|String|No|Yes|The system disk name.|N/A|
|PeriodUnit|String|No|Yes|The unit of the billing cycle.| Valid values: Week | Month.

 Default value: Month.

 |
|Description|String|No|No|The instance description.|The description can be up to 256 characters in length.|
|Tags|List|No|Yes|The custom tags.|A maximum of four tags are supported. The format is \[\{"Key":"tagKey","Value":"tagValue"\},\{"Key":"tagKey2","Value":"tagValue2"\}\].|
|MinAmount|Integer|Yes|No|Specifies the minimum number of ECS instances to be created.|Value range: 1 to 100. The MinAmount parameter must be set to a value smaller than or equal to the value of MaxAmount.|
|AutoRenewPeriod|Number|No|Yes|The period the subscription is automatically extended by after an instance expires.|Valid values: 1 | 2 | 3 | 6 | 12. Default value: 1.|
|ImageId|String|No|Yes|The ID of the image used to launch ECS instances. You can use public images, custom images and Alibaba Cloud Marketplace images.|N/A|
|AutoRenew|String|No|Yes|Specifies whether the automatic renewal feature is enabled for an instance.| Valid values: True | False.

 Default value: False.

 |
|SourceInstanceId|String|Yes|No|The ID of the source ECS instance you want to clone.|When the source instance is cloned, its type, image file, network bandwidth billing method, bandwidth limit, and network type are cloned. If the source ECS instance is added to more than one security group, the new ECS instance is automatically added to the first security group that the source instance joined.|
|EniMappings|List|No|Yes|The elastic network interface \(ENI\) attached to an instance.|You can only attach one ENI to an instance.|
|Password|String|No|Yes|The password used to log on to an ECS instance.|The password must be 8 to 30 characters in length and must contain at least an uppercase letter, lowercase letter, digit, and special character. The password can contain any of the following characters: \( \) \` ~ !@ \# $ % ^ & \* - + = | \{ \} \[ \] : ; ‘ < \> , . ? /. If the Password parameter is specified in the API request, make sure that you use the HTTPS protocol to secure the API call.|
|MaxAmount|Integer|Yes|No|Specifies the maximum number of ECS instances to be created.|Value range: 1 to 100. The MaxAmount parameter must be set to a value equal to or greater than the value of MinAmount.|
|DiskMappings|List|No|Yes|Specifies the disks to be attached to an instance.|A maximum of 16 disks can be attached to an instance.|
|LaunchTemplateName |String|No|No|The name of the launch template for an instance.|N/A|
|LaunchTemplateVersion|String|No|Yes|The version of the launch template for an instance. If you do not specify a particular version, the default version is used.|N/A|
|ZoneId|String|No|No|The ID of the zone to which an instance is assigned.|N/A|
|InternetMaxBandwidthOut|String|No|No|The maximum outbound bandwidth of the public network, measured in Mbit/s.| The value range is from 0 to 200 if the Internet service is billed by fixed bandwidth.

 The value range is from 1 to 200 if the Internet service is billed by network traffic. This parameter is required.

 |
|InstanceName|String|No|No|The instance name.|The name can be up to 128 characters, and can contain letters, Chinese characters, digits, underscores \(\_\), periods \(.\), and hyphens \(-\).|
|InternetMaxBandwidthIn|Integer|No|No|The maximum inbound bandwidth of the public network, measured in Mbit/s. Default value: 200.|Value range: 1 to 200.|
|SecurityGroupId|String|No|No|The ID of the security group associated with the instance to be created.|N/A|
|LaunchTemplateId|String|No|Yes|The ID of the launch template for an instance.|N/A|
|Period|Number|Yes|No|The subscription period.| Value range: 1 to 9.

 -   The value range is from 1 to 9 if the service is billed on a monthly basis.
-   The value range is from 1 to 3 if the service is billed on a yearly basis.

 |
|SystemDiskDescription|String|No|Yes|The system disk description.|N/A|

## Tags syntax { .section}

```
"Tags": [
  {
    "Key": String,
    "Value": String
  }
]
```

## Tags properties { .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Key|String|Yes|No|None|N/A|
|Value|String|No|No|None|N/A|

## EniMappings syntax { .section}

```
"EniMappings": [
  {
    "SecurityGroupId": String,
    "VSwitchId": String,
    "Description": String,
    "NetworkInterfaceName": String,
    "PrimaryIpAddress": String
  }
]
```

## EniMappings properties { .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|SecurityGroupId|String|Yes|Yes|The security group ID. The security group and the ENI associated with the security group must be connected to the same VPC.|N/A|
|VSwitchId|String|Yes|No|The VSwitch ID.|N/A|
|Description|String|No|Yes|The ENI description.|N/A|
|NetworkInterfaceName|String|No|Yes|The ENI name.|N/A|
|PrimaryIpAddress|String|No|No|The primary IP address of an instance. The specified IP address must share the same host ID with the VSwitch. If this parameter is unspecified, a random network ID is automatically assigned by the system to the ENI.|N/A|

## DiskMappings syntax { .section}

```
"DiskMappings": [
  {
    "Category": String,
    "DiskName": String,
    "Description": String,
    "Device": String,
    "SnapshotId": String,
    "Size": String
  }
]
```

## DiskMappings properties { .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Category|String|No|No|The data disk type.| Valid values: cloud | cloud\_efficiency | cloud\_ssd | ephemeral\_ssd.

 Default value: cloud\_efficiency.

 |
|DiskName|String|No|No|The data disk name.|The name can be up to 128 characters in length, including letters, Chinese characters, digits, underscores \(-\), periods \(.\), and hyphens \(\_\).|
|Description|String|No|No|The data disk description.|Value range: 2 to 256. Default value: empty.|
|Device|String|No|No|Specifies the device name of the data disk attached to an ECS instance.|Example: /dev/xvd\[a-z\].|
|Snapshotid|String|No|No|The ID of the snapshot used to create a data disk.|N/A|
|Size|String|Yes|No|The capacity of a data disk, measured in GB.|N/A|

## Response elements {#section_fsg_t4n_4fb .section}

**FN::GetAtt**

-   OrderId: indicates the order ID.
-   InnerIps: indicates the list of the private IP addresses of instances connected to the classic network.
-   PrivateIps: indicates the list of private IP addresses of VPC-connected instances.
-   ZoneIds: indicates the list of available zones.
-   PublicIps: indicates the public IP addresses of instances that are connected to the classic network.
-   HostNames: indicates the list of hostnames.
-   RelatedOrderIds: indicates the list of relevant order IDs.
-   InstanceIds: indicates the list of instance IDs.

## Example {#section_klp_54n_4fb .section}

```
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
    "Description": {
      "Type": "String",
      "Description": "Description of the instance, [2, 256] characters. Do not fill or empty, the default is empty."
    },
    "DiskMappings": {
      "Type": "CommaDelimitedList",
      "Description": "Disk mappings to attach to instance. Max support 16 disks.\nIf the image contains a data disk, you can specify other parameters of the data disk via the same value of parameter \"Device\". If parameter \"Category\" is not specified, it will be cloud_efficiency instead of \"Category\" of data disk in the image.Old instances will not be changed.",
      "MaxLength": 16
    },
    "SystemDiskDescription": {
      "Type": "String",
      "Description": "Description of created system disk.Old instances will not be changed."
    },
    "AutoRenew": {
      "Type": "String",
      "Description": "Whether renew the fee automatically? When the parameter InstanceChargeType is PrePaid, it will take effect. Range of value:True: automatic renewal.False: no automatic renewal. Default value is False.Old instances will not be changed.",
      "AllowedValues": [
        "True",
        "False"
      ],
      "Default": "False"
    },
    "SourceInstanceId": {
      "Type": "String",
      "Description": "Source ecs instance used to copy properties to clone new ecs instance. It will copy the InstanceType, ImageId, InternetChargeType, InternetMaxBandwidthIn, InternetMaxBandwidthOut and the system disk and data disk configurations. If the instance network is VPC, it will also clone the relative properties. If specified instance with more than one security group, it will use the first security group to create instance. you can also specify the SecurityGroupId to override it."
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
      "Description": "Name of created system disk.Old instances will not be changed."
    },
    "Tags": {
      "Type": "CommaDelimitedList",
      "Description": "Tags to attach to instance. Max support 20 tags to add during create instance. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
    },
    "Password": {
      "Type": "String",
      "Description": "Password of created ecs instance. Must contain at least 3 types of special character, lower character, upper character, number."
    },
    "AutoRenewPeriod": {
      "Type": "Number",
      "Description": "The time period of auto renew. When the parameter InstanceChargeType is PrePaid, it will take effect.It could be 1, 2, 3, 6, 12. Default value is 1. Old instances will not be changed.",
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
      "Description": "SSH key pair name.Old instances will not be changed."
    },
    "LaunchTemplateName": {
      "Type": "String",
      "Description": "Name of launch template. Launch template id or name must be specified to use launch template"
    },
    "ZoneId": {
      "Type": "String",
      "Description": "current zone to create the instance."
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
    "LaunchTemplateId": {
      "Type": "String",
      "Description": "ID of launch template. Launch template id or name must be specified to use launch template"
    },
    "SystemDiskCategory": {
      "Type": "String",
      "Description": "Category of system disk. Default is cloud_efficiency. support cloud|cloud_efficiency|cloud_ssd|ephemeral_ssd.Old instances will not be changed.",
      "AllowedValues": [
        "cloud",
        "cloud_efficiency",
        "cloud_ssd",
        "ephemeral_ssd"
      ],
      "Default": "cloud_efficiency"
    },
    "EniMappings": {
      "Type": "CommaDelimitedList",
      "Description": "NetworkInterface to attach to instance. Max support 1 ENI.",
      "MaxLength": 1
    },
    "InstanceName": {
      "Type": "String",
      "Description": "Display name of the instance, [2, 128] English or Chinese characters, must start with a letter or Chinese in size, can contain numbers, '_' or '.', '-'"
    },
    "InternetMaxBandwidthOut": {
      "Type": "Number",
      "Description": "Set internet output bandwidth of instance. Unit is Mbps(Mega bit per second). Range is [0,200]. Default is 1. While the property is not 0, public ip will be assigned for instance.",
      "MinValue": 0,
      "MaxValue": 200
    },
    "InternetMaxBandwidthIn": {
      "Type": "Number",
      "Description": "Max internet out band width setting, unit in Mbps(Mega bit per second). The range is [1,200], default is 200 Mbps.",
      "MinValue": 1,
      "MaxValue": 200,
      "Default": 200
    },
    "LaunchTemplateVersion": {
      "Type": "String",
      "Description": "Version of launch template. Default version is used if version is not specified.",
      "AllowedPattern": "^[1-9]\\d*$"
    },
    "PeriodUnit": {
      "Type": "String",
      "Description": "Unit of prepaid time period, it could be Week/Month. Default value is Month.Old instances will not be changed.",
      "AllowedValues": [
        "Week",
        "Month"
      ],
      "Default": "Month"
    }
  },
  "Resources": {
    "PrepayInstanceGroupClone": {
      "Type": "ALIYUN::ECS::PrepayInstanceGroupClone",
      "Properties": {
        "PeriodType": {
          "Ref": "PeriodType"
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
        "SystemDiskDescription": {
          "Ref": "SystemDiskDescription"
        },
        "AutoRenew": {
          "Ref": "AutoRenew"
        },
        "SourceInstanceId": {
          "Ref": "SourceInstanceId"
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
        "Password": {
          "Ref": "Password"
        },
        "AutoRenewPeriod": {
          "Ref": "AutoRenewPeriod"
        },
        "KeyPairName": {
          "Ref": "KeyPairName"
        },
        "LaunchTemplateName": {
          "Ref": "LaunchTemplateName"
        },
        "ZoneId": {
          "Ref": "ZoneId"
        },
        "SecurityGroupId": {
          "Ref": "SecurityGroupId"
        },
        "Period": {
          "Ref": "Period"
        },
        "LaunchTemplateId": {
          "Ref": "LaunchTemplateId"
        },
        "SystemDiskCategory": {
          "Ref": "SystemDiskCategory"
        },
        "EniMappings": {
          "Fn::Split": [
            ",",
            {
              "Ref": "EniMappings"
            },
            {
              "Ref": "EniMappings"
            }
          ]
        },
        "InstanceName": {
          "Ref": "InstanceName"
        },
        "InternetMaxBandwidthOut": {
          "Ref": "InternetMaxBandwidthOut"
        },
        "InternetMaxBandwidthIn": {
          "Ref": "InternetMaxBandwidthIn"
        },
        "LaunchTemplateVersion": {
          "Ref": "LaunchTemplateVersion"
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
          "PrepayInstanceGroupClone",
          "PublicIps"
        ]
      }
    },
    "RelatedOrderIds": {
      "Description": "The related order id list of created ecs instances",
      "Value": {
        "Fn::GetAtt": [
          "PrepayInstanceGroupClone",
          "RelatedOrderIds"
        ]
      }
    },
    "PrivateIps": {
      "Description": "Private IP address list of created ecs instance. Only for VPC instance.",
      "Value": {
        "Fn::GetAtt": [
          "PrepayInstanceGroupClone",
          "PrivateIps"
        ]
      }
    },
    "HostNames": {
      "Description": "Host names of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "PrepayInstanceGroupClone",
          "HostNames"
        ]
      }
    },
    "InnerIps": {
      "Description": "Inner IP address list of the specified instance. Only for classical instance.",
      "Value": {
        "Fn::GetAtt": [
          "PrepayInstanceGroupClone",
          "InnerIps"
        ]
      }
    },
    "ZoneIds": {
      "Description": "Zone id of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "PrepayInstanceGroupClone",
          "ZoneIds"
        ]
      }
    },
    "OrderId": {
      "Description": "The order id list of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "PrepayInstanceGroupClone",
          "OrderId"
        ]
      }
    },
    "InstanceIds": {
      "Description": "The instance id list of created ecs instance",
      "Value": {
        "Fn::GetAtt": [
          "PrepayInstanceGroupClone",
          "InstanceIds"
        ]
      }
    }
  }
}
```

