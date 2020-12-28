# ALIYUN::OSS::Bucket

ALIYUN::OSS::Bucket类型用于创建OSS存储空间。

## 语法

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

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|BucketName|String|是|否|存储空间名称。|长度为3~63个字符。必须以小写英文字母或数字开头和结尾，可包含小写英文字母、数字和短划线（-）。|
|AccessControl|String|否|否|访问权限。|取值：-   private（默认值）：私有。
-   public-read：公共读。
-   public-read-write：公共读写。 |
|CORSConfiguration|Map|否|否|跨域访问配置。|更多信息，请参见[CORSConfiguration属性](#section_yjn_9wn_1uf)。|
|LifecycleConfiguration|Map|否|是|文件生命周期配置。|更多信息，请参见[LifecycleConfiguration属性](#section_atv_cwg_8up)。|
|LoggingConfiguration|Map|否|否|日志存储配置。|更多信息，请参见[LoggingConfiguration属性](#section_0ki_o27_lpm)。|
|RefererConfiguration|Map|否|否|防盗链配置。|更多信息，请参见[RefererConfiguration属性](#section_0bz_1v3_xc3)。|
|DeletionForce|Boolean|否|否|是否强制删除OSS中的文件。|取值范围： -   true
-   false（默认值） |
|WebsiteConfiguration|Map|否|否|静态托管页配置。|更多信息，请参见[WebsiteConfiguration属性](#section_lp3_0nn_fby)。|
|ServerSideEncryptionConfiguration|Map|否|否|服务端加密规则配置。|更多信息，请参见[ServerSideEncryptionConfiguration属性](#section_2ro_n9s_6u8)。|
|Tags|Map|否|否|存储空间标签。Key-Value形式的键值对。|最多设置20个标签。Key长度为1~64个字节，不能以`http://`、`https://`或`Aliyun`开头。

Value长度为0~128个字节，必须为UTF-8编码。 |
|StorageClass|String|否|否|存储空间类型。|取值：-   Standard（默认值）：标准存储。
-   IA：低频访问。
-   Archive：归档存储。 |
|Policy|Map|否|否|存储空间策略。|无|

## CORSConfiguration语法

```
"CORSConfiguration": {
  "CORSRule": List
}
```

## CORSConfiguration属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|CORSRule|List|否|否|跨域访问规则。|更多信息，请参见[CORSRule属性](#section_g2p_7xy_s5m)。|

## CORSRule语法

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

## CORSRule属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|AllowedHeader|List|否|否|允许的跨域请求Header。|取值：-   \*
-   Cache-Control
-   Content-Language
-   Content-Type
-   Expires
-   Last-Modified
-   Pragma |
|AllowedMethod|List|否|否|允许的跨域请求的方法。|取值：-   \*
-   GET
-   PUT
-   POST
-   DELETE
-   HEAD |
|AllowedOrigin|List|否|否|允许的跨域请求的来源。|无|
|ExposeHeader|List|否|否|允许用户从应用程序中访问的响应头 。|不允许使用星号（\*）。|
|MaxAgeSeconds|Number|否|否|浏览器对特定资源的OPTIONS请求返回结果的缓存时间。|无|

## LifecycleConfiguration语法

```
"LifecycleConfiguration": {
  "Rule": List
}
```

## LifecycleConfiguration属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Rule|List|是|否|生命周期规则。|更多信息，请参见[Rule属性](#section_dqr_7ol_mj1)。|

## Rule语法

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

## Rule属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ID|String|否|否|规则的唯一ID。|最长为255字节。当没有指定ID或者ID为空时，OSS会自动生成一个唯一值。|
|Prefix|String|是|否|规则所适用的前缀。|只有匹配前缀的对象才可能被该规则所影响。|
|Status|String|否|是|启用或停用规则。|取值： -   Enabled：启用规则。
-   Disabled：停用规则。 |
|Expiration|Map|否|否|对象规则的过期属性。|更多信息，请参见[Expiration属性](#section_r13_ya5_be4)。|
|AbortMultipartUpload|Map|否|否|未完成分片上传的过期属性。|更多信息，请参见[AbortMultipartUpload属性](#section_etz_fbo_qjj)。|

## Expiration语法

```
"Expiration":{
  "Days": Number,
  "CreatedBeforeDate": String,
  "Date": String
}
```

## Expiration属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Days|Number|否|否|对象最后修改后，规则会在多少天后生效。|以文件最后修改时间为起点开始计算，超过设定天数时即执行规则，则将对象删除。如果设置时间为30天，则最后修改日期为2016年1月1号的对象会在2016年1月31号被后端程序删除。|
|CreatedBeforeDate|String|否|否|规则在何时之前生效。|日期为ISO8601的格式，并且值为UTC的零点。例如：2002-10-11T00:00:00.000Z。|
|Date|String|否|否|规则在何时之前生效。|与CreatedBeforeDate作用相同，二者只能设置一个。|

## AbortMultipartUpload语法

```
"AbortMultipartUpload": {
  "CreatedBeforeDate": String,
  "Days": Number
}
```

## AbortMultipartUpload属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Days|Number|否|否|对象最后修改后，规则会在多少天后生效。|以文件最后修改时间为起点开始计算，超过设定天数时即执行规则，则将对象删除。如果设置时间为30天，则最后修改日期为2016年1月1号的对象会在2016年1月31号被后端程序删除。|
|CreatedBeforeDate|String|否|否|规则在何时之前生效。|日期为ISO8601的格式，并且值为UTC的零点。例如：2002-10-11T00:00:00.000Z。|

## LoggingConfiguration语法

```
"LoggingConfiguration": {
  "TargetBucket": String,
  "TargetPrefix": String
}
```

## LoggingConfiguration属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|TargetBucket|String|否|否|存放访问日志的存储空间。|无|
|TargetPrefix|String|否|否|最终被保存的访问日志文件前缀。|无|

## WebsiteConfiguration语法

```
"WebsiteConfiguration":{
  "IndexDocument": String,
  "ErrorDocument": String
}
```

## WebsiteConfiguration属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|IndexDocument|String|否|否|托管的静态首页。|无|
|ErrorDocument|String|否|否|托管的静态错误页。|无|

## RefererConfiguration语法

```
"RefererConfiguration":{
  "AllowEmptyReferer": String,
  "RefererList": List
}
```

## RefererConfiguration属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|AllowEmptyReferer|Boolean|否|否|是否允许referer字段为空的请求访问。|取值：-   true
-   false |
|RefererList|List|否|否|允许referer字段的白名单。|无|

## ServerSideEncryptionConfiguration语法

```
"ServerSideEncryptionConfiguration":{
  "KMSMasterKeyID": String,
  "SSEAlgorithm": String
}
```

## ServerSideEncryptionConfiguration属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|KMSMasterKeyID|String|否|否|密钥ID。|只有当SSEAlgorithm值为KMS，且使用指定的密钥加密时，才需输入密钥ID。|
|SSEAlgorithm|String|是|否|服务端默认加密方式。|取值：-   KMS
-   AES256 |

## 返回值

Fn::GetAtt

-   Name：存储空间名称，全局唯一。
-   DomainName：通过公网访问存储空间的域名。
-   InternalDomainName：通过内网访问存储空间的域名。

## 示例

`JSON`格式

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

`YAML`格式

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

