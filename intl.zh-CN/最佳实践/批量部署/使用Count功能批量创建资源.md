# 使用Count功能批量创建资源

资源编排服务ROS（Resource Orchestration Service）支持Count功能，用于批量创建资源。

ALIYUN::VPC::EIP类型用于申请弹性公网IP（EIP）。如果需要申请多个弹性公网IP，则需要在模板中写多个ALIYUN::VPC::EIP资源，这样模板会变得冗长。此时您可以使用Count功能批量创建资源。Count功能详情，请参见[Count](/intl.zh-CN/模板/模板语法/资源（Resources）.md)。

本文将使用Count功能，批量创建ECS实例和EIP，并为ECS实例绑定EIP。本示例将会创建以下资源：

-   1个VPC（专有网络）
-   1个VSwitch（交换机）
-   1个SecurityGroup（安全组）
-   2个ECS（按量付费的ECS）
-   2个EIP（弹性公网IP）

1.  登录[资源编排控制台](http://ros.console.aliyun.com)。

2.  在左侧导航栏单击**资源栈**。

3.  在页面左上角的地域下拉列表，选择资源栈的所在地域。

4.  在资源栈列表页面，单击**创建资源栈**。

5.  在选择模板页面的**指定模板**区域，单击**选择已有模板**。

6.  在**模板录入方式**区域单击**输入模板**，输入模板内容，单击**下一步**。

    ![创建资源栈](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6494649951/p131713.png)

    模板代码如下：

    ```
    {
      "ROSTemplateFormatVersion": "2015-09-01",
      "Parameters": {
        "Count": {
          "Type": "Number",
          "Default": 2
        },
        "ZoneId": {
          "Type": "String"
        },
        "InstanceType": {
          "Type": "String",
          "Default": "ecs.c6.large"
        },
        "Password": {
          "Type": "String",
          "Default": "Abc1****",
          "NoEcho": true
        }
      },
      "Resources": {
        "Vpc": {
          "Type": "ALIYUN::ECS::VPC",
          "Properties": {
            "CidrBlock": "10.0.0.0/8",
            "VpcName": "test-resource-count"
          }
        },
        "VSwitch": {
          "Type": "ALIYUN::ECS::VSwitch",
          "Properties": {
            "CidrBlock": "10.0.10.0/24",
            "ZoneId": {
              "Ref": "ZoneId"
            },
            "VpcId": {
              "Ref": "Vpc"
            }
          }
        },
        "SecurityGroup": {
          "Type": "ALIYUN::ECS::SecurityGroup",
          "Properties": {
            "SecurityGroupName": "test-resource-count",
            "VpcId": {
              "Ref": "Vpc"
            }
          }
        },
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
            "ImageId": "centos_7",
            "InstanceType": {
              "Ref": "InstanceType"
            },
            "VpcId": {
              "Ref": "Vpc"
            },
            "VSwitchId": {
              "Ref": "VSwitch"
            },
            "SecurityGroupId": {
              "Ref": "SecurityGroup"
            },
            "Password": {
              "Ref": "Password"
            },
            "AllocatePublicIP": false,
            "MaxAmount": {
              "Ref": "Count"
            }
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

    模板说明如下：

    -   创建2个EIP。

        Count取值为2。使用Count功能，创建了2个EIP资源。通过ROS的预处理，会生成名为Eip\[0\]和Eip\[1\]的两个资源。

        ```
        {
            "Eip": {
                "Type": "ALIYUN::VPC::EIP",
                "Count": {
                    "Ref": "Count"
                },
                "Properties": {
                    "Bandwidth": 5
                }
            }
        }
        ```

    -   创建2个ECS实例。

        Count取值为2。将ALIYUN::ECS::InstanceGroup的MaxAmount指定为Count，取值为2，生成两个ECS资源。

        ```
        {
            "Servers": {
                "Type": "ALIYUN::ECS::InstanceGroup",
                "Properties": {
                    "ImageId": "centos_7",
                    "InstanceType": {
                        "Ref": "InstanceType"
                    },
                    "VpcId": {
                        "Ref": "Vpc"
                    },
                    "VSwitchId": {
                        "Ref": "VSwitch"
                    },
                    "SecurityGroupId": {
                        "Ref": "SecurityGroup"
                    },
                    "Password": {
                        "Ref": "Password"
                    },
                    "AllocatePublicIP": false,
                    "MaxAmount": {
                        "Ref": "Count"
                    }
                }
            }
        }
        ```

    -   创建2个EipBind资源，通过ALIYUN::Index伪参数逐一绑定ECS实例和EIP。

        Count取值为2。使用Count功能，创建了2个EipBind资源。通过ROS的预处理，会生成名为EipBind\[0\]和EipBind\[1\]的两个资源。ALIYUN::Index在Count中使用，在预处理时会被替换为相应的数值。本示例中将逐一绑定ECS实例与EIP，即第一个实例绑定Eip\[0\]，第二个实例绑定Eip\[1\]。

        ```
        {
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
        }
        ```

7.  在配置模板参数页面，根据控制台提示，配置**资源栈名称**和**参数录入**，单击**下一步**。

8.  在配置资源栈页面，根据控制台提示，配置**资源栈策略**、**失败时回滚**、**超时设置**、**删除保护**、**RAM角色**和**标签**，单击**下一步**。

    资源的创建或更新未在**超时设置**的时间内完成，系统自动判断该操作失败，再根据**失败时回滚**设置，判断是否回滚到创建或更新资源之前的状态。

9.  在检查并确认页面，单击**创建**。


资源栈创建后，您可以在资源栈详情页面单击**资源**页签，查看经过ROS预处理后的资源信息。

您也可以在资源栈详情页面单击**模板**页签，查看经过ROS预处理后的模板信息。

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "Count": {
      "Default": 2,
      "Type": "Number"
    },
    "Password": {
      "Default": "Abc12345",
      "NoEcho": true,
      "Type": "String"
    },
    "InstanceType": {
      "Default": "ecs.c6.large",
      "Type": "String"
    },
    "ZoneId": {
      "Type": "String"
    }
  },
  "Resources": {
    "Vpc": {
      "Type": "ALIYUN::ECS::VPC",
      "Properties": {
        "VpcName": "test-resource-count",
        "CidrBlock": "10.0.0.0/8"
      }
    },
    "VSwitch": {
      "Type": "ALIYUN::ECS::VSwitch",
      "Properties": {
        "VpcId": {
          "Ref": "Vpc"
        },
        "CidrBlock": "10.0.10.0/24",
        "ZoneId": {
          "Ref": "ZoneId"
        }
      }
    },
    "SecurityGroup": {
      "Type": "ALIYUN::ECS::SecurityGroup",
      "Properties": {
        "VpcId": {
          "Ref": "Vpc"
        },
        "SecurityGroupName": "test-resource-count"
      }
    },
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
        "VpcId": {
          "Ref": "Vpc"
        },
        "MinAmount": {
          "Ref": "Count"
        },
        "SecurityGroupId": {
          "Ref": "SecurityGroup"
        },
        "ImageId": "centos_7",
        "AllocatePublicIP": false,
        "VSwitchId": {
          "Ref": "VSwitch"
        },
        "Password": {
          "Ref": "Password"
        },
        "InstanceType": {
          "Ref": "InstanceType"
        },
        "MaxAmount": {
          "Ref": "Count"
        }
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
    "InstanceIds": {
      "Value": {
        "Fn::GetAtt": [
          "Servers",
          "InstanceIds"
        ]
      }
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

