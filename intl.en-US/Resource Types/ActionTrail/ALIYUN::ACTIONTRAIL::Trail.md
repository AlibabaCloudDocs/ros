# ALIYUN::ACTIONTRAIL::Trail {#concept_266635 .concept}

ALIYUN::ACTIONTRAIL::Trail is used to create a trail to help save audit data to a specified OSS bucket.

## Syntax {#section_t1y_arv_ljn .section}

```language-json
{
  "Type": "ALIYUN::ACTIONTRAIL::Trail",
  "Properties": {
    "Name": String,
    "OssBucketName": String,
    "RoleName": String,
    "OssKeyPrefix": String,
    "EventRW": String,
    "SlsProjectArn": String,
    "SlsWriteRoleArn": String
  }
}            
```

## Properties {#section_no2_bw5_2mb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Name|String|Yes|No|The name of the trail to be created. This name must be unique within the account.|None|
|OssBucketName|String|Yes|Yes|The OSS bucket to which the trail delivers logs. Ensure that this is an existing OSS bucket.|None|
|RoleName|String|Yes|Yes|The name of the RAM role in ActionTrail permitted by the user.|None|
|OssKeyPrefix|String|No|Yes|The prefix of the specified OSS bucket name. This parameter can be left empty.|None|
|EventRW|String|No|Yes|Specifies whether the event is a read or write event.| Valid values: Read, Write, and All

 Default value: Write|
|SlsProjectArn|String|No|Yes|The unique Alibaba Cloud Resource Name \(ARN\) of the Log Service project.|None|
|SlsWriteRoleArn|String|No|Yes|The unique ARN of the Log Service role.|None|

## Response parameters {#section_y5a_2if_n88 .section}

 **Fn::GetAtt** 

Name: the name of the created trail.

## Examples {#section_omv_cs6_mhg .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "Trail": {
      "Type": "ALIYUN::ACTIONTRAIL::Trail",
      "Properties": {
        "SlsWriteRoleArn": {
          "Ref": "SlsWriteRoleArn"
        },
        "OssBucketName": {
          "Ref": "OssBucketName"
        },
        "Name": {
          "Ref": "Name"
        },
        "EventRW": {
          "Ref": "EventRW"
        },
        "RoleName": {
          "Ref": "RoleName"
        },
        "SlsProjectArn": {
          "Ref": "SlsProjectArn"
        },
        "OssKeyPrefix": {
          "Ref": "OssKeyPrefix"
        }
      }
    }
  },
  "Parameters": {
    "SlsWriteRoleArn": {
      "Type": "String",
      "Description": "The unique ARN of the Log Service role."
    },
    "OssBucketName": {
      "Type": "String",
      "Description": "The OSS bucket to which the trail delivers logs. Ensure that this is an existing OSS bucket."
    },
    "Name": {
      "Type": "String",
      "Description": "The name of the trail to be created, which must be unique for an account."
    },
    "EventRW": {
      "Default": "Write",
      "Type": "String",
      "Description": "Indicates whether the event is a read or write event. Valid values: Read, Write, and All. Default value: Write.",
      "AllowedValues": [
        "All",
        "Read",
        "Write"
      ]
    },
    "RoleName": {
      "Type": "String",
      "Description": "The RAM role in ActionTrail permitted by the user."
    },
    "SlsProjectArn": {
      "Type": "String",
      "Description": "The unique ARN of the Log Service project."
    },
    "OssKeyPrefix": {
      "Type": "String",
      "Description": "The prefix of the specified OSS bucket name. This parameter can be left empty."
    }
  },
  "Outputs": {
    "Name": {
      "Description": "The name of the trail to be created, which must be unique for an account.",
      "Value": {
        "Fn::GetAtt": [
          "Trail",
          "Name"
        ]
      }
    }
  }
}
```

