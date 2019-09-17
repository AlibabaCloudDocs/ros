# 输出（Outputs） {#concept_28864_zh .concept}

在输出（Outputs）中，定义在调用查询资源栈接口时返回的值。例如，定义 ECS 实例 ID 的输出，然后可在调用查询资源栈的接口时，查看该实例 ID。

## 语法 {#section_ezz_zrv_kfb .section}

Outputs 由输出 ID 和输出描述组成。所有输出描述都被括在大括号里。如果声明多个输出项，则用逗号分隔开。请参见以下 Outputs 的语法结构示例代码段：

``` {#codeblock_cjz_sbn_htj .language-json}
"Outputs" : {
  "输出１ ID" : {
    "Description" : "输出的描述",
    "Condition": "是否输出此资源属性的条件",
    "Value" : "输出值的表达式"
  },
  "输出 2 ID" : {
    "Description" : "输出的描述",
    "Condition": "是否输出此资源属性的条件",
    "Value" : "输出值的表达式"
  }
}
			
```

**输出 ID**

输出项的标识符，在模板中具有唯一性。

**Description（可选）**

用于描述输出值的 String 类型。

**Value（必需）**

在调用查询资源栈接口时，返回的属性值。

**Condition（可选）**

使用 Condition 属性可以指定是否需要创建某个资源和输出资源的信息。当 Condition 所指定的条件值为 true 时，才创建此资源和输出资源信息。

如以下代码段所示，根据 MaxAmount 的值判断是否创建 WebServer：

``` {#codeblock_260_9k3_ouv .language-json}
{
  "ROSTemplateFormatVersion" : "2015-09-01",
  "Parameters": {
    "MaxAmount": {
      "Type": "Number",
      "Default": 1
    }
  },
  "Conditions": {
    "CreateWebServer": {"Fn::Not": {"Fn::Equals": [0, {"Ref": "MaxAmount"}]}}
  }
  "Resources" : {
    "WebServer": {
      "Type": "ALIYUN::ECS::InstanceGroup",
      "Condition": "CreateWebServer",
      "Properties": {
        "ImageId" : "m-25l0rcfjo",
        "InstanceType": "ecs.t1.small"
        "MaxAmount": {"Ref": "MaxAmount"}
      }
    }
  }
  "Outputs": {
    "WebServerIP": {
      "Condition": "CreateWebServer",
      "Value": {
        "Fn::GetAtt": ["WebServer", "PublicIps"]
      }
    }
  }
}
			
```

## 示例 {#section_ybw_vsv_kfb .section}

在以下示例中，输出部分有 ２ 个输出项。第一个输出资源 ID 为 WebServer 的 InstanceId 属性，第二个输出资源 ID 为 WebServer 的 PublicIp 属性。

``` {#codeblock_l84_2lb_auy .language-json}
"Outputs": {
  "InstanceId": {
       "Value" : {"Fn::GetAtt": ["WebServer","InstanceId"]}
  },
  "PublicIp": {
       "Value" : {"Fn::GetAtt": ["WebServer","PublicIp"]}
  }
}
			
```

