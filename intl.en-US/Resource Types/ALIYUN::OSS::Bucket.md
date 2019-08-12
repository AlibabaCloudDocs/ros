# ALIYUN::OSS::Bucket {#concept_48327_zh .concept}

The ALIYUN::OSS::Bucket type is used to create an OSS bucket.

## Syntax {#section_m5x_pf1_mfb .section}

```language-json
{
   "Type" : "ALIYUN::OSS::Bucket",
   "Properties" : {
      "BucketName" : String,
      "AccessControl" : String,
      "CORSConfiguration" : Map,
      "LifecycleConfiguration " : Map,
      "LoggingConfiguration" : Map,
      "RefererConfiguration" : Map,
      "WebsiteConfiguration" : Map
   }
}

```

## Properties {#section_oct_qf1_mfb .section}

|Name|Type|Required|Description|Constraint|
|BucketName|string|Yes|Bucket name.|The bucket name is a string of 3 to 63 characters and can contain only lowercase letters, digits, and underscores\(\_\). It must start and end with a lowercase letter or digit.|
|AccessControl|string|No|Access permission.|Value options: private, public-read, and public-read-write.|
|CORSConfiguration|map|No|Cross-origin access configuration.|N/A|
|LifecycleConfiguration|map|No|File lifecycle configuration.|N/A|
|LoggingConfiguration|map|No|Log storage configuration.|N/A|
|RefererConfiguration|map|No|Referer configuration.|N/A|
|WebsiteConfiguration|map|No|Static hosting page configuration.|N/A|

## CORSConfiguration syntax { .section}

```language-json
"CORSConfiguration": {
    "CORSRule": [
	    {
		     "AllowedHeader" : String,
			 "AllowedMethod" : List,
			 "AllowedOrigin" : List,
			 "ExposeHeader" : List,
			 "MaxAgeSeconds" : Integer
		}
	]
}

```

## CORSConfiguration properties { .section}

|Name|Type|Required|Description|Constraint|
|CORSRule|list|No|Multiple cross-origin access rules.|N/A|
|AllowedHeader|string|No|Cross-origin access request header.|Value options: \*, Cache-Control, Content-Language, Content-Type, Expires, Last-Modified, and Pragma.|
|AllowedMethod|list|No|Cross-origin access request method.|Value options: \*, GET, PUT, POST, DELETE, HEAD.|
|AllowedOrigin|list|No|Cross-origin access request source.|N/A|
|ExposeHeader|list|No|Response header that users are allowed to access from an application \(for example, a JavaScript XMLHttpRequest object\).|N/A|
|MaxAgeSeconds|integer|No|Cache time for the returned results of browser prefetching \(OPTIONS\) requests for a specific resource.|N/A|

## LifecycleConfiguration syntax { .section}

```language-json
"LifecycleConfiguration": {
     "Rule": [
	     {
             "ID": String,
             "Prefix" : String,
             "Status" : String,
             "Expiration" :{
                 "Days" : Integer,
				 "CreatedBeforeDate" : String
             },
             "AbortMultipartUpload" : {
                 "CreatedBeforeDate": String,
				 "Days" : String
             }
         }
	 ]
}

```

## LifecycleConfiguration properties { .section}

|Name|Type|Required|Description|Constraint|
|Rule|list|No|Lifecycle rule.|N/A|
|ID|string|No|Unique rule ID.|The ID can contain a maximum of 255 bytes. When this parameter is unspecified or null, OSS generates a unique rule ID.|
|Prefix|string|No|Prefix applicable to the lifecycle rule.|The rule takes effect only for the objects that match the prefix. Overlapping prefixes are not allowed.|
|Status|string|No|Whether to enable or disable the lifecycle rule.|Value options: Enable and Disable.|
|Expiration|map|No|Object rule expiration attribute.|N/A|
|Days|string|No|Number of days after which the rule takes effect following the last object modification time.|When the number of days from the last modification time of the object exceeds the specified number of days, the rule is executed to delete the object. For example, if it is set to 30 days, the objects whose last modification date is January 1, 2016 are scanned and deleted by the backend program on January 31, 2016.|
|CreatedBeforeDate|string|No|Date before which the rule takes effect.|The date must follow the ISO8601 format and always be UTC 00:00 AM, for example, 2002-10-11T00:00:00.000Z.|
|AbortMultipartUpload|map|No|Expiration time.|N/A|

## LoggingConfiguration syntax { .section}

```language-json
"LoggingConfiguration": {
     "TargetBucket": String,
     "TargetPrefix": String
}

```

## LoggingConfiguration propertoes { .section}

|Name|Type|Required|Description|Constraint|
|TargetBucket|string|No|Bucket that stores access logs.|N/A|
|TargetPrefix|string|No|Prefix of the name of the finally saved access log file.|N/A|

## WebsiteConfiguration syntax { .section}

```language-json
"WebsiteConfiguration":{
    "IndexDocument": String,
    "ErrorDocument": String
}

```

## WebsiteConfiguration properties { .section}

|Name|Type|Required|Description|Constraint|
|IndexDocument|string|No|Static homepage.|N/A|
|ErrorDocument|string|No|Static error page.|N/A|

## RefererConfiguration syntax { .section}

```language-json
"RefererConfiguration":{
    "AllowEmptyReferer": String,
    "RefererList": List
}

```

## RefererConfiguration properties { .section}

|Name|Type|Required|Description|Constraint|
|AllowEmptyReferer|string|No|Whether to allow access requests with a null referer field.|N/A|
|RefererList|list|No|White list of allowed referers|Whitelist of allowed referers.|

## Response value {#section_o2p_gg1_mfb .section}

**Fn::GetAtt**

-   Name: bucket name, which is globally unique.
-   DomainName: domain name used by bucket access.
-   InternalDomainName: domain name used by bucket access through the internal network.

## Example {#section_rpk_jg1_mfb .section}

```language-json
{
  "ROSTemplateFormatVersion" : "2015-09-01",
  "Resources" : {
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
         "Value" : {"Fn::GetAtt": ["Bucket","Name"]}
    },
    "DomainName": {
         "Value" : {"Fn::GetAtt": ["Bucket","DomainName"]}
    }
  }
}

```

