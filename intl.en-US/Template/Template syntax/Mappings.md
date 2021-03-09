# Mappings

The Mappings section is a key-value mapping table. When mappings are used in Resources or Outputs definitions, use Fn::FindInMap to match a key to a corresponding set of named values.

## Syntax

A mapping consists of one or more key-value pairs where both the keys and values can be strings or numbers. Multiple mappings are separated by commas \(,\). Mapping names must be unique.

**Note:** Mappings must be pure data and cannot contain functions.

## Examples

-   The following example shows a correct mapping definition:

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

-   The following example shows an incorrect mapping definition:

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

-   The following example shows how to use Fn::FindInMap to find the return value:

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


