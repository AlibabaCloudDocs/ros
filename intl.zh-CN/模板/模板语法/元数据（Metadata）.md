# 元数据（Metadata）

元数据（Metadata）用于对Parameters中定义的参数进行分组，并且可以为每一组分别定义标签。

在[资源编排控制台](http://ros.console.aliyun.com)上创建资源栈时，Parameters中定义的参数会展示在配置模板参数的**参数录入**中。Metadata用于对Parameters中定义的参数进行分组，并且可以为每一组分别定义标签。

## 语法

```
"Metadata": {
    "ALIYUN::ROS::Interface": {
        "ParameterGroups": [
            //ParameterGroups为必填项
            <Group1>,
            <Group2>,
            ...
        ],
        "TemplateTags":  [
            //TemplateTags可选，为自定义字符串
            <Tag1>,
            <Tag2>,
        ]
    }
}
```

## Group语法

```
{
    "Parameters": [
        //Parameters为必填项
        <Parameter1>,
        <Parameter2>,
        ...
    ],
    "Label": {
        //Label为必填项
        "default": <自定义字符串>
    }
}
```

## 示例

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Description": "Metadata演示",
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
      "Label": "名称",
      "Description": "长度为2~128个字符，以英文字母或汉字开头，可包含英文字母、汉字、数字、下划线（_）和短划线（-）。",
      "Default": "MyVPC"
    },
    "VswName": {
      "Type": "String",
      "Label": "名称",
      "Description": "长度为2~128个字符，以英文字母或汉字开头，可包含英文字母、汉字、数字、下划线（_）和短划线（-）。",
      "Default": "MyVSwitch"
    },
    "VpcCidrBlock": {
      "Type": "String",
      "AllowedValues": [
        "10.0.0.0/8",
        "172.16.0.0/12",
        "192.168.0.0/16"
      ],
      "Description": "专有网络网段。如需自定义网段，请更改模板此参数的可用值，网段必须属于可用值范围的子网网段。",
      "Label": "IPv4网段",
      "Default": "192.168.0.0/16"
    },
    "VswCidrBlock": {
      "Type": "String",
      "Description": "必须是所属专有网络的子网段，并且没有被其他交换机占用。",
      "Label": "IPv4网段",
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

