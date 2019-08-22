# 函数（Functions） {#concept_28865_zh .concept}

资源编排服务提供多个内置函数，帮助您管理您的资源栈。您可以在定义资源（Resources\) 和输出 \(Outputs\) 时，使用内部函数。

可在资源栈模板中使用的内部函数包括：Fn::Str、Fn::Base64、Fn::FindInMap、Fn::GetAtt、Fn::Join、Fn::Select、Ref、Fn::GetAZs、Fn::Replace、Fn::Split、Fn::Equals、Fn::And、Fn::Or、Fn::Not、Fn::If、Fn::ListMerge、Fn::GetJsonValue、Fn::MergeMapToList和Fn::Avg。

## Fn::Str {#section_hqj_vtv_kfb .section}

内部函数Fn::Str返回输入数字的字符串结果。

声明

``` {#codeblock_sbq_s6y_j45 .language-json}
"Fn::Str" : ToString
```

参数

`ToString`：需要转换的Number/Integer类型的值。

返回值

该值的字符串类型。

示例

``` {#codeblock_3nv_kl0_6az .language-json}
"Fn::Str": 123456
```

返回：`"123456"`。

## Fn::Base64 {#section_hqj_vtv_kfb .section}

内部函数Fn::Base64返回输入字符串的Base64编码结果。

声明

``` {#codeblock_7oc_a0e_4il .language-json}
"Fn::Base64" : stringToEncode
```

参数

`stringToEncode`：转换成Base64的字符串。

返回值

用Base64表示的原始字符串。

示例

``` {#codeblock_1ad_wee_ip7 .language-json}
"Fn::Base64" : "string to encode"
```

## Fn::FindInMap {#section_dlh_15v_kfb .section}

内部函数Fn::FindInMap返回与Mappings声明的双层映射中的键对应的值。

声明

``` {#codeblock_172_6d5_uf8 .language-json}
"Fn::FindInMap" : [ "MapName", "TopLevelKey", "SecondLevelKey"]
```

参数

-   `MapName`：Mappings中所声明映射的ID，包含键和值。
-   `TopLevelKey`：第一级键，其值是一个键/值对列表。
-   `SecondLevelKey`：第二级键，其值是一个字符串或者数字。

返回值

分配给SecondLevelKey的值。

示例

在创建名为WebServer的资源时，需要指定ImageId属性。在Mappings中，描述根据区域区分的ImageId映射。在Parameters中，描述需要用户指定的区域。Fn::FindInMap会根据用户指定的区域，在RegionMap中查找对应的ImageId映射，然后在映射中找到对应的ImageId。

-   MapName可按照个人意愿设置。在本示例中为 `"RegionMap"`。
-   TopLevelKey设置为创建资源栈的地区。在本示例中，通过 `{ "Ref" : "regionParam" }`确定。
-   SecondLevelKey设置为所需的架构。在本示例中为`"32"`。

``` {#codeblock_e9m_0z8_ums .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "regionParam": {
        "Description": "选择创建 ECS 的区域",
        "Type": "String",
        "AllowedValues": ["hangzhou", "beijing"]
    }
  },
  "Mappings" : {
    "RegionMap" : {
      "hangzhou" : { "32" : "m-25l0rcfjo", "64" : "m-25l0rcfj1" },
      "beijing" : { "32" : "m-25l0rcfj2", "64" : "m-25l0rcfj3" }
    }
  },
  "Resources": {
    "WebServer": {
      "Type": "ALIYUN::ECS::Instance",
      "Properties": {
        "ImageId" : { "Fn::FindInMap" : [ "RegionMap", { "Ref" : "regionParam" }, "32"]},
        "InstanceType": "ecs.t1.small",
        "SecurityGroupId": "sg-25zwc3se0",
        "ZoneId": "cn-beijing-b",
        "Tags": [{
            "Key": "key1",
            "Value": "value1"
        },{
            "Key": "key2",
            "Value": "value2"
        }
        ]
      }
    }
  }
}
```

支持的函数

-   Fn::FindInMap
-   Ref

## Fn::GetAtt {#section_z2k_15v_kfb .section}

内部函数Fn::GetAtt返回模板中的资源的属性值。

声明

``` {#codeblock_ncz_5kr_g8w .language-json}
"Fn::GetAtt": [ "resourceID", "attributeName" ]
```

参数

-   `resourceID`：目标资源的ID。
-   `attributeName`：目标资源的属性名称。

返回值

属性值。

示例

返回Resource ID为MyEcsInstance的ImageId属性：

``` {#codeblock_h73_d5x_tat .language-json}
"Fn::GetAtt" : [ "MyEcsInstance" , "ImageID" ]
```

## Fn::Join {#section_owl_15v_kfb .section}

内部函数Fn::Join将一组值连接起来，用特定分隔符隔开。

声明

``` {#codeblock_7hp_rt4_enp .language-json}
{ "Fn::Join" : [ "delimiter", [ "string1", "string2", ... ]] }
```

参数

-   `delimiter`：分隔符。分隔符可以为空，表示将所有的值直接连接起来。
-   `[ "string1", "string2", ... ]`：被连接起来的值列表示例。

返回值

被连接起来的字符串。

示例

``` {#codeblock_ot8_88d_chi .language-json}
"Fn::Join" : [ ",", [ "a", "b", "c" ] ]
```

返回：`"a,b,c"`。

支持的函数

-   Fn::Base64
-   Fn::GetAtt
-   Fn::Join
-   Fn::Select
-   Ref

## Fn::Select {#section_t3n_15v_kfb .section}

内部函数Fn::Select通过索引返回数据元列表中的单个数据元。

声明

-   数据元列表是一个数组：

    ``` {#codeblock_qff_56v_kxi .language-json}
    "Fn::Select" : [ "index", [ "value1", "value2", ... ] ]        
    ```

-   数据元列表是一个映射表：

    ``` {#codeblock_cvq_g98_a70 .language-json}
    "Fn::Select" : [ "index", { "key1": "value1", ... } ]
    ```


参数

`index`：待检索数据元的索引。如果数据元列表是一个数组，则索引是 0 到 N-1 之间的某个值（其中 N 代表阵列中元素的数量）。如果数据元列表是一个映射表，则索引是映射表中的某个键。

如果找不到索引对应的值，则返回空字符串。

返回值

选定的数据元。

示例

-   如果数据元列表是一个数组：

    ``` {#codeblock_69e_r2b_tps .language-json}
    { "Fn::Select" : [ "1", [ "apples", "grapes", "oranges", "mangoes" ] ] }        
    ```

    返回：`"grapes"`。

-   如果数据元列表是一个映射表：

    ``` {#codeblock_96m_cek_gxb .language-json}
    { "Fn::Select" : [ "key1", { "key1": "grapes", "key2": "mangoes" } ] }     
    ```

    返回：`"grapes"`。

-   如果数据元列表是一个CommaDelimitedList：

    ``` {#codeblock_rck_njo_uc7 .language-json}
    "Parameters" : {
      "userParam": {
        "Type": "CommaDelimitedList",
          "Default": "10.0.100.0/24, 10.0.101.0/24, 10.0.102.0/24"
      }
    }
    
    "Resources": {
      "resourceID": {
          "Properties": {
              "CidrBlock": { "Fn::Select" : [ "0", {"Ref": "userParam"} ] }
        }
      }
    }
    ```


支持的函数

对于Fn::Select索引值，您可以使用Ref函数。

对于对象的 Fn::Select 列表，您可以使用以下函数：

-   Fn::Base64
-   Fn::FindInMap
-   Fn::GetAtt
-   Fn::Join
-   Fn::Select
-   Ref

## Ref {#section_yxv_5vv_kfb .section}

内部函数Ref返回指定参数或资源的值。

如果指定参数是Resource ID，则返回资源的值。否则系统将认为指定参数是参数，将尝试返回参数的值。

声明

``` {#codeblock_nt2_tug_p8g .language-json}
"Ref" : "logicalName"
```

参数

`logicalName`：要引用的资源或参数的逻辑名称。

返回值

资源的值或者参数的值。

示例

使用Ref函数指定regionParam作为WebServer的RegionMap的区域参数：

``` {#codeblock_q8w_lz6_7pl .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "regionParam": {
        "Description": "选择创建 ECS 的区域",
        "Type": "String",
        "AllowedValues": ["hangzhou", "beijing"]
    }
  },
  "Mappings" : {
    "RegionMap" : {
      "hangzhou" : { "32" : "m-25l0rcfjo", "64" : "m-25l0rcfj1" },
      "beijing" : { "32" : "m-25l0rcfj2", "64" : "m-25l0rcfj3" }
    }
  },
  "Resources": {
    "WebServer": {
      "Type": "ALIYUN::ECS::Instance",
      "Properties": {
        "ImageId" : { "Fn::FindInMap" : [ "RegionMap", { "Ref" : "regionParam" }, "32"]},
        "InstanceType": "ecs.t1.small",
        "SecurityGroupId": "sg-25zwc3se0",
        "ZoneId": "cn-beijing-b",
        "Tags": [{
            "Key": "tiantt",
            "Value": "ros"
        },{
            "Key": "tiantt1",
            "Value": "ros1"
        }
        ]
      }
    }
  }
}
```

支持的函数

不能在Ref函数中使用任何函数。必须指定为资源逻辑ID的字符串。

## Fn::GetAZs {#section_pwy_5vv_kfb .section}

内部函数Fn::GetAZs返回指定Region的可用区列表。

声明

``` {#codeblock_hx7_qzd_0e5 .language-json}
"Fn::GetAZs": "region"    
```

参数

`region`：region ID。

返回值

指定Region下的可用区列表。

示例

在指定Region的第一个可用区内创建一个ECS实例：

``` {#codeblock_w7h_8ia_0sv .language-json}
{
  "ROSTemplateFormatVersion" : "2015-09-01",
  "Resources" : {
    "WebServer": {
      "Type": "ALIYUN::ECS::Instance",
      "Properties": {
        "ImageId" : "centos7u2_64_40G_cloudinit_20160728.raw",
        "InstanceType": "ecs.n1.tiny",
        "SecurityGroupId": "sg-2zedcm7ep5quses05fs4",
        "Password": "Ros12345",
        "AllocatePublicIP": true,
        "InternetChargeType": "PayByTraffic",
        "InternetMaxBandwidthIn": 100,
        "InternetMaxBandwidthOut": 100,
        "SystemDiskCategory": "cloud_efficiency",
        "IoOptimized": "optimized",
        "ZoneId": {"Fn::Select": ["0", {"Fn::GetAZs": {"Ref": "ALIYUN::Region"}}]}
      }
    }
  },
  "Outputs": {
    "InstanceId": {
         "Value" : {"Fn::GetAtt": ["WebServer","InstanceId"]}
    },
    "PublicIp": {
         "Value" : {"Fn::GetAtt": ["WebServer","PublicIp"]}
    }
  }
}
```

支持的函数

-   Fn::Base64
-   Fn::FindInMap
-   Fn::GetAtt
-   Fn::Join
-   Fn::Select
-   Ref

## Fn::Replace {#section_ppz_kwv_kfb .section}

内部函数Fn::Replace将字符串中指定子字符串用新字符串替换。

声明

``` {#codeblock_ox9_v42_v8z .language-json}
{ "Fn::Replace" : [ {"object_key": "object_value"}, "object_string"]     
```

参数

-   `object_key`：将要被替换的字符串。
-   `object_value`：将要替换成的最终字符串。
-   `object_string`：包含被替换`object_key`的字符串。

返回值

被替换后的字符串。

示例

所指定脚本中的print替换成echo：

``` {#codeblock_iqe_655_a7f .language-json}
{
  "ROSTemplateFormatVersion" : "2015-09-01",
  "Resources" : {
    "WebServer": {
      "Type": "ALIYUN::ECS::Instance",
      "Properties": {
        "ImageId" : "centos_7_2_64_40G_base_20170222.vhd",
        "InstanceType": "ecs.n1.medium",
        "SecurityGroupId": "sg-94q49gota",
        "Password": "MytestPassword1234",
        "IoOptimized": "optimized",
        "VSwitchId": "vsw-94vdvonyi",
        "VpcId": "vpc-949uzr8c9",
        "SystemDiskCategory": "cloud_ssd",
        "UserData": {"Fn::Replace": [{"print": "echo"},
         {"Fn::Join": ["", [
             "#!/bin/sh\n",
             "mkdir ~/test_ros\n",
             "print hello > ~/1.txt\n"
         ]]}]}
      }
    }
  },
  "Outputs": {
    "InstanceId": {
         "Value" : {"Fn::GetAtt": ["WebServer","InstanceId"]}
    },
    "PublicIp": {
         "Value" : {"Fn::GetAtt": ["WebServer","PublicIp"]}
    }
  }
} 
```

支持的函数

-   Fn::Base64
-   Fn::GetAtt
-   Fn::Join
-   Fn::Select
-   Ref

## Fn::Split {#section_nwc_lwv_kfb .section}

内部函数Fn::Split通过指定分隔符对字符串进行切片，并返回所有切片组成的列表。

声明

``` {#codeblock_rlh_ekj_h2a .language-json}
"Fn::Split" : [ "delim",  "original_string" ]         
```

参数

-   `delim`：分隔符，例如: ','，';'，'\\n'，'\\t' 等。
-   `original_string`：将要被切片的字符串。

返回值

返回切片后所有字符串组成的列表。

示例

-   如果数据元列表是一个数组：

``` {#codeblock_3vg_sdf_m5x .language-json}
{"Fn::Split": [";", "foo; bar; achoo"]}
```

    返回：`["foo", " bar", "achoo "]`。

-   使用Fn::Split对InstanceIds进行切片：

``` {#codeblock_3ad_p4p_05b .language-json}
"Parameters" : {
  "InstanceIds": {
    "Type": "String",
    "Default": "instane1_id,instance2_id,instance2_id"
  }
},
"Resources": {
  "resourceID": {
      "Type": "ALIYUN::SLB::BackendServerAttachment":
      "Properties": {
          "BackendServerList": { "Fn::Split" : [ ",", {"Ref": "InstanceIds"} ] }
    }
  }
}            
```


支持的函数

-   Fn::Base64
-   Fn::FindInMap
-   Fn::GetAtt
-   Fn::Join
-   Fn::Select
-   Fn::Replace
-   Fn::GetAZs
-   Fn::If
-   Ref

## Fn::Equals {#section_r32_lwv_kfb .section}

比较两个值是否相等。如果两个值相等，则返回true；如果不相等，则返回false。

声明

``` {#codeblock_29e_69w_34e .language-json}
{"Fn::Equals": ["value_1", "value_2"]}      
```

参数

`value`：要比较的任意类型的值。

返回值

true或false。

示例

在Conditions中使用Fn::Equals定义条件：

``` {#codeblock_x2j_nwl_j75 .language-json}
{
  "ROSTemplateFormatVersion" : "2015-09-01",
  "Parameters":{
    "EnvType":{
      "Default":"pre",
      "Type":"String"
    }
  },
  "Conditions": {
    "TestEqualsCond": {"Fn::Equals": ["prod", {"Ref": "EnvType"}]}
  }
}
```

支持的函数

-   Fn::Or
-   Fn::Not
-   Fn::Equals
-   Fn::FindInMap
-   Fn::And
-   Ref

## Fn::And {#section_cqg_lwv_kfb .section}

代表AND运算符，最少包含两个条件。如果所有指定条件计算为true，则返回true；如果任意条件计算为false，则返回false。

声明

``` {#codeblock_3i4_pav_mc9 .language-json}
{"Fn::And": ["condition", {...}]} 
```

参数

`condition`：计算为true或false的条件。

返回值

true或false。

示例

在Conditions中使用Fn::And定义一个条件：

``` {#codeblock_k08_uu8_xb0 .language-json}
{
  "ROSTemplateFormatVersion" : "2015-09-01",
  "Parameters":{
    "EnvType":{
      "Default":"pre",
      "Type":"String"
    }
  },
  "Conditions": {
    "TestEqualsCond": {"Fn::Equals": ["prod", {"Ref": "EnvType"}]},
    "TestAndCond": {"Fn::And": ["TestEqualsCond", {"Fn::Equals": ["pre", {"Ref": "EnvType"}]}]}
  }
}
```

支持的函数

-   Fn::Or
-   Fn::Not
-   Fn::Equals
-   Fn::FindInMap
-   Fn::And
-   Ref

## Fn::Or {#section_o2l_3xv_kfb .section}

代表OR运算符，最少包含两个条件。如果任意一个指定条件计算为true，则返回true；如果所有条件都计算为false，则返回false。

声明

``` {#codeblock_nax_dxn_a63 .language-json}
{"Fn::Or": ["condition", {...}]}
```

参数

`condition`：计算为true或false的条件。

返回值

true或false。

示例

在Conditions中使用Fn::Or定义一个条件：

``` {#codeblock_n6w_ibs_dvt .language-json}
{
  "ROSTemplateFormatVersion" : "2015-09-01",
  "Parameters":{
    "EnvType":{
      "Default":"pre",
      "Type":"String"
    }
  },
  "Conditions": {
    "TestEqualsCond": {"Fn::Equals": ["prod", {"Ref": "EnvType"}]},
    "TestOrCond": {"Fn::And": ["TestEqualsCond", {"Fn::Equals": ["pre", {"Ref": "EnvType"}]}]}
  }
}  
```

支持的函数

-   Fn::Or
-   Fn::Not
-   Fn::Equals
-   Fn::FindInMap
-   Fn::And
-   Ref

## Fn::Not {#section_otm_3xv_kfb .section}

代表NOT运算符。对计算为false的条件，返回true；对计算为true的条件，返回false。

声明

``` {#codeblock_src_okn_pl6 .language-json}
{"Fn::Not": "condition"}
```

参数

`condition`：计算为true或false的条件。

返回值

true或false。

示例

在Conditions中使用Fn::Not定义一个条件：

``` {#codeblock_eo0_4n0_bwg .language-json}
{
  "ROSTemplateFormatVersion" : "2015-09-01",
  "Parameters":{
    "EnvType":{
      "Default":"pre",
      "Type":"String"
    }
  },
  "Conditions": {
    "TestNotCond": {"Fn::Not": {"Fn::Equals": ["pre", {"Ref": "EnvType"}]}}
  }
}
```

支持的函数

-   Fn::Or
-   Fn::Not
-   Fn::Equals
-   Fn::FindInMap
-   Fn::And
-   Ref

## Fn::If {#section_zy4_3xv_kfb .section}

如果指定的条件计算为true，则返回一个值；如果指定的条件计算为false，则返回另一个值。在模板Resources和Outputs属性值中支持Fn::If内部函数。您可以使用`ALIYUN::NoValue`伪参数作为返回值来删除相应的属性。

声明

``` {#codeblock_ket_xvk_v3c .language-json}
{"Fn::If": ["condition_name", "value_if_true", "value_if_false"]}            
```

参数

-   `condition_name`：Conditions中条件对应的条件名称。通过条件名称引用条件。
-   `value_if_true`：当指定的条件计算为true时，返回此值。
-   `value_if_false`：当指定的条件计算为false时，返回此值。

示例

根据输入的参数，确定是否创建数据盘：

``` {#codeblock_00d_cd2_gtj .language-json}
{
    "ROSTemplateFormatVersion":"2015-09-01",
    "Parameters":{
        "EnvType":{
            "Default":"pre",
            "Type":"String"
        }
    },
    "Conditions":{
        "CreateDisk":{
            "Fn::Equals":[
                "prod",
                {
                    "Ref":"EnvType"
                }
            ]
        }
    },
    "Resources":{
        "WebServer":{
            "Type":"ALIYUN::ECS::Instance",
            "Properties":{
                "DiskMappings":{
                    "Fn::If":[
                        "CreateDisk",
                        [
                            {
                                "Category":"cloud_efficiency",
                                "DiskName":"FirstDataDiskName",
                                "Size":40
                            },
                            {
                                "Category":"cloud_ssd",
                                "DiskName":"SecondDataDiskName",
                                "Size":40
                            }
                        ],
                        {
                            "Ref":"ALIYUN::NoValue"
                        }
                    ]
                },
                "VpcId":"vpc-2zew9pxh2yirtzqxdboi1",
                "SystemDiskCategory":"cloud_efficiency",
                "SecurityGroupId":"sg-2zece6wcqriejf1v91sr",
                "SystemDiskSize":40,
                "ImageId":"centos_6_8_64_40G_base_20170222.vhd",
                "IoOptimized":"optimized",
                "VSwitchId":"vsw-2zed9txvy7h2srqo6jmgq",
                "InstanceType":"ecs.n1.medium"
            }
        }
    },
    "Outputs":{
        "InstanceId":{
            "Value":{
                "Fn::GetAtt":[
                    "WebServer",
                    "InstanceId"
                ]
            }
        },
        "ZoneId":{
            "Value":{
                "Fn::GetAtt":[
                    "WebServer",
                    "ZoneId"
                ]
            }
        }
    }
}
```

支持的函数

-   Fn::Or
-   Fn::Not
-   Fn::Equals
-   Fn::FindInMap
-   Fn::And
-   Ref

## Fn::ListMerge {#section_rv4_2zv_kfb .section}

合并多个列表为一个列表。

声明

``` {#codeblock_05f_ovp_ocz .language-json}
{"Fn::ListMerge": [["list_1_item_1", "list_1_imte_2", ...], ["list_2_item_1", "list_2_imte_2", ...]]}
```

参数

-   `["list_1_item_1", "list_1_imte_2", ...]`：将要合并的第一个列表。
-   `["list_2_item_1", "list_2_imte_2", ...]`：将要和第一个列表合并的列表。

示例

把两个ECS组挂载到同一个负载均衡实例上：

``` {#codeblock_1iv_ci0_kso .language-json}
{
  "ROSTemplateFormatVersion" : "2015-09-01",
  "Resources" : {
    "LoadBalancer": {
      "Type": "ALIYUN::SLB::LoadBalancer",
      "Properties": {
        "LoadBalancerName": "ros",
        "AddressType": "internet",
        "InternetChargeType": "paybybandwidth",
      }
    },
    "BackendServer1": {
      "Type": "ALIYUN::ECS::InstanceGroup",
      "Properties": {
        "ImageId" : "m-2ze9uqi7wo61hwep5q52",
        "InstanceType": "ecs.t1.small",
        "SecurityGroupId": "sg-2ze8yxgempcdsq3iucsi",
        "MaxAmount": 1,
        "MinAmount": 1
      }
    },
    "BackendServer2": {
      "Type": "ALIYUN::ECS::InstanceGroup",
      "Properties": {
        "ImageId" : "m-2ze9uqi7wo61hwep5q52",
        "InstanceType": "ecs.t1.small",
        "SecurityGroupId": "sg-2ze8yxgempcdsq3iucsi",
        "MaxAmount": 1,
        "MinAmount": 1
      }
    },
    "Attachment": {
      "Type": "ALIYUN::SLB::BackendServerAttachment",
      "Properties": {
        "LoadBalancerId": {"Ref": "LoadBalancer"},
        "BackendServerList": { "Fn::ListMerge": [
            {"Fn::GetAtt": ["BackendServer1", "InstanceIds"]},
            {"Fn::GetAtt": ["BackendServer2", "InstanceIds"]}
          ]
        }
      }
    }
  }
}
```

支持的函数

-   Fn::Base64
-   Fn::GetAtt
-   Fn::Join
-   Fn::Select
-   Ref
-   Fn::Join
-   Fn::If

## Fn::GetJsonValue {#section_alq_2zv_kfb .section}

解析JSON字符串，获取指定的Key在第一层所对应的值。

声明

``` {#codeblock_5ku_cf4_bho .language-json}
{"Fn::GetJsonValue": ["key", "json_string"]}       
```

参数

-   `key`：键值。
-   `json_string`：指定的需要解析的JSON字符串。

示例

WebServer2从WebServer实例执行完UserData返回的JSON字符串中，获取对应的值：

``` {#codeblock_uep_9b1_443 .language-json}
{
  "ROSTemplateFormatVersion" : "2015-09-01",
  "Resources" : {
    "WebServer": {
      "Type": "ALIYUN::ECS::Instance",
      "Properties": {
        "ImageId" : "m-2ze45uwova5fedlufpz7",
        "InstanceType": "ecs.n1.medium",
        "SecurityGroupId": "sg-2ze7pxymaix640qrg3vu",
        "Password": "Wenqiao1234",
        "IoOptimized": "optimized",
        "VSwitchId": "vsw-2zei67xd9nhcqxzec7qt7",
        "VpcId": "vpc-2zevx9ios1rszqv0azijb",
        "SystemDiskCategory": "cloud_ssd",
        "UserData": {"Fn::Join": ["", [
             "#!/bin/sh\n",
             "mkdir ~/test_ros\n",
             "print hello > ~/1.txt\n",
             "Fn::GetAtt": ["WaitConHandle", "CurlCli"],
             "\n",
             "Fn::GetAtt": ["WaitConHandle", "CurlCli"],
             " -d '{\\"id\\" : \\"1\\", \\"data\\": [\\"1111\\", \\"2222\\"]}'\n"
         ]]},
         "PrivateIpAddress": "192.168.2.110",
         "HostName": "userdata-1"
      }
    },
    "WaitConHandle": {
        "Type": "ALIYUN::ROS::WaitConditionHandle"
    },
    "WaitCondition": {
        "Type": "ALIYUN::ROS::WaitCondition",
        "Properties": {
          "Handle": {"Ref": "WaitConHandle"},
          "Timeout": 900
        }
    },
    "WebServer2": {
      "Type": "ALIYUN::ECS::Instance",
      "Properties": {
        "ImageId" : "m-2ze45uwova5fedlufpz7",
        "InstanceType": "ecs.n1.medium",
        "SecurityGroupId": "sg-2ze7pxymaix640qrg3vu",
        "Password": "Wenqiao1234",
        "IoOptimized": "optimized",
        "VSwitchId": "vsw-2zei67xd9nhcqxzec7qt7",
        "VpcId": "vpc-2zevx9ios1rszqv0azijb",
        "SystemDiskCategory": "cloud_ssd",
        "UserData":
          {"Fn::Join": ["", [
             "#!/bin/sh\n",
             "mkdir ~/test_ros\n",
             "echo hello > ~/1.txt\n",
             "server_1_token=",
             {"Fn::GetJsonValue": ["1", { "Fn::GetAtt": ["WaitCondition", "Data"]}]},
             "\n"
         ]]},
         "PrivateIpAddress": "192.168.2.111",
         "HostName": "userdata-2"
      }
    },
  },
  "Outputs": {
    "InstanceId": {
         "Value" : {"Fn::GetAtt": ["WebServer","InstanceId"]}
    },
    "PublicIp": {
         "Value" : {"Fn::GetAtt": ["WebServer","PublicIp"]}
    }
  }
} 
```

支持的函数

-   Fn::Base64
-   Fn::GetAtt
-   Fn::Join
-   Fn::Select
-   Ref
-   Fn::Join
-   Fn::If

## Fn::MergeMapToList {#section_vs4_15v_kfb .section}

将多个Mapping合并成一个以Mapping为元素的列表。

声明

``` {#codeblock_6gj_ofc_28h .language-json}
{"Fn::MergeMapToList": [{"key_1": ["key_1_item_1", "key_1_item_2", ...]}, {"key_2":["key_2_item_1", "key_2_item_2", ...]}, ... ]}
```

参数

-   `{"key_1": ["key_1_item_1", "key_1_item_2", ...]}`：将要合并的第一个Mapping。`"key_1"`所对应的值必须是一个列表。`"key_1"`将是合并后的列表元素中，每个Mapping 的一个键。其对应的值在第一个Mapping中将是`"key_1_item_1"`，在第二个Mapping中是 `"key_1_item_2"`，以此类推。最终合并的列表长度是所有将要合并的参数Mapping中，`"key_x"` 所对应的列表中最长的长度。如果有的`"key_y"`所对应的列表长度比较短，会重复此列表的最后一个元素，使列表长度都达到最长。
-   `{"key_2": ["key_2_item_1", "key_2_item_2", ...]}`：将要合并的第二个Mapping。`"key_2"`所对应的值必须是一个列表。`"key_2"`将是合并后的列表元素中每个Mapping的一个键。其对应的值在第一个 Mapping中将是`"key_2_item_1"`，在第二个Mapping中是`"key_2_item_2"`，以此类推。

示例

-   合并三个Mapping，每个Mapping中键值对应的列表长度一致：

``` {#codeblock_3hi_40t_uhb .language-json}
{
   "Fn::MeregMapToList": [
      {"key_1": ["kye_1_item_1", "kye_1_item_2"]},
      {"key_2": ["kye_2_item_1", "kye_2_item_2"]},
      {"key_3": ["kye_3_item_1", "kye_3_item_2"]}
   ]
}     
```

    最终的合并结果是：

    ``` {#codeblock_0d0_gaq_cc6 .language-json}
    [  
       {
          "key_1": "kye_1_item_1",
          "key_2": "kye_2_item_1",
          "key_3": "kye_3_item_1"
        },
        {
          "key_1": "kye_1_item_2",
          "key_2": "kye_2_item_2",
          "key_3": "kye_3_item_2"
        }
    ]
    ```

-   合并三个Mapping，每个Mapping中键值对应的列表长度不一致：

``` {#codeblock_b1y_kax_cln .language-json}
{
   "Fn::MeregMapToList": [
      {"key_1": ["kye_1_item_1", "kye_1_item_2"]},
      {"key_2": ["kye_2_item_1", "kye_2_item_2", "key_2_item_3"]},
      {"key_3": ["kye_3_item_1", "kye_3_item_2"]}
   ]
}   
```

    最终的合并结果是：

    ``` {#codeblock_zh6_jvz_gia .language-json}
    [  
       {
          "key_1": "kye_1_item_1", 
          "key_2": "kye_2_item_1",
          "key_3": "kye_3_item_1"
        },
        {
          "key_1": "kye_1_item_2", 
          "key_2": "kye_2_item_2",
          "key_3": "kye_3_item_2"
        },
        {
          "key_1": "kye_1_item_2", 
          "key_2": "kye_2_item_3",
          "key_3": "kye_3_item_2"
        }
    ]  
    ```

-   以下模板示例中，把WebServer中创建的所有实例，都加入到一个负载均衡的虚拟服务器组中：

``` {#codeblock_dvk_pfz_hjz .language-json}
{
    "ROSTemplateFormatVersion": "2015-09-01",
    "Resources": {
        "WebServer": {
          "Type": "ALIYUN::ECS::InstanceGroupClone",
          "Properties": {
              "SourceInstanceId": "i-xxxxx",
               "Password": "Hello1234",
               "MinAmount": 1,
               "MaxAmount": 1
          }
        },
        "CreateVServerGroup": {
            "Type": "ALIYUN::SLB::VServerGroup",
            "Properties": {
                "LoadBalancerId": "lb-yyyy",
                "VServerGroupName": "VServerGroup-test",
                "BackendServers": {
                   "Fn::MergeMapToList": [
                       {"Port": [6666, 9090, 8080]},
                       {"ServerId": {"Fn::GetAtt": ["WebServer", "InstanceIds"]}},
                       {"Weight": [20, 100]}
                   ]
                }
            }
        }
    }
}
```


支持的函数

-   Fn::Base64
-   Fn::GetAtt
-   Fn::Join
-   Fn::Select
-   Ref
-   Fn::Join
-   Fn::If
-   Fn::ListMerge
-   Fn::GetJsonValue

## Fn::Avg {#section_ahc_g4m_xgb .section}

内部函数 Fn::Avg 对一组数求平均值。

声明

``` {#codeblock_p17_40e_v5l .language-json}
{ "Fn::Avg" : [ ndigits, [number1, number2, ... ]]}
```

参数

-   ndigits：平均值保留几位小数，必须为整数。
-   \[ number1, number2, ... \]：一组用来求取平均值的数字。组内每个元素可以是数字或能转换成数字的字符串。

返回值

给定一组数字的平均值。

示例

``` {#codeblock_5ur_t0i_el9 .language-json}
{ "Fn::Avg": [ 1, [1, 2, 6.0] ] } 
{ "Fn::Avg": [ 1, ['1', '2', '6.0'] ] }
```

返回：3.0。

支持的函数

-   Fn::GetAtt
-   Ref

