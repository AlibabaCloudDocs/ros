# ALIYUN::ROS::WaitCondition {#concept_48502_zh .concept}

ALIYUN::ROS::WaitCondition 类型可用于创建处理 UserData 消息的实例。

## 语法 {#section_mjp_jj1_mfb .section}

``` {#codeblock_963_wer_00n .language-json}
{
  "Type": "ALIYUN::ROS::WaitCondition",
  "Properties": {
    "Count": Number ,
    "Handle": String,
    "Timeout": Number 
  }
}
```

## 属性 {#section_jgi_nh1_agc .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Handle|String|是|是|引用的 ALIYUN::ROS::WaitConditionHandle 实例。|无|
|Timeout|Number|是|否|接收 UserData 消息的超时时间。|取值范围：\[1,43200\], 单位：秒。|
|Count|Number|否|否|准备接收的消息总数。|无|

## 返回值 {#section_p9t_1i4_69r .section}

 **Fn::GetAtt** 

-   Data: JSON序列化字典类型字符串，最近一次创建或更新后的信号数据
-   LastData: JSON序列化字典类型字符串，最近一次更新前的信号数据。
-   JoinedErrorData: 字符串，ErrorData信号内容的拼接。
-   JoinedLastErrorData: 字符串，LastErrorData信号内容的拼接。
-   ErrorData: JSON序列化字典类型字符串，最近一次创建或更新后的错误信号数据。
-   LastErrorData: JSON序列化字典类型字符串，最近一次更新前的错误信号数据。

## 示例 {#section_991_3fy_jqi .section}

``` {#codeblock_sf3_tgf_y7g .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "WaitCondition": {
      "Type": "ALIYUN::ROS::WaitCondition",
      "Properties": {
        "Handle": {
          "Ref": "WaitConHandle"
        },
        "Timeout": 5,
        "Count": 2
      }
    },
    "WaitConHandle": {
      "Type": "ALIYUN::ROS::WaitConditionHandle"
    }
  },
  "Outputs": {
    "CurlCli": {
      "Value": {
        "Fn::GetAtt": [
          "WaitConHandle",
          "CurlCli"
        ]
      }
    },
    "Data": {
      "Value": {
        "Fn::GetAtt": [
          "WaitCondition",
          "Data"
        ]
      }
    }
  }
}          
```

