# ALIYUN::WAF::Instance

ALIYUN::WAF::Instance is used to create a Web Application Firewall \(WAF\) instance.

**Note:** Only the Singapore \(Singapore\) region is supported. The region ID is ap-southeast-1.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|BigScreen|String|Yes|No|Specifies whether to enable the data visualization service.|Valid values:-   0: The data visualization service is disabled.
-   1: The single-dashboard data visualization service is enabled.
-   all: The multi-dashboard data visualization service is enabled. |
|PrefessionalService|String|Yes|No|Specifies whether to enable the expert service.**Note:** The expert service allows you to consult experts about product configuration, policy optimization, and routine monitoring over DingTalk groups.

|Valid values:-   false: The expert service is disabled.
-   true: The expert service is enabled. |
|ExtDomainPackage|String|Yes|No|The number of extra domain packages.|Valid values: 0 to 1000.|
|LogTime|String|Yes|No|The log storage duration.|Valid values:-   180
-   360

Unit: days. |
|RenewalStatus|String|No|No|The auto-renewal status of the instance.|Default value: ManualRenewal. Valid values:-   AutoRenewal
-   ManualRenewal |
|RenewPeriod|String|No|No|The auto-renewal period for the created instance.|This parameter is required when the RenewalStatus parameter is set to AutoRenewal.Unit: months. |
|Period|String|No|No|The subscription period.|Unit: months. |
|ExclusiveIpPackage|String|Yes|No|The number of exclusive IP address packages.|Valid values: 0 to 100.|
|LogStorage|String|Yes|No|The log storage capacity.|Valid values:-   3
-   5
-   10
-   20
-   50
-   100

Unit: TiB. |
|SubscriptionType|String|Yes|No|The billing method.|Set the value to Subscription. |
|ExtBandwidth|String|Yes|No|The extra traffic.|Valid values: 0 to 20000.Unit: Mbit/s. |
|WafLog|String|Yes|No|Specifies whether to enable Log Service.|Valid values:-   true
-   false |
|PackageCode|String|Yes|No|The subscription WAF.|Valid values:-   version\_pro\_asia: WAF Pro
-   version\_business\_asia: WAF Business
-   version\_enterprise\_asia: WAF Enterprise
-   version\_exclusive\_cluster\_asia: WAF Exclusive |

## Response parameters

Fn::GetAtt

-   SubscriptionType: the billing method of the instance.
-   InstanceId: the ID of the WAF instance.
-   EndDate: the expiration time of the instance.

## Examples

`JSON` format

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

`YAML` format

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

