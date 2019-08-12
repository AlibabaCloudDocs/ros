# ALIYUN::ECS::DedicatedHost {#concept_xsc_jmm_4fb .concept}

Creates dedicated hosts \(DDHs\).

## Syntax {#section_xyg_tn2_lfb .section}

```language-json
{
  "Type": "ALIYUN::ECS::DedicatedHost",
  "Properties": {
    "DedicatedHostType": String,
    "DedicatedHostName": String,
    "PeriodUnit": String,
    "AutoReleaseTime": String,
    "Description": String,
    "AutoRenewPeriod": String,
    "Period": String,
    "ZoneId": String,
    "AutoRenew": String,
    "ChargeType": String
  }
}
```

## Properties {#section_cgd_53n_4fb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|DedicatedHostType|String|Yes|Yes|The specifications of a DDH.|N/A|
|DedicatedHostName|String|No|No|The name of a DDH. The name must be 2 to 128 characters in length, including digits, colons \(:\), underscores \(\_\) and hyphens \(-\). It must start with an uppercase letter, a lowercase letter, or a Chinese character and must not start with http:// or https://.|N/A|
|PeriodUnit|String|No|No|The unit of the billing cycle you select to extend the subscription.| Valid values:

 -   Week. Valid values of the Period parameter: 1 | 2 | 3.

 -   Month \(default value\). Valid values of the Period parameter: 1 | 2 | 3 | 6 | 12.

 |
|AutoReleaseTime|String|No|No| The time scheduled for a DDH to be automatically released. If you do not specify the AutoReleaseTime parameter, the automatic release feature is disabled. In this case, the DDH is not released as scheduled.

 -   The specified release time for the DDH cannot be earlier than 30 minutes after the start time

 -   or three years later than the start time.

 -   If the `ss` parameter is not set to 00, the default value for the`mm` parameter is set to the current start time.``

 |N/A|
|Description|String|No|No|The description of a DDH.|N/A|
|AutoRenewPeriod|Number|No|No|The billing cycle for automatic renewal after a DDH expires. Unit: month.|Valid values: 1 | 2 | 3 | 6 | 12.|
|Period|Number|No|No|The subscription period of a DDH. Unit: month.|Valid values: 1 to 9 | 12 | 24 | 36 | 48 | 60.|
|ZoneId|String|No|No| The ID of the zone where a DDH is located.

 This parameter is unspecified by default. The DDH is randomly assigned to a zone by default.

 |N/A|
|AutoRenew|String|No|No| Specifies whether the automatic renewal feature of a DDH is enabled.

 Default value: False.

 |Valid value: True.|
|ChargeType|String|No|No|The billing method of a DDH.| Valid value: PrePaid. The subscription, or prepaid service, is billed on a yearly or monthly basis.

 You must ensure the balance of your account or credit balance can cover the cost of subscription. Otherwise, you will receive an `InvalidPayMethod`error code.

 |

## Response elements {#section_fsg_t4n_4fb .section}

**Fn::GetAtt**

-   OrderId: indicates the ID of a DDH order.
-   DedicatedHostIds: indicates the list of DDH IDs.

## Example {#section_klp_54n_4fb .section}

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "AutoRenewPeriod": {
      "Type": "Number",
      "Description": "The time period of auto renew. When the parameter InstanceChargeType is PrePaid, it will take effect.It could be 1, 2, 3, 6, 12\. Default value is 1.",
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
    "ZoneId": {
      "Type": "String",
      "Description": "The zone to create the host."
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
    "AutoRenew": {
      "Type": "String",
      "Description": "Whether renew the fee automatically? The subscription is automatically renewed when the parameter InstanceChargeType is PrePaid. Range of value:True: automatic renewal.False: no automatic renewal. Default value is False.",
      Alliwedvalues ":[
        "True",
        "False"
      ],
      "Default": "False"
    },
    "Period": {
      "Type": "Number",
      "Description": "Prepaid time period. Unit is month, it can be from 1 to 9 or 12, 24, 36, 48, 60\. Default value is 1.",
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
    "DedicatedHostType": {
      "Type": "String",
      "Description": "The instance type of host."
    },
    "PeriodUnit": {
      "Type": "String",
      "Description": "Unit of prepaid time period, it can be Week/Month. Default value is Month.",
      "AllowedValues": [
        "Week",
        "Month"
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
        "ZoneId": {
          "Ref": "ZoneId"
        },
        "DedicatedHostName": {
          "Ref": "DedicatedHostName"
        },
        "ChargeType": {
          "Ref": "ChargeType"
        },
        "AutoRenew": {
          "Ref": "AutoRenew"
        },
        "Period": {
          "Ref": "Period"
        },
        "DedicatedHostType": {
          "Ref": "DedicatedHostType"
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
      "Description": "The order id list of a created instance.",
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

