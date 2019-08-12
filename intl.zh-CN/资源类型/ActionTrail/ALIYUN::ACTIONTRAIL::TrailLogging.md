# ALIYUN::ACTIONTRAIL::TrailLogging {#concept_266645 .concept}

ALIYUN::ACTIONTRAIL::TrailLogging 类型用于启用或关闭跟踪的日志记录。

## 语法 {#section_t1y_arv_ljn .section}

```language-json
{
  "Type": "ALIYUN::ACTIONTRAIL::TrailLogging",
  "Properties": {
    "Name": String,
    "Enable": Boolean
  }
}   
```

## 属性 {#section_no2_bw5_2mb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Name|String|是|否|跟踪的名称。|无。|
|Enable|Boolean|是|是|启用或关闭跟踪的日志记录。|无。|

## 返回值 {#section_y5a_2if_n88 .section}

**Fn::GetAtt**

-   IsLogging：服务是否打开。
-   LatestDeliveryError：最后一次行为追踪异常的日志信息。
-   LatestDeliveryTime：最后一次成功记录行为的时间。
-   StartLoggingTime：用户上一次开启该跟踪的时间。
-   StopLoggingTime：用户上一次停止该跟踪的时间。

## 示例 {#section_omv_cs6_mhg .section}

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

