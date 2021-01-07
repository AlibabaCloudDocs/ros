# Use SDK for Python

This topic describes how to use ROS SDK for Python to create and manage stacks.

You can also use the ROS console or call API operations to create and manage stacks.

## Preparations

1.  Download and install SDK for Python.

    1.  Use pip to install aliyun-python-sdk-core.

        ```
        pip install aliyun-python-sdk-core
        ```

        **Note:** aliyun-python-sdk-core is included in all SDKs for Python of Alibaba Cloud. If the installation fails and an error message appears, a likely reason is that you do not have the write permission to the Python installation path. In this case, modify the preceding command to `sudo pip install aliyun-python-sdk-core`.

    2.  Install ROS SDK.

        ```
        pip install aliyun-python-sdk-ros
        ```

2.  Initialize the SDK.

    1.  Import the required libraries.

        ```
        from aliyunsdkcore.client import AcsClient
        from aliyunsdkros.request.v20190910.CreateStackRequest import CreateStackRequest
        from aliyunsdkros.request.v20190910.GetStackRequest import GetStackRequest
        from aliyunsdkros.request.v20190910.DeleteStackRequest import DeleteStackRequest
        from aliyunsdkros.request.v20190910.DescribeRegionsRequest import DescribeRegionsRequest
        from aliyunsdkros.request.v20190910.ListStacksRequest import ListStacksRequest
        ```

    2.  Initialize the SDK client.

        ```
        AK = '<yourAccessKeyId>'
        SECRET = '<yourAccessKeySecrect>'
        Region = '<yourRegionId>'
        client = AcsClient(AK, SECRET, Region) 
        ```


**Note:**

-   The commands in the example run in Linux Shell. Windows or DOS users must modify the syntax.
-   ROS SDK for Python is only compatible with Python 2.7 and later.
-   ROS SDK for Python 3.0.0 and later support the 20150901 and 20190910 versions of the ROS API.

## Query the list of available regions

You can use SDK for Python to query the list of available regions.

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

## Create a stack

When you create a stack, you must specify the following parameters:

-   StackName: the name of the stack to be created. The specified name must be unique in a userspace.
-   TimeoutInMinutes: the timeout period for the stack creation request. Unit: minutes. If the stack is not created within the specified period of time, creation times out and fails.
-   TemplateBody: the template based on which the stack is created.
-   TemplateURL: the URL for the file that contains the template body. You must specify one of the TemplateBody and TemplateURL parameters, but you cannot specify both of them.
-   Parameters: the parameters required to create the stack. Keys must be defined in the template.

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
    # If the length of the template body is longer than required, we recommend that you use the TemplateURL parameter to avoid request failures due to excessive length of URLs.
    # You can also add parameters to the HTTP POST request body.
    # request.set_method("POST")
    # request.add_body_params("TemplateBody", template_body)
    request.set_TemplateBody(template_body)
    request.set_Parameterss(params)
    response = client.do_action_with_exception(request)

    return response.decode("utf-8")
```

## Query information about a stack

Enter the ID of the target stack.

```
def get_stack():
    """get descriptions of the stack"""
    request = GetStackRequest()
    request.set_accept_format("json")
    request.set_StackId(stack_id)
    response = client.do_action_with_exception(request)

    return response.decode("utf-8")
```

## Delete a stack

Enter the ID of the target stack.

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
Region = '<yourRegionId>'  # For example, 'cn-beijing' and 'cn-hangzhou'.

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
    # If the length of the template body is longer than required, we recommend that you use the TemplateURL parameter to avoid request failures due to excessive length of URLs.
    # You can also add parameters to the HTTP POST request body.
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
    sleep(3)  # Wait for the stack to be created successfully.
    delete_stack(json.loads(stack)["StackId"])
```

