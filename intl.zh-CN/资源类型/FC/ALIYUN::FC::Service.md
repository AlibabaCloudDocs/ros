# ALIYUN::FC::Service {#concept_186414 .concept}

ALIYUN::FC::Service类型是函数计算资源管理的单位。服务下的所有函数共享一些相同的设置，例如服务授权、配置日志。同一服务下有多个函数，这些函数共享服务配置的资源\( 例如日志库，服务角色等\)。

服务能帮助您更清晰的组织业务逻辑。

服务是运维管理的基本单位。一个服务可以表示一个应用，构建同一应用的不同函数放到同一服务下。服务之间不共享任何资源，没有任何依赖。

## 语法 {#section_6t7_q5i_pg6 .section}

``` {#codeblock_w5q_3aw_23z .language-json}
{
  "Type": "ALIYUN::FC::Service",
  "Properties": {
    "Description": String,
    "VpcConfig": Map,
    "ServiceName": String,
    "Role": String,
    "NasConfig": Map,
    "LogConfig": Map,
    "InternetAccess": Boolean
  }
}
```

## 属性 {#section_rvv_qi1_0pn .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Description|String|否|是|service的简短描述。|无|
|VpcConfig|Map|否|是|vpc配置， 配置后function可以访问指定VPC。|无|
|ServiceName|String|是|是|service名称。|长度为1-128字符。|
|Role|String|否|是|授予函数计算所需权限的RAM role，使用场景包含： 1. 1.  把 function产生的 log 发送到用户的 logstore 中。
2.  为function 在执行中访问其它云资源生成 token。

 |无|
|NasConfig|Map|否|是|NAS配置， 配置后function可以访问指定NAS。|无|
|LogConfig|Map|否|是|log配置，function产生的log会写入这里配置的logstore。|无|
|InternetAccess|Boolean|否|是|设为 true 可让函数访问公网。|无|

## LogConfig语法 {#section_ojs_31w_7l4 .section}

``` {#codeblock_0fb_hij_f7h .language-json}
"LogConfig": {
  "Project": String,
  "Logstore": String
}
```

## LogConfig属性 {#section_axf_5ea_8q5 .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Project|String|否|是|loghub中的project名称。|无|
|Logstore|String|否|是|loghub中的logstore名称。|无|

## VpcConfig语法 {#section_r1y_txd_ksw .section}

``` {#codeblock_ju9_2on_hhn .language-json}
"VpcConfig": {
  "SecurityGroupId": String,
  "VSwitchIds": String,
  "VpcId": String
}
```

## VpcConfig属性 {#section_9l4_hcb_3f6 .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|SecurityGroupId|String|是|是|安全组ID。|无|
|VSwitchIds|String|是|是|一个或多个VSwitch ID。如: \[String, ...\]|数量\>=1。|
|VpcId|String|是|是|VPC ID。|无|

## NasConfig语法 {#section_vkm_bok_02j .section}

``` {#codeblock_g8x_0fk_etk .language-json}
"NasConfig": {
  "MountPoints": List,
  "UserId": Integer,
  "GroupId": Integer
}
```

## NasConfig属性 {#section_zgf_pgd_3o9 .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|MountPoints|List|是|是|挂载点。|无。|
|UserId|Integer|是|是|用户ID。|\[-1, 65534\]。|
|GroupId|Integer|是|是|组ID。|\[-1, 65534\]。|

## MountPoints 语法 {#section_vkm_bok_02j .section}

``` {#codeblock_80z_466_k51 .language-json}
"MountPoints": [
  {
    "ServerAddr": String,
    "MountDir": String
  }
]
```

## MountPoints 属性 {#section_zgf_pgd_3o9 .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|ServerAddr|String|是|是|NAS 服务器地址。|无|
|MountDir|String|是|是|本地挂载目录。|无|

## 返回值 {#section_qyb_v2v_323 .section}

**Fn::GetAtt**

ServiceId：系统为每个service生成的唯一ID。

## 示例 {#section_e7w_wzo_4sd .section}

``` {#codeblock_ixl_ep9_ip4 .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "Service": {
      "Type": "ALIYUN::FC::Service",
      "Properties": {
        "Description": {
          "Ref": "Description"
        },
        "VpcConfig": {
          "Ref": "VpcConfig"
        },
        "ServiceName": {
          "Ref": "ServiceName"
        },
        "Role": {
          "Ref": "Role"
        },
        "NasConfig": {
          "Ref": "NasConfig"
        },
        "LogConfig": {
          "Ref": "LogConfig"
        },
        "InternetAccess": {
          "Ref": "InternetAccess"
        }
      }
    }
  },
  "Parameters": {
    "Description": {
      "Type": "String",
      "Description": "Service description"
    },
    "VpcConfig": {
      "Type": "Json",
      "Description": "VPC configuration. Function Compute uses the config to setup ENI in the specific VPC."
    },
    "ServiceName": {
      "MinLength": 1,
      "Type": "String",
      "Description": "Service name",
      "MaxLength": 128
    },
    "Role": {
      "Type": "String",
      "Description": "The role grants Function Compute the permission to access user\u2019s cloud resources, such as pushing logs to user\u2019s log store. The temporary STS token generated from this role can be retrieved from function context and used to access cloud resources. "
    },
    "NasConfig": {
      "Type": "Json",
      "Description": "NAS configuration. Function Compute uses a specified NAS configured on the service."
    },
    "LogConfig": {
      "Type": "Json",
      "Description": "Log configuration. Function Compute pushes function execution logs to the configured log store."
    },
    "InternetAccess": {
      "Type": "Boolean",
      "Description": "Set it to true to enable Internet access.",
      "AllowedValues": [
        "True",
        "true",
        "False",
        "false"
      ]
    }
  },
  "Outputs": {
    "ServiceId": {
      "Description": "The service ID",
      "Value": {
        "Fn::GetAtt": [
          "Service",
          "ServiceId"
        ]
      }
    }
  }
}
```

