# Update a stack by replacing its resource properties

If you need to update a stack but the resource properties cannot be modified, you can update the stack by replacing its resource properties.

If you need to modify only the resource properties of a stack but keep the physical ID unchanged, you can modify the parameter settings of the specified stack in the template.

If you need to update a stack but the resource properties cannot be modified, you can replace the stack. To replace a stack, you must recreate the stack by using a new ID after you delete the stack. This topic describes how to update a stack by replacing it. The CidrBlock property of the ALIYUN::ECS::VSwitch resource is replaced in the example.

## Procedure

1.  Log on to the [ROS console](http://ros.console.aliyun.com).

2.  Create a stack.

    Use the following template to create a stack that contains the ALIYUN::ECS::VSwitch resource. Set the CidrBlock property to 172.16.100.0/24.

    For more information about how to create a stack, see [t23186.md\#](/intl.en-US/Stack Management/Create a stack.md).

    ```
    {
        "ROSTemplateFormatVersion": "2015-09-01",
        "Parameters": {
            "ZoneId": {
                "Type": "String",
                "Default": "cn-hangzhou-i"
            },
            "VSwitchCidrBlock": {
                "Type": "String",
                "Default": "172.16.100.0/24"
            }
        },
        "Resources": {
            "EcsVpc": {
                "Type": "ALIYUN::ECS::VPC",
                "Properties": {
                    "CidrBlock": "172.16.0.0/12",
                    "VpcName": "MyTestVpc"
                }
            },
            "VSwitch": {
                "Type": "ALIYUN::ECS::VSwitch",
                "Properties": {
                    "ZoneId": {
                        "Ref": "ZoneId"
                    },
                    "CidrBlock": {
                        "Ref": "VSwitchCidrBlock"
                    },
                    "VpcId": {
                        "Fn::GetAtt": [
                            "EcsVpc",
                            "VpcId"
                        ]
                    },
                    "VSwitchName": "VSwitch"
                }
            }
        },
        "Outputs": {
        }
    }
    ```

3.  Replace the stack.

    1.  In the left-side navigation pane, click **Stacks**.

    2.  In the upper-left corner, select the region where the target stack resides from the drop-down list.

    3.  On the Stacks page, find the stack that you want to update and click **Update** in the **Actions** column.

    4.  In the Configure Template Parameters step of the Edit Stack wizard, update the VSwitchCidrBlock value from 172.16.100.0/24 to 172.16.200.0/24 in the **Parameters** section.

        ![replace](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4406919951/p148908.png)

    5.  Click **Next**.

    6.  In the Configure Stack step of the Edit Stack wizard, select **Enable** to enable replacement update.

        ![replace2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4406919951/p148911.png)

    7.  Click **Confirm**.

        After the replacement update is complete, the physical ID of the VSwitch resource changes. The CidrBlock value is changed from 172.16.100.0/24 to 172.16.200.0/24. If you want to view the resource information, click the **Resources** tab on the stack details page, and then click the new ID of the VSwitch resource to go to the VSwitch Details page.


