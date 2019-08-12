# ALIYUN::ECS::DedicatedHost {#concept_xsc_jmm_4fb .concept}

ALIYUN::ECS::DedicatedHost资源类型用于创建专有宿主机。

## 语法 {#section_xyg_tn2_lfb .section}

``` {#codeblock_pfh_h4v_o5j .language-json}
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

## 属性 {#section_cgd_53n_4fb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|DedicatedHostType|String|是|是|专有宿主机规格。|无|
|DedicatedHostName|String|否|否|专有宿主机的名称。长度为 \[2, 128\] 个英文或中文字符。必须以大小字母或中文开头，不能以 http:// 和 https:// 开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。|无|
|PeriodUnit|String|否|否|续费单位。| 取值范围：

 -   Week：周。此时，参数 Period 的取值范围为 \{1, 2, 3\}。

 -   Month（默认）：月。此时，参数 Period 的取值范围为 \{ 1, 2, 3, 6, 12\}。

 |
|AutoReleaseTime|String|否|否| 自动释放时间。如果不输入 AutoReleaseTime 参数，表示取消自动释放，专有宿主机在预约时间点不再自动释放。

 -   最短不能晚于当前时间半小时内。

 -   最长不能超过当前时间三年以后。

 -   如果秒（`ss`）取值不是 `00`，则自动取为当前分钟（`mm`）开始时刻。

 |无|
|Description|String|否|否|专有宿主机的描述。|无|
|AutoRenewPeriod|Number|否|否|单次自动续费的周期，单位：月。|可用值：1，2，3，6，12。|
|Period|Number|否|否|预付费时长。单位：月。|取值范围：1-9，12，24，36，48，60。|
|ZoneId|String|否|否| 专有宿主机所属的可用区编号。

 默认值：空，表示由系统选择。

 |无|
|AutoRenew|String|否|否| 是否自动续费预付费的专有宿主机。

 默认值：False

 |取值范围： True|
|ChargeType|String|否|否|专有宿主机的计费方式。| 取值范围：PrePaid：预付费，即包年包月。

 选择预付费时，请确认您的支付方式支持余额或者信用额度支付，否则会提示 `InvalidPayMethod`。

 |

## 返回值 {#section_fsg_t4n_4fb .section}

**Fn::GetAtt**

-   OrderId: 订单id。
-   DedicatedHostIds：主机id列表。

## 示例 {#section_klp_54n_4fb .section}

``` {#codeblock_kwl_c1b_8mv}
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
      "Description": "Whether renew the fee automatically? When the parameter InstanceChargeType is PrePaid, it will take effect. Range of value:True: automatic renewal.False: no automatic renewal. Default value is False.",
      "AllowedValues": [
        "True",
        "False"
      ],
      "Default": "False"
    },
    "Period": {
      "Type": "Number",
      "Description": "Prepaid time period. Unit is month, it could be from 1 to 9 or 12, 24, 36, 48, 60\. Default value is 1.",
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
      "Description": "Unit of prepaid time period, it could be Week/Month. Default value is Month.",
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

