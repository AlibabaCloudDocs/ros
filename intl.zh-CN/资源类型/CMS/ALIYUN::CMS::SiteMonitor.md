# ALIYUN::CMS::SiteMonitor

ALIYUN::CMS::SiteMonitor类型用于创建站点监控的监控任务。

## 语法

```
{
  "Type": "ALIYUN::CMS::SiteMonitor",
  "Properties": {
    "Address": String,
    "OptionsJson": String,
    "TaskName": String,
    "TaskType": String,
    "IspCities": List,
    "Interval": Integer,
    "AlertIds": List
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Address|String|是|是|监控任务的URL或IP地址。|无|
|OptionsJson|String|否|是|监控任务对应协议类型的高级扩展选项。不同监控任务的协议类型对应不同的扩展选项。|无|
|TaskName|String|是|是|监控任务名称。|长度为4~100个字符，可包含英文字母、汉字、数字和下划线（\_）。|
|TaskType|String|是|否|监控任务类型。|取值：-   HTTP（s）
-   PING
-   TCP
-   UDP
-   DNS
-   SMTP
-   POP3
-   FTP |
|IspCities|List|否|是|探针信息。|如果该参数取值为空，则系统随机选择3个探测点。更多信息，请参见[IspCities属性](#section_run_2se_hms)。 |
|Interval|Integer|否|是|监控频率。|取值：-   1（默认值）
-   5
-   15

单位：分钟。|
|AlertIds|List|否|否|报警规则ID。|您可以调用[DescribeMetricRuleList](/intl.zh-CN/API参考/时序指标报警规则/DescribeMetricRuleList.md)接口查询云监控中已存在的报警规则ID。|

## IspCities语法

```
"IspCities": [
  {
    "Isp": String,
    "City": String
  }
]
```

## IspCities属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Isp|String|是|否|探测的运营商名称或ID。运营商名称支持模糊查询。|更多信息，请参见[DescribeSiteMonitorISPCityList](/intl.zh-CN/API参考/站点监控/DescribeSiteMonitorISPCityList.md)。|
|City|String|是|否|探测的城市名称或ID。城市名称支持模糊查询。|无|

## 返回值

Fn::GetAtt

TaskId：监控任务ID。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Address": {
      "Type": "String",
      "Description": "The URL or IP address monitored by the monitoring task."
    },
    "OptionsJson": {
      "Type": "String",
      "Description": "The extended options of the protocol that is used by the site monitoring task. The\noptions vary based on the protocol."
    },
    "TaskName": {
      "Type": "String",
      "Description": "The name of the site monitoring task. The name must be 4 to 100 characters in length.\nIt can contain letters, digits, and underscores (_)."
    },
    "TaskType": {
      "Type": "String",
      "Description": "The protocol used by the site monitoring task. Valid values: HTTP, HTTPS, PING, TCP,\nUDP, DNS, SMTP, POP3, and FTP."
    },
    "IspCities": {
      "Type": "Json",
      "Description": "The information about detection points, which is specified in a JSON array. Example:\n[{\"city\":\"546\",\"isp\":\"465\"},{\"city\":\"572\",\"isp\":\"465\"},{\"city\":\"738\",\"isp\":\"465\"}]. The three city codes represent Beijing, Hangzhou, and Qingdao.\nNote You can call the DescribeSiteMonitorISPCityList API operation to query the detection\npoints that can be used to create site monitoring tasks. For more information, see\nDescribeSiteMonitorISPCityList . If this parameter is not specified, the system randomly selects three detection\npoints for site monitoring."
    },
    "Interval": {
      "Type": "Number",
      "Description": "The interval at which detection requests are sent. Valid values: 1, 5, and 15. Unit:\nminutes. Default value: 1."
    },
    "AlertIds": {
      "Type": "Json",
      "Description": ""
    }
  },
  "Resources": {
    "SiteMonitor": {
      "Type": "ALIYUN::CMS::SiteMonitor",
      "Properties": {
        "Address": {
          "Ref": "Address"
        },
        "OptionsJson": {
          "Ref": "OptionsJson"
        },
        "TaskName": {
          "Ref": "TaskName"
        },
        "TaskType": {
          "Ref": "TaskType"
        },
        "IspCities": {
          "Ref": "IspCities"
        },
        "Interval": {
          "Ref": "Interval"
        },
        "AlertIds": {
          "Ref": "AlertIds"
        }
      }
    }
  },
  "Outputs": {
    "TaskId": {
      "Description": "The ID of the site monitoring task.",
      "Value": {
        "Fn::GetAtt": [
          "SiteMonitor",
          "TaskId"
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
  Address:
    Type: String
    Description: The URL or IP address monitored by the monitoring task.
  OptionsJson:
    Type: String
    Description: >-
      The extended options of the protocol that is used by the site monitoring
      task. The

      options vary based on the protocol.
  TaskName:
    Type: String
    Description: >-
      The name of the site monitoring task. The name must be 4 to 100 characters
      in length.

      It can contain letters, digits, and underscores (_).
  TaskType:
    Type: String
    Description: >-
      The protocol used by the site monitoring task. Valid values: HTTP, HTTPS,
      PING, TCP,

      UDP, DNS, SMTP, POP3, and FTP.
  IspCities:
    Type: Json
    Description: >-
      The information about detection points, which is specified in a JSON
      array. Example:

      [{"city":"546","isp":"465"},{"city":"572","isp":"465"},{"city":"738","isp":"465"}].
      The three city codes represent Beijing, Hangzhou, and Qingdao.

      Note You can call the DescribeSiteMonitorISPCityList API operation to
      query the detection

      points that can be used to create site monitoring tasks. For more
      information, see

      DescribeSiteMonitorISPCityList . If this parameter is not specified, the
      system randomly selects three detection

      points for site monitoring.
  Interval:
    Type: Number
    Description: >-
      The interval at which detection requests are sent. Valid values: 1, 5, and
      15. Unit:

      minutes. Default value: 1.
  AlertIds:
    Type: Json
    Description: ''
Resources:
  SiteMonitor:
    Type: 'ALIYUN::CMS::SiteMonitor'
    Properties:
      Address:
        Ref: Address
      OptionsJson:
        Ref: OptionsJson
      TaskName:
        Ref: TaskName
      TaskType:
        Ref: TaskType
      IspCities:
        Ref: IspCities
      Interval:
        Ref: Interval
      AlertIds:
        Ref: AlertIds
Outputs:
  TaskId:
    Description: The ID of the site monitoring task.
    Value:
      'Fn::GetAtt':
        - SiteMonitor
        - TaskId
            
```

