# Metadata

Metadata is used to group the parameters defined in the Parameters section and define tags for each group.

When you create a stack in the [ROS console](http://ros.console.aliyun.com), the parameters defined in Parameters are displayed in the Parameters section of the **Configure Template Parameters** step. Metadata is used to group the parameters defined in the Parameters section and define tags for each group.

## Syntax

```
"Metadata": {
    "ALIYUN::ROS::Interface": {
        "ParameterGroups": [
            //Required.
            <Group1>,
            <Group2>,
            ...
        ],
        "TemplateTags":  [
            //Optional. A custom string.
            <Tag1>,
            <Tag2>,
        ]
    }
}
```

## Group syntax

```
{
    "Parameters": [
        //Required.
        <Parameter1>,
        <Parameter2>,
        ...
    ],
    "Label": {
        //Required.
        "default": <Custom string>
    }
}
```

## Examples

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Description": "Metadata demo",
  "Metadata": {
    "ALIYUN::ROS::Interface": {
      "ParameterGroups": [
        {
          "Parameters": [
            "VpcName",
            "VpcCidrBlock"
          ],
          "Label": {
            "default": "VPC"
          }
        },
        {
          "Parameters": [
            "VswName",
            "VswCidrBlock"
          ],
          "Label": {
            "default": "VSwitch"
          }
        }
      ],
      "TemplateTags": [
        "VPC-VSwitch"
      ]
    }
  },
  "Parameters": {
    "VpcName": {
      "Type": "String",
      "Label": "Name",
      "Description": "The name must be 2 to 128 characters in length and can contain letters, digits, underscores (_), and hyphens (-). It must start with a letter.",
      "Default": "MyVPC"
    },
    "VswName": {
      "Type": "String",
      "Label": "Name",
      "Description": "The name must be 2 to 128 characters in length and can contain letters, digits, underscores (_), and hyphens (-). It must start with a letter.",
      "Default": "MyVSwitch"
    },
    "VpcCidrBlock": {
      "Type": "String",
      "AllowedValues": [
        "10.0.0.0/8",
        "172.16.0.0/12",
        "192.168.0.0/16"
      ],
      "Description": "The CIDR block of the VPC. To customize the CIDR block, change the available values of this parameter in the template. The CIDR block must be contained within the range of available values.",
      "Label": "IPv4 CIDR block",
      "Default": "192.168.0.0/16"
    },
    "VswCidrBlock": {
      "Type": "String",
      "Description": "The configured CIDR block must be a subset of the CIDR block assigned to the VPC where the VSwitch resides and cannot be in use by other VSwitches.",
      "Label": "IPv4 CIDR block",
      "Default": "192.168.1.0/24"
    }
  },
  "Resources": {
    "VSwitch": {
      "Type": "ALIYUN::ECS::VSwitch",
      "Properties": {
        "VpcId": {
          "Ref": "VPC"
        },
        "ZoneId": {
          "Fn::Select": [
            "1",
            {
              "Fn::GetAZs": {
                "Ref": "ALIYUN::Region"
              }
            }
          ]
        },
        "CidrBlock": {
          "Ref": "VswCidrBlock"
        },
        "VSwitchName": {
          "Ref": "VswName"
        }
      }
    },
    "VPC": {
      "Type": "ALIYUN::ECS::VPC",
      "Properties": {
        "CidrBlock": {
          "Ref": "VpcCidrBlock"
        },
        "VpcName": {
          "Ref": "VpcName"
        }
      }
    }
  }
}
```

