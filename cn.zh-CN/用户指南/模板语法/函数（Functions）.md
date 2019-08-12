# 函数（Functions） {#concept_28865_zh .concept}

资源编排服务提供多个内置函数，帮助您管理您的资源栈。您可以在定义资源（Resources\) 和输出 \(Outputs\) 时，使用内部函数。

可在资源栈模板中使用的内部函数：Fn::Base64、Fn::FindInMap、Fn::GetAtt、Fn::Join、Fn::Select、Ref、 Fn::GetAZs、Fn::Replace、Fn::Split、Fn::Equals、Fn::And、Fn::Or、Fn::Not、Fn::If、Fn::ListMerge、Fn::GetJsonValue、 Fn::MergeMapToList 和Fn::Avg。

## Fn::Base64 {#section_hqj_vtv_kfb .section}

内部函数 Fn::Base64 返回输入字符串的 Base64 编码结果。

**声明**

``` {#codeblock_8n1_vri_ai7 .language-json}
"Fn::Base64" : stringToEncode
			
```

**参数**

`stringToEncode`：转换成 Base64 的字符串。

**返回值**

用 Base64 表示的原始字符串。

**示例**

``` {#codeblock_1ad_wee_ip7 .language-json}
"Fn::Base64" : "string to encode"
			
```

## Fn::FindInMap {#section_dlh_15v_kfb .section}

内部函数 Fn::FindInMap 返回与 Mappings 声明的双层映射中的键对应的值。

**声明**

``` {#codeblock_172_6d5_uf8 .language-json}
"Fn::FindInMap" : [ "MapName", "TopLevelKey", "SecondLevelKey"]
			
```

**参数**

`MapName`：Mappings 中所声明映射的 ID，包含键和值。

`TopLevelKey`：第一级键，其值是一个键/值对列表。

`SecondLevelKey`：第二级键，其值是一个字符串或者数字。

**返回值**

分配给 SecondLevelKey 的值。

**示例**

如下示例，在创建名为 WebServer 的资源时，需要指定 ImageId 属性。在 Mappings 中，描述根据区域区分的 ImageId 映射。在 Parameters 中，描述需要用户指定的区域。Fn::FindInMap 会根据用户指定的区域，在 RegionMap 中查找对应的 ImageId 映射，然后在映射中找到对应的 ImageId。

-   MapName 可按照个人意愿设置。在本示例中为 `"RegionMap"`。
-   TopLevelKey 设置为创建资源栈的地区。在本示例中，通过 `{ "Ref" : "regionParam" }` 确定。
-   SecondLevelKey 设置为所需的架构。在本示例中为`"32"`。

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

**支持的函数**

您可以在 Fn::FindInMap 函数中使用以下函数：

-   Fn::FindInMap
-   Ref

## Fn::GetAtt {#section_z2k_15v_kfb .section}

内部函数 Fn::GetAtt 返回模板中的资源的属性值。

**声明**

``` {#codeblock_ncz_5kr_g8w .language-json}
"Fn::GetAtt": [ "resourceID", "attributeName" ]
			
```

**参数**

`resourceID`：目标资源的 ID。

`attributeName`：目标资源的属性名称。

**返回值**

属性值。

**示例**

此示例返回 Resource ID 为 MyEcsInstance 的ImageId 属性。

``` {#codeblock_cfh_97r_4zr .language-json}
"Fn::GetAtt" : [ "MyEcsInstance" , "ImageID" ]
			
```

## Fn::Join {#section_owl_15v_kfb .section}

内部函数 Fn::Join 将一组值连接起来，用特定分隔符隔开。

**声明**

``` {#codeblock_lvm_2ou_7wz .language-json}
{ "Fn::Join" : [ "delimiter", [ "string1", "string2", ... ]] }
			
```

**参数**

`delimiter`：分隔符。分隔符可以为空，这样就将所有的值直接连接起来。

`[ "string1", "string2", ... ]`：被连接起来的值列表示例。

**返回值**

被连接起来的字符串。

**示例**

``` {#codeblock_6mi_hn4_fif .language-json}
"Fn::Join" : [ ",", [ "a", "b", "c" ] ]
			
```

返回：`"a,b,c"`。

**支持的函数**

-   Fn::Base64
-   Fn::GetAtt
-   Fn::Join
-   Fn::Select
-   Ref

## Fn::Select {#section_t3n_15v_kfb .section}

内部函数 Fn::Select 通过索引返回数据元列表中的单个数据元。

**声明**

数据元列表是一个数组：

``` {#codeblock_6tv_lrd_nn5 .language-json}
"Fn::Select" : [ "index", [ "value1", "value2", ... ] ]
			
```

数据元列表是一个映射表：

``` {#codeblock_tu2_k30_9wl .language-json}
"Fn::Select" : [ "index", { "key1": "value1", ... } ]
			
```

**参数**

`index`：待检索数据元的索引。如果数据元列表是一个数组，则索引是 0 到 N-1 之间的某个值（其中 N 代表阵列中元素的数量）。如果数据元列表是一个映射表，则索引是映射表中的某个键。

如果找不到索引对应的值，则返回空字符串。

**返回值**

选定的数据元。

**示例**

如果数据元列表是一个数组：

``` {#codeblock_ta8_0th_nut .language-json}
{ "Fn::Select" : [ "1", [ "apples", "grapes", "oranges", "mangoes" ] ] }
			
```

返回：`"grapes"`。

如果数据元列表是一个映射表：

``` {#codeblock_zbe_0xs_znv .language-json}
{ "Fn::Select" : [ "key1", { "key1": "grapes", "key2": "mangoes" } ] }
			
```

返回：`"grapes"`。

如果数据元列表是一个 CommaDelimitedList：

``` {#codeblock_ytq_adg_ldo .language-json}
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
},
			
```

**支持的函数**

对于 Fn::Select 索引值，您可以使用 Ref 函数。

对于对象的 Fn::Select 列表，您可以使用以下函数：

-   Fn::Base64
-   Fn::FindInMap
-   Fn::GetAtt
-   Fn::Join
-   Fn::Select
-   Ref

## Ref {#section_yxv_5vv_kfb .section}

内部函数 Ref 返回指定参数或资源的值。

如果指定参数是 Resource ID，则返回资源的值。否则系统将认为指定参数是参数，将尝试返回参数的值。

**声明**

``` {#codeblock_nt2_tug_p8g .language-json}
"Ref" : "logicalName"
			
```

**参数**

`logicalName`：要引用的资源或参数的逻辑名称。

**返回值**

资源的值或者参数的值。

**示例**

使用 Ref 函数指定 regionParam 作为 WebServer 的 RegionMap 的区域参数：

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

**支持的函数**

不能在 Ref 函数中使用任何函数。必须指定为资源逻辑 ID 的字符串。

## Fn::GetAZs {#section_pwy_5vv_kfb .section}

内部函数 Fn::GetAZs 返回指定 Region 的可用区列表。

**声明**

``` {#codeblock_yrt_5pd_uc5 .language-json}
"Fn::GetAZs": "region"
			
```

**参数**

`region`：region ID。

**返回值**

指定 Region 下的可用区列表。

**示例**

在指定的 Region 的第一个可用区内创建一个 ECS 实例：

``` {#codeblock_k1l_2au_rbb .language-json}
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

**支持的函数**

-   Fn::Base64
-   Fn::FindInMap
-   Fn::GetAtt
-   Fn::Join
-   Fn::Select
-   Ref

## Fn::Replace {#section_ppz_kwv_kfb .section}

内部函数 Fn::Replace 将字符串中指定子字符串用新字符串替换。

**声明**

``` {#codeblock_pml_noc_jgx .language-json}
{ "Fn::Replace" : [ {"object_key": "object_value"}, "object_string"]
			
```

**参数**

`{"object_key": "object_value"}`：

-   `object_key` 是将要被替换的字符串。
-   `object_value` 是将要替换成的最终字符串。

`object_string`：包含被替换 `object_key` 的字符串。

**返回值**

被替换后的字符串。

**示例 UserData**

所指定的脚本中的 print 将被替换成 echo。

``` {#codeblock_h37_fl1_8lz .language-json}
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

**支持的函数**

-   Fn::Base64
-   Fn::GetAtt
-   Fn::Join
-   Fn::Select
-   Ref

## Fn::Split {#section_nwc_lwv_kfb .section}

内部函数 Fn::Split 通过指定分隔符对字符串进行切片，并返回所有切片组成的列表。

**声明**

``` {#codeblock_0q7_0pc_u1e .language-json}
"Fn::Split" : [ "delim",  "original_string" ]
			
```

**参数**

`delim`：分隔符, 例如: ','，';'，'\\n'，'\\t' 等。

`original_string`：将要被切片的字符串。

**返回值**

返回切片后所有字符串组成的列表。

**示例**

如果数据元列表是一个数组：

``` {#codeblock_hbn_it5_s76 .language-json}
{"Fn::Split": [";", "foo; bar; achoo"]}
			
```

返回：`["foo", " bar", "achoo "]`。

使用 Fn::Split 对 InstanceIds 进行切片 ：

``` {#codeblock_icb_uyv_400 .language-json}
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

**支持的函数**

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

比较两个值是否相等。如果两个值相等，则返回 true；如果不相等，则返回 false。

**声明**

``` {#codeblock_29e_69w_34e .language-json}
{"Fn::Equals": ["value_1", "value_2"]}
			
```

**参数**

`value`：要比较的任意类型的值。

**返回值**

true 或 false。

**示例**

在 Conditions 中使用 Fn::Equals 定义条件。

``` {#codeblock_qlh_wj2_ra8 .language-json}
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

**支持的函数**

-   Fn::Or
-   Fn::Not
-   Fn::Equals
-   Fn::FindInMap
-   Fn::And
-   Ref

## Fn::And {#section_cqg_lwv_kfb .section}

代表 AND 运算符，最少包含两个条件。如果所有指定条件计算为 true，则返回 true；如果任意条件计算为 false，则返回 false。

**声明**

``` {#codeblock_ow5_puu_ig6 .language-json}
{"Fn::And": ["condition", {...}]}
			
```

**参数**

`condition`：计算为 true 或 false 的条件。

**返回值**

true 或 false。

**示例**

在 Conditions 中使用 Fn::And 定义一个条件。

``` {#codeblock_209_x39_k2f .language-json}
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

**支持的函数**

-   Fn::Or
-   Fn::Not
-   Fn::Equals
-   Fn::FindInMap
-   Fn::And
-   Ref

## Fn::Or {#section_o2l_3xv_kfb .section}

代表 OR 运算符，最少包含两个条件。如果任意一个指定条件计算为 true，则返回 true；如果所有条件都计算为 false，则返回 false。

**声明**

``` {#codeblock_nax_dxn_a63 .language-json}
{"Fn::Or": ["condition", {...}]}
			
```

**参数**

`condition`：计算为 true 或 false 的条件。

**返回值**

true 或 false。

**示例**

在 Conditions 中使用 Fn::Or 定义一个条件。

``` {#codeblock_nq2_t7b_f4e .language-json}
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

**支持的函数**

-   Fn::Or
-   Fn::Not
-   Fn::Equals
-   Fn::FindInMap
-   Fn::And
-   Ref

## Fn::Not {#section_otm_3xv_kfb .section}

代表 NOT 运算符。对计算为 false 的条件，返回 true；对计算为 true 的条件，返回 false。

**声明**

``` {#codeblock_src_okn_pl6 .language-json}
{"Fn::Not": "condition"}
			
```

**参数**

`condition`：计算为 true 或 false 的条件。

**返回值**

true 或 false。

**示例**

在 Conditions 中使用 Fn::Not 定义一个条件。

``` {#codeblock_ut4_tp2_03p .language-json}
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

**支持的函数**

-   Fn::Or
-   Fn::Not
-   Fn::Equals
-   Fn::FindInMap
-   Fn::And
-   Ref

## Fn::If {#section_zy4_3xv_kfb .section}

如果指定的条件计算为 true，则返回一个值；如果指定的条件计算为 false，则返回另一个值。在模板 Resources 和 Outputs 属性值中支持 Fn::If 内部函数。您可以使用 `ALIYUN::NoValue` 伪参数作为返回值来删除相应的属性。

**声明**

``` {#codeblock_6se_xko_igm .language-json}
{"Fn::If": ["condition_name", "value_if_true", "value_if_false"]}
			
```

**参数**

`condition_name`：Conditions 中条件对应的条件名称。通过条件名称引用条件。

`value_if_true`：当指定的条件计算为 true 时，返回此值。

`value_if_false`：当指定的条件计算为 false 时，返回此值。

**示例**

根据输入的参数，确定是否创建数据盘：

``` {#codeblock_9oz_55n_hq6 .language-json}
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

**支持的函数**

-   Fn::Or
-   Fn::Not
-   Fn::Equals
-   Fn::FindInMap
-   Fn::And
-   Ref

## Fn::ListMerge {#section_rv4_2zv_kfb .section}

合并多个列表为一个列表。

**声明**

``` {#codeblock_g5c_ayq_pv1 .language-json}
{"Fn::ListMerge": [["list_1_item_1", "list_1_imte_2", ...], ["list_2_item_1", "list_2_imte_2", ...]]}
			
```

**参数**

`["list_1_item_1", "list_1_imte_2", ...]`：将要合并的第一个列表

`["list_2_item_1", "list_2_imte_2", ...]`：将要和第一个列表合并的列表

**示例**

把两个 ECS 组挂载到同一个负载均衡实例上：

``` {#codeblock_4eo_ttx_plr .language-json}
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

**支持的函数**

-   Fn::Base64
-   Fn::GetAtt
-   Fn::Join
-   Fn::Select
-   Ref
-   Fn::Join
-   Fn::If

## Fn::GetJsonValue {#section_alq_2zv_kfb .section}

解析 JSON 字符串，获取指定的 Key 在第一层所对应的值。

**声明**

``` {#codeblock_a1p_07y_358 .language-json}
{"Fn::GetJsonValue": ["key", "json_string"]}
			
```

**参数**

`key`：键值

`json_string`：指定的需要解析的 JSON 字符串。

**示例**

WebServer2 从 WebServer 实例执行完 UserData 返回的 JSON 字符串中，获取对应的值：

``` {#codeblock_946_ku9_odb .language-json}
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

**支持的函数**

-   Fn::Base64
-   Fn::GetAtt
-   Fn::Join
-   Fn::Select
-   Ref
-   Fn::Join
-   Fn::If

## Fn::MergeMapToList {#section_vs4_15v_kfb .section}

将多个 Mapping 合并成一个以 Mapping 为元素的列表。

**声明**

``` {#codeblock_6gj_ofc_28h .language-json}
{"Fn::MergeMapToList": [{"key_1": ["key_1_item_1", "key_1_item_2", ...]}, {"key_2":["key_2_item_1", "key_2_item_2", ...]}, ... ]}
			
```

**参数**

`{"key_1": ["key_1_item_1", "key_1_item_2", ...]}`：将要合并的第一个 Mapping，`"key_1"` 所对应的值必须是一个列表。`"key_1"` 将是合并后的列表元素中，每个 Mapping 的一个键。其对应的值在第一个 Mapping 中将是 `"key_1_item_1"`，在第二个 Mapping 中是 `"key_1_item_2"`，以此类推。最终合并的列表长度是所有将要合并的参数 Mapping 中，`"key_x"` 所对应的列表中最长的长度。如果有的 `"key_y"` 所对应的列表长度比较短，会重复此列表的最后一个元素，使列表长度都达到最长。

`{"key_2": ["key_2_item_1", "key_2_item_2", ...]}`：将要合并的第二个 Mapping，`"key_2"` 所对应的值必须是一个列表。`"key_2"` 将是合并后的列表元素中每个 Mapping 的一个键。其对应的值在第一个 Mapping 中将是 `"key_2_item_1"`，在第二个 Mapping 中是 `"key_2_item_2"`，以此类推。

**示例**

合并三个 Mapping，每个 Mapping 中键值对应的列表长度一致：

``` {#codeblock_665_7tb_z2p .language-json}
{
   "Fn::MeregMapToList": [
      {"key_1": ["kye_1_item_1", "kye_1_item_2"]},
      {"key_2": ["kye_2_item_1", "kye_2_item_2"]},
      {"key_3": ["kye_3_item_1", "kye_3_item_2"]}
   ]
}
			
```

最终的合并结果是：

``` {#codeblock_7u8_rd1_x68 .language-json}
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

合并三个 Mapping，每个 Mapping 中键值对应的列表长度不一致：

``` {#codeblock_fic_zdd_59l .language-json}
{
   "Fn::MeregMapToList": [
      {"key_1": ["kye_1_item_1", "kye_1_item_2"]},
      {"key_2": ["kye_2_item_1", "kye_2_item_2", "key_2_item_3"]},
      {"key_3": ["kye_3_item_1", "kye_3_item_2"]}
   ]
}
			
```

最终的合并结果是：

``` {#codeblock_j8d_75i_nz7 .language-json}
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

以下模板示例中，把 WebServer 中创建的所有实例，都加入到一个负载均衡的虚拟服务器组中：

``` {#codeblock_2mb_krn_pop .language-json}
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

**支持的函数**

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

**声明**

``` {#codeblock_p17_40e_v5l .language-json}
{ "Fn::Avg" : [ ndigits, [number1, number2, ... ]]}
```

**参数**

ndigits：平均值保留几位小数，必须为整数。

\[ number1, number2, ... \]：一组用来求取平均值的数字。组内每个元素可以是数字或能转换成数字的字符串。

**返回值**

给定一组数字的平均值。

**示例**

``` {#codeblock_j3c_om1_llb .language-json}
{ "Fn::Avg": [ 1, [1, 2, 6.0] ] } 
{ "Fn::Avg": [ 1, ['1', '2', '6.0'] ] }
```

返回：3.0。

**支持的函数**

-   Fn::GetAtt

-   Ref

