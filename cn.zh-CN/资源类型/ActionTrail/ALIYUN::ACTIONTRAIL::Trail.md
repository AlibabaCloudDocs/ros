# ALIYUN::ACTIONTRAIL::Trail {#concept_266635 .concept}

ALIYUN::ACTIONTRAIL::Trail 类型用于跟踪，帮助用户将审计数据保存到指定的OSS桶中。

## 语法 {#section_t1y_arv_ljn .section}

``` {#codeblock_mxt_4ex_3w6 .language-json}
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

## 属性 {#section_no2_bw5_2mb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Name|String|是|否|创建的跟踪名称。同一个账户内跟踪名称不可重复。|无。|
|OssBucketName|String|是|是|跟踪写入的 OSS bucket。创建跟踪时必须保证该 bucket 已经存在。|无。|
|RoleName|String|是|是|用户允许 ActionTrail服务扮演的RAM角色名称。|无。|
|OssKeyPrefix|String|否|是|写入的OSS bucket文件名的前缀，可为空。|无。|
|EventRW|String|否|是|投递事件的读写类型。| 可选值：Read、Write、All。

 默认值为Write。|
|SlsProjectArn|String|否|是|日志服务项目的阿里云唯一标识符（ Aliyun Resource Name, ARN）。|无。|
|SlsWriteRoleArn|String|否|是|日志服务角色的阿里云唯一标识符（ Aliyun Resource Name, ARN）。|无。|

## 返回值 {#section_y5a_2if_n88 .section}

**Fn::GetAtt**

Name：创建的跟踪名称。

## 示例 {#section_omv_cs6_mhg .section}

``` {#codeblock_k6k_j5c_vgs .language-json}
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
      "Description": "Indicates whether the event is a read or a write event. Valid values: Read, Write, and All. Default value: Write.",
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

