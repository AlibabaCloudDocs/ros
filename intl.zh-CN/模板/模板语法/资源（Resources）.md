# 资源（Resources）

资源（Resources）用于描述资源栈中每个资源的属性和资源之间的依赖关系。一个资源可以被其它资源和Outputs所引用。

## 语法

Resources由资源ID和资源描述组成。资源描述用大括号（\{ \}）括起。如果声明多个资源，用半角逗号（,）分隔开。Resources的语法结构示例代码段如下：

```
"Resources" : {
    "资源1 ID" : {
        "Type" : "资源类型",
        "Condition": "是否创建此资源的条件"，
        "Properties" : {
            资源属性描述
        }
    },
    "资源 2 ID" : {
        "Type" : "资源类型",
        "Condition": "是否创建此资源的条件"，
        "Properties" : {
            资源属性描述
        }
    }
}
```

参数说明如下：

-   资源ID在模板中具有唯一性。在创建模板其它部分时，可以通过资源ID引用该资源。
-   资源类型（Type）表示正在声明的资源的类型。例如，ALIYUN::ECS::Instance表示阿里云ECS实例。有关ROS支持的所有资源类型列表和详细信息，请参见[资源类型索引](/intl.zh-CN/资源类型/资源类型索引.md)。
-   资源属性（Properties）是为资源指定的附加选项。例如，必须为每个阿里云ECS实例指定一个Image ID。

示例

```
"Resources" : {
  "ECSInstance" : {
    "Type" : "ALIYUN::ECS::Instance",
    "Properties" : {
      "ImageId" : "m-25l0r****"
    }
  }
}
```

如果资源不需要声明任何属性，可以忽略该资源的属性部分。

属性值可以是文本字符串、字符串列表、布尔值、引用参数或者函数返回值。

-   如果属性值为文本字符串，该值会被双引号（" "）括起来。
-   如果属性值为任一类型的字符串列表，则会被方括号（\[ \]）括起来。
-   如果属性值为内部函数或引用的参数，则会被大括号（\{ \}）括起来。

当您将文字、列表、引用参数和函数返回值合并起来取值时，上述规则也适用。

声明不同的属性值类型示例如下：

```
"Properties" : {
    "String" : "string",
    "LiteralList" : [ "value1", "value2" ],
    "Boolean" : "true"
    "ReferenceForOneValue" :  { "Ref" : "ResourceID" } ,
    "FunctionResultWithFunctionParams" : {
        "Fn::Join" : [ "%", [ "Key=", { "Ref" : "SomeParameter" } ] ] }
}
```

## DeletionPolicy

在模板中，设置DeletionPolicy属性，可以声明在资源栈被删除时保留某个资源。例如，设置在资源栈删除时保留ECS实例，可按照以下代码段进行声明：

```
"Resources" : {
  "ECSInstance" : {
    "Type" : "ALIYUN::ECS::Instance",
    "Properties" : {
      "ImageId" : "m-25l0r****"
    },
    "DeletionPolicy" : "Retain"
  }
}
```

在本示例中，如果该模板对应的资源栈被删除，则会保留ECSInstance资源。

## DependsOn

在模板中，设置DependsOn属性，可以指定特定资源紧跟着另一个资源后创建。为某个资源添加DependsOn属性后，该资源仅在DependsOn属性中指定的资源之后创建。

**说明：** 允许DependsOn依赖的资源Condition为False，为False时不影响该资源的创建。

用法示例包括以下两种：

-   依赖单个资源：

    ```
    "DependsOn": "ResourceName"
    ```

-   依赖多个资源：

    ```
    "DependsOn": [
                   "ResourceName1",
                   "ResourceName2"
                 ]   
    ```


如以下代码段所示，WebServer将在DatabaseServer创建成功后才开始创建：

```
{
  "ROSTemplateFormatVersion" : "2015-09-01",
  "Resources" : {
    "WebServer": {
      "Type": "ALIYUN::ECS::Instance",
      "DependsOn": "DatabseServer"
    },
    "DatabseServer": {
      "Type": "ALIYUN::ECS::Instance",
      "Properties": {
        "ImageId" : "m-25l0r****",
        "InstanceType": "ecs.t1.small"
      }
    }
  }
}        
```

## Condition

在模板中，使用Condition属性可以指定是否需要创建此资源。只有Condition所指定的条件值为True时，才会创建此资源。

如以下代码段所示，根据MaxAmount的值判断否创建WebServer：

```
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
        "ImageId" : "m-25l0rc****",
        "InstanceType": "ecs.t1.small"
        "MaxAmount": {"Ref": "MaxAmount"}
      }
    },
    "DatabseServer": {
      "Type": "ALIYUN::ECS::Instance",
      "Properties": {
        "ImageId" : "m-25l0r****",
        "InstanceType": "ecs.t1.small"
      }
    }
  }
}
```

## Count

在模板中，为资源指定`Count`后，ROS会对模板进行预处理，把该资源展开成多个资源。 操作资源栈时使用处理后的模板。

-   例如，资源名为`A`，其`Count`值为3。在处理后的模板中，没有`A`资源，取而代之的是`A[0]`、`A[1]`和`A[2]`这3个资源。

    ```
    "Resources": {
      "A": {
        "Count": 3,
        ...
      },
      ...
    }
    ```

    处理后：

    ```
    "Resources": {
      "A[0]": {
        ...
      },
      "A[1]": {
        ...
      },
      "A[2]": {
        ...
      },
      ...
    }
    ```

    **说明：** 如果展开后的资源的名称在原模板中已存在，比如`A[1]`在原模板中已经定义，则预处理失败，校验不通过。

    请避免向已有资源添加`Count`属性，因为这会导致资源名发生变化，引发删除操作。

-   `Count`最终结果必须为自然数，仅支持如下函数：
    -   Ref（仅引用参数）
    -   Fn::FindInMap
    -   Fn::Select
    -   Fn::Join
    -   Fn::Split
    -   Fn::Replace
    -   Fn::Base64Encode
    -   Fn::Base64Decode
    -   Fn::MemberListToMap
    -   Fn::If
    -   Fn::ListMerge
    -   Fn::GetJsonValue
    -   Fn::MergeMapToList
    -   Fn::SelectMapList
    -   Fn::Add
    -   Fn::Avg
    -   Fn::Str
    -   Fn::Calculate
    -   Fn::Max
    -   Fn::Min
-   处理后的模板资源总数需要符合限制，目前最多支持300个。
-   指定了`Count`的资源的属性\(`Properties`\)中可以使用伪参数`ALIYUN::Index`，在预处理的时候会被替换为相应的数值。例如，`A[0]`使用的`ALIYUN::Index`会被替换为0，`A[1]`使用的`ALIYUN::Index`会被替换为1。模板其他地方不能使用`ALIYUN::Index`。
-   如果指定了`Count`的资源出现在`DependsOn`中，会被展开。

    ```
    "DependsOn": "A"
    ```

    处理后：

    ```
    "DependsOn": ["A[0]", "A[1]", "A[2]"]
    ```

-   如果指定了`Count`的资源出现在函数`Ref`、`Fn::GetAtt`中，会被展开。

    ```
    {
      "Ref": "A"
    }
    
    
    {
      "Fn::GetAtt": ["A", "PropertyName"]
    }
    ```

    处理后：

    ```
    [
      {
        "Ref": "A[0]"
      },
      {
        "Ref": "A[1]"
      },
      {
        "Ref": "A[2]"
      }
    ]
    
    
    [
      {
        "Fn::GetAtt": [
          "A[0]",
          "PropertyName"
        ]
      },
      {
        "Fn::GetAtt": [
          "A[1]",
          "PropertyName"
        ]
      },
      {
        "Fn::GetAtt": [
          "A[2]",
          "PropertyName"
        ]
      }
    ]
    ```

    如果多个资源使用`Count`，并且存在引用关系。建议与`Fn::Select`以及`ALIYUN::Index`联合使用。

    ```
    {
      "Fn::Select": [
        {
          "Ref": "ALIYUN::Index"
        },
        {
          "Ref": "A"
        }
      ]
    }
    ```

    以`A`为例，`B`引用了`A`，且`B`的`Count`为2，转换后`B[0]`、`B[1]`中部分表达式分别如下：

    ```
    {
      "Ref": "A[0]"
    }
    
    {
      "Ref": "A[1]"
    }
    ```


下面是简单的示例。示例模板中创建了一组EIP和同等数量的ECS，并把EIP与ECS逐一绑定。

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Count": {
      "Type": "Number"
    }
  },
  "Resources": {
    "Eip": {
      "Type": "ALIYUN::VPC::EIP",
      "Count": {
        "Ref": "Count"
      },
      "Properties": {
        "Bandwidth": 5
      }
    },
    "Servers": {
      "Type": "ALIYUN::ECS::InstanceGroup",
      "Properties": {
        "MinAmount": {
          "Ref": "Count"
        },
        "MaxAmount": {
          "Ref": "Count"
        },
        "AllocatePublicIP": false,
        ...
      }
    },
    "EipBind": {
      "Type": "ALIYUN::VPC::EIPAssociation",
      "Count": {
        "Ref": "Count"
      },
      "Properties": {
        "InstanceId": {
          "Fn::Select": [
            {
              "Ref": "ALIYUN::Index"
            },
            {
              "Fn::GetAtt": [
                "Servers",
                "InstanceIds"
              ]
            }
          ]
        },
        "AllocationId": {
          "Fn::Select": [
            {
              "Ref": "ALIYUN::Index"
            },
            {
              "Ref": "Eip"
            }
          ]
        }
      }
    }
  },
  "Outputs": {
    "InstanceIds": {
      "Value": {
        "Fn::GetAtt": [
          "Servers",
          "InstanceIds"
        ]
      }
    },
    "AllocationIds": {
      "Value": {
        "Ref": "Eip"
      }
    },
    "EipAddresses": {
      "Value": {
        "Fn::GetAtt": [
          "Eip",
          "EipAddress"
        ]
      }
    }
  }
}
```

处理后：

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Count": {
      "Type": "Number"
    }
  },
  "Resources": {
    "Eip[0]": {
      "Type": "ALIYUN::VPC::EIP",
      "Properties": {
        "Bandwidth": 5
      }
    },
    "Eip[1]": {
      "Type": "ALIYUN::VPC::EIP",
      "Properties": {
        "Bandwidth": 5
      }
    },
    "Servers": {
      "Type": "ALIYUN::ECS::InstanceGroup",
      "Properties": {
        "MinAmount": {
          "Ref": "Count"
        },
        "MaxAmount": {
          "Ref": "Count"
        },
        "AllocatePublicIP": false,
        ...
      }
    },
    "EipBind[0]": {
      "Type": "ALIYUN::VPC::EIPAssociation",
      "Properties": {
        "InstanceId": {
          "Fn::Select": [
            0,
            {
              "Fn::GetAtt": [
                "Servers",
                "InstanceIds"
              ]
            }
          ]
        },
        "AllocationId": {
          "Ref": "Eip[0]"
        }
      }
    },
    "EipBind[1]": {
      "Type": "ALIYUN::VPC::EIPAssociation",
      "Properties": {
        "InstanceId": {
          "Fn::Select": [
            1,
            {
              "Fn::GetAtt": [
                "Servers",
                "InstanceIds"
              ]
            }
          ]
        },
        "AllocationId": {
          "Ref": "Eip[1]"
        }
      }
    }
  },
  "Outputs": {
    "InstanceIds": {
      "Value": {
        "Fn::GetAtt": [
          "Servers",
          "InstanceIds"
        ]
      }
    },
    "AllocationIds": {
      "Value": [
        {
          "Ref": "Eip[0]"
        },
        {
          "Ref": "Eip[1]"
        }
      ]
    },
    "EipAddresses": {
      "Value": [
        {
          "Fn::GetAtt": [
            "Eip[0]",
            "EipAddress"
          ]
        },
        {
          "Fn::GetAtt": [
            "Eip[1]",
            "EipAddress"
          ]
        }
      ]
    }
  }
}
```

## 资源声明示例

典型的资源声明示例如下：

```
"Resources" : {
    "WebServer": {
      "Type": "ALIYUN::ECS::Instance",
      "Properties": {
        "ImageId" : "m-25l0r****",
        "InstanceType": "ecs.t1.small",
        "SecurityGroupId": "sg-25zwc****",
        "ZoneId": "cn-beijing-b",
        "Tags": [{
            "Key": "Department1",
            "Value": "HumanResource"
        },{
            "Key": "Department2",
            "Value": "Finance"
        }
        ]
      }
    },
    "ScalingConfiguration": {
      "Type": "ALIYUN::ESS::ScalingConfiguration",
      "Properties": {
        "ImageId": "ubuntu_14_04_64_20G_aliaegis_2015****.vhd",
        "InstanceType": "ecs.t1.small",
        "InstanceId": "i-25xhh****",
        "InternetChargeType": "PayByTraffic",
        "InternetMaxBandwidthIn": 1,
        "InternetMaxBandwidthOut": 20,
        "SystemDisk_Category": "cloud",
        "ScalingGroupId": "bwhtvpcBcKYac9fe3vd0****",
        "SecurityGroupId": "sg-25zwc****",
        "DiskMappings": [
            {
                "Size": 10
            },
            {
                "Category": "cloud",
                "Size": 10
            }
        ]
      }
    }
}
```

