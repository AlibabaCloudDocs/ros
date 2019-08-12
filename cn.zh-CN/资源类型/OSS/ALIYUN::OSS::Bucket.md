# ALIYUN::OSS::Bucket {#concept_48327_zh .concept}

ALIYUN::OSS::Bucket 类型用于创建 OSS 存储空间。

## 语法 {#section_m5x_pf1_mfb .section}

```language-json
{
  "Type": "ALIYUN::OSS::Bucket",
  "Properties": {
    "BucketName": String,
    "AccessControl": String,
    "CORSConfiguration": Map,
    "LifecycleConfiguration": Map,
    "LoggingConfiguration": Map,
    "RefererConfiguration": Map,
    "WebsiteConfiguration": Map
  }
}
```

## 属性 {#section_oct_qf1_mfb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|BucketName|string|是|否|存储空间的名字。|长度限制在 3-63 个字符之间；只能包含小写字母，数字和连字符（-）；必须以小写字母和数字开头和结尾。|
|AccessControl|string|否|否|访问权限。|可选值：private、public-read和 ublic-read-write。|
|CORSConfiguration|map|否|否|跨域访问配置。|无|
|LifecycleConfiguration|map|否|否|文件生命周期配置。|无|
|LoggingConfiguration|map|否|否|日志存储配置。|无|
|RefererConfiguration|map|否|否|防盗链配置。|无|
|WebsiteConfiguration|map|否|否|静态托管页配置。|无|

## CORSConfiguration 语法 { .section}

```language-json
"CORSConfiguration": {
  "CORSRule": [
    {
      "AllowedHeader": String,
      "AllowedMethod": List,
      "AllowedOrigin": List,
      "ExposeHeader": List,
      "MaxAgeSeconds": Integer
    }
  ]
}
```

## CORSConfiguration 属性 { .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|CORSRule|list|否|否|跨域访问规则。|无|
|AllowedHeader|string|否|否|允许的跨域请求 Header。|可选值：\\\*、Cache-Control、Content-Language、Content-Type、Expires、Last-Modified和 Pragma。|
|AllowedMethod|list|否|否|允许的跨域请求的方法。|可选值：\\\*、GET、PUT、POST、DELETE和 HEAD。|
|AllowedOrigin|list|否|否|允许的跨域请求的来源。|无|
|ExposeHeader|list|否|否|允许的用户从应用程序中访问的响应头（例如一个 Javascript 的 XMLHttpRequest 对象\) 。|无|
|MaxAgeSeconds|integer|否|否|浏览器对特定资源的预取（OPTIONS）请求返回结果的缓存时间。|无|

## LifecycleConfiguration 语法 { .section}

```language-json
"LifecycleConfiguration": {
  "Rule": [
    {
      "ID": String,
      "Prefix": String,
      "Status": String,
      "Expiration":{
        "Days": Integer,
        "CreatedBeforeDate": String
      },
      "AbortMultipartUpload": {
        "CreatedBeforeDate": String,
        "Days": String
      }
    }
  ]
}
```

## LifecycleConfiguration 属性 { .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Rule|list|否|否|生命周期规则。|无|
|ID|string|否|否|规则的唯一 ID。|最长为 255 字节。当没有指定，或者该值为空时，OSS 会自动生成一个唯一值。|
|Prefix|string|否|否|规则所适用的前缀。|只有匹配前缀的对象才可能被该规则所影响。不可重叠。|
|Status|string|否|否|启用或停用规则。|可选值： Enable 和 Disable。|
|Expiration|map|否|否|Object 规则的过期属性。|无|
|Days|string|否|否|规则在对象最后修改后多少天后生效。|以文件最后修改时间为起始计算，超过设定天数时即执行规则，将对象删除。如设置时间为 30 天，最后修改日期为 2016-1-1 的对象会在 1 月 31 号被后端程序删除。|
|CreatedBeforeDate|string|否|否|规则在何时之前生效。|日期必需服从 ISO8601 的格式，并且总是 UTC 的零点。 例如：2002-10-11T00:00:00.000Z。|
|AbortMultipartUpload|map|否|否|指定过期时间。|无|

## LoggingConfiguration 语法 { .section}

```language-json
"LoggingConfiguration": {
  "TargetBucket": String,
  "TargetPrefix": String
}
```

## LoggingConfiguration 属性 { .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|TargetBucket|string|否|否|存放访问日志的 Bucket。|无|
|TargetPrefix|string|否|否|最终被保存的访问日志文件前缀。|无|

## WebsiteConfiguration 语法 { .section}

```language-json
"WebsiteConfiguration":{
  "IndexDocument": String,
  "ErrorDocument": String
}
```

## WebsiteConfiguration 属性 { .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|IndexDocument|string|否|否|托管的静态首页。|无|
|ErrorDocument|string|否|否|托管的静态错误页。|无|

## RefererConfiguration 语法 { .section}

```language-json
"RefererConfiguration":{
  "AllowEmptyReferer": String,
  "RefererList": List
}
```

## RefererConfiguration 属性 { .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|AllowEmptyReferer|string|否|否|指定是否允许 referer 字段为空的请求访问。|无|
|RefererList|list|否|否|指定允许 referer 的白名单。|无|

## 返回值 {#section_o2p_gg1_mfb .section}

**Fn::GetAtt**

-   Name：Bucket 名称，全局唯一。
-   DomainName：通过公网访问 Bucket 的域名。
-   InternalDomainName：通过内网访问 Bucket 的域名。

## 示例 {#section_rpk_jg1_mfb .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "Bucket": {
      "Type": "ALIYUN::OSS::Bucket",
      "Properties": {
        "AccessControl": "private",
        "BucketName": "rostest",
        "WebsiteConfiguration":{
            "IndexDocument": "index1.html",
            "ErrorDocument": "error404.html"
        },
        "LoggingConfiguration": {
            "TargetBucket": "cos-mirror",
            "TargetPrefix": "test404"
        },
        "CORSConfiguration": {
            "CORSRule": [{
                "AllowedHeader": ["*"],
                "AllowedMethod": ["GET", "PUT"],
                "AllowedOrigin": ["*"],
                "ExposeHeader": ["Date"],
                "MaxAgeSeconds": 3600
            }]
        },
        "LifecycleConfiguration": {
            "Rule": [{
                "ID": "deleteRule",
                "Prefix": "test/",
                "Status": "Enabled",
                "Expiration":{
                    "Days": 2
                },
                "AbortMultipartUpload":{
                    "CreatedBeforeDate": "2014-10-11T00:00:00.000Z"
                }
            }]
        },
        "RefererConfiguration": {
            "AllowEmptyReferer": true,
            "RefererList": ["http://www.aliyun.com", "https://www.?.aliyuncs.com"]
        }
      }
    }
  },
  "Outputs": {
    "Name": {
         "Value": {"Fn::GetAtt": ["Bucket","Name"]}
    },
    "DomainName": {
         "Value": {"Fn::GetAtt": ["Bucket","DomainName"]}
    }
  }
}
```

