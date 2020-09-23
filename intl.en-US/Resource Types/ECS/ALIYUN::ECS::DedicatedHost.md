# ALIYUN::ECS::DedicatedHost

ALIYUN::ECS::DedicatedHost is used to create a dedicated host.

## Syntax

```
{
  "Type": "ALIYUN::ECS::DedicatedHost",
  "Properties": {
    "DedicatedHostType": String,
    "DedicatedHostName": String,
    "PeriodUnit": String,
    "AutoReleaseTime": String,
    "Description": String,
    "AutoPlacement": String,
    "Tags": List,
    "AutoRenewPeriod": Number,
    "ActionOnMaintenance": String,
    "Period": Number,
    "AutoRenew": String,
    "NetworkAttributesSlbUdpTimeout": Integer,
    "ChargeType": String,
    "ResourceGroupId": String,
    "ZoneId": String,
    "NetworkAttributesUdpTimeout": Integer,
    "Quantity": Integer
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|DedicatedHostType|String|Yes|No|The type of the dedicated host.|None|
|DedicatedHostName|String|No|No|The name of the dedicated host.|The name must be 2 to 128 characters in length. It must start with a letter and cannot start with `http://` or `https://`. It can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\).|
|PeriodUnit|String|No|No|The unit of the billing cycle.|Default value: Month. Valid values:

 -   Week
-   Month
-   Year |
|AutoReleaseTime|String|No|No|The time scheduled for the dedicated host to be automatically released. If you do not specify the AutoReleaseTime parameter, the dedicated host will not be automatically released.

|-   The scheduled release time must be at least 30 minutes from the current time.
-   The scheduled release time must be at most three years from the current time.
-   If the value of `ss` is not `00`, the start time is automatically rounded to the nearest minute based on the value of `mm`. |
|Description|String|No|No|The description of the dedicated host.|None|
|AutoRenewPeriod|Number|No|No|The auto-renewal period of the dedicated host.|Valid values: 1, 2, 3, 6, and 12. Unit: months. |
|Period|Number|No|No|The subscription period of the dedicated host.|-   Valid values when the PeriodUnit parameter is set to Week: 1, 2, and 3.
-   Valid values when the PeriodUnit parameter is set to Month: 1, 2, 3, 4, 5, 6, 7, 8, and 9.
-   Valid values when the PeriodUnit parameter is set to Year: 1, 2, 3, 4, and 5.

  |
|ZoneId|String|No|No|The ID of the zone where the dedicated host resides.|This parameter is empty by default. If this parameter is not specified, the system automatically selects a zone.|
|AutoRenew|String|No|No|Specifies whether to enable auto-renewal for the dedicated host.|Default value: False. Valid values: -   True
-   False |
|ChargeType|String|No|No|The billing method of the dedicated host.|Valid values: -   PrePaid: the subscription billing method.

If you set this parameter to PrePaid, make sure that you have a valid payment method. Otherwise, an `InvalidPayMethod` error is returned.

-   PostPaid: the pay-as-you-go billing method. |
|AutoPlacement|String|No|No|Specifies whether to add the dedicated host to the resource pool for automatic deployment. If you do not specify the DedicatedHostId parameter when you create an ECS instance on a dedicated host, Alibaba Cloud automatically selects a dedicated host from the resource pool to host the instance. For more information, see [Features](/intl.en-US/Product Introduction/Features.md).|Valid values: -   on
-   off

 **Note:**

If you do not specify this parameter, the dedicated host is added to the automatic deployment resource pool.

If you do not want to add the dedicated host to the automatic deployment resource pool, set this parameter to off. |
|Tags|List|No|No|The custom tags of the dedicated host.|A maximum of 20 tags can be specified in the `[{"Key":"tagKey","Value":"tagValue"},{"Key":"tagKey2","Value":"tagValue2"}]` format. For more information, see [Tags properties](#section_13a_v8h_9ev). |
|ActionOnMaintenance|String|No|No|The policy used to migrate the instances from the dedicated host when the dedicated host fails or needs to be repaired online.|Valid values: -   Migrate: The instances are migrated to another physical server and restarted.
-   Stop: The instances on the dedicated host are stopped. If the dedicated host cannot be repaired, the instances are migrated to another physical server and restarted.

 If the dedicated host is attached with cloud disks, the default value is Migrate. If the dedicated host is attached with local disks, the default value is Stop.|
|NetworkAttributesSlbUdpTimeout|Integer|No|No|The timeout period for a UDP session between Server Load Balancer \(SLB\) and the dedicated host.|Valid values: 15 to 310. Unit: seconds. |
|ResourceGroupId|String|No|No|The ID of the resource group to which the dedicated host belongs.|None|
|NetworkAttributesUdpTimeout|Integer|No|No|The timeout period for a UDP session between a user and an Alibaba Cloud service on the dedicated host.|Valid values: 15 to 310. Unit: seconds. |
|Quantity|Integer|No|No|The number of dedicated hosts that you want to create.|Valid values: 1 to 100. Default value: 1. |

## Tags syntax

```
"Tags": [
  {
    "Key": String,
    "Value": String
  }
]
```

## Tags properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Key|String|Yes|No|The tag key.|The tag key must be 1 to 128 characters in length and cannot start with `acs:` or `aliyun`. It cannot contain `http://` or `https://`.|
|Value|String|No|No|The tag value.|The tag value must be 0 to 128 characters in length and cannot start with `acs:` or `aliyun`. It cannot contain `http://` or `https://`.|

## Response parameters

Fn::GetAtt

-   OrderId: the ID of the order.
-   DedicatedHostIds: the list of dedicated host IDs.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "AutoRenewPeriod": {
      "Type": "Number",
      "Description": "The time period of auto renew. When the parameter InstanceChargeType is PrePaid, it will take effect.It could be 1, 2, 3, 6, 12. Default value is 1.",
      "AllowedValues": [
        1,
        2,
        3,
        6,
        12
      ],
      "Default": 1
    },
    "Description": {
      "Type": "String",
      "Description": "The description of host."
    },
    "NetworkAttributesSlbUdpTimeout": {
      "Type": "Number",
      "Description": "The duration of UDP timeout for sessions between Server Load Balancer (SLB) and the dedicated host. Unit: seconds. Valid values: 15 to 310.",
      "MinValue": 15,
      "MaxValue": 310
    },
    "ResourceGroupId": {
      "Type": "String",
      "Description": "The ID of the resource group. If this is left blank, the system automatically fills in the ID of the default resource group."
    },
    "ZoneId": {
      "Type": "String",
      "Description": "The zone to create the host."
    },
    "NetworkAttributesUdpTimeout": {
      "Type": "Number",
      "Description": "The duration of UDP timeout for sessions between users and instances on the dedicated host. Unit: seconds. Valid values: 15 to 310.",
      "MinValue": 15,
      "MaxValue": 310
    },
    "AutoRenew": {
      "Type": "String",
      "Description": "Whether renew the fee automatically? When the parameter InstanceChargeType is PrePaid, it will take effect. Range of value:True: automatic renewal.False: no automatic renewal. Default value is False.",
      "AllowedValues": [
        "True",
        "False"
      ],
      "Default": "False"
    },
    "AutoPlacement": {
      "Type": "String",
      "Description": "Specifies whether the dedicated host is added to the resource pool for automatic deployment. If you do not specify the DedicatedHostId parameter when you create an instance on a dedicated host, Alibaba Cloud automatically selects a dedicated host from the resource pool to host the instance. For more information, see Automatic deployment. Valid values:on: The dedicated host is added to the resource pool for automatic deployment.off: The dedicated host is not added to the resource pool for automatic deployment.Default value: on.Note When you create a dedicated host: If you do not specify this parameter, the dedicated host is added to the automatic deployment resource pool.If you do not want to add the dedicated host to the automatic deployment resource pool, set the value to off.",
      "AllowedValues": [
        "on",
        "off"
      ]
    },
    "Period": {
      "Type": "Number",
      "Description": "Prepaid time period. Unit is month, it could be from 1 to 9 or 12, 24, 36, 48, 60. Default value is 1.",
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
        36,
        48,
        60
      ],
      "Default": 1
    },
    "Quantity": {
      "Type": "Number",
      "Description": "The number of dedicated hosts that you want to create. Valid values: 1 to 100.Default value: 1.",
      "MinValue": 1,
      "MaxValue": 100,
      "Default": 1
    },
    "DedicatedHostType": {
      "Type": "String",
      "Description": "The instance type of host."
    },
    "DedicatedHostName": {
      "Type": "String",
      "Description": "The name of the dedicated host, [2, 128] English or Chinese characters. It must begin with an uppercase/lowercase letter or a Chinese character, and may contain numbers, '_' or '-'. It cannot begin with http:// or https://."
    },
    "ChargeType": {
      "Type": "String",
      "Description": "Instance Charge type, allowed value: Prepaid and Postpaid. If specified Prepaid, please ensure you have sufficient balance in your account. Or instance creation will be failure. Default value is Postpaid.",
      "AllowedValues": [
        "PrePaid",
        "PostPaid"
      ],
      "Default": "PostPaid"
    },
    "ActionOnMaintenance": {
      "Type": "String",
      "Description": "The policy used to migrate the instances from the dedicated hostwhen the dedicated host fails or needs to be repaired online.Valid values: Migrate: Instances are migrated to another physical server and restarted.If the dedicated host is attached with disks that are not local disks, the default value is Migrate.Stop: Instances on the dedicated host are stopped. If the dedicated host cannot be repaired,the instances are migrated to another physical server and restarted.If the dedicated host is attached with local disks, the default value is Stop.",
      "AllowedValues": [
        "Migrate",
        "Stop"
      ]
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to DedicatedHost. Max support 20 tags to add during create DedicatedHost. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
    },
    "PeriodUnit": {
      "Type": "String",
      "Description": "Unit of prepaid time period, it could be Week/Month/Year. Default value is Month.",
      "AllowedValues": [
        "Week",
        "Month",
        "Year"
      ],
      "Default": "Month"
    },
    "AutoReleaseTime": {
      "Type": "String",
      "Description": "Auto release time for created host, Follow ISO8601 standard using UTC time. format is 'yyyy-MM-ddTHH:mm:ssZ'. Not bigger than 3 years from this day onwards"
    }
  },
  "Resources": {
    "Host": {
      "Type": "ALIYUN::ECS::DedicatedHost",
      "Properties": {
        "AutoRenewPeriod": {
          "Ref": "AutoRenewPeriod"
        },
        "Description": {
          "Ref": "Description"
        },
        "NetworkAttributesSlbUdpTimeout": {
          "Ref": "NetworkAttributesSlbUdpTimeout"
        },
        "ResourceGroupId": {
          "Ref": "ResourceGroupId"
        },
        "ZoneId": {
          "Ref": "ZoneId"
        },
        "NetworkAttributesUdpTimeout": {
          "Ref": "NetworkAttributesUdpTimeout"
        },
        "AutoRenew": {
          "Ref": "AutoRenew"
        },
        "AutoPlacement": {
          "Ref": "AutoPlacement"
        },
        "Period": {
          "Ref": "Period"
        },
        "Quantity": {
          "Ref": "Quantity"
        },
        "DedicatedHostType": {
          "Ref": "DedicatedHostType"
        },
        "DedicatedHostName": {
          "Ref": "DedicatedHostName"
        },
        "ChargeType": {
          "Ref": "ChargeType"
        },
        "ActionOnMaintenance": {
          "Ref": "ActionOnMaintenance"
        },
        "Tags": {
          "Ref": "Tags"
        },
        "PeriodUnit": {
          "Ref": "PeriodUnit"
        },
        "AutoReleaseTime": {
          "Ref": "AutoReleaseTime"
        }
      }
    }
  },
  "Outputs": {
    "OrderId": {
      "Description": "The order id list of created instance.",
      "Value": {
        "Fn::GetAtt": [
          "Host",
          "OrderId"
        ]
      }
    },
    "DedicatedHostIds": {
      "Description": "The host id list of created hosts",
      "Value": {
        "Fn::GetAtt": [
          "Host",
          "DedicatedHostIds"
        ]
      }
    }
  }
}
```

`YAML` format

```
ROSTemplateFormatVersion: '2015-09-01'
Parameters:
  AutoRenewPeriod:
    Type: Number
    Description: >-
      The time period of auto renew. When the parameter InstanceChargeType is
      PrePaid, it will take effect.It could be 1, 2, 3, 6, 12. Default value is
      1.
    AllowedValues:
      - 1
      - 2
      - 3
      - 6
      - 12
    Default: 1
  Description:
    Type: String
    Description: The description of host.
  NetworkAttributesSlbUdpTimeout:
    Type: Number
    Description: >-
      The duration of UDP timeout for sessions between Server Load Balancer
      (SLB) and the dedicated host. Unit: seconds. Valid values: 15 to 310.
    MinValue: 15
    MaxValue: 310
  ResourceGroupId:
    Type: String
    Description: >-
      The ID of the resource group. If this is left blank, the system
      automatically fills in the ID of the default resource group.
  ZoneId:
    Type: String
    Description: The zone to create the host.
  NetworkAttributesUdpTimeout:
    Type: Number
    Description: >-
      The duration of UDP timeout for sessions between users and instances on
      the dedicated host. Unit: seconds. Valid values: 15 to 310.
    MinValue: 15
    MaxValue: 310
  AutoRenew:
    Type: String
    Description: >-
      Whether renew the fee automatically? When the parameter InstanceChargeType
      is PrePaid, it will take effect. Range of value:True: automatic
      renewal.False: no automatic renewal. Default value is False.
    AllowedValues:
      - 'True'
      - 'False'
    Default: 'False'
  AutoPlacement:
    Type: String
    Description: >-
      Specifies whether the dedicated host is added to the resource pool for
      automatic deployment. If you do not specify the DedicatedHostId parameter
      when you create an instance on a dedicated host, Alibaba Cloud
      automatically selects a dedicated host from the resource pool to host the
      instance. For more information, see Automatic deployment. Valid values:on:
      The dedicated host is added to the resource pool for automatic
      deployment.off: The dedicated host is not added to the resource pool for
      automatic deployment.Default value: on.Note When you create a dedicated
      host: If you do not specify this parameter, the dedicated host is added to
      the automatic deployment resource pool.If you do not want to add the
      dedicated host to the automatic deployment resource pool, set the value to
      off.
    AllowedValues:
      - 'on'
      - 'off'
  Period:
    Type: Number
    Description: >-
      Prepaid time period. Unit is month, it could be from 1 to 9 or 12, 24, 36,
      48, 60. Default value is 1.
    AllowedValues:
      - 1
      - 2
      - 3
      - 4
      - 5
      - 6
      - 7
      - 8
      - 9
      - 12
      - 24
      - 36
      - 48
      - 60
    Default: 1
  Quantity:
    Type: Number
    Description: >-
      The number of dedicated hosts that you want to create. Valid values: 1 to
      100.Default value: 1.
    MinValue: 1
    MaxValue: 100
    Default: 1
  DedicatedHostType:
    Type: String
    Description: The instance type of host.
  DedicatedHostName:
    Type: String
    Description: >-
      The name of the dedicated host, [2, 128] English or Chinese characters. It
      must begin with an uppercase/lowercase letter or a Chinese character, and
      may contain numbers, '_' or '-'. It cannot begin with http:// or https://.
  ChargeType:
    Type: String
    Description: >-
      Instance Charge type, allowed value: Prepaid and Postpaid. If specified
      Prepaid, please ensure you have sufficient balance in your account. Or
      instance creation will be failure. Default value is Postpaid.
    AllowedValues:
      - PrePaid
      - PostPaid
    Default: PostPaid
  ActionOnMaintenance:
    Type: String
    Description: >-
      The policy used to migrate the instances from the dedicated hostwhen the
      dedicated host fails or needs to be repaired online.Valid values: Migrate:
      Instances are migrated to another physical server and restarted.If the
      dedicated host is attached with disks that are not local disks, the
      default value is Migrate.Stop: Instances on the dedicated host are
      stopped. If the dedicated host cannot be repaired,the instances are
      migrated to another physical server and restarted.If the dedicated host is
      attached with local disks, the default value is Stop.
    AllowedValues:
      - Migrate
      - Stop
  Tags:
    Type: Json
    Description: >-
      Tags to attach to DedicatedHost. Max support 20 tags to add during create
      DedicatedHost. Each tag with two properties Key and Value, and Key is
      required.
    MaxLength: 20
  PeriodUnit:
    Type: String
    Description: >-
      Unit of prepaid time period, it could be Week/Month/Year. Default value is
      Month.
    AllowedValues:
      - Week
      - Month
      - Year
    Default: Month
  AutoReleaseTime:
    Type: String
    Description: >-
      Auto release time for created host, Follow ISO8601 standard using UTC
      time. format is 'yyyy-MM-ddTHH:mm:ssZ'. Not bigger than 3 years from this
      day onwards
Resources:
  Host:
    Type: 'ALIYUN::ECS::DedicatedHost'
    Properties:
      AutoRenewPeriod:
        Ref: AutoRenewPeriod
      Description:
        Ref: Description
      NetworkAttributesSlbUdpTimeout:
        Ref: NetworkAttributesSlbUdpTimeout
      ResourceGroupId:
        Ref: ResourceGroupId
      ZoneId:
        Ref: ZoneId
      NetworkAttributesUdpTimeout:
        Ref: NetworkAttributesUdpTimeout
      AutoRenew:
        Ref: AutoRenew
      AutoPlacement:
        Ref: AutoPlacement
      Period:
        Ref: Period
      Quantity:
        Ref: Quantity
      DedicatedHostType:
        Ref: DedicatedHostType
      DedicatedHostName:
        Ref: DedicatedHostName
      ChargeType:
        Ref: ChargeType
      ActionOnMaintenance:
        Ref: ActionOnMaintenance
      Tags:
        Ref: Tags
      PeriodUnit:
        Ref: PeriodUnit
      AutoReleaseTime:
        Ref: AutoReleaseTime
Outputs:
  OrderId:
    Description: The order id list of created instance.
    Value:
      'Fn::GetAtt':
        - Host
        - OrderId
  DedicatedHostIds:
    Description: The host id list of created hosts
    Value:
      'Fn::GetAtt':
        - Host
        - DedicatedHostIds
```

