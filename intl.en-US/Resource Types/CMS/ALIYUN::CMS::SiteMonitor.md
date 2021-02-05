# ALIYUN::CMS::SiteMonitor

ALIYUN::CMS::SiteMonitor is used to create a site monitoring job.

## Syntax

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

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Address|String|Yes|Yes|The URL or IP address of the site to be monitored.|None|
|OptionsJson|String|No|Yes|The extended options of the protocol that is used by the monitoring job. The options vary based on the protocol.|None|
|TaskName|String|Yes|Yes|The name of the monitoring job.|The name must be 4 to 100 characters in length, and can contain letters, digits, and underscores \(\_\).|
|TaskType|String|Yes|No|The type of the monitoring job.|Valid values:-   HTTP\(S\)
-   PING
-   TCP
-   UDP
-   DNS
-   SMTP
-   POP3
-   FTP |
|IspCities|List|No|Yes|The information about the detection points.|If you leave this parameter empty, the system randomly selects three detection points.For more information, see [Isthroughput properties](#section_run_2se_hms). |
|Interval|Integer|No|Yes|The interval at which detection requests are sent.|Default value: 1. Valid values:-   1
-   5
-   15

Unit: minutes.|
|AlertIds|List|No|No|The IDs of one or more alert rules.|You can call the [DescribeMetricRuleList](/intl.en-US/API Reference/Alert rules for time series metrics/DescribeMetricRuleList.md) operation to query the IDs of existing alert rules in Cloud Monitor.|

## IspCities syntax

```
"IspCities": [
  {
    "Isp": String,
    "City": String
  }
]
```

## Isthroughput properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Isp|String|Yes|No|The name or ID of the carrier to which the detection point belongs. Fuzzy query is supported for carrier names.|For more information, see [DescribeSiteMonitorISPCityList](/intl.en-US/API Reference/Site monitoring/DescribeSiteMonitorISPCityList.md).|
|City|String|Yes|No|The name or ID of the city where the detection point resides. Fuzzy query is supported for city names.|None|

## Response parameters

Fn::GetAtt

TaskId: the ID of the monitoring job.

## Examples

`JSON` format

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

`YAML` format

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

