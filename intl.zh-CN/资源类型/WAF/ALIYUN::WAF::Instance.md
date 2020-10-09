# ALIYUN::WAF::Instance

ALIYUN::WAF::Instance类型用于创建Web应用防火墙实例。

**说明：** 支持的地域为亚太东南1（新加坡）：ap-southeast-1。

## 语法

```
{
  "Type": "ALIYUN::WAF::Instance",
  "Properties": {
    "BigScreen": String,
    "PrefessionalService": String,
    "ExtDomainPackage": String,
    "LogTime": String,
    "RenewalStatus": String,
    "RenewPeriod": String,
    "Period": String,
    "ExclusiveIpPackage": String,
    "LogStorage": String,
    "SubscriptionType": String,
    "ExtBandwidth": String,
    "WafLog": String,
    "PackageCode": String
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|BigScreen|String|是|否|可视化大屏服务。|取值：-   0：不开启服务。
-   1：单屏服务。
-   all：多屏服务。 |
|PrefessionalService|String|是|否|是否使用产品专家服务。**说明：** 专家服务：提供钉钉群交流，负责产品配置、策略优化、日常监控。

|取值：-   false：不使用。
-   true：使用。 |
|ExtDomainPackage|String|是|否|域名扩展包数量。|取值范围：0~1000。|
|LogTime|String|是|否|日志存储时长。|取值：-   180
-   360

单位：天。 |
|RenewalStatus|String|否|否|自动续费状态。|取值：-   AutoRenewal：自动续费。
-   ManualRenewal（默认值）：手动续费。 |
|RenewPeriod|String|否|否|自动续费周期 。|当设置RenewalStatus为AutoRenewal时，必须指定该参数。单位：月。 |
|Period|String|否|否|预付费周期。|单位：月。 |
|ExclusiveIpPackage|String|是|否|域名独享资源包数量。|取值范围：0~100。|
|LogStorage|String|是|否|日志存储容量。|取值：-   3
-   5
-   10
-   20
-   50
-   100

单位：TiB 。 |
|SubscriptionType|String|是|否|付费类型。|取值：Subscription：预付费。 |
|ExtBandwidth|String|是|否|带宽扩展包。|取值范围：0～20,000。单位：Mbps。 |
|WafLog|String|是|否|是否启用日志服务。|取值：-   true
-   false |
|PackageCode|String|是|否|套餐。|取值：-   version\_pro\_asia：高级版。
-   version\_business\_asia：企业版。
-   version\_enterprise\_asia：旗舰版。
-   version\_exclusive\_cluster\_asia：独享版。 |

## 返回值

Fn::GetAtt

-   SubscriptionType：付费类型。
-   InstanceId：WAF实例ID。
-   EndDate：实例到期时间。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "PrefessionalService": {
      "Type": "String",
      "Description": ""
    },
    "BigScreen": {
      "Type": "String",
      "Description": ""
    },
    "ExtDomainPackage": {
      "Type": "String",
      "Description": ""
    },
    "LogTime": {
      "Type": "String",
      "Description": ""
    },
    "RenewalStatus": {
      "Type": "String",
      "Description": ""
    },
    "RenewPeriod": {
      "Type": "String",
      "Description": ""
    },
    "Period": {
      "Type": "String",
      "Description": ""
    },
    "ExclusiveIpPackage": {
      "Type": "String",
      "Description": ""
    },
    "LogStorage": {
      "Type": "String",
      "Description": ""
    },
    "SubscriptionType": {
      "Type": "String",
      "Description": "Subscription type of the instance"
    },
    "ExtBandwidth": {
      "Type": "String",
      "Description": ""
    },
    "WafLog": {
      "Type": "String",
      "Description": ""
    },
    "PackageCode": {
      "Type": "String",
      "Description": ""
    }
  },
  "Resources": {
    "WAFInstance": {
      "Type": "ALIYUN::WAF::Instance",
      "Properties": {
        "PrefessionalService": {
          "Ref": "PrefessionalService"
        },
        "BigScreen": {
          "Ref": "BigScreen"
        },
        "ExtDomainPackage": {
          "Ref": "ExtDomainPackage"
        },
        "LogTime": {
          "Ref": "LogTime"
        },
        "RenewalStatus": {
          "Ref": "RenewalStatus"
        },
        "RenewPeriod": {
          "Ref": "RenewPeriod"
        },
        "Period": {
          "Ref": "Period"
        },
        "ExclusiveIpPackage": {
          "Ref": "ExclusiveIpPackage"
        },
        "LogStorage": {
          "Ref": "LogStorage"
        },
        "SubscriptionType": {
          "Ref": "SubscriptionType"
        },
        "ExtBandwidth": {
          "Ref": "ExtBandwidth"
        },
        "WafLog": {
          "Ref": "WafLog"
        },
        "PackageCode": {
          "Ref": "PackageCode"
        }
      }
    }
  },
  "Outputs": {
    "SubscriptionType": {
      "Description": "Subscription type of the instance",
      "Value": {
        "Fn::GetAtt": [
          "WAFInstance",
          "SubscriptionType"
        ]
      }
    },
    "Trial": {
      "Description": "Trial version",
      "Value": {
        "Fn::GetAtt": [
          "WAFInstance",
          "Trial"
        ]
      }
    },
    "InstanceId": {
      "Description": "Instance ID",
      "Value": {
        "Fn::GetAtt": [
          "WAFInstance",
          "InstanceId"
        ]
      }
    },
    "InDebt": {
      "Description": "Instance is overdue",
      "Value": {
        "Fn::GetAtt": [
          "WAFInstance",
          "InDebt"
        ]
      }
    },
    "RemainDay": {
      "Description": "Number of available days for WAF Trial version",
      "Value": {
        "Fn::GetAtt": [
          "WAFInstance",
          "RemainDay"
        ]
      }
    },
    "EndDate": {
      "Description": "Due date of the instance",
      "Value": {
        "Fn::GetAtt": [
          "WAFInstance",
          "EndDate"
        ]
      }
    }
  }
}
```

`YAML`格式

```
ROSTemplateFormatVersion: '2015-09-01'
Parameters:
  PrefessionalService:
    Type: String
    Description: ''
  BigScreen:
    Type: String
    Description: ''
  ExtDomainPackage:
    Type: String
    Description: ''
  LogTime:
    Type: String
    Description: ''
  RenewalStatus:
    Type: String
    Description: ''
  RenewPeriod:
    Type: String
    Description: ''
  Period:
    Type: String
    Description: ''
  ExclusiveIpPackage:
    Type: String
    Description: ''
  LogStorage:
    Type: String
    Description: ''
  SubscriptionType:
    Type: String
    Description: Subscription type of the instance
  ExtBandwidth:
    Type: String
    Description: ''
  WafLog:
    Type: String
    Description: ''
  PackageCode:
    Type: String
    Description: ''
Resources:
  WAFInstance:
    Type: 'ALIYUN::WAF::Instance'
    Properties:
      PrefessionalService:
        Ref: PrefessionalService
      BigScreen:
        Ref: BigScreen
      ExtDomainPackage:
        Ref: ExtDomainPackage
      LogTime:
        Ref: LogTime
      RenewalStatus:
        Ref: RenewalStatus
      RenewPeriod:
        Ref: RenewPeriod
      Period:
        Ref: Period
      ExclusiveIpPackage:
        Ref: ExclusiveIpPackage
      LogStorage:
        Ref: LogStorage
      SubscriptionType:
        Ref: SubscriptionType
      ExtBandwidth:
        Ref: ExtBandwidth
      WafLog:
        Ref: WafLog
      PackageCode:
        Ref: PackageCode
Outputs:
  SubscriptionType:
    Description: Subscription type of the instance
    Value:
      'Fn::GetAtt':
        - WAFInstance
        - SubscriptionType
  Trial:
    Description: Trial version
    Value:
      'Fn::GetAtt':
        - WAFInstance
        - Trial
  InstanceId:
    Description: Instance ID
    Value:
      'Fn::GetAtt':
        - WAFInstance
        - InstanceId
  InDebt:
    Description: Instance is overdue
    Value:
      'Fn::GetAtt':
        - WAFInstance
        - InDebt
  RemainDay:
    Description: Number of available days for WAF Trial version
    Value:
      'Fn::GetAtt':
        - WAFInstance
        - RemainDay
  EndDate:
    Description: Due date of the instance
    Value:
      'Fn::GetAtt':
        - WAFInstance
        - EndDate
```

