# ALIYUN::SLS::Audit

ALIYUN::SLS::Audit类型用于配置日志审计服务。

**说明：** 关于日志审计服务的更多信息，请参见[简介](/cn.zh-CN/应用中心（App）/日志审计服务/简介.md)。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|VariableMap|Map|是|是|日志审计服务的详细配置。|更多信息，请参见[VariableMap属性](#section_m5f_x9l_q4r)。|
|DisplayName|String|是|否|日志审计服务的名称。|长度不超过128个字符。|
|MultiAccount|List|否|是|日志审计服务的多账号配置。|请填写多个阿里云账号ID，多个阿里云账号ID间用半角逗号（,）分隔。最多支持配置100个阿里云账号。 |

## VariableMap语法

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

## VariableMap属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ApigatewayTtl|Number|否|是|API网关的访问日志在日志库的存储时间。|取值范围：3~3000。默认值：180。

单位：天。 |
|SasCrackEnabled|Boolean|否|是|是否审计云安全中心SAS的暴力破解日志。|取值：-   true
-   false（默认值） |
|CpsEnabled|Boolean|否|是|是否审计移动推送的推送回执事件。|取值：-   true（默认值）
-   false |
|ApigatewayEnabled|Boolean|否|是|是否审计API网关的访问日志。|取值：-   true（默认值）
-   false |
|WafEnabled|Boolean|否|是|是否审计应用防火墙WAF的访问日志。|取值：-   true（默认值）
-   false |
|OssSyncTtl|Number|否|是|对象存储OSS的日志在日志库的中心化存储时间。|取值范围：3~3000。默认值：180。

单位：天。

关于中心化存储的更多信息，请参见[技术优势](/cn.zh-CN/应用中心（App）/日志审计服务/简介.md)。 |
|SasTtl|Number|否|是|云安全中心SAS的日志在日志库的存储时间。|取值范围：3~3000。默认值：180。

单位：天。 |
|ActiontrailTtl|Number|否|是|操作审计的操作日志在日志库的存储时间。|无|
|OssAccessEnabled|Boolean|否|是|是否审计对象存储OSS的访问日志。|取值：-   true（默认值）
-   false |
|OssSyncEnabled|Boolean|否|是|是否将对象存储OSS的日志存储到中心化Project。|取值：-   true（默认值）
-   false

**说明：** 您可以将采集到的日志存储到中心化Project，方便后续查询分析、可视化与告警、二次开发等。 |
|SasSnapshotAccountEnabled|Boolean|否|是|是否采集云安全中心SAS的账号快照。|取值：-   true
-   false（默认值） |
|SlbSyncEnabled|Boolean|否|是|是否将负载均衡SLB的日志存储到中心化Project。|取值：-   true（默认值）
-   false |
|SlbAccessTtl|Number|否|是|负载均衡SLB的访问日志在日志库的存储时间。|取值范围：3~3000。默认值：180。

单位：天。 |
|BastionEnabled|Boolean|否|是|是否审计堡垒机的操作日志。|取值：-   true（默认值）
-   false |
|RdsEnabled|Boolean|否|是|是否审计云数据库RDS的日志。|取值：-   true（默认值）
-   false |
|SasSessionEnabled|Boolean|否|是|是否审计云安全中心SAS的网络会话日志。|取值：-   true
-   false（默认值） |
|SasLocalDnsEnabled|Boolean|否|是|是否审计云安全中心SAS的本地DNS日志。|取值：-   true
-   false（默认值） |
|OssAccessTtl|Number|否|是|对象存储OSS的访问日志在日志库的存储时间。|取值范围：3~3000。默认值：180。

单位：天。 |
|SasHttpEnabled|Boolean|否|是|是否审计云安全中心的Web访问日志。|取值：-   true
-   false（默认值） |
|BastionTtl|Number|否|是|堡垒机的操作日志在在日志库的存储时间。|取值范围：3~3000。默认值：180。

单位：天。 |
|OssMeteringEnabled|Boolean|否|是|是否审计对象存储OSS的计量日志。|取值：-   true（默认值）
-   false |
|SasProcessEnabled|Boolean|否|是|是否审计云安全中心SAS的进程启动日志。|取值：-   true
-   false（默认值） |
|NasEnabled|Boolean|否|是|是否审计文件存储NAS的访问日志。|取值：-   true（默认值）
-   false |
|SasDnsEnabled|Boolean|否|是|是否审计云安全中心SAS的 DNS解析日志。|取值：-   true
-   false（默认值） |
|SasSnapshotPortEnabled|Boolean|否|是|是否审计云安全中心SAS的端口快照。|取值：-   true
-   false（默认值） |
|SasSecurityAlertEnabled|Boolean|否|是|是否审计云安全中心SAS的安全告警日志。|取值：-   true
-   false（默认值） |
|SlbAccessEnabled|Boolean|否|是|是否审计负载均衡SLB的访问日志。|取值：-   true（默认值）
-   false |
|NasTtl|Number|否|是|文件存储NAS的访问日志在日志库的存储时间。|取值范围：3~3000。默认值：180。

单位：天。 |
|SasNetworkEnabled|Boolean|否|是|是否审计云安全中心SAS的网络连接日志。|取值：-   true
-   false（默认值） |
|SasLoginEnabled|Boolean|否|是|是否审计云安全中心SAS的登录流水日志。|取值：-   true
-   false（默认值） |
|WafTtl|Number|否|是|应用防火墙WAF的访问日志在日志库的存储时间。|取值：-   true（默认值）
-   false |
|OssMeteringTtl|Number|否|是|对象存储OSS的计量日志在日志库的存储时间。|取值范围：3~3000。默认值：180。

单位：天。 |
|SasSnapshotProcessEnabled|Boolean|否|是|是否审计云安全中心SAS的进程快照。|取值：-   true
-   false（默认值） |
|SasSecurityHcEnabled|Boolean|否|是|是否审计云安全中心SAS的基线日志。|取值：-   true
-   false（默认值） |
|RdsTtl|Number|否|是|云数据库RDS的日志在日志库的存储时间。|取值范围：3~3000。默认值：180。

单位：天。 |
|CpsTtl|Number|否|是|移动推送的推送回执事件在日志库的存储时间。|取值范围：3~3000。默认值：180。

单位：天。 |
|SlbSyncTtl|Number|否|是|负载均衡SLB的访问日志在日志库的中心化存储时间。|取值范围：3~3000。默认值：180。

单位：天。 |
|CloudfirewallTtl|Number|否|是|云防火墙的互联网访问日志在日志库的存储时间。|取值范围：3~3000。默认值：180。

单位：天。 |
|ActiontrailEnabled|Boolean|否|是|是否审计操作审计的操作日志。|取值：-   true（默认值）
-   false |
|SasSecurityVulEnabled|Boolean|否|是|是否审计云安全中心SAS的漏洞日志。|取值：-   true
-   false（默认值） |

## 返回值

Fn::GetAtt

DisplayName：SLS日志审计的名称。

## 示例

`JSON`格式

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

`YAML`格式

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

