# 函数（Functions）

资源编排服务提供多个内置函数，帮助您管理资源栈。您可以在定义资源（Resources）和输出（Outputs）时，使用内部函数。

可在资源栈模板中使用的内部函数包括：Fn::Str、Fn::Base64Encode、Fn::Base64Decode、Fn::FindInMap、Fn::GetAtt、Fn::Join、Fn::Select、Ref、Fn::GetAZs、Fn::Replace、Fn::Split、Fn::Equals、Fn::And、Fn::Or、Fn::Not、Fn::If、Fn::Length、Fn::ListMerge、Fn::GetJsonValue、Fn::MergeMapToList、Fn::Avg、Fn::SelectMapList、Fn::Add、Fn::Calculate、Fn::Sub、Fn::Max、Fn::Min、Fn::GetStackOutput和Fn::Jq。

## Fn::Str

内部函数Fn::Str返回输入数字的字符串结果。

声明

```
"Fn::Str" : toString
```

参数

`toString`：需要转换的Number/Integer类型的值。

返回值

该值的字符串类型。

示例

```
{"Fn::Str": 123456}
```

返回：`"123456"`。

## Fn::Base64Encode

内部函数Fn::Base64Encode返回输入字符串的Base64编码结果。

声明

```
"Fn::Base64Encode": "stringToEncode"
```

参数

`stringToEncode`：转换成Base64的字符串。

返回值

用Base64表示的原始字符串。

示例

```
{"Fn::Base64Encode": "string to encode"}
```

返回：`c3RyaW5nIHRvIGVuY29kZQ==`。

## Fn::Base64Decode

内部函数Fn::Base64Decode返回Base64编码的字符串解码的结果。

声明

```
{"Fn::Base64Decode": "stringToEncode"}
```

参数

`stringToDecode`：将Base64编码的字符串解码。

返回值

字符串。

示例

```
{"Fn::Base64Decode": "c3RyaW5nIHRvIGVuY29kZQ=="}
```

返回：`string to encode`。

## Fn::FindInMap

内部函数Fn::FindInMap返回与Mappings声明的双层映射中的键对应的值。

声明

```
"Fn::FindInMap": ["MapName", "TopLevelKey", "SecondLevelKey"]
```

参数

-   `MapName`：Mappings中所声明映射的ID，包含键和值。
-   `TopLevelKey`：第一级键，其值是一个键/值对列表。
-   `SecondLevelKey`：第二级键，其值是一个字符串或者数字。

返回值

分配给SecondLevelKey的值。

示例

在创建名为WebServer的资源时，需要指定ImageId属性。在Mappings中，描述根据区域区分的ImageId映射。在Parameters中，描述需要用户指定的区域。Fn::FindInMap会根据用户指定的区域，在RegionMap中查找对应的ImageId映射，然后在映射中找到对应的ImageId。

-   MapName可按照个人意愿设置。在本示例中为`"RegionMap"`。
-   TopLevelKey设置为创建资源栈的地区。在本示例中，通过`{ "Ref" : "regionParam" }`确定。
-   SecondLevelKey设置为所需的架构。在本示例中为`"32"`。

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "regionParam": {
      "Description": "选择创建ECS的区域",
      "Type": "String",
      "AllowedValues": [
        "hangzhou",
        "beijing"
      ]
    }
  },
  "Mappings": {
    "RegionMap": {
      "hangzhou": {
        "32": "m-25l0rcfjo",
        "64": "m-25l0rcfj1"
      },
      "beijing": {
        "32": "m-25l0rcfj2",
        "64": "m-25l0rcfj3"
      }
    }
  },
  "Resources": {
    "WebServer": {
      "Type": "ALIYUN::ECS::Instance",
      "Properties": {
        "ImageId": {
          "Fn::FindInMap": [
            "RegionMap",
            {"Ref": "regionParam"},
            "32"
          ]
        },
        "InstanceType": "ecs.t1.small",
        "SecurityGroupId": "sg-25zwc****",
        "ZoneId": "cn-beijing-b",
        "Tags": [
          {
            "Key": "key1",
            "Value": "value1"
          },
          {
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

## Fn::GetAtt

内部函数Fn::GetAtt返回模板中的资源的属性值。

声明

```
"Fn::GetAtt": ["resourceID", "attributeName"]
```

参数

-   `resourceID`：目标资源的ID。
-   `attributeName`：目标资源的属性名称。

返回值

属性值。

示例

返回Resource ID为MyEcsInstance的ImageId属性。

```
{"Fn::GetAtt" : ["MyEcsInstance" , "ImageID"]}
```

## Fn::Join

内部函数Fn::Join将一组值连接起来，用特定分隔符隔开。

声明

```
{"Fn::Join": ["delimiter", ["string1", "string2", ... ]]}
```

参数

-   `delimiter`：分隔符。分隔符可以为空，表示将所有的值直接连接起来。
-   `[ "string1", "string2", ... ]`：被连接起来的值列表示例。

返回值

被连接起来的字符串。

示例

```
{"Fn::Join": [ ",", ["a", "b", "c"]]}
```

返回：`"a,b,c"`。

支持的函数

-   Fn::Base64Encode
-   Fn::GetAtt
-   Fn::Join
-   Fn::Select
-   Ref

## Fn::Select

内部函数Fn::Select通过索引返回列表或字典中的数据。

声明

-   获取列表（数组）中的数据
    -   根据索引获取单个数据

        ```
        {"Fn::Select": ["index", ["value1", "value2", ... ]]}     
        ```

    -   获取多个数据

        ```
        {"Fn::Select": ["start:stop", ["value1", "value2", ... ]]}
        ```

        ```
        {"Fn::Select": ["start:stop:step", ["value1", "value2", ... ]]}
        ```

-   获取字典（映射表）某个键对应的值：

    ```
    {"Fn::Select": ["key", {"key1": "value1", "key2": "value2", ... }]}
    ```


参数

-   `index`：待检索数据的索引。索引是0到N-1之间或-N到-1之间的某个值（其中N代表列表中元素的数量），负数表示从右往左第几个元素。如果索引不在取值范围内，则返回空字符串。
-   `start`、`stop`和`step`：根据指定的起始位置和终止位置获取列表中的元素，可以指定步长，即每隔step-1个元素取一个元素，返回一个列表。
    -   `start:stop`：start、stop取值同index，start不填时默认为0，stop不填时默认为N。返回列表中第start+1到第stop个元素组成的列表，如果二者取值不在取值范围内则返回空列表。
    -   `start:stop:step`：step不填时默认为1，如果step为负数，则start表示的元素的索引应大于stop表示的元素的索引，从第start个元素到第stop+1元素，每隔-step-1个元素取一个元素，返回一个列表。
-   `key`：字典的某个键，返回键对应的值，如果字典中不存在该键则返回空字符串。

返回值

选定的数据。

示例

-   从列表或数组中取值：
    -   ```
{"Fn::Select": ["1", ["apples", "grapes", "oranges", "mangoes"]]}        
```

        返回：`"grapes"`。

    -   ```
{"Fn::Select": ["1:3", [1, 2, 3, 4, 5]]}
```

        返回：`[2, 3]`

    -   ```
{"Fn::Select": ["::2", [1, 2, 3, 4, 5]]}
```

        返回：`[1, 3, 5]`

    -   ```
{"Fn::Select": ["5:0:-2", [1, 2, 3, 4, 5]]}
```

        返回：`[5, 3]`

-   获取字典某个键对应的值：

    ```
    {"Fn::Select": ["key1", {"key1": "grapes", "key2": "mangoes"}]}     
    ```

    返回：`"grapes"`。

-   如果数据元列表是一个CommaDelimitedList：

    ```
    "Parameters": {
      "userParam": {
        "Type": "CommaDelimitedList",
          "Default": "10.0.0.1, 10.0.0.2, 10.0.0.3"
      }
    }
    
    "Resources": {
      "resourceID": {
          "Properties": {
              "CidrBlock": {"Fn::Select": ["0", {"Ref": "userParam"}]}
        }
      }
    }
    ```

    返回：`10.0.0.1`


支持的函数

对于Fn::Select索引值，您可以使用Ref函数。

对于对象的 Fn::Select 列表，您可以使用以下函数：

-   Fn::Base64Encode
-   Fn::FindInMap
-   Fn::GetAtt
-   Fn::Join
-   Fn::Select
-   Ref

## Ref

内部函数Ref返回指定参数或资源的值。

如果指定参数是Resource ID，则返回资源的值。否则系统将认为指定参数是参数，将尝试返回参数的值。

声明

```
"Ref": "logicalName"
```

参数

`logicalName`：要引用的资源或参数的逻辑名称。

返回值

资源的值或者参数的值。

示例

使用Ref函数指定regionParam作为WebServer的RegionMap的区域参数。

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "regionParam": {
      "Description": "选择创建ECS的区域",
      "Type": "String",
      "AllowedValues": [
        "hangzhou",
        "beijing"
      ]
    }
  },
  "Mappings": {
    "RegionMap": {
      "hangzhou": {
        "32": "m-25l0rcfjo",
        "64": "m-25l0rcfj1"
      },
      "beijing": {
        "32": "m-25l0rcfj2",
        "64": "m-25l0rcfj3"
      }
    }
  },
  "Resources": {
    "WebServer": {
      "Type": "ALIYUN::ECS::Instance",
      "Properties": {
        "ImageId": {
          "Fn::FindInMap": [
            "RegionMap",
            {"Ref": "regionParam"},
            "32"
          ]
        },
        "InstanceType": "ecs.t1.small",
        "SecurityGroupId": "sg-25zwc****",
        "ZoneId": "cn-beijing-b",
        "Tags": [
          {
            "Key": "tiantt",
            "Value": "ros"
          },
          {
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

## Fn::GetAZs

内部函数Fn::GetAZs返回指定Region的可用区列表。

**说明：** 该函数只适用于ECS和VPC类型的资源。

声明

```
"Fn::GetAZs": "region"    
```

参数

`region`：region ID。

返回值

指定Region下的可用区列表。

示例

在指定Region的第一个可用区内创建一个ECS实例。

```
{
  "ROSTemplateFormatVersion" : "2015-09-01",
  "Resources" : {
    "WebServer": {
      "Type": "ALIYUN::ECS::Instance",
      "Properties": {
        "ImageId": "centos7u2_64_40G_cloudinit_2016072****",
        "InstanceType": "ecs.n1.tiny",
        "SecurityGroupId": "sg-2zedcm7ep5quses0****",
        "Password": "Ros1****",
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
         "Value": {"Fn::GetAtt": ["WebServer","InstanceId"]}
    },
    "PublicIp": {
         "Value": {"Fn::GetAtt": ["WebServer","PublicIp"]}
    }
  }
}
```

支持的函数

-   Fn::Base64Encode
-   Fn::FindInMap
-   Fn::GetAtt
-   Fn::Join
-   Fn::Select
-   Ref

## Fn::Replace

内部函数Fn::Replace将字符串中指定子字符串用新字符串替换。

声明

```
{"Fn::Replace": [{"object_key": "object_value"}, "object_string"]} 
```

参数

-   `object_key`：将要被替换的字符串。
-   `object_value`：将要替换成的最终字符串。
-   `object_string`：包含被替换`object_key`的字符串。

返回值

被替换后的字符串。

示例

所指定脚本中的print替换成echo。

```
{
  "ROSTemplateFormatVersion" : "2015-09-01",
  "Resources" : {
    "WebServer": {
      "Type": "ALIYUN::ECS::Instance",
      "Properties": {
        "ImageId" : "centos_7_2_64_40G_base_20170222****",
        "InstanceType": "ecs.n1.medium",
        "SecurityGroupId": "sg-94q49****",
        "Password": "MytestPassword****",
        "IoOptimized": "optimized",
        "VSwitchId": "vsw-94vdv****",
        "VpcId": "vpc-949uz****",
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

-   Fn::Base64Encode
-   Fn::GetAtt
-   Fn::Join
-   Fn::Select
-   Ref

## Fn::Split

内部函数Fn::Split通过指定分隔符对字符串进行切片，并返回所有切片组成的列表。

声明

```
"Fn::Split": ["delim",  "original_string"]         
```

参数

-   `delim`：分隔符，例如：半角逗号（,）、半角分号（;）、换行符（\\n）、缩进（\\t）等。
-   `original_string`：将要被切片的字符串。

返回值

返回切片后所有字符串组成的列表。

示例

-   如果数据元列表是一个数组：

    ```
    {"Fn::Split": [";", "foo; bar; achoo"]}
    ```

    返回：`["foo", " bar", "achoo "]`。

-   使用Fn::Split对InstanceIds进行切片：

    ```
    {
      "Parameters": {
        "InstanceIds": {
          "Type": "String",
          "Default": "instane1_id,instance2_id,instance2_id"
        }
      },
      "Resources": {
        "resourceID": {
          "Type": "ALIYUN::SLB::BackendServerAttachment",
          "Properties": {
            "BackendServerList": {
              "Fn::Split": [
                ",",
                {
                  "Ref": "InstanceIds"
                }
              ]
            }
          }
        }
      }
    }
    ```


支持的函数

-   Fn::Base64Encode
-   Fn::FindInMap
-   Fn::GetAtt
-   Fn::Join
-   Fn::Select
-   Fn::Replace
-   Fn::GetAZs
-   Fn::If
-   Ref

## Fn::Equals

比较两个值是否相等。如果两个值相等，则返回true；如果不相等，则返回false。

声明

```
{"Fn::Equals": ["value_1", "value_2"]}      
```

参数

`value`：要比较的任意类型的值。

返回值

true或false。

示例

在Conditions中使用Fn::Equals定义条件。

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "EnvType": {
      "Default": "pre",
      "Type": "String"
    }
  },
  "Conditions": {
    "TestEqualsCond": {
      "Fn::Equals": [
        "prod",
        {"Ref": "EnvType"}
      ]
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

## Fn::And

代表AND运算符，最少包含两个条件。如果所有指定条件计算为true，则返回true；如果任意条件计算为false，则返回false。

声明

```
{"Fn::And": ["condition", {...}]} 
```

参数

`condition`：计算为true或false的条件。

返回值

true或false。

示例

在Conditions中使用Fn::And定义一个条件：

```
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

## Fn::Or

代表OR运算符，最少包含两个条件。如果任意一个指定条件计算为true，则返回true；如果所有条件都计算为false，则返回false。

声明

```
{"Fn::Or": ["condition", {...}]}
```

参数

`condition`：计算为true或false的条件。

返回值

true或false。

示例

在Conditions中使用Fn::Or定义一个条件。

```
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
    "TestOrCond": {"Fn::Or": ["TestEqualsCond", {"Fn::Equals": ["pre", {"Ref": "EnvType"}]}]}
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

## Fn::Not

代表NOT运算符。对计算为false的条件，返回true；对计算为true的条件，返回false。

声明

```
{"Fn::Not": "condition"}
```

参数

`condition`：计算为true或false的条件。

返回值

true或false。

示例

在Conditions中使用Fn::Not定义一个条件。

```
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

## Fn::If

如果指定的条件计算为true，则返回一个值；如果指定的条件计算为false，则返回另一个值。在模板Resources和Outputs属性值中支持Fn::If内部函数。您可以使用`ALIYUN::NoValue`伪参数作为返回值来删除相应的属性。

声明

```
{"Fn::If": ["condition_name", "value_if_true", "value_if_false"]}            
```

参数

-   `condition_name`：Conditions中条件对应的条件名称。通过条件名称引用条件。
-   `value_if_true`：当指定的条件计算为true时，返回此值。
-   `value_if_false`：当指定的条件计算为false时，返回此值。

示例

根据输入的参数，确定是否创建数据盘。

```
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
                "VpcId":"vpc-2zew9pxh2yirtzqxd****",
                "SystemDiskCategory":"cloud_efficiency",
                "SecurityGroupId":"sg-2zece6wcqriejf1v****",
                "SystemDiskSize":40,
                "ImageId":"centos_6_8_64_40G_base_20170222****",
                "IoOptimized":"optimized",
                "VSwitchId":"vsw-2zed9txvy7h2srqo6****",
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

## Fn::Length

内部函数Fn::Length返回对象的长度。

声明

```
{"Fn::Length" : Object}
```

参数

Object：需要计算长度的对象。支持字符串、列表和字典三种类型。

返回值

该对象的长度，整型。

示例

-   ```
{"Fn::Length": {"key1": "v1", "key2": "v2"}}
```

    返回：`2`

-   ```
{"Fn::Length": [1, 2, 3]}
```

    返回：`3`

-   ```
{"Fn::Length": "length"}
```

    返回：`6`


## Fn::ListMerge

合并多个列表为一个列表。

声明

```
{"Fn::ListMerge": [["list_1_item_1", "list_1_imte_2", ...], ["list_2_item_1", "list_2_imte_2", ...]]}
```

参数

-   `["list_1_item_1", "list_1_imte_2", ...]`：将要合并的第一个列表。
-   `["list_2_item_1", "list_2_imte_2", ...]`：将要和第一个列表合并的列表。

示例

把两个ECS组挂载到同一个负载均衡实例上。

```
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
        "ImageId" : "m-2ze9uqi7wo61hwep****",
        "InstanceType": "ecs.t1.small",
        "SecurityGroupId": "sg-2ze8yxgempcdsq3i****",
        "MaxAmount": 1,
        "MinAmount": 1
      }
    },
    "BackendServer2": {
      "Type": "ALIYUN::ECS::InstanceGroup",
      "Properties": {
        "ImageId" : "m-2ze9uqi7wo61hwep****",
        "InstanceType": "ecs.t1.small",
        "SecurityGroupId": "sg-2ze8yxgempcdsq3i****",
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

-   Fn::Base64Encode
-   Fn::GetAtt
-   Fn::Join
-   Fn::Select
-   Ref
-   Fn::If

## Fn::GetJsonValue

解析JSON字符串，获取指定的Key在第一层所对应的值。

声明

```
{"Fn::GetJsonValue": ["key", "json_string"]}       
```

参数

-   `key`：键值。
-   `json_string`：指定的需要解析的JSON字符串。

示例

WebServer2从WebServer实例执行完UserData返回的JSON字符串中，获取对应的值。

```
{
  "ROSTemplateFormatVersion" : "2015-09-01",
  "Resources" : {
    "WebServer": {
      "Type": "ALIYUN::ECS::Instance",
      "Properties": {
        "ImageId" : "m-2ze45uwova5fedlu****",
        "InstanceType": "ecs.n1.medium",
        "SecurityGroupId": "sg-2ze7pxymaix640qr****",
        "Password": "Wenqiao****",
        "IoOptimized": "optimized",
        "VSwitchId": "vsw-2zei67xd9nhcqxzec****",
        "VpcId": "vpc-2zevx9ios1rszqv0a****",
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
         "PrivateIpAddress": "192.168.XX.XX",
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
        "ImageId" : "m-2ze45uwova5fedlu****",
        "InstanceType": "ecs.n1.medium",
        "SecurityGroupId": "sg-2ze7pxymaix640qr****",
        "Password": "Wenqiao****",
        "IoOptimized": "optimized",
        "VSwitchId": "vsw-2zei67xd9nhcqxzec****",
        "VpcId": "vpc-2zevx9ios1rszqv0a****",
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
         "PrivateIpAddress": "192.168.XX.XX",
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

-   Fn::Base64Encode
-   Fn::GetAtt
-   Fn::Join
-   Fn::Select
-   Ref
-   Fn::Join
-   Fn::If

## Fn::MergeMapToList

将多个Mapping合并成一个以Mapping为元素的列表。

声明

```
{"Fn::MergeMapToList": [{"key_1": ["key_1_item_1", "key_1_item_2", ...]}, {"key_2":["key_2_item_1", "key_2_item_2", ...]}, ... ]}
```

参数

-   `{"key_1": ["key_1_item_1", "key_1_item_2", ...]}`：将要合并的第一个Mapping。`"key_1"`所对应的值必须是一个列表。`"key_1"`将是合并后的列表元素中，每个Mapping的一个键。其对应的值在第一个Mapping中将是`"key_1_item_1"`，在第二个Mapping中是 `"key_1_item_2"`，以此类推。最终合并的列表长度是所有将要合并的参数Mapping中，`"key_x"` 所对应的列表中最长的长度。如果有的`"key_y"`所对应的列表长度比较短，会重复此列表的最后一个元素，使列表长度都达到最长。
-   `{"key_2": ["key_2_item_1", "key_2_item_2", ...]}`：将要合并的第二个Mapping。`"key_2"`所对应的值必须是一个列表。`"key_2"`将是合并后的列表元素中每个Mapping的一个键。其对应的值在第一个Mapping中将是`"key_2_item_1"`，在第二个Mapping中是`"key_2_item_2"`，以此类推。

示例

-   合并三个Mapping，每个Mapping中键值对应的列表长度一致：

    ```
    {
       "Fn::MergeMapToList": [
          {"key_1": ["kye_1_item_1", "kye_1_item_2"]},
          {"key_2": ["kye_2_item_1", "kye_2_item_2"]},
          {"key_3": ["kye_3_item_1", "kye_3_item_2"]}
       ]
    }     
    ```

    合并结果如下：

    ```
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

    ```
    {
       "Fn::MergeMapToList": [
          {"key_1": ["kye_1_item_1", "kye_1_item_2"]},
          {"key_2": ["kye_2_item_1", "kye_2_item_2", "key_2_item_3"]},
          {"key_3": ["kye_3_item_1", "kye_3_item_2"]}
       ]
    }   
    ```

    合并结果如下：

    ```
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

-   以下模板示例中，把WebServer中创建的所有实例，都加入到一个负载均衡的虚拟服务器组中。

    ```
    {
        "ROSTemplateFormatVersion": "2015-09-01",
        "Resources": {
            "WebServer": {
              "Type": "ALIYUN::ECS::InstanceGroupClone",
              "Properties": {
                  "SourceInstanceId": "i-xxxxx",
                   "Password": "Hello****",
                   "MinAmount": 1,
                   "MaxAmount": 1
              }
            },
            "CreateVServerGroup": {
                "Type": "ALIYUN::SLB::VServerGroup",
                "Properties": {
                    "LoadBalancerId": "lb-****",
                    "VServerGroupName": "VServerGroup-****",
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

-   Fn::Base64Encode
-   Fn::GetAtt
-   Fn::Join
-   Fn::Select
-   Ref
-   Fn::Join
-   Fn::If
-   Fn::ListMerge
-   Fn::GetJsonValue

## Fn::Avg

内部函数Fn::Avg对一组数求平均值。

声明

```
{"Fn::Avg": [ndigits, [number1, number2, ... ]]}
```

参数

-   `ndigits`：平均值保留几位小数，必须为整数。
-   `[ number1, number2, ... ]`：一组用来求取平均值的数字。组内每个元素可以是数字或能转换成数字的字符串。

返回值

给定一组数字的平均值。

示例

```
{ "Fn::Avg": [ 1, [1, 2, 6.0] ] } 
{ "Fn::Avg": [ 1, ['1', '2', '6.0'] ] }
```

返回：3.0。

支持的函数

-   Fn::GetAtt
-   Ref

## Fn::SelectMapList

内部函数Fn::SelectMapList返回一个由map中元素构成的列表。

声明

```
{"Fn::SelectMapList": ["key2", [{"key1": "value1-1", "key3": "value1-3"}, {"key1": "value2-1", "key2": "value2-2"}, {"key1": "value3-1", "key2": "value3-2"}, ...] ] }
```

参数

-   `key2`：在map中查询的key。
-   `[{ "key1": "value1-1", "key3": "value1-3" }, ... ]`：由map组成的List。

返回值

对map\_list中的每个map，取出key对应的值，合并成一个列表。

示例

```
{
 "Fn::SelectMapList": [
   "key2",
   [
      {"key1": "value1-1", "key3": "value1-3"},
      {"key1": "value2-1", "key2": "value2-2"},
      {"key1": "value3-1", "key2": "value3-2"}
   ]
 ]
}
```

返回：`["value2-2","value3-2"]`。

## Fn::Add

内部函数Fn::Add对参数进行求和。

声明

```
{"Fn::Add": [{"Product": "ROS"}, {"Fn": "Add"}]}
```

参数

-   参数为一个列表。
-   列表内元素可以是数字、列表、字典，但是所有元素必须是同一类型，至少2个元素。

返回值

如果是数字类型，对参数进行求和；如果是列表类型，对参数进行拼接；如果是字典类型，对参数进行合并，key相同的情况下，后面的覆盖前面的。

示例

```
{
 "Fn::Add": [
   {"Product": "ROS"},
   {"Fn": "Add"}
 ]
}
```

返回：`{"Fn":"Add","Product":"ROS"}`。

## Fn::Calculate

内部函数Fn::Calculate对字符串形式的表达式进行计算。

声明

```
 {"Fn::Calculate" : [expression, ndigits, [<number1>, <number2>, ... ]]}
```

参数

-   `expression`：字符串形式的表达式。
-   `ndigits`：取值：0或正整数，表示保留小数的位数，如果表达式中不包含浮点数，则此参数不生效。
-   `[<number0>, <number1>, <number2>, ... ]`：非必需参数。expression中可以定义\{n\}，n为列表中某个number的索引，在计算表达式时用number的值替换\{n\}。

返回值

表达式的计算结果。

示例

```
{"Fn::Calculate": ["(2+3)/2*3-1", 1]}  
{"Fn::Calculate": ["(2.0+3)/2*3-1", 1]}
{"Fn::Calculate": ["({1}+3)/2*3-1", 1, [3, 5, 6]]}
```

返回：

```
6
6.5
11
```

## Fn::Sub

内部函数Fn::Sub用于将输入字符串中的变量替换为您指定的值。

声明

```
{ "Fn::Sub": [ String, { Var1Name: Var1Value, Var2Name: Var2Value, ... } ] }
```

参数

-   String

    一个能进行变量替换字符串，ROS在运行时会将这些变量替换为指定值。以 $\{VarName\} 形式编写变量，变量可以是模板参数、伪参数、资源逻辑ID、资源属性或键值映射中的变量等。如果您仅指定模板参数、伪参数、资源逻辑ID和资源属性，则不需要指定键值映射。

    如果您指定模板参数名、伪参数或资源逻辑ID（如 $\{MyParameter\}），则ROS返回的值与您使用`Ref`内部函数时返回的值相同。如果您指定资源属性（如$\{MyInstance.InstanceId\}），则ROS返回的值与您使用`Fn::GetAtt`内部函数时返回的值相同。

    要按字面书写美元符号（$）和大括号（\{ \}），请在左大括号后面添加感叹号（!），如`${!Literal}`。ROS将该文本解析为`${Literal}`。

-   VarName

    String参数中包含的变量的名称。

-   VarValue

    ROS在运行时要将关联的变量名称替换为的值。


如果不需要使用键值映射，可使用以下声明方式：

```
{ "Fn::Sub": String }
```

返回值

ROS返回原始字符串，并替换所有变量的值。

示例

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "VpcName": {
      "Type": "String",
      "Default": "vpc"
    }
  },
  "Resources": {
    "Vpc": {
      "Type": "ALIYUN::ECS::VPC",
      "Properties": {
        "VpcName": {
          "Ref": "VpcName"
        },
        "CidrBlock": "10.0.XX.XX"
      }
    }
  },
  "Outputs": {
    "Pseudo": {
      "Value": {
        "Fn::Sub": [
          "Var1: ${Var1}, Var2: ${Var2}, StackName: ${ALIYUN::StackName}, Region: ${ALIYUN::Region}",
          {
            "Var1": "Var1Value",
            "Var2": "Var2Value"
          }
        ]
      }
    },
    "VpcId": {
      "Value": {
        "Fn::Sub": "资源的返回值: ${Vpc.VpcId}, 资源ID: ${Vpc}"
      }
    }
  }
}
```

返回

```
Var1: Var1Value, Var2: Var2Value, StackName: SubTest, Region: cn-hangzhou
资源的返回值: vpc-bp11eu7avmtvr37hl****, 资源ID: vpc-bp11eu7avmtvr37hl****
```

## Fn::Max

内部函数Fn::Max用于获取由数字组成的列表中的最大数字。

声明

```
{"Fn::Max": [Number1, Number2, Number3, ...]}
```

返回值

列表中的最大数字。

示例

```
{"Fn::Max": [1.1, 2, 3]}
```

返回

```
3
```

## Fn::Min

内部函数Fn::Min用于获取由数字组成的列表中的最小数字。

声明

```
{"Fn::Min": [Number1, Number2, Number3, ...]}
```

返回值

列表中的最小数字。

示例

```
{"Fn::Min": [1.1, 2, 3]}
```

返回

```
1.1
```

## Fn::GetStackOutput

内部函数Fn::GetStackOutput用于获取指定资源栈的输出。

声明

```
{"Fn::GetStackOutput": [Stack, OutputName, RegionId]}
```

参数

-   `Stack`：必选，String类型。资源栈的名称或ID。
-   `OutputName`：必选，String类型。资源栈某一输出名。
-   `RegionId`：可选，String类型。资源栈所属地域，若不指定，则与调用资源栈相同。

返回值

资源栈Stack的名为OutputName的输出，类型依赖于输出值，不确定。若符合如下条件则返回空值：

-   传递的参数中有一个值为空值。
-   Stack不存在（含已删除）。
-   Stack运行中或删除失败。
-   Output不存在。

限制

-   单向引用：A-\>B-\>C（允许），A-\>B-\>A（不允许），A-\>A（不允许）。
-   引用最大长度为3：A-\>B-\>C（允许），A-\>B-\>C-\>D（不允许）。

示例

```
{"Fn::GetStackOutput": ["4a6c9851-3b0f-4f5f-b4ca-a14bf691****", "InstanceId"]}
```

## Fn::Jq

内部函数Fn::Jq用于支持Jq功能。Jq功能详情请参见[Jq文档](https://stedolan.github.io/jq/manual/)。

声明

```
{"Fn::Jq": [method,script,object]}
```

参数

-   `method`：必选，字符串。取值：
    -   First：符合条件的第一个值。
    -   All：符合条件的所有值。
-   `script`：必选，字符串。Jq脚本。
-   `object`：必选，JSON字符串。

返回值

选定的字符串。

示例

-   使用过滤器`.test`过滤出的值取第一个。当给定一个JSON字符串作为输入时，它将在键`test`处产生值；如果值不存在，则为null。

    ```
    {"Fn::Jq":["First",".test","{\"test\":\"test\"}"]}
    ```

    返回

    ```
    "test"
    ```

-   使用过滤器`.parameters[]`过滤出的内容，再次通过新的过滤器进行过滤。它们之间通过竖线（\|）进行连接。给定一个JSON字符串作为输入时，它将在键`.parameters[] | {\"param_name\": .name, \"param_type\":.type}`处产生值；如果值不存在，则为null。

    ```
    {
        "Fn::Jq": [
            "All",
            ".parameters[] | {\"param_name\": .name, \"param_type\":.type}",
            {
                "changeSet": {
                    "items": [
                    ],
                    "kind": "git"
                },
                "id": "2013-12-27_00-09-37",
                "parameters": [
                    {
                        "name": "PKG_TAG_NAME",
                        "value": "trunk"
                    },
                    {
                        "name": "GIT_COMMIT",
                        "value": "master"
                    },
                    {
                        "name": "TRIGGERED_JOB",
                        "value": "trunk-buildall"
                    }]
            }]
    }
    ```

    返回

    ```
    "[{u'param_name': u'PKG_TAG_NAME', u'param_type': None}, {u'param_name': u'GIT_COMMIT', u'param_type': None}, {u'param_name': u'TRIGGERED_JOB', u'param_type': None}]"
    ```


