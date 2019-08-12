# ALIYUN::OSS::Bucket {#concept_48327_zh .concept}

ALIYUN::OSS::Bucket is used to create an OSS bucket.

## Syntax {#section_m5x_pf1_mfb .section}

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

## Properties {#section_oct_qf1_mfb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|BucketName|String|Yes|No|The name of the bucket.|The name must be 3 to 63 characters in length and can contain lowercase letters, digits, and hyphens \(-\). It must start and end with a lowercase letter or digit.|
|AccessControl|String|No|No|The access control list \(ACL\) that grants predefined permissions to the bucket.|Valid values: private, public-read, and public-read-write.|
|CORSConfiguration|Map|No|No|The cross-origin access configuration for objects in the bucket.|None|
|LifecycleConfiguration|Map|No|No|The lifecycle configuration for objects in the bucket.|None|
|LoggingConfiguration|Map|No|No|The settings that define the location where logs are stored.|None|
|RefererConfiguration|Map|No|No|The hotlinking protection configuration.|None|
|WebsiteConfiguration|Map|No|No|The information used to configure the bucket as a static website.|None|

## CORSConfiguration syntax { .section}

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

## CORSConfiguration properties { .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|CORSRule|List|No|No|The rules that define cross-origin resource sharing of objects in the bucket.|None|
|AllowedHeader|String|No|No|The permitted request header for a cross-origin request.|Valid values: \\\*, Cache-Control, Content-Language, Content-Type, Expires, Last-Modified, and Pragma.|
|AllowedMethod|List|No|No|The permitted request method for a cross-origin request.|Valid values: \\\*, GET, PUT, POST, DELETE, and HEAD.|
|AllowedOrigin|List|No|No|The sources that are authorized to send cross-origin requests to the bucket.|None|
|ExposeHeader|List|No|No|The response headers that allow users to send access requests from applications to bucket objects, such as a JavaScript XMLHttpRequest object.|None|
|MaxAgeSeconds|Integer|No|No|The time in seconds during which the results of OPTIONS requests to objects are cached by the browser.|None|

## LifecycleConfiguration syntax { .section}

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

## LifecycleConfiguration properties { .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Rule|List|No|No|The rules that define how the bucket manages objects during their lifetime.|None|
|ID|String|No|No|The unique ID of a rule.|The ID can be a maximum of 255 bytes in length. When this parameter is unspecified or null, OSS generates a unique rule ID.|
|Prefix|String|No|No|The prefix to which the rule applies.|The rule takes effect only on objects that have a matching prefix. Overlapping prefixes are not allowed.|
|Status|String|No|No|Indicates whether to enable or disable a lifecycle rule.|Valid values: Enable and Disable.|
|Expiration|Map|No|No|The time that an object specified by the rule expires.|None|
|Days|String|No|No|The number of days after which the rule takes effect following the last modification time of the object.|When the number of days since an object has been modified reaches the specified number of days, the object is deleted. If this parameter is set to 30, an object that was last modified on January 1, 2016 is automatically deleted on January 31, 2016.|
|CreatedBeforeDate|String|No|No|The date before which the rule takes effect.|The date must conform to the ISO 8601 format and always be UTC 00:00. For example, 2002-10-11T00:00:00.000Z.|
|AbortMultipartUpload|Map|No|No|Indicates whether multipart upload tasks that have not completed are subject to the expiration rules.|None|

## LoggingConfiguration syntax { .section}

```language-json
"LoggingConfiguration": {
  "TargetBucket": String,
  "TargetPrefix": String
}
```

## LoggingConfiguration properties { .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|TargetBucket|String|No|No|The bucket in which access logs are stored.|None|
|TargetPrefix|String|No|No|The prefix of the names of saved access log objects.|None|

## WebsiteConfiguration syntax { .section}

```language-json
"WebsiteConfiguration":{
  "IndexDocument": String,
  "ErrorDocument": String
}
```

## WebsiteConfiguration properties { .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|IndexDocument|String|No|No|The default homepage.|None|
|ErrorDocument|String|No|No|The default error page.|None|

## RefererConfiguration syntax { .section}

```language-json
"RefererConfiguration":{
  "AllowEmptyReferer": String,
  "RefererList": List
}
```

## RefererConfiguration properties { .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|AllowEmptyReferer|String|No|No|Indicates whether the Referer field can be left unspecified in an access request.|None|
|RefererList|List|No|No|The referer whitelist. Access is only allowed to these referers.|None|

## Response parameters {#section_o2p_gg1_mfb .section}

**Fn::GetAtt**

-   Name: the bucket name, which must be globally unique.
-   DomainName: The public DNS name of the specified bucket.
-   InternalDomainName: the internal DNS name of the specified bucket.

## Examples {#section_rpk_jg1_mfb .section}

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

