# ALIYUN::ACTIONTRAIL::TrailLogging {#concept_266645 .concept}

ALIYUN::ACTIONTRAIL::TrailLogging is used to enable or disable trail logging.

## Syntax {#section_t1y_arv_ljn .section}

```language-json
{
  "Type": "ALIYUN::ACTIONTRAIL::TrailLogging",
  "Properties": {
    "Name": String,
    "Enable": Boolean
  }
}   
```

## Properties {#section_no2_bw5_2mb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Name|String|Yes|No|The name of the trail to be enabled.|None|
|Enable|Boolean|Yes|Yes|Specifies whether to enable trail logging.|None|

## Response parameters {#section_y5a_2if_n88 .section}

 **Fn::GetAtt** 

-   IsLogging: indicates whether the trail logging service is enabled.
-   LatestDeliveryError: the most recent error that the trail encountered when attempting to deliver log files.
-   LatestDeliveryTime: the date and time of the most recent successful delivery of a log file.
-   StartLoggingTime: the date and time of the most recent trail enabled by the user.
-   StopLoggingTime: the date and time of the most recent trail disabled by the user.

## Examples {#section_omv_cs6_mhg .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "TrailLogging": {
      "Type": "ALIYUN::ACTIONTRAIL::TrailLogging",
      "Properties": {
        "Name": "test-trail",
        "Enable": true
      }
    }
  }
}
```

