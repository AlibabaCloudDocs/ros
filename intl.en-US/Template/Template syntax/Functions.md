# Functions

Resource Orchestration Service \(ROS\) provides several built-in functions to help you manage stacks. You can use built-in functions to define Resources and Outputs.

You can use the following built-in functions in templates: Fn::Str, Fn::Base64Encode, Fn::Base64Decode, Fn::FindInMap, Fn::GetAtt, Fn::Join, Fn::Sub, Fn::Select, Ref, Fn::GetAZs, Fn::Replace, Fn::Split, Fn::Equals, Fn::And, Fn::Or, Fn::Not, Fn::Index, Fn::If, Fn::Length, Fn::ListMerge, Fn::GetJsonValue, Fn::MergeMapToList, Fn::Avg, Fn::SelectMapList, Fn::Add, Fn::Calculate, Fn::Max, Fn::Min, Fn::GetStackOutput, and Fn::Jq.

## Fn::Str

The Fn::Str function is used to return the string representation of a value.

Declaration

```
"Fn::Str" : toString
```

Parameters

`toString`: the value of the Number or Integer type to be converted to a string.

Return value

The string representation of the value.

Examples

```
{"Fn::Str": 123456}
```

`"123456"` is returned in this example.

## Fn::Base64Encode

The Fn::Base64Encode function is used to return the Base64 representation of the input string.

Declaration

```
"Fn::Base64Encode": "stringToEncode"
```

Parameters

`stringToEncode`: the string to be encoded in Base64.

Return value

The Base64 representation of the input string.

Examples

```
{"Fn::Base64Encode": "string to encode"}
```

`c3RyaW5nIHRvIGVuY29kZQ==` is returned in this example.

## Fn::Base64Decode

The Fn::Base64Decode function is used to return a string decoded from a Base64-encoded string.

Declaration

```
{"Fn::Base64Decode": "stringToEncode"}
```

Parameters

`stringToDecode`: the string decoded from the Base64-encoded string.

Return value

The string decoded from the Base64-encoded string.

Examples

```
{"Fn::Base64Decode": "c3RyaW5nIHRvIGVuY29kZQ=="}
```

`string to encode` is returned in this example.

## Fn::FindInMap

The Fn::FindInMap function is used to return the values based on keys in a two-level mapping that is declared in the Mappings section.

Declaration

```
"Fn::FindInMap": ["MapName", "TopLevelKey", "SecondLevelKey"]
```

Parameters

-   `MapName`: the ID of a mapping declared in the Mappings section.
-   `TopLevelKey`: the top-level key name. The value is a list of key-value pairs.
-   `SecondLevelKey`: the second-level key name. The value is a string or a number.

Return value

The value that is assigned to the SecondLevelKey parameter.

Examples

The ImageId property must be specified when you create a WebServer instance. The Mappings section describes the ImageId mappings by region. The Parameters section describes the regions that must be specified by template users. Fn::FindInMap finds the corresponding ImageId mapping in RegionMap based on the region specified by a user, and then finds the corresponding ImageId in the mapping.

-   The MapName value can be customized by the user. `"RegionMap"` is used in this example.
-   TopLevelKey is set to the region where the stack is created, which is `{ "Ref" : "regionParam" }` in this example.
-   SecondLevelKey is set to the required architecture, which is `"32"` in this example.

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "regionParam": {
      "Description": "The region where the ECS instance is created",
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

Supported functions

-   Fn::FindInMap
-   Ref

## Fn::GetAtt

The Fn::GetAtt function is used to return the value of a property from a resource in a template.

Declaration

```
"Fn::GetAtt": ["resourceID", "attributeName"]
```

Parameters

-   `resourceID`: the ID of the resource.
-   `attributeName`: the name of the resource property.

Return value

The value of the resource property.

Examples

The ImageId property of MyEcsInstance is returned in this example.

```
{"Fn::GetAtt" : ["MyEcsInstance" , "ImageID"]}
```

## Fn::Join

The Fn::Join function is used to append a set of values into a single value that is separated by a specified delimiter.

**Note:** Both Fn::Sub and Fn::Join can be used to combine strings. Fn::Join can combine only strings into a single string. Fn::Sub can combine strings and numbers into a single string. For your convenience, we recommend that you use Fn::Sub.

Declaration

```
{"Fn::Join": ["delimiter", ["string1", "string2", ... ]]}
```

Parameters

-   `delimiter`: the value used to divide the string. The delimiter value can be left blank so that all the values are directly combined.
-   `[ "string1", "string2", ... ]`: the list of values that are combined into a string.

Return value

The combined string.

Examples

```
{"Fn::Join": [ ",", ["a", "b", "c"]]}
```

`"a,b,c"` is returned in this example.

Supported functions

-   Fn::Base64Encode
-   Fn::GetAtt
-   Fn::Join
-   Fn::Select
-   Ref

## Fn::Sub

The Fn::Sub function is used to substitute variables in an input string with values that you specify.

Declaration

```
{ "Fn::Sub": [ String, { Var1Name: Var1Value, Var2Name: Var2Value, ... } ] }
```

Parameters

-   String

    A string with variables that are substituted with specified values at runtime. Write variables in the `${VarName}` format. Variables can be template parameters, pseudo parameters, logical resource IDs, resource properties, or variables in key-value mappings. If you specify only template parameters, pseudo parameters, resource logical IDs, and resource properties, you do not need to specify variables in key-value mappings.

    If you specify template parameters, pseudo parameters, or resource logical IDs such as `${MyParameter}`, ROS returns the same values as if you used the `Ref` built-in function. If you specify resource properties such as `${MyInstance.InstanceId}`, ROS returns the same values as if you used the `Fn::GetAtt` built-in function.

    To use the combination of a dollar sign \($\) and braces \(\{\}\) as normal characters without being escaped, add an exclamation point \(!\) after the open brace, such as `${! Literal}`. ROS resolves this text as `${Literal}`.

-   VarName

    The name of a variable that you included in the String parameter.

-   VarValue

    The value that ROS substitutes for the associated variable name at runtime.


If key-value mappings are not required, you can use the following declaration:

```
{ "Fn::Sub": String }
```

Return value

ROS returns the original string and substitutes the values of all variables.

Examples

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
        "Fn::Sub": "Return value of the resource: ${Vpc.VpcId}. Resource ID: ${Vpc}".
      }
    }
  }
}
```

In this example, the following values are returned:

```
Var1: Var1Value, Var2: Var2Value, StackName: SubTest, Region: cn-hangzhou
Return value of the resource: vpc-bp11eu7avmtvr37hl****. Resource ID: vpc-bp11eu7avmtvr37hl****.
```

## Fn::Select

The Fn::Select function is used to return data from a list or a dictionary based on an index.

Declaration

-   The following examples assume that the list of data elements is an array:
    -   Obtain a single data element based on an index:

        ```
        {"Fn::Select": ["index", ["value1", "value2", ... ]]}     
        ```

    -   Obtain multiple data elements:

        ```
        {"Fn::Select": ["start:stop", ["value1", "value2", ... ]]}
        ```

        ```
        {"Fn::Select": ["start:stop:step", ["value1", "value2", ... ]]}
        ```

-   The following example assumes that the dictionary of data elements is a mapping table:

    ```
    {"Fn::Select": ["key", {"key1": "value1", "key2": "value2", ... }]}
    ```


Parameters

-   `index`: the index of the object data element that you want to retrieve. The index is an integer ranging from 0 to N-1 or from -N to -1. N indicates the number of elements in the array. The negative sign indicates that the elements are read from right to left. If the corresponding value of the index cannot be found, the system returns an empty string.
-   `start`, `stop`, and `step`: The function obtains data elements from the list based on the specified start and end positions. If the step is specified, the function obtains a data element and returns a list every step-1 elements.
    -   `start:stop`: the values of start and stop are both the same as the index. By default, the value of start is set to 0, and the value of stop is set to N. The function returns a list of data elements from position start+1 to stop in the list. If the values of start and stop are both out of the value range, an empty list is returned.
    -   `start:stop:step`: By default, the value of step is set to 1. If the step value is a negative number, the index of the element represented by start must be greater than that represented by stop. The function obtains an element and returns a list every step-1 elements from position start to stop+1.
-   `key`: a key in the dictionary. The value of the key is returned. If the key does not exist in the dictionary, an empty string is returned.

Return value

The selected data.

Examples

-   Values are obtained from a list or an array in the following examples:
    -   ```
{"Fn::Select": ["1", ["apples", "grapes", "oranges", "mangoes"]]}        
```

        `"grapes"` is returned in this example.

    -   ```
{"Fn::Select": ["1:3", [1, 2, 3, 4, 5]]}
```

        `[2, 3]` is returned in this example.

    -   ```
{"Fn::Select": ["::2", [1, 2, 3, 4, 5]]}
```

        `[1, 3, 5]` is returned in this example.

    -   ```
{"Fn::Select": ["5:0:-2", [1, 2, 3, 4, 5]]}
```

        `[5, 3]` is returned in this example.

-   The value of a key is obtained from a dictionary in the following example:

    ```
    {"Fn::Select": ["key1", {"key1": "grapes", "key2": "mangoes"}]}     
    ```

    `"grapes"` is returned in this example.

-   The following example assumes that the list of data elements is a comma-delimited list:

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

    `10.0.0.1` is returned in this example.


Supported functions

For the Fn::Select index value, you can use the Ref function.

For the Fn::Select list of object data elements, you can use the following functions:

-   Fn::Base64Encode
-   Fn::FindInMap
-   Fn::GetAtt
-   Fn::Join
-   Fn::Select
-   Ref

## Ref

The Ref function is used to return the value of a specified parameter or resource.

If the specified parameter is a resource ID, the value of the resource is returned. Otherwise, the system returns the value of the specified parameter.

Declaration

```
"Ref": "logicalName"
```

Parameters

`logicalName`: the logical name of the resource or parameter that you want to reference.

Return value

The value of the resource or parameter.

Examples

The Ref function is used in the following example to specify regionParam as the region parameter for RegionMap of WebServer:

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "regionParam": {
      "Description": "The region where the ECS instance is created",
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

Supported functions

When you use the Ref function, you cannot use other functions in it at the same time. You must specify a string value for the resource logical ID.

## Fn::GetAZs

The Fn::GetAZs function is used to return a list of one or more zones for a specified region.

**Note:** This function is applicable only to ECS and VPC resources.

Declaration

```
"Fn::GetAZs": "region"    
```

Parameters

`region`: the ID of the region.

Return value

The list of zones within the specified region.

Examples

The following example demonstrates how to create an ECS instance in the first zone of a specified region:

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

Supported functions

-   Fn::Base64Encode
-   Fn::FindInMap
-   Fn::GetAtt
-   Fn::Join
-   Fn::Select
-   Ref

## Fn::Replace

The Fn::Replace function is used to replace a specified substring contained in a string with a new substring.

Declaration

```
{"Fn::Replace": [{"object_key": "object_value"}, "object_string"]} 
```

Parameters

-   `object_key`: the substring to be replaced.
-   `object_value`: the new substring to replace the previous substring.
-   `object_string`: the string that contains the replaced substring specified by the `object_key` parameter.

Return value

The string after replacement.

Examples

The following example demonstrates how to replace "print" with "echo" in the specified script:

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

-   Fn::Base64Encode
-   Fn::GetAtt
-   Fn::Join
-   Fn::Select
-   Ref

## Fn::Split

The Fn::Split function is used to split a string into a list of values separated by a specified delimiter and return the list.

Declaration

```
"Fn::Split": ["delim",  "original_string"]         
```

Parameters

-   `delim`: the specified delimiter, which can contain commas \(,\), semicolons \(;\), line feeds \(\\n\), and indents \(\\t\).
-   `original_string`: the string to be split.

Return value

A list of string values.

Examples

-   The following example assumes that the list of data elements is an array:

    ```
    {"Fn::Split": [";", "foo; bar; achoo"]}
    ```

    `["foo", " bar", "achoo "]` is returned in this example.

-   Fn::Split is used in the following example to split InstanceIds:

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


Supported functions

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

The Fn::Equals function is used to compare whether two values are equal. If the two values are equal, true is returned. If the two values are not equal, false is returned.

Declaration

```
{"Fn::Equals": ["value_1", "value_2"]}      
```

Parameters

`value`: the values to be compared.

Return value

true or false.

Examples

Fn::Equals is used in the following example to define a condition in the Conditions section:

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

Supported functions

-   Fn::Or
-   Fn::Not
-   Fn::Equals
-   Fn::FindInMap
-   Fn::And
-   Ref

## Fn::And

The Fn::And function is used to represent the AND operator, and must contain at least two conditions. If all the specified conditions are evaluated as true, true is returned. If any condition is evaluated as false, false is returned.

Declaration

```
{"Fn::And": ["condition", {...}]} 
```

Parameters

`condition`: the condition to be evaluated.

Return value

true or false.

Examples

Fn::And is used in the following example to define a condition in the Conditions section:

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

Supported functions

-   Fn::Or
-   Fn::Not
-   Fn::Equals
-   Fn::FindInMap
-   Fn::And
-   Ref

## Fn::Or

The Fn::Or function is used to represent the OR operator, and must contain at least two conditions. If any specified condition is evaluated as true, true is returned. If all the conditions are evaluated as false, false is returned.

Declaration

```
{"Fn::Or": ["condition", {...}]}
```

Parameters

`condition`: the condition to be evaluated.

Return value

true or false.

Examples

Fn::Or is used in the following example to define a condition in the Conditions section:

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

Supported functions

-   Fn::Or
-   Fn::Not
-   Fn::Equals
-   Fn::FindInMap
-   Fn::And
-   Ref

## Fn::Not

The Fn::Not function is used to represent the NOT operator. If a condition is evaluated as false, true is returned. If a condition is evaluated as true, false is returned.

Declaration

```
{"Fn::Not": "condition"}
```

Parameters

`condition`: the condition to be evaluated.

Return value

true or false.

Examples

Fn::Not is used in the following example to define a condition in the Conditions section:

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

Supported functions

-   Fn::Or
-   Fn::Not
-   Fn::Equals
-   Fn::FindInMap
-   Fn::And
-   Ref

## Fn::Index

The Fn::Index function is used to find the index of an element in a list.

Declaration

```
{"Fn::Index": ["item", [ ... ]]}
```

Parameters

`item`: the element in the list.

Return value

The index of the element in the list. If the element does not exist, an empty value is returned.

Examples

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "ZoneIds": {
      "Type": "Json",
      "Default": ["cn-beijing-a", "cn-beijing-b", "cn-beijing-f"]
    },
    "ZoneId": {
      "Type": "String",
      "Default": "cn-beijing-b"
    }
  },
  "Outputs": {
    "Index": {
      "Value": {
        "Fn::Index": [
          { "Ref": "ZoneId" },
          { "Ref": "ZoneIds" }
        ]
      }
    }
  }
}
```

## Fn::If

The Fn::If function is used to return one of two possible values. If a specified condition is evaluated as true, one value is returned. If the specified condition is evaluated as false, the other value is returned. The property values of Resources and Outputs in templates support the Fn::If function. You can use the `ALIYUN::NoValue` pseudo parameter as the return value to delete the corresponding property.

Declaration

```
{"Fn::If": ["condition_name", "value_if_true", "value_if_false"]}            
```

Parameters

-   `condition_name`: the name of the condition in the Conditions section. A condition is referenced by using the condition name.
-   `value_if_true`: If the specified condition is evaluated as true, this value is returned.
-   `value_if_false`: If the specified condition is evaluated as false, this value is returned.

Examples

The following example demonstrates how to determine whether to create a data disk based on input parameters:

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

Supported functions

-   Fn::Or
-   Fn::Not
-   Fn::Equals
-   Fn::FindInMap
-   Fn::And
-   Ref

## Fn::Length

The Fn::Length function is used to return the number of the elements inside an object.

Declaration

```
{"Fn::Length" : Object}
```

Parameters

Object: the object whose length is to be calculated. The String, List, and Dictionary types are supported.

Return value

The number of elements, which is an integer.

Examples

-   ```
{"Fn::Length": {"key1": "v1", "key2": "v2"}}
```

    `2` is returned in this example.

-   ```
{"Fn::Length": [1, 2, 3]}
```

    `3` is returned in this example.

-   ```
{"Fn::Length": "length"}
```

    `6` is returned in this example.


## Fn::ListMerge

The Fn::ListMerge function is used to merge multiple lists into one list.

Declaration

```
{"Fn::ListMerge": [["list_1_item_1", "list_1_imte_2", ...], ["list_2_item_1", "list_2_imte_2", ...]]}
```

Parameters

-   `["list_1_item_1", "list_1_imte_2", ...]`: the first list to merge.
-   `["list_2_item_1", "list_2_imte_2", ...]`: the second list to merge into the first list.

Examples

The following example demonstrates how to attach two ECS instance groups to a Server Load Balancer \(SLB\) instance:

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

Supported functions

-   Fn::Base64Encode
-   Fn::GetAtt
-   Fn::Join
-   Fn::Select
-   Ref
-   Fn::If

## Fn::GetJsonValue

The Fn::GetJsonValue function is used to resolve a JSON string and obtain its key value from the first layer.

Declaration

```
{"Fn::GetJsonValue": ["key", "json_string"]}       
```

Parameters

-   `key`: the key value.
-   `json_string`: the specified JSON string to be resolved.

Examples

In the following example, the WebServer instance executes UserData and a JSON string is returned. Then, the WebServer2 instance obtains the corresponding key value from the string.

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
             "#! /bin/sh\n",
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
             "#! /bin/sh\n",
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

Supported functions

-   Fn::Base64Encode
-   Fn::GetAtt
-   Fn::Join
-   Fn::Select
-   Ref
-   Fn::Join
-   Fn::If

## Fn::MergeMapToList

The Fn::MergeMapToList function is used to merge multiple mappings into a list of mapping elements.

Declaration

```
{"Fn::MergeMapToList": [{"key_1": ["key_1_item_1", "key_1_item_2", ...]}, {"key_2":["key_2_item_1", "key_2_item_2", ...]}, ... ]}
```

Parameters

-   `{"key_1": ["key_1_item_1", "key_1_item_2", ...]}`: the first mapping to merge. The `" key_1"` value must be a list. `" key_1"` is the key for each mapping in the list of merged mappings. The "key\_1" value is `"key_1_item_1"` for the first merged mapping and `"key_1_item_2"` for the second merged mapping. All values follow the same format. The length of the final list of merged mappings is the length of the longest list `"key_x"` from all mappings to be merged. If a `"key_y"` list is shorter, the last element of the list is repeated until the list is the longest.
-   `{"key_2": ["key_2_item_1", "key_2_item_2", ...]}`: the second mapping to merge into the first mapping. The `" key_2"` value must be a list. `" key_2"` is the key for each mapping in the merged list. The "key\_2" value is `"key_2_item_1"` for the first merged mapping and `"key_2_item_2"` for the second merged mapping. All values follow the same format.

Examples

-   The following example demonstrates how to merge three mappings. The length of the list corresponding to the key value in each mapping is the same.

    ```
    {
       "Fn::MergeMapToList": [
          {"key_1": ["kye_1_item_1", "kye_1_item_2"]},
          {"key_2": ["kye_2_item_1", "kye_2_item_2"]},
          {"key_3": ["kye_3_item_1", "kye_3_item_2"]}
       ]
    }     
    ```

    The following code shows the merged result:

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

-   In the following example, the length of the list corresponding to the key value in each mapping varies.

    ```
    {
       "Fn::MergeMapToList": [
          {"key_1": ["kye_1_item_1", "kye_1_item_2"]},
          {"key_2": ["kye_2_item_1", "kye_2_item_2", "key_2_item_3"]},
          {"key_3": ["kye_3_item_1", "kye_3_item_2"]}
       ]
    }   
    ```

    The following code shows the merged result:

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

-   In the following template example, all instances created in WebServer are added to the vServer group of an SLB instance:

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


Supported functions

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

The Fn::Avg function is used to return the average value of a set of numbers.

Declaration

```
{"Fn::Avg": [ndigits, [number1, number2, ... ]]}
```

Parameters

-   `ndigits`: the number of decimal places to display. This parameter value must be an integer.
-   `[ number1, number2, ... ]`: the set of numbers for which the average value is calculated. Each element in the group must be a number or a string that can be converted into a number.

Return value

The average value of the set of numbers.

Examples

```
{ "Fn::Avg": [ 1, [1, 2, 6.0] ] } 
{ "Fn::Avg": [ 1, ['1', '2', '6.0'] ] }
```

3.0 is returned in this example.

Supported functions

-   Fn::GetAtt
-   Ref

## Fn::SelectMapList

The Fn::SelectMapList function is used to return a list of map elements.

Declaration

```
{"Fn::SelectMapList": ["key2", [{"key1": "value1-1", "key3": "value1-3"}, {"key1": "value2-1", "key2": "value2-2"}, {"key1": "value3-1", "key2": "value3-2"}, ...] ] }
```

Parameters

-   `key2`: the key to be queried in the map.
-   `[{ "key1": "value1-1", "key3": "value1-3" }, ... ]`: the list of maps.

Return value

A list of key values for all maps in the map list.

Examples

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

`["value2-2","value3-2"]` is returned in this example.

## Fn::Add

The Fn::Add function is used to sum the values of parameters.

Declaration

```
{"Fn::Add": [{"Product": "ROS"}, {"Fn": "Add"}]}
```

Parameters

-   The parameters must be arranged as a list.
-   The parameters in the list can be of the Number, List, or Dictionary type. All the parameters must be of the same type. The list must contain at least two parameters.

Return value

If the parameter values are numbers, sum the parameter values. If the parameter values are lists, concatenate the values. If the parameter values are dictionaries, merge the values, and overwrite the former parameter value with the latter one if the two parameters have the same key.

Examples

```
{
 "Fn::Add": [
   {"Product": "ROS"},
   {"Fn": "Add"}
 ]
}
```

`{"Fn":"Add","Product":"ROS"}` is returned in this example.

## Fn::Calculate

The Fn::Calculate function is used to calculate an expression of the String type.

Declaration

```
 {"Fn::Calculate" : [expression, ndigits, [<number1>, <number2>, ... ]]}
```

Parameters

-   `expression`: the expression of the String type.
-   `ndigits`: the number of decimal places to report. This parameter value must be 0 or a positive integer. This parameter takes effect only if the expression contains floating-point numbers.
-   `[<number0>, <number1>, <number2>, ... ]`: optional. You can define \{n\} in the expression. n indicates the index of a specific number. You can replace \{n\} with the number when the expression is being calculated.

Return value

The calculation result of the expression, which is of the Number type.

Examples

```
{"Fn::Calculate": ["(2+3)/2*3-1", 1]}  
{"Fn::Calculate": ["(2.0+3)/2*3-1", 1]}
{"Fn::Calculate": ["({1}+3)/2*3-1", 1, [3, 5, 6]]}
```

The following calculation results are returned:

```
5  
6.5
11
```

**Note:** For the quotient of integers, decimal places are not retained. Example: 5/2 = 2. Therefore, the return value of `{"Fn::Calculate": ["(2 + 3)/2 × 3 - 1", 1]}` is `5`.

## Fn::Max

The Fn::Max function is used to obtain the largest number in a list of numbers.

Declaration

```
{"Fn::Max": [Number1, Number2, Number3, ...]}
```

Return value

The largest number in the list.

Examples

```
{"Fn::Max": [1.1, 2, 3]}
```

In this example, the following value is returned:

```
3
```

## Fn::Min

The Fn::Min function is used to obtain the smallest number in a list of numbers.

Declaration

```
{"Fn::Min": [Number1, Number2, Number3, ...]}
```

Return value

The smallest number in the list.

Examples

```
{"Fn::Min": [1.1, 2, 3]}
```

In this example, the following value is returned:

```
1.1
```

## Fn::GetStackOutput

The Fn::GetStackOutput function is used to obtain an output of a specific stack.

Declaration

```
{"Fn::GetStackOutput": [Stack, OutputName, RegionId]}
```

Parameters

-   `Stack`: required. This parameter is of the String type. It indicates the name or ID of the stack.
-   `OutputName`: required. This parameter is of the String type. It indicates the name of an output of the stack.
-   `RegionId`: optional. This parameter is of the String type. It indicates the region of the stack. If this parameter is not specified, it is set to the region of the called stack.

Return value

The OutputName value of the called stack. The value type depends on the output value. Null is returned in the following cases:

-   One of the passed parameters is empty.
-   The specified stack does not exist or has been deleted.
-   The stack is running or fails to be deleted.
-   The output does not exist.

Limits

-   Only one-way reference is allowed. For example, A-\>B-\>C is allowed, but A-\>B-\>A or A-\>A is not allowed.
-   The maximum reference depth allowed is 3. For example, A-\>B-\>C is allowed, but A-\>B-\>C-\>D is not allowed.

Examples

```
{"Fn::GetStackOutput": ["4a6c9851-3b0f-4f5f-b4ca-a14bf691****", "InstanceId"]}
```

## Fn::Jq

The Fn::Jq function is used to support the Jq program. For more information about the Jq program, visit [jq Manual](https://stedolan.github.io/jq/manual/).

Declaration

```
{"Fn::Jq": [method,script,object]}
```

Parameters

-   `method`: required. This parameter is of the String type. Valid values:
    -   First: the first value that satisfies the condition.
    -   All: all values that satisfy the condition.
-   `script`: required. This parameter is of the String type. The Jq script.
-   `object`: required. The parameter value must be a JSON string.

Return value

The selected string.

Examples

-   In the following example, the function returns the first value produced by the `.test` filter. When a string in the JSON format is specified as the input, the filter produces the value at the `test` key. If the value does not exist, null is returned.

    ```
    {"Fn::Jq":["First",".test","{\"test\":\"test\"}"]}
    ```

    In this example, the following value is returned:

    ```
    "test"
    ```

-   In the following example, the output of the `.parameters[]` filter is passed through another filter. The two filters are separated by a vertical bar \(\|\). When a string in the JSON format is specified as the input, the filter produces the value at the `.parameters[] | {\"param_name\": .name, \"param_type\":.type}` key. If the value does not exist, null is returned.

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

    In this example, the following values are returned:

    ```
    "[{u'param_name': u'PKG_TAG_NAME', u'param_type': None}, {u'param_name': u'GIT_COMMIT', u'param_type': None}, {u'param_name': u'TRIGGERED_JOB', u'param_type': None}]"
    ```


