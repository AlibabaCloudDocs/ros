# Python SDK使用示例

本文为您介绍如何使用资源编排服务（ROS）的Python SDK来创建和管理资源栈。

您除了可以在ROS控制台创建资源栈，还可以使用API代码来创建和管理资源栈。

## 准备工作

1.  下载及安装Python SDK。

    1.  使用pip安装aliyun-python-sdk-core。

        ```
        pip install aliyun-python-sdk-core
        ```

        **说明：** aliyun-python-sdk-core是所有阿里云官方Python SDK的公共组件。如果安装过程提示权限错误，可能是因为您没有Python安装路径的写权限。您也可以将此命令更改为`sudo pip install aliyun-python-sdk-core`。

    2.  安装ROS SDK。

        ```
        pip install aliyun-python-sdk-ros
        ```

2.  初始化SDK。

    1.  导入相关的包。

        ```
        from aliyunsdkcore.client import AcsClient
        from aliyunsdkros.request.v20190910.CreateStackRequest import CreateStackRequest
        from aliyunsdkros.request.v20190910.GetStackRequest import GetStackRequest
        from aliyunsdkros.request.v20190910.DeleteStackRequest import DeleteStackRequest
        from aliyunsdkros.request.v20190910.DescribeRegionsRequest import DescribeRegionsRequest
        from aliyunsdkros.request.v20190910.ListStacksRequest import ListStacksRequest
        ```

    2.  初始化SDK客户端对象。

        ```
        AK = '<yourAccessKeyId>'
        SECRET = '<yourAccessKeySecrect>'
        Region = '<yourRegionId>'
        client = AcsClient(AK, SECRET, Region) 
        ```


**说明：**

-   示例中的命令行都使用Linux的shell，如果您是Windows/DOS用户，则需要根据情况修改。
-   ROS Python SDK依赖Python 2.7以上版本。
-   ROS Python SDK 3.0.0及以上版本，支持v20150901版和v20190910版API。

## 查询可用地域列表

您可以使用Python SDK查询可用地域列表。

```
def describe_region():
    """describe regions list """
    request = DescribeRegionsRequest()
    request.set_connect_timeout(10000)
    request.set_read_timeout(10000)
    request.set_accept_format("json")
    response = client.do_action_with_exception(request)

    return response.decode("utf-8")
```

## 创建资源栈

创建资源栈时，您必须指定以下参数：

-   StackName：将要创建的资源栈的名称。每个用户空间下的资源栈名称不能重复。
-   TimeoutInMinutes：资源栈创建时长，单位为分钟。如果在指定时间内不能完成创建，则超时失败。
-   TemplateBody：创建的资源栈使用的模板内容。
-   TemplateURL：模板主体的文件的位置。必须指定TemplateBody或TemplateURL，但不能同时指定两者。
-   Parameters：创建的资源栈所需要的参数。需要在模板中定义key。

```
stack_name = "MyStack"
timeout = 10
template_body = """
    {
      "ROSTemplateFormatVersion": "2015-09-01",
      "Parameters": {
        "VpcName": {
          "Type": "String",
          "Description": "Vpc Name",
          "Label": "Vpc Name"
        },
        "CidrBlock": {
          "Type": "String",
          "Description": "Vpc CidrBlock",
          "Label": "Vpc CidrBlock"
         }
        },
      "Resources": {
        "Vpc": {
          "Type": "ALIYUN::ECS::VPC",
          "Properties": {
            "CidrBlock": {
              "Ref": "CidrBlock"
            },
            "VpcName": {
              "Ref": "VpcName"
            }
          }
        }
      }
    }
"""
params = [
    {
        "ParameterValue": "192.168.0.0/16",
        "ParameterKey": "CidrBlock"
    },
    {
        "ParameterValue": "TestVpc",
        "ParameterKey": "VpcName"
    }
]
```

```
def create_stack():
    """create stack"""
    request = CreateStackRequest()
    request.set_accept_format("json")
    request.set_StackName(stack_name)
    request.set_TimeoutInMinutes(timeout)
    # 若模板较大，建议使用TemplateURL参数，避免URL过长，调用失败。
    # 您也可以使用Body Param + HTTP POST的方式传递模板内容。
    # request.set_method("POST")
    # request.add_body_params("TemplateBody", template_body)
    request.set_TemplateBody(template_body)
    request.set_Parameterss(params)
    response = client.do_action_with_exception(request)

    return response.decode("utf-8")
```

## 查询资源栈

输入目标资源栈的ID。

```
def get_stack():
    """get descriptions of the stack"""
    request = GetStackRequest()
    request.set_accept_format("json")
    request.set_StackId(stack_id)
    response = client.do_action_with_exception(request)

    return response.decode("utf-8")
```

## 删除资源栈

输入目标资源栈的ID。

```
def delete_stack():
    """delete stack"""
    request = DeleteStackRequest()
    request.set_accept_format("json")
    request.set_StackId(stack_id)
    response = client.do_action_with_exception(request)

    return response.decode("utf-8")
```

```
import json
from time import sleep
from aliyunsdkcore.client import AcsClient
from aliyunsdkros.request.v20190910.CreateStackRequest import CreateStackRequest
from aliyunsdkros.request.v20190910.GetStackRequest import GetStackRequest
from aliyunsdkros.request.v20190910.DeleteStackRequest import DeleteStackRequest
from aliyunsdkros.request.v20190910.DescribeRegionsRequest import DescribeRegionsRequest
from aliyunsdkros.request.v20190910.ListStacksRequest import ListStacksRequest


AK = '<yourAccessKeyId>'
SECRET = '<yourAccessKeySecret>'
Region = '<yourRegionId>'  # 例如：'cn-beijing'、'cn-hangzhou'

client = AcsClient(AK, SECRET, Region)


def describe_region():
    """describe regions list """
    request = DescribeRegionsRequest()
    request.set_connect_timeout(10000)
    request.set_read_timeout(10000)
    request.set_accept_format("json")
    response = client.do_action_with_exception(request)

    return response.decode("utf-8")


def create_stack(stack_name, timeout, template_body, params=[]):
    """create stack"""
    request = CreateStackRequest()
    request.set_accept_format("json")
    request.set_StackName(stack_name)
    request.set_TimeoutInMinutes(timeout)
    # 若模板较大，建议使用TemplateURL参数，避免URL过长，调用失败。
    # 您也可以使用Body Param + HTTP POST的方式传递模板内容。
    # request.set_method("POST")
    # request.add_body_params("TemplateBody", template_body)
    request.set_TemplateBody(template_body)
    response = client.do_action_with_exception(request)

    return response.decode("utf-8")


def get_stack(stack_id):
    """get descriptions of the stack"""
    request = GetStackRequest()
    request.set_accept_format("json")
    request.set_StackId(stack_id)
    response = client.do_action_with_exception(request)

    return response.decode("utf-8")


def delete_stack(stack_id):
    """delete stack"""
    request = DeleteStackRequest()
    request.set_accept_format("json")
    request.set_StackId(stack_id)
    response = client.do_action_with_exception(request)

    return response.decode("utf-8")


if __name__ == '__main__':
    test_template = """
        {
          "ROSTemplateFormatVersion": "2015-09-01",
          "Parameters": {
            "VpcName": {
              "Type": "String",
              "Description": "Vpc Name",
              "Label": "Vpc Name"
            },
            "CidrBlock": {
              "Type": "String",
              "Description": "Vpc CidrBlock",
              "Label": "Vpc CidrBlock"
             }
            },
          "Resources": {
            "Vpc": {
              "Type": "ALIYUN::ECS::VPC",
              "Properties": {
                "CidrBlock": {
                  "Ref": "CidrBlock"
                },
                "VpcName": {
                  "Ref": "VpcName"
                }
              }
            }
          }
        }
    """

    parameters = [
        {"ParameterKey": "CidrBlock", "ParameterValue": "192.168.0.0/16"},
        {"ParameterKey": "VpcName", "ParameterValue": "TestVpc"}
    ]

    describe_region()
    stack = create_stack('MyStack', 10, test_template, parameters)
    get_stack(json.loads(stack)["StackId"])
    sleep(3)  # 等待创建资源栈任务执行完毕
    delete_stack(json.loads(stack)["StackId"])
```

