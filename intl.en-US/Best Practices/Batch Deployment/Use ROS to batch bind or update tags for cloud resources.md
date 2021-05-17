# Use ROS to batch bind or update tags for cloud resources

You can use Resource Orchestration Service \(ROS\) to create stacks and create resources within the stacks. To facilitate subsequent O&M, you can also bind tags to your resources by using ROS. ROS allows you to batch bind or update tags for multiple resources at a time to enhance O&M efficiency.

## Background information

In this topic, ROS SDK for Python is used to create stacks. For more information, see [Use SDK for Python](/intl.en-US/SDK Reference/Use SDK for Python.md).

## Bind the same tag to multiple cloud resources

In the following example, ROS is used to create a virtual private cloud \(VPC\) named `mytest-vpc` and a vSwitch named `mytest-vsw-h`. An `app:test` tag is also bound to both the VPC and vSwitch.

1.  Create a template.

    ```
    {
      "ROSTemplateFormatVersion": "2015-09-01",
      "Resources": {
        "VPC": {
          "Type": "ALIYUN::ECS::VPC",
          "Properties": {
            "VpcName": "mytest-vpc"
          }
        },
        "VSwitch": {
          "Type": "ALIYUN::ECS::VSwitch",
          "Properties": {
            "VpcId": { "Ref": "VPC" },
            "ZoneId": "cn-hangzhou-h",
            "CidrBlock": "172.16.0.0/24",
            "VSwitchName": "mytest-vsw-h"
          }
        }
      }
    }
    ```

    In the template, a VPC and a vSwitch are created.

2.  Create a stack and bind the `app:test` tag to the VPC and vSwitch.

    ```
    # pip install aliyun-python-sdk-ros
    import json
    from aliyunsdkcore.client import AcsClient
    from aliyunsdkros.request.v20190910.CreateStackRequest import CreateStackRequest
    
    client = AcsClient(
        '<AccessKeyId>',
        '<AccessKeySecret>',
        'cn-hangzhou',
    )
    template = '''
    <Template>
    '''
    
    req = CreateStackRequest()
    req.set_StackName('vpc-vswitch-test')
    req.set_TemplateBody(template)
    req.set_TimeoutInMinutes(10)
    req.set_Tags([{'Key': 'app', 'Value': 'test'}])
    ret = client.do_action_with_exception(req)
    print(ret)
    ```

    Parameter description:

    -   Replace <AccessKeyId\> and <AccessKeySecret\> with your AccessKey ID and AccessKey secret.
    -   Replace <Template\> with the template created in [Step 1](#step_m52_wju_m48).
3.  Log on to the [VPC console](https://vpcnext.console.aliyun.com/vpc) and check whether the tag is bound to both the VPC and the vSwitch.




## Bind different tags to different cloud resources

In the following example, ROS is used to create a VPC named `mytest-vpc` and a vSwitch named `mytest-vsw-h`. An `app:test` tag is bound to both the VPC and the vSwitch, and a `group:test` tag is bound only to the vSwitch. Result description:

-   The tag bound to the `mytest-vpc` VPC is `app:test`.
-   The tags bound to `mytest-vsw-h` are `app:test` and `group:test`.

1.  Create a template.

    ```
    {
      "ROSTemplateFormatVersion": "2015-09-01",
      "Resources": {
        "VPC": {
          "Type": "ALIYUN::ECS::VPC",
          "Properties": {
            "VpcName": "mytest-vpc"
          }
        },
        "VSwitch": {
          "Type": "ALIYUN::ECS::VSwitch",
          "Properties": {
            "VpcId": { "Ref": "VPC" },
            "ZoneId": "cn-hangzhou-h",
            "CidrBlock": "172.16.0.0/24",
            "VSwitchName": "mytest-vsw-h",
            "Tags": [{ "Key": "group", "Value": "test" }]
          }
        }
      }
    }
    ```

    A VPC and a vSwitch are created, and the `group:test` tag is bound to the vSwitch.

2.  Create a stack and bind the `app:test` tag to the VPC and vSwitch.

    ```
    # pip install aliyun-python-sdk-ros
    import json
    from aliyunsdkcore.client import AcsClient
    from aliyunsdkros.request.v20190910.CreateStackRequest import CreateStackRequest
    
    client = AcsClient(
        '<AccessKeyId>',
        '<AccessKeySecret>',
        'cn-hangzhou',
    )
    template = '''
    <Template>
    '''
    
    req = CreateStackRequest()
    req.set_StackName('vpc-vswitch-test')
    req.set_TemplateBody(template)
    req.set_TimeoutInMinutes(10)
    req.set_Tags([{'Key': 'app', 'Value': 'test'}])
    ret = client.do_action_with_exception(req)
    print(ret)
    ```

    Parameter description:

    -   Replace <AccessKeyId\> and <AccessKeySecret\> with your AccessKey ID and AccessKey secret.
    -   Replace <Template\> with the template created in [Step 1](#step_tz0_5f6_kdg).
3.  Log on to the [VPC console](https://vpcnext.console.aliyun.com/vpc) and check whether

    the `app:test` tag is bound to the VPC and whether the `app:test` and `group:test` tags are bound to the vSwitch.


## Update tags for multiple cloud resources

In the following example, the `app:test` tag bound to `mytest-vpc` and `mytest-vsw-h` in the [Bind the same tag to multiple cloud resources](#section_e7b_jwh_8gn) section is changed to `app:normal`.

1.  Create a stack and bind the `app:normal` tag to the VPC and vSwitch.

    ```
    # pip install aliyun-python-sdk-ros
    import json
    from aliyunsdkcore.client import AcsClient
    from aliyunsdkros.request.v20190910.UpdateStackRequest import UpdateStackRequest
    
    client = AcsClient(
        '<AccessKeId>',
        '<AccessKeySecret>',
        'cn-hangzhou',
    )
    template = '''
    <Template>
    '''
    
    req = UpdateStackRequest()
    req.set_StackId('<StackId>')
    req.set_TemplateBody(template)
    req.set_Tags([{'Key': 'app', 'Value': 'normal'}])
    ret = client.do_action_with_exception(req)
    print(ret)
    ```

    Parameter description:

    -   Replace <AccessKeyId\> and <AccessKeySecret\> with your AccessKey ID and AccessKey secret.
    -   Replace <Template\> with the template created in Step 1 of the [Bind the same tag to multiple cloud resources](#section_e7b_jwh_8gn) section.
2.  Log on to the [VPC console](https://vpcnext.console.aliyun.com/vpc) and check whether

    the `app:normal` tag is bound to the VPC and vSwitch.


