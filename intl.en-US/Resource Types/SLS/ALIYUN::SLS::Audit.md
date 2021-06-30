# ALIYUN::SLS::Audit

ALIYUN::SLS::Audit is used to configure the Log Audit Service application.

**Note:** For more information about the Log Audit Service application, see [Background information](/intl.en-US/Application/Log Audit Service/Background information.md).

## Syntax

```
{
  "Type": "ALIYUN::SLS::Audit",
  "Properties": {
    "VariableMap": Map,
    "DisplayName": String,
    "MultiAccount": List
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|VariableMap|Map|Yes|Yes|The detailed configurations of the Log Audit Service application.|For more information, see [VariableMap properties](#section_m5f_x9l_q4r).|
|DisplayName|String|Yes|No|The display name of the Log Audit Service application.|The name can be up to 128 characters in length.|
|MultiAccount|List|No|Yes|The list of accounts from which the Log Audit Service application collects and audits logs.|Separate multiple Alibaba Cloud account IDs with commas \(,\). A maximum of 100 Alibaba Cloud accounts can be configured. |

## VariableMap syntax

```
"VariableMap": {
  "ApigatewayTtl": Number,
  "SasCrackEnabled": Boolean,
  "CpsEnabled": Boolean,
  "ApigatewayEnabled": Boolean,
  "WafEnabled": Boolean,
  "OssSyncTtl": Number,
  "SasTtl": Number,
  "ActiontrailTtl": Number,
  "OssAccessEnabled": Boolean,
  "OssSyncEnabled": Boolean,
  "SasSnapshotAccountEnabled": Boolean,
  "SlbSyncEnabled": Boolean,
  "SlbAccessTtl": Number,
  "BastionEnabled": Boolean,
  "RdsEnabled": Boolean,
  "SasSessionEnabled": Boolean,
  "SasLocalDnsEnabled": Boolean,
  "OssAccessTtl": Number,
  "SasHttpEnabled": Boolean,
  "BastionTtl": Number,
  "OssMeteringEnabled": Boolean,
  "SasProcessEnabled": Boolean,
  "NasEnabled": Boolean,
  "SasDnsEnabled": Boolean,
  "SasSnapshotPortEnabled": Boolean,
  "SasSecurityAlertEnabled": Boolean,
  "SlbAccessEnabled": Boolean,
  "NasTtl": Number,
  "SasNetworkEnabled": Boolean,
  "SasLoginEnabled": Boolean,
  "WafTtl": Number,
  "OssMeteringTtl": Number,
  "SasSnapshotProcessEnabled": Boolean,
  "SasSecurityHcEnabled": Boolean,
  "RdsTtl": Number,
  "CpsTtl": Number,
  "SlbSyncTtl": Number,
  "CloudfirewallTtl": Number,
  "ActiontrailEnabled": Boolean,
  "SasSecurityVulEnabled": Boolean
}
```

## VariableMap properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ApigatewayTtl|Number|No|Yes|The retention period of the access logs of API Gateway in the Logstore.|Valid values: 3 to 3000. Default value: 180.

Unit: days. |
|SasCrackEnabled|Boolean|No|Yes|Specifies whether to audit the brute-force attack logs in Security Center \(SAS\).|Default value: false. Valid values:-   true
-   false |
|CpsEnabled|Boolean|No|Yes|Specifies whether to audit the push receipt events of Alibaba Cloud Mobile Push.|Default value: true. Valid values:-   true
-   false |
|ApigatewayEnabled|Boolean|No|Yes|Specifies whether to audit the access logs of API Gateway.|Default value: true. Valid values:-   true
-   false |
|WafEnabled|Boolean|No|Yes|Specifies whether to audit the access logs of Web Application Firewall \(WAF\).|Default value: true. Valid values:-   true
-   false |
|OssSyncTtl|Number|No|Yes|The period during which the Object Storage Service \(OSS\) logs are centrally stored in the Logstore.|Valid values: 3 to 3000. Default value: 180.

Unit: days.

For more information about centralized storage, see [Benefits](/intl.en-US/Application/Log Audit Service/Background information.md). |
|SasTtl|Number|No|Yes|The retention period of the SAS logs in the Logstore.|Valid values: 3 to 3000. Default value: 180.

Unit: days. |
|ActiontrailTtl|Number|No|Yes|The retention period of the operation logs of ActionTrail in the Logstore.|None|
|OssAccessEnabled|Boolean|No|Yes|Specifies whether to audit the access logs of OSS.|Default value: true. Valid values:-   true
-   false |
|OssSyncEnabled|Boolean|No|Yes|Specifies whether to store the OSS logs in the central project.|Default value: true. Valid values:-   true
-   false

**Note:** You can store the collected logs in the central project. This improves efficiency when you query, analyze, and visualize the collected logs. You can also configure alerts for the logs and perform secondary development. |
|SasSnapshotAccountEnabled|Boolean|No|Yes|Specifies whether to collect the account snapshots in SAS.|Default value: false. Valid values:-   true
-   false |
|SlbSyncEnabled|Boolean|No|Yes|Specifies whether to store the Server Load Balancer \(SLB\) logs in the central project.|Default value: true. Valid values:-   true
-   false |
|SlbAccessTtl|Number|No|Yes|The retention period of the access logs of SLB in the Logstore.|Valid values: 3 to 3000. Default value: 180.

Unit: days. |
|BastionEnabled|Boolean|No|Yes|Specifies whether to audit the operation logs of Bastionhost.|Default value: true. Valid values:-   true
-   false |
|RdsEnabled|Boolean|No|Yes|Specifies whether to audit the ApsaraDB RDS logs.|Default value: true. Valid values:-   true
-   false |
|SasSessionEnabled|Boolean|No|Yes|Specifies whether to audit the network session logs in SAS.|Default value: false. Valid values:-   true
-   false |
|SasLocalDnsEnabled|Boolean|No|Yes|Specifies whether to audit the local Domain Name System \(DNS\) logs in SAS.|Default value: false. Valid values:-   true
-   false |
|OssAccessTtl|Number|No|Yes|The retention period of the access logs of OSS in the Logstore.|Valid values: 3 to 3000. Default value: 180.

Unit: days. |
|SasHttpEnabled|Boolean|No|Yes|Specifies whether to audit the web access logs in SAS.|Default value: false. Valid values:-   true
-   false |
|BastionTtl|Number|No|Yes|The retention period of the operation logs of Bastionhost in the Logstore.|Valid values: 3 to 3000. Default value: 180.

Unit: days. |
|OssMeteringEnabled|Boolean|No|Yes|Specifies whether to audit the metering logs of OSS.|Default value: true. Valid values:-   true
-   false |
|SasProcessEnabled|Boolean|No|Yes|Specifies whether to audit the process startup logs in SAS.|Default value: false. Valid values:-   true
-   false |
|NasEnabled|Boolean|No|Yes|Specifies whether to audit the access logs of Apsara File Storage NAS.|Default value: true. Valid values:-   true
-   false |
|SasDnsEnabled|Boolean|No|Yes|Specifies whether to audit the DNS logs in SAS.|Default value: false. Valid values:-   true
-   false |
|SasSnapshotPortEnabled|Boolean|No|Yes|Specifies whether to audit the port snapshots in SAS.|Default value: false. Valid values:-   true
-   false |
|SasSecurityAlertEnabled|Boolean|No|Yes|Specifies whether to audit the security alert logs in SAS.|Default value: false. Valid values:-   true
-   false |
|SlbAccessEnabled|Boolean|No|Yes|Specifies whether to audit the access logs of SLB.|Default value: true. Valid values:-   true
-   false |
|NasTtl|Number|No|Yes|The retention period of the access logs of NAS in the Logstore.|Valid values: 3 to 3000. Default value: 180.

Unit: days. |
|SasNetworkEnabled|Boolean|No|Yes|Specifies whether to audit the network connection logs in SAS.|Default value: false. Valid values:-   true
-   false |
|SasLoginEnabled|Boolean|No|Yes|Specifies whether to audit the logon logs in SAS.|Default value: false. Valid values:-   true
-   false |
|WafTtl|Number|No|Yes|The retention period of the access logs of WAF in the Logstore.|Default value: true. Valid values:-   true
-   false |
|OssMeteringTtl|Number|No|Yes|The retention period of the metering logs of OSS in the Logstore.|Valid values: 3 to 3000. Default value: 180.

Unit: days. |
|SasSnapshotProcessEnabled|Boolean|No|Yes|Specifies whether to audit the process snapshots in SAS.|Default value: false. Valid values:-   true
-   false |
|SasSecurityHcEnabled|Boolean|No|Yes|Specifies whether to audit the baseline logs in SAS.|Default value: false. Valid values:-   true
-   false |
|RdsTtl|Number|No|Yes|The retention period of the ApsaraDB RDS logs in the Logstore.|Valid values: 3 to 3000. Default value: 180.

Unit: days. |
|CpsTtl|Number|No|Yes|The retention period of the push receipt events of Alibaba Cloud Mobile Push in the Logstore.|Valid values: 3 to 3000. Default value: 180.

Unit: days. |
|SlbSyncTtl|Number|No|Yes|The period during which the access logs of SLB are centrally stored in the Logstore.|Valid values: 3 to 3000. Default value: 180.

Unit: days. |
|CloudfirewallTtl|Number|No|Yes|The retention period of the Internet access logs of Cloud Firewall \(CFW\) in the Logstore.|Valid values: 3 to 3000. Default value: 180.

Unit: days. |
|ActiontrailEnabled|Boolean|No|Yes|Specifies whether to audit the operation logs of ActionTrail.|Default value: true. Valid values:-   true
-   false |
|SasSecurityVulEnabled|Boolean|No|Yes|Specifies whether to audit the vulnerability logs in SAS.|Default value: false. Valid values:-   true
-   false |

## Response parameters

Fn::GetAtt

DisplayName: the display name of the Log Audit Service application.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "VariableMap": {
      "Type": "Json",
      "Description": "Log audit detailed configuration."
    },
    "DisplayName": {
      "Type": "String",
      "Description": "Name of SLS log audit.",
      "MaxLength": 128
    },
    "MultiAccount": {
      "Type": "Json",
      "Description": "Multi-account configuration, please fill in multiple aliuid.",
      "MinLength": 0,
      "MaxLength": 100
    }
  },
  "Resources": {
    "Audit": {
      "Type": "ALIYUN::SLS::Audit",
      "Properties": {
        "VariableMap": {
          "Ref": "VariableMap"
        },
        "DisplayName": {
          "Ref": "DisplayName"
        },
        "MultiAccount": {
          "Ref": "MultiAccount"
        }
      }
    }
  },
  "Outputs": {
    "DisplayName": {
      "Description": "Name of SLS log audit.",
      "Value": {
        "Fn::GetAtt": [
          "Audit",
          "DisplayName"
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
  DisplayName:
    Description: Name of SLS log audit.
    MaxLength: 128
    Type: String
  MultiAccount:
    Description: Multi-account configuration, please fill in multiple aliuid.
    MaxLength: 100
    MinLength: 0
    Type: Json
  VariableMap:
    Description: Log audit detailed configuration.
    Type: Json
Resources:
  Audit:
    Properties:
      DisplayName:
        Ref: DisplayName
      MultiAccount:
        Ref: MultiAccount
      VariableMap:
        Ref: VariableMap
    Type: ALIYUN::SLS::Audit
Outputs:
  DisplayName:
    Description: Name of SLS log audit.
    Value:
      Fn::GetAtt:
      - Audit
      - DisplayName
```

