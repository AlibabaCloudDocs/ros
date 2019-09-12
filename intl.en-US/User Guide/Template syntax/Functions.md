# Functions {#concept_28865_zh .concept}

Resource Orchestration Service \(ROS\) provides several built-in functions to help you manage your resource stack. You can use intrinsic functions when defining Resources and Outputs.

Intrinsic functions that can be used in resource stack templates include: Fn::Str, Fn::Base64, Fn::FindInMap, Fn::GetAtt, Fn::Join, Fn::Select, Ref, Fn::GetAZs, Fn::Replace, Fn::Split, Fn::Equals, Fn::And, Fn::Or, Fn::Not, Fn::If, Fn::ListMerge, Fn::GetJsonValue, Fn::MergeMapToList, and Fn::Avg.

## Fn::Str {#section_hqj_vtv_kfb .section}

The Fn::Str function returns the string representation of a value.

Declaration

``` {#codeblock_sbq_s6y_j45 .language-json}
"Fn::Str" : ToString
```

Parameters

`ToString`: the Number or Integer type value to be converted to a string.

Return value

The string representation of the value.

Examples

``` {#codeblock_3nv_kl0_6az .language-json}
"Fn::Str": 123456
```

`"123456"` is returned in this example.

## Fn::Base64 {#section_hqj_vtv_kfb .section}

The Fn::Base64 function returns the Base64 representation of the input string.

Declaration

``` {#codeblock_7oc_a0e_4il .language-json}
"Fn::Base64" : stringToEncode
```

Parameters

`stringToEncode`: the string to be encoded in Base64.

Return value

The Base64 representation of the input string.

Examples

``` {#codeblock_1ad_wee_ip7 .language-json}
"Fn::Base64" : "string to encode"
```

## Fn::FindInMap {#section_dlh_15v_kfb .section}

The Fn::FindInMap function returns the value corresponding to keys in a two-level map that is declared in the Mappings section.

Declaration

``` {#codeblock_172_6d5_uf8 .language-json}
"Fn::FindInMap" : [ "MapName", "TopLevelKey", "SecondLevelKey"]
```

Parameters

-   `MapName`: the logical name of a mapping declared in the Mappings section that contains the keys and values.
-   `TopLevelKey`: the top-level key name. Its value is a list of key-value pairs.
-   `SecondLevelKey`: the second-level key name. Its value is a string or number.

Return value

The value that is assigned to SecondLevelKey.

Examples

In the following example, the ImageId property must be specified when a resource named WebServer is created. The Mappings section describes the ImageId mappings differentiated by region. The Parameters section describes the regions that must be specified by template users. Fn::FindInMap will find the corresponding ImageId mapping in RegionMap based on the region specified by a user, and then find the corresponding ImageId in the mapping.

-   MapName is set to the map of interest, `"RegionMap"` in this example.
-   TopLevelKey is set to the region where the resource stack is created, which in this example is specified by `{ "Ref" : "regionParam" }`.
-   SecondLevelKey is set to the required architecture, `"32"` in this example.

``` {#codeblock_e9m_0z8_ums .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "regionParam": {
        "Description": "Select a region to create an ECS instance",
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

Supported functions

-   Fn::FindInMap
-   Ref

## Fn::GetAtt {#section_z2k_15v_kfb .section}

The Fn::GetAtt function returns the value of an attribute from a resource in a template.

Declaration

``` {#codeblock_ncz_5kr_g8w .language-json}
"Fn::GetAtt": [ "resourceID", "attributeName" ]
```

Parameters

-   `resourceID`: the ID of the resource that contains your desired attribute.
-   `attributeName`: the name of the resource attribute whose value you want.

Return value

The attribute value.

Examples

In the following example, the returned resource ID is the ImageId property of MyEcsInstance.

``` {#codeblock_h73_d5x_tat .language-json}
"Fn::GetAtt" : [ "MyEcsInstance" , "ImageID" ]
```

## Fn::Join {#section_owl_15v_kfb .section}

The Fn::Join function appends a set of values into a single value separated by a specified delimiter.

Declaration

``` {#codeblock_7hp_rt4_enp .language-json}
{ "Fn::Join" : [ "delimiter", [ "string1", "string2", ... ]] }
```

Parameters

-   `delimiter`: the value you want to occur between fragments. The delimiter can be left blank so that all the values are directly combined.
-   `[ "string1", "string2", ... ]`: the list of values you want combined.

Return value

The combined string.

Examples

``` {#codeblock_ot8_88d_chi .language-json}
"Fn::Join" : [ ",", [ "a", "b", "c" ] ]
```

`"a,b,c"` is returned in this example.

Supported functions

-   Fn::Base64
-   Fn::GetAtt
-   Fn::Join
-   Fn::Select
-   Ref

## Fn::Select {#section_t3n_15v_kfb .section}

The Fn::Select function returns a single object from a list of objects by index.

Declaration

-   If the list of objects is an array, the syntax is as follows:

    ``` {#codeblock_qff_56v_kxi .language-json}
    "Fn::Select" : [ "index", [ "value1", "value2", ... ] ]        
    ```

-   If the list of objects is a mapping table, the syntax is as follows:

    ``` {#codeblock_cvq_g98_a70 .language-json}
    "Fn::Select" : [ "index", { "key1": "value1", ... } ]
    ```


Parameters

`index`: the index of the object to retrieve. If the list of objects is an array, the index must be an integer ranging from 0 and N-1, where N represents the number of elements in the array. If the list of objects is a mapping table, the index must be a key in the mapping table.

If the corresponding value of the index cannot be found, the system returns an empty string.

Return value

The selected object.

Examples

-   The following example assumes that the list of objects is an array:

    ``` {#codeblock_69e_r2b_tps .language-json}
    { "Fn::Select" : [ "1", [ "apples", "grapes", "oranges", "mangoes" ] ] }        
    ```

    `"grapes"` is returned in this example.

-   The following example assumes that the list of objects is a mapping table:

    ``` {#codeblock_96m_cek_gxb .language-json}
    { "Fn::Select" : [ "key1", { "key1": "grapes", "key2": "mangoes" } ] }     
    ```

    `"grapes"` is returned in this example.

-   The following example assumes that the list of objects is a CommaDelimitedList:

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


Supported functions

For the Fn::Select index value, you can use the Ref function.

For the Fn::Select list of objects, you can use the following functions:

-   Fn::Base64
-   Fn::FindInMap
-   Fn::GetAtt
-   Fn::Join
-   Fn::Select
-   Ref

## Ref {#section_yxv_5vv_kfb .section}

The Ref function returns the value of a specified parameter or resource.

If the specified parameter is a resource ID, the value of the resource is returned. Otherwise, the system will return the value of the specified parameter.

Declaration

``` {#codeblock_nt2_tug_p8g .language-json}
"Ref" : "logicalName"
```

Parameters

`LogicalName`: the logical name of the resource or parameter you want to reference.

Return value

The value of the resource or parameter.

Examples

The following example uses the Ref function to specify regionParam as the region parameter for RegionMap of WebServer:

``` {#codeblock_q8w_lz6_7pl .language-json}
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "regionParam": {
        "Description": "Select a region to create an ECS instance",
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

Supported functions

You cannot use any functions in the Ref function. You must specify the string for a logical resource ID.

## Fn::GetAZs {#section_pwy_5vv_kfb .section}

The Fn::GetAZs function returns an array that lists zones for a specified region.

Declaration

``` {#codeblock_hx7_qzd_0e5 .language-json}
"Fn::GetAZs": "region"    
```

Parameters

`Region`: the ID of the region.

Return value

The list of zones for the specified region.

Examples

The following example demonstrates how to create an ECS instance in the first zone of a specified region:

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

Supported functions

-   Fn::Base64
-   Fn::FindInMap
-   Fn::GetAtt
-   Fn::Join
-   Fn::Select
-   Ref

## Fn::Replace {#section_ppz_kwv_kfb .section}

The Fn::Replace function replaces a specified substring contained in a string with a new substring.

Declaration

``` {#codeblock_ox9_v42_v8z .language-json}
{ "Fn::Replace" : [ {"object_key": "object_value"}, "object_string"]     
```

Parameters

-   `object_key`: the substring to be replaced.
-   `object_value`: the new substring to replace the previous substring.
-   `object_string`: the target string whose `object_key` is to be replaced.

Return value

The string after replacement.

Examples

The following example demonstrates how to replace "print" in the specified script with "echo":

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
             "#! /bin/sh\n",
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

Supported functions

-   Fn::Base64
-   Fn::GetAtt
-   Fn::Join
-   Fn::Select
-   Ref

## Fn::Split {#section_nwc_lwv_kfb .section}

The Fn::Split function splits a string into a list of values separated by a specified delimiter.

Declaration

``` {#codeblock_rlh_ekj_h2a .language-json}
"Fn::Split" : [ "delim",  "original_string" ]         
```

Parameters

-   `delim`: the value used to divide the string. This value can be a comma \(,\), a semicolon \(;\), a \\n, or a \\t.
-   `original_string`: the string to be split.

Return value

A list of string values.

Examples

-   The following example assumes that the list of objects is an array:

``` {#codeblock_3vg_sdf_m5x .language-json}
{"Fn::Split": [";", "foo; bar; achoo"]}
```

    `["foo", " bar", "achoo "]` is returned in this example.

-   The following example uses Fn::Split to split InstanceIds:

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


Supported functions

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

The Fn::Equals function is used to compare whether two values are equal. If the two values are equal, TRUE is returned. If the two values are not equal, FALSE is returned.

Declaration

``` {#codeblock_29e_69w_34e .language-json}
{"Fn::Equals": ["value_1", "value_2"]}      
```

Parameters

`value`: the values to be compared. These values can be of any type.

Return value

TRUE or FALSE.

Examples

The following example uses Fn::Equals to define a condition in Conditions:

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

Supported functions

-   Fn::Or
-   Fn::Not
-   Fn::Equals
-   Fn::FindInMap
-   Fn::And
-   Ref

## Fn::And {#section_cqg_lwv_kfb .section}

The Fn::And function represents the AND operator that must contain at least two conditions. If all the specified conditions are evaluated as TRUE, TRUE is returned. If any condition is evaluated as FALSE, FALSE is returned.

Declaration

``` {#codeblock_3i4_pav_mc9 .language-json}
{"Fn::And": ["condition", {...}]} 
```

Parameters

`condition`: the conditions to be evaluated.

Return value

TRUE or FALSE.

Examples

The following example uses Fn::And to define a condition in Conditions:

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

Supported functions

-   Fn::Or
-   Fn::Not
-   Fn::Equals
-   Fn::FindInMap
-   Fn::And
-   Ref

## Fn::Or {#section_o2l_3xv_kfb .section}

The Fn::Or function represents the OR operator that must contain at least two conditions. If any specified condition is evaluated as TRUE, TRUE is returned. If all the conditions are evaluated as FALSE, FALSE is returned.

Declaration

``` {#codeblock_nax_dxn_a63 .language-json}
{"Fn::Or": ["condition", {...}]}
```

Parameters

`condition`: the conditions to be evaluated.

Return value

TRUE or FALSE.

Examples

The following example uses Fn::Or to define a condition in Conditions:

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

Supported functions

-   Fn::Or
-   Fn::Not
-   Fn::Equals
-   Fn::FindInMap
-   Fn::And
-   Ref

## Fn::Not {#section_otm_3xv_kfb .section}

The Fn::Not function represents the NOT operator. If a condition is evaluated as FALSE, TRUE is returned. If a condition is evaluated as TRUE, FALSE is returned.

Declaration

``` {#codeblock_src_okn_pl6 .language-json}
{"Fn::Not": "condition"}
```

Parameters

`condition`: the condition to be evaluated.

Return value

TRUE or FALSE.

Examples

The following example uses Fn::Not to define a condition in Conditions:

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

Supported functions

-   Fn::Or
-   Fn::Not
-   Fn::Equals
-   Fn::FindInMap
-   Fn::And
-   Ref

## Fn::If {#section_zy4_3xv_kfb .section}

If a specified condition is evaluated as TRUE, a value is returned. If the specified condition is evaluated as FALSE, another value is returned. The Resources and Outputs attribute values in templates support the Fn::If function. You can use the `ALIYUN::NoValue` pseudo parameter as the return value to delete the corresponding attribute.

Declaration

``` {#codeblock_ket_xvk_v3c .language-json}
{"Fn::If": ["condition_name", "value_if_true", "value_if_false"]}            
```

Parameters

-   `condition_name`: the name of the condition in Conditions. A condition is referenced using the condition name.
-   `value_if_true`: If the specified condition is evaluated as TRUE, this value is returned.
-   `value_if_false`: If the specified condition is evaluated as FALSE, this value is returned.

Examples

The following example demonstrates how to determine whether to create a data disk based on the input parameters:

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

Supported functions

-   Fn::Or
-   Fn::Not
-   Fn::Equals
-   Fn::FindInMap
-   Fn::And
-   Ref

## Fn::ListMerge {#section_rv4_2zv_kfb .section}

The Fn::ListMerge function merges multiple lists into one list.

Declaration

``` {#codeblock_05f_ovp_ocz .language-json}
{"Fn::ListMerge": [["list_1_item_1", "list_1_imte_2", ...], ["list_2_item_1", "list_2_imte_2", ...]]}
```

Parameters

-   `["list_1_item_1", "list_1_imte_2", ...]`: the first list to be merged.
-   `["list_2_item_1", "list_2_imte_2", ...]`: the list to be merged with the first list.

Examples

The following example demonstrates how to attach two ECS instance groups to the same SLB instance:

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

Supported functions

-   Fn::Base64
-   Fn::GetAtt
-   Fn::Join
-   Fn::Select
-   Ref
-   Fn::Join
-   Fn::If

## Fn::GetJsonValue {#section_alq_2zv_kfb .section}

The Fn::GetJsonValue function resolves a JSON string and obtains the value of the specified Key at the first layer.

Declaration

``` {#codeblock_5ku_cf4_bho .language-json}
{"Fn::GetJsonValue": ["key", "json_string"]}       
```

Parameters

-   `key`: the key value.
-   `json_string`: the specified JSON string to be resolved.

Examples

The following example demonstrates that after the WebServer instance executes UserData and returns a JSON string, the WebServer2 instance obtains the corresponding value from the string.

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
             "#! /bin/sh\n",
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
             "#! /bin/sh\n",
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

Supported functions

-   Fn::Base64
-   Fn::GetAtt
-   Fn::Join
-   Fn::Select
-   Ref
-   Fn::Join
-   Fn::If

## Fn::MergeMapToList {#section_vs4_15v_kfb .section}

The Fn::MergeMapToList function merges multiple mappings into a list of mapping elements.

Declaration

``` {#codeblock_6gj_ofc_28h .language-json}
{"Fn::MergeMapToList": [{"key_1": ["key_1_item_1", "key_1_item_2", ...]}, {"key_2":["key_2_item_1", "key_2_item_2", ...]}, ... ]}
```

Parameters

-   `{"key_1": ["key_1_item_1", "key_1_item_2", ...]}`: the first mapping to be merged. The `" key_1"` value must be a list. `" key_1"` is a key of each mapping in the list of merged mappings. The "key\_1" value is `"key_1_item_1"` in the first mapping and `"key_1_item_2"` in the second mapping. The length of the final list of merged mappings is the length of the longest list `"key_x"` in all mappings to be merged. If a `"key_y"` list is shorter, the last element of the list is repeated to make the list the longest.
-   `{"key_2": ["key_2_item_1", "key_2_item_2", ...]}`: the second mapping to be merged. The `" key_2"` value must be a list. `" key_2"` is a key of each mapping in the merged list. The "key\_2" value is `"key_2_item_1"` in the first mapping and `"key_2_item_2"` in the second mapping.

Examples

-   The following example demonstrates how to merge three mappings. The length of the list corresponding to the key value in each mapping is the same.

``` {#codeblock_3hi_40t_uhb .language-json}
{
   "Fn::MeregMapToList": [
      {"key_1": ["kye_1_item_1", "kye_1_item_2"]},
      {"key_2": ["kye_2_item_1", "kye_2_item_2"]},
      {"key_3": ["kye_3_item_1", "kye_3_item_2"]}
   ]
}     
```

    The result is:

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

-   In the following example, the length of the list corresponding to the key value in each mapping varies.

``` {#codeblock_b1y_kax_cln .language-json}
{
   "Fn::MeregMapToList": [
      {"key_1": ["kye_1_item_1", "kye_1_item_2"]},
      {"key_2": ["kye_2_item_1", "kye_2_item_2", "key_2_item_3"]},
      {"key_3": ["kye_3_item_1", "kye_3_item_2"]}
   ]
}   
```

    The result is:

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

-   In the following template example, all instances created in WebServer are added to the VServer group of an SLB instance.

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


Supported functions

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

The Fn::Avg function returns the average value of a set of numbers.

Declaration

``` {#codeblock_p17_40e_v5l .language-json}
{ "Fn::Avg" : [ ndigits, [number1, number2, ... ]]}
```

Parameters

-   ndigits: the number of decimal places to calculate the average value to. This parameter value must be an integer.
-   \[ number1, number2, ... \]: a set of numbers for which to calculate the average value. Each element in the group must be either a number or a string that can be converted into a number.

Return value

The average value of a set of numbers.

Examples

``` {#codeblock_5ur_t0i_el9 .language-json}
{ "Fn::Avg": [ 1, [1, 2, 6.0] ] } 
{ "Fn::Avg": [ 1, ['1', '2', '6.0'] ] }
```

3.0 is returned in this example.

Supported functions

-   Fn::GetAtt
-   Ref

