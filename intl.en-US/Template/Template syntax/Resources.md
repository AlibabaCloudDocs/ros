# Resources

This topic describes the properties of each resource and dependencies of resources in a stack. A resource can be referenced by other resources and output items.

## Syntax

Each resource consists of an ID and a description. All resource descriptions are enclosed in braces \{\}. Multiple resources are separated by commas \(,\). The following sample code shows the Resources syntax:

```
"Resources" : {
    "Resource1 ID": {
        "Type": "The resource type",
        "Condition": "The condition that specifies whether to create the resource",
        "Properties" : {
            The description of the resource properties
        }
    },
    "Resource2 ID" : {
        "Type": "The resource type",
        "Condition": "The condition that specifies whether to create the resource",
        "Properties" : {
            The description of the resource properties
        }
    }
}
```

Parameter description:

-   A resource ID must be unique within a template. You can use a resource ID to reference a resource in other parts of a template.
-   The Type parameter specifies the type of the resource that is being declared. For example, ALIYUN::ECS::Instance indicates that the resource is an Elastic Cloud Service \(ECS\) instance. For more information about resource types in Resource Orchestration Service \(ROS\), see [Resource type index](/intl.en-US/Resource Types/Resource type index.md).
-   The Properties section provides additional options that you can specify for a resource. For example, you must specify an image ID for each Alibaba Cloud ECS instance.

Examples

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

If a resource does not need properties to be declared, omit the Properties section of that resource.

Property values can be text strings, string lists, Boolean values, referenced parameters, or return values of functions.

-   Text strings are enclosed in double quotation marks \('' ''\).
-   String lists are enclosed in brackets \[\].
-   Referenced parameters or return values of built-in functions are enclosed in braces \{\}.

The preceding rules also apply when property values are the combinations of text strings, string lists, referenced parameters, and return values of functions.

The following sample code shows how to declare different types of properties:

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

You can use the DeletionPolicy parameter to retain a resource when its stack is deleted. The following sample code shows how to use the DeletionPolicy parameter to retain an ECS instance when the stack is deleted:

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

In this example, the ECS instance is retained when the stack created based on the template is deleted.

## DependsOn

You can use the DependsOn parameter to create a specific resource after you create its dependent resource. If you specify the DependsOn parameter for a resource, the resource is created only after its dependent resource specified by the DependsOn parameter is created.

**Note:** The Condition parameter of the resource that is specified by the DependsOn parameter can be set to False. The value of False does not affect resource creation.

The following sample code shows how to configure dependent resources:

-   Configure a single dependent resource:

    ```
    "DependsOn": "ResourceName"
    ```

-   Configure multiple dependent resources:

    ```
    "DependsOn": [
                   "ResourceName1",
                   "ResourceName2"
                 ]   
    ```


In the following example, WebServer is created only after DatabaseServer is created:

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

You can use the Condition parameter to specify whether to create a resource. The resource can be created only when the Condition parameter is set to True.

In the following example, WebServer is created only if the condition determined by the MaxAmount parameter is true:

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

You can use the `Count` parameter to preprocess the template of a resource and expand the resource into multiple ones. The resulting template is used when you manage the stack.

-   In the following example, the `Count` parameter is set to 3 for a resource named `A`. In the resulting template, the `A` resource is replaced with resources named `A[0]`, `A[1]`, and `A[2]`.

    ```
    "Resources": {
      "A": {
        "Count": 3,
        ...
      },
      ...
    }
    ```

    Result after preprocessing:

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

    **Note:** After a resource is expanded, if a resource name such as `A[1]` already exists in the original template, the preprocessing fails.

    We recommend that you do not specify the `Count` property for existing resources, because the changes of resource names it entails will cause deletion of the resources.

-   The value of the `Count` parameter must be a natural number. The parameter supports only the following functions:
    -   Ref \(for parameter references only\)
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
-   The number of resulting template resources cannot exceed 300.
-   In `Properties` of the resource for which the `Count` parameter is specified, the `ALIYUN::Index` pseudo parameter can be used and will be replaced with the corresponding value during preprocessing. For example, `ALIYUN::Index` used for `A[0]` will be replaced with 0. `ALIYUN::Index` used for `A[1]` will be replaced with 1. `ALIYUN::Index` cannot be used in other parts of a template.
-   A resource for which `Count` is specified will be expanded if it is part of the `DependsOn` parameter. Example:

    ```
    "DependsOn": "A"
    ```

    Result after preprocessing:

    ```
    "DependsOn": ["A[0]", "A[1]", "A[2]"]
    ```

-   A resource for which `Count` is specified will be expanded if it is part of the `Ref` and `Fn::GetAtt` functions. Example:

    ```
    {
      "Ref": "A"
    }
    
    
    {
      "Fn::GetAtt": ["A", "PropertyName"]
    }
    ```

    Result after preprocessing:

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

    If multiple resources use the `Count` parameter and reference each other, use Count in combination with `Fn::Select` and `ALIYUN::Index`. Example:

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

    In this example of the `A` resource, `B` references `A`, and the `Count` parameter of `B` is set to 2. The following segment is a part of the expressions of `B[0]` and `B[1]` after preprocessing:

    ```
    {
      "Ref": "A[0]"
    }
    
    {
      "Ref": "A[1]"
    }
    ```


In the following sample template, a group of elastic IP addresses \(EIPs\) and a corresponding number of ECS instances are created, and the EIPs are associated with the ECS instances.

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

Result after preprocessing:

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

## Resource declaration example

The following sample code shows how to declare resources:

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

