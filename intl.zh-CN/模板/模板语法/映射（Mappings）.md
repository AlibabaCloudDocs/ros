# 映射（Mappings）

映射是一个Key-Value映射表。在模板的Resources和Outputs中，可以使用Fn::FindInMap内部函数，通过指定Key而获取映射表的Value。

## 语法

映射由Key-Value对组成。其中Key和Value可以为字符串类型或者数字类型。如果声明多个映射，用英文逗号（,）分隔。每个映射的名称不能重复。

**说明：** 映射须为纯数据，映射中不能使用函数。

## 示例

-   正确的映射示例

    ```
    "Mappings": {
        "ValidMapping": {
            "TestKey1": {"TestValu1": "value1"},
            "TestKey2": {"TestValu2": "value2"},
            1234567890: {"TestValu3": "value3"},
            "TestKey4": {"TestValu4": 1234}
        }
    }          
    ```

-   错误的映射示例

    ```
    "Mappings": {
        "InvalidMapping1": {
            "ValueList": ["foo", "bar"],
              "ValueString": "baz"
        },
        "InvalidMapping2": ["foo", {"bar" : "baz"}],
        "InvalidMapping3": "foobar"
    }           
    ```

-   使用内部函数Fn::FindInMap返回对应的值示例

    ```
    {
      "ROSTemplateFormatVersion": "2015-09-01",
      "Parameters": {
        "regionParam": {
          "Description": "选择创建ECS的地域",
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
                {
                  "Ref": "regionParam"
                },
                "32"
              ]
            },
            "InstanceType": "ecs.t1.small",
            "SecurityGroupId": "sg-25zwc****",
            "ZoneId": "cn-beijing-b",
            "Tags": [
              {
                "Key": "Department1",
                "Value": "HumanResource"
              },
              {
                "Key": "Department2",
                "Value": "Finance"
              }
            ]
          }
        }
      }
    }    
    ```


