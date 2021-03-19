# Use the Count feature to create multiple resources at a time

In Resource Orchestration Service \(ROS\), you can use the Count feature to create multiple resources at a time.

ALIYUN::VPC::EIP is used to apply for an elastic IP address \(EIP\). To apply for multiple EIPs, you must specify multiple ALIYUN::VPC::EIP resources in a template. However, this makes the template verbose. In this case, you can use the Count feature to create multiple resources at a time. For more information about the Count feature, see [Count](/intl.en-US/Template/Template syntax/Resources.md).

The Count feature is used in this topic to create multiple ECS instances and EIPs, and bind the EIPs to the ECS instances. The following resources are created in the examples:

-   One VPC
-   One VSwitch
-   One security group
-   Two pay-as-you-go ECS instances
-   Two EIPs

1.  Log on to the [ROS console](http://ros.console.aliyun.com).

2.  In the left-side navigation pane, click **Stacks**.

3.  In the upper-left corner, select the region where the target stack resides from the drop-down list.

4.  On the Stacks page, click **Create Stack**.

5.  In the Select Template step of the Create Stack wizard, click **Select an Existing Template** in the **Specify Template** section.

6.  Set **Template Import Method** to **Enter Template Content**. Enter the template content, and then click **Next**.

    ![Create stack](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5404498951/p148849.png)

    The following code provides an example on the template content.

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

    The following description provides details of the template:

    -   Set the Count parameter to 2 to create two EIPs. The value indicates that two EIPs are created using the Count feature. ROS preprocesses the template to generate two resources named Eip\[0\] and Eip\[1\].

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

    -   Set the Count parameter to 2 to create two ECS instances. Set the MaxAmount property of the ALIYUN::ECS::InstanceGroup resource to Count to create two ECS instances.

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

    -   Create two EipBind resources. You can use the ALIYUN::Index pseudo parameter to bind the EIPs to the ECS instances in sequence.

        Set the Count parameter to 2 to create two EipBind resources. ROS preprocesses the template to generate two resources named EipBind\[0\] and EipBind\[1\]. The ALIYUN::Index resource is used for the Count parameter. The Count value is replaced with the index value when ROS preprocesses the template. In the following example, the ECS instances are bound with the EIPs in sequence. The first ECS instance is bound with Eip\[0\], and the second ECS instance is bound with Eip\[1\].

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

7.  In the Configure Template Parameters step of the Create Stack wizard, set **Stack Name** and **Parameters**, and then click **Next**.

8.  In the Configure Stack step of the Create Stack wizard, set **Stack Policy**, **Rollback on Failure**, **Timeout Period**, **Deletion Protection**, **RAM Role**, and **Tags**, and then click **Next**.

    If no resources are created or updated within the time limit specified by **Timeout Period**, the system considers the operation to have failed. Based on the **Rollback on Failure** configuration, the system then determines whether to roll back to the status before the resource was created or updated.

9.  In the Check and Confirm step of the Create Stack wizard, click **Create**.


After the stack is created, you can click the **Resources** tab on the stack details page to view the resource information after preprocessing.

You can also click the **Template** tab on the stack details page to view the template information after preprocessing.

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

