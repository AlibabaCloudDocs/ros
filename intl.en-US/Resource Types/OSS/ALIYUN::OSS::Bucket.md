# ALIYUN::OSS::Bucket

ALIYUN::OSS::Bucket is used to create an Object Storage Service \(OSS\) bucket.

## Syntax

```
{
  "Type": "ALIYUN::OSS::Bucket",
  "Properties": {
    "AccessControl": String,
    "RefererConfiguration": Map,
    "ServerSideEncryptionConfiguration": Map,
    "CORSConfiguration": Map,
    "Tags": Map,
    "LoggingConfiguration": Map,
    "LifecycleConfiguration": Map,
    "StorageClass": String,
    "DeletionForce": Boolean,
    "WebsiteConfiguration": Map,
    "Policy": Map,
    "BucketName": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|BucketName|String|Yes|No|The name of the bucket.|The name must be 3 to 63 characters in length and can contain lowercase letters, digits, and hyphens \(-\). It must start and end with a lowercase letter or digit.|
|AccessControl|String|No|No|The Access Control List \(ACL\) of the bucket.|Default value: private. Valid values:-   private
-   public-read
-   public-read-write |
|CORSConfiguration|Map|No|No|The configurations of cross-origin resource sharing \(CORS\) for objects in the bucket.|For more information, see [CORSConfiguration properties](#section_yjn_9wn_1uf).|
|LifecycleConfiguration|Map|No|No|The lifecycle configurations for objects in the bucket.|For more information, see [LifecycleConfiguration properties](#section_atv_cwg_8up).|
|LoggingConfiguration|Map|No|No|The logging configurations.|For more information, see [LoggingConfiguration properties](#section_0ki_o27_lpm).|
|RefererConfiguration|Map|No|No|The hotlink protection configurations.|For more information, see [RefererConfiguration properties](#section_0bz_1v3_xc3).|
|DeletionForce|Boolean|No|No|Specifies whether to forcibly delete objects from the OSS bucket.|Default value: false. Valid values: -   true
-   false |
|WebsiteConfiguration|Map|No|No|The information that is used to configure the bucket as a static website.|For more information, see [WebsiteConfiguration properties](#section_lp3_0nn_fby).|
|ServerSideEncryptionConfiguration|Map|No|No|The server-side encryption rules.|For more information, see [ServerSideEncryptionConfiguration properties](#section_2ro_n9s_6u8).|
|Tags|Map|No|No|The tags of the bucket. Tags exist as key-value pairs.|A maximum of 20 tags can be specified.A tag key must be 1 to 64 bytes in length and cannot start with `http://`, `https://`, or `Aliyun`.

A tag value must be 0 to 128 bytes in length and must be encoded in UTF-8. |
|StorageClass|String|No|No|The type of the bucket.|Default value: Standard. Valid values:-   Standard
-   IA
-   Archive |
|Policy|Map|No|No|The bucket policy configurations.|None|

## CORSConfiguration syntax

```
"CORSConfiguration": {
  "CORSRule": List
}
```

## CORSConfiguration properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|CORSRule|List|No|No|The rules that define CORS of objects in the bucket.|For more information, see [CORSRule properties](#section_g2p_7xy_s5m).|

## CORSRule syntax

```
"CORSRule": [
  {
    "MaxAgeSeconds": Number,
    "AllowedMethod": List,
    "ExposeHeader": List,
    "AllowedOrigin": List,
    "AllowedHeader": List
  }
]
```

## CORSRule properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|AllowedHeader|List|No|No|The allowed cross-origin request headers.|Valid values:-   \*
-   Cache-Control
-   Content-Language
-   Content-Type
-   Expires
-   Last-Modified
-   Pragma |
|AllowedMethod|List|No|No|The allowed cross-origin request methods.|Valid values:-   \*
-   GET
-   PUT
-   POST
-   DELETE
-   HEAD |
|AllowedOrigin|List|No|No|The origins from which cross-origin requests are allowed.|None|
|ExposeHeader|List|No|No|The response headers for allowed access requests from applications.|Asterisks \(\*\) cannot be used as wildcard characters.|
|MaxAgeSeconds|Number|No|No|The period of time that the browser can cache the response of a preflight \(OPTIONS\) request to a specific resource.|None|

## LifecycleConfiguration syntax

```
"LifecycleConfiguration": {
  "Rule": List
}
```

## LifecycleConfiguration properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Rule|List|Yes|No|The rules that define how the bucket manages objects during their lifetime.|For more information, see [Rule properties](#section_dqr_7ol_mj1).|

## Rule syntax

```
"Rule": [
  {
    "Status": String,
    "AbortMultipartUpload": Map,
    "Expiration": Map,
    "Prefix": String,
    "ID": String
  }
]
```

## Rule properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ID|String|No|No|The unique ID of the rule.|The ID can be up to 255 characters in length. When this parameter is null or not specified, OSS generates a unique ID for the lifecycle rule.|
|Prefix|String|Yes|No|The prefix to which the rule applies.|The rule takes effect only on objects that have a matching prefix.|
|Status|String|Yes|No|Specifies whether to enable the rule.|Valid values: -   Enabled
-   Disabled |
|Expiration|Map|No|No|The expiration attributes of the rule for the specified object.|For more information, see [Expiration properties](#section_r13_ya5_be4).|
|AbortMultipartUpload|Map|No|No|The expiration attributes of the multipart upload tasks that are not complete.|For more information, see [AbortMultipartUpload properties](#section_etz_fbo_qjj).|

## Expiration syntax

```
"Expiration":{
  "Days": Number,
  "CreatedBeforeDate": String,
  "Date": String
}
```

## Expiration properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Days|Number|No|No|The number of days since the object was last modified after which the rule will take effect.|When the number of days since the object was last modified exceeds the specified number of days, the object is deleted. If you set the Days parameter to 30, objects that were last modified on January 1, 2016 are deleted by the backend application on January 31, 2016.|
|CreatedBeforeDate|String|No|No|The time before which the rule takes effect.|Specify the time in the ISO 8601 standard. The time must be in UTC. Example: 2002-10-11T00:00:00.000Z.|
|Date|String|No|No|The time before which the rule takes effect.|This parameter has the same function as CreatedBeforeDate. You can specify only one of the CreatedBeforeDate and Date parameters.|

## AbortMultipartUpload syntax

```
"AbortMultipartUpload": {
  "CreatedBeforeDate": String,
  "Days": Number
}
```

## AbortMultipartUpload properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Days|Number|No|No|The number of days since the object was last modified after which the rule will take effect.|When the number of days since the object was last modified exceeds the specified number of days, the object is deleted. If you set the Days parameter to 30, objects that were last modified on January 1, 2016 are deleted by the backend application on January 31, 2016.|
|CreatedBeforeDate|String|No|No|The time before which the rule takes effect.|Specify the time in the ISO 8601 standard. The time must be in UTC. Example: 2002-10-11T00:00:00.000Z.|

## LoggingConfiguration syntax

```
"LoggingConfiguration": {
  "TargetBucket": String,
  "TargetPrefix": String
}
```

## LoggingConfiguration properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|TargetBucket|String|No|No|The storage space that is used to store access logs.|None|
|TargetPrefix|String|No|No|The prefix of the names of saved access log objects.|None|

## WebsiteConfiguration syntax

```
"WebsiteConfiguration":{
  "IndexDocument": String,
  "ErrorDocument": String
}
```

## WebsiteConfiguration properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|IndexDocument|String|No|No|The default homepage for a static website.|None|
|ErrorDocument|String|No|No|The default error page for a static website.|None|

## RefererConfiguration syntax

```
"RefererConfiguration":{
  "AllowEmptyReferer": String,
  "RefererList": List
}
```

## RefererConfiguration properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|AllowEmptyReferer|Boolean|No|No|Specifies whether the Referer field can be left empty in an access request.|Valid values:-   true
-   false |
|RefererList|List|No|No|The referer whitelist. OSS allows requests whose Referer field values are in the referer whitelist.|None|

## ServerSideEncryptionConfiguration syntax

```
"ServerSideEncryptionConfiguration":{
  "KMSMasterKeyID": String,
  "SSEAlgorithm": String
}
```

## ServerSideEncryptionConfiguration properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|KMSMasterKeyID|String|No|No|The ID of the customer master key.|The key ID is required only when the SSEAlgorithm parameter is set to KMS and a specified key is used for encryption.|
|SSEAlgorithm|String|Yes|No|The default server-side encryption method.|Valid values:-   KMS
-   AES256 |

## Response parameters

Fn::GetAtt

-   Name: the bucket name, which must be globally unique.
-   DomainName: the public domain name of the specified bucket.
-   InternalDomainName: the internal domain name of the specified bucket.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Policy": {
      "Type": "Json",
      "Description": "Bucket policy"
    },
    "CORSConfiguration": {
      "Type": "Json",
      "Description": "Rules that define cross-origin resource sharing of objects in this bucket."
    },
    "DeletionForce": {
      "Type": "Boolean",
      "Description": "Whether force delete the relative objects in the bucket. Default value is false.",
      "AllowedValues": [
        "true",
        "false"
      ],
      "Default": false
    },
    "BucketName": {
      "Type": "String",
      "Description": "bucket name."
    },
    "StorageClass": {
      "Type": "String",
      "Description": "Specifies the storage class of the bucket. Default is \"Standard\".",
      "AllowedValues": [
        "Standard",
        "IA",
        "Archive"
      ]
    },
    "LoggingConfiguration": {
      "Type": "Json",
      "Description": "Settings that defines where logs are stored."
    },
    "WebsiteConfiguration": {
      "Type": "Json",
      "Description": "The properties of website config."
    },
    "RefererConfiguration": {
      "Type": "Json"
    },
    "LifecycleConfiguration": {
      "Type": "Json",
      "Description": "Rules that define how oss bucket manages objects during their lifetime."
    },
    "ServerSideEncryptionConfiguration": {
      "Type": "Json",
      "Description": "Specifies the bucket used to store the server-side encryption rule."
    },
    "AccessControl": {
      "Type": "String",
      "Description": "The access control list.",
      "AllowedValues": [
        "private",
        "public-read",
        "public-read-write"
      ],
      "Default": "private"
    },
    "Tags": {
      "Type": "Json",
      "Description": "Bucket tags in k-v pairs format."
    }
  },
  "Resources": {
    "Bucket": {
      "Type": "ALIYUN::OSS::Bucket",
      "Properties": {
        "Policy": {
          "Ref": "Policy"
        },
        "CORSConfiguration": {
          "Ref": "CORSConfiguration"
        },
        "DeletionForce": {
          "Ref": "DeletionForce"
        },
        "BucketName": {
          "Ref": "BucketName"
        },
        "StorageClass": {
          "Ref": "StorageClass"
        },
        "LoggingConfiguration": {
          "Ref": "LoggingConfiguration"
        },
        "WebsiteConfiguration": {
          "Ref": "WebsiteConfiguration"
        },
        "RefererConfiguration": {
          "Ref": "RefererConfiguration"
        },
        "LifecycleConfiguration": {
          "Ref": "LifecycleConfiguration"
        },
        "ServerSideEncryptionConfiguration": {
          "Ref": "ServerSideEncryptionConfiguration"
        },
        "AccessControl": {
          "Ref": "AccessControl"
        },
        "Tags": {
          "Ref": "Tags"
        }
      }
    }
  },
  "Outputs": {
    "DomainName": {
      "Description": "The public DNS name of the specified bucket.",
      "Value": {
        "Fn::GetAtt": [
          "Bucket",
          "DomainName"
        ]
      }
    },
    "InternalDomainName": {
      "Description": "The internal DNS name of the specified bucket.",
      "Value": {
        "Fn::GetAtt": [
          "Bucket",
          "InternalDomainName"
        ]
      }
    },
    "Name": {
      "Description": "The name of Bucket",
      "Value": {
        "Fn::GetAtt": [
          "Bucket",
          "Name"
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
  Policy:
    Type: Json
    Description: Bucket policy
  CORSConfiguration:
    Type: Json
    Description: Rules that define cross-origin resource sharing of objects in this bucket.
  DeletionForce:
    Type: Boolean
    Description: >-
      Whether force delete the relative objects in the bucket. Default value is
      false.
    AllowedValues:
      - 'true'
      - 'false'
    Default: false
  BucketName:
    Type: String
    Description: bucket name.
  StorageClass:
    Type: String
    Description: Specifies the storage class of the bucket. Default is "Standard".
    AllowedValues:
      - Standard
      - IA
      - Archive
  LoggingConfiguration:
    Type: Json
    Description: Settings that defines where logs are stored.
  WebsiteConfiguration:
    Type: Json
    Description: The properties of website config.
  RefererConfiguration:
    Type: Json
  LifecycleConfiguration:
    Type: Json
    Description: Rules that define how oss bucket manages objects during their lifetime.
  ServerSideEncryptionConfiguration:
    Type: Json
    Description: Specifies the bucket used to store the server-side encryption rule.
  AccessControl:
    Type: String
    Description: The access control list.
    AllowedValues:
      - private
      - public-read
      - public-read-write
    Default: private
  Tags:
    Type: Json
    Description: Bucket tags in k-v pairs format.
Resources:
  Bucket:
    Type: 'ALIYUN::OSS::Bucket'
    Properties:
      Policy:
        Ref: Policy
      CORSConfiguration:
        Ref: CORSConfiguration
      DeletionForce:
        Ref: DeletionForce
      BucketName:
        Ref: BucketName
      StorageClass:
        Ref: StorageClass
      LoggingConfiguration:
        Ref: LoggingConfiguration
      WebsiteConfiguration:
        Ref: WebsiteConfiguration
      RefererConfiguration:
        Ref: RefererConfiguration
      LifecycleConfiguration:
        Ref: LifecycleConfiguration
      ServerSideEncryptionConfiguration:
        Ref: ServerSideEncryptionConfiguration
      AccessControl:
        Ref: AccessControl
      Tags:
        Ref: Tags
Outputs:
  DomainName:
    Description: The public DNS name of the specified bucket.
    Value:
      'Fn::GetAtt':
        - Bucket
        - DomainName
  InternalDomainName:
    Description: The internal DNS name of the specified bucket.
    Value:
      'Fn::GetAtt':
        - Bucket
        - InternalDomainName
  Name:
    Description: The name of Bucket
    Value:
      'Fn::GetAtt':
        - Bucket
        - Name
```

