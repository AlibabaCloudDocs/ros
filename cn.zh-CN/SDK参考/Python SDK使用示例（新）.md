# Python SDK使用示例（新） {#concept_2118428 .concept}

您除了可以在ROS控制台创建资源栈外，还可以使用API代码来创建和管理资源栈。

## 准备工作 {#section_59d_1qc_c7v .section}

1.  下载及安装Python SDK。

    1.  使用pip安装aliyun-python-sdk-core。

        ``` {#codeblock_5ft_al5_n0x}
        pip install aliyun-python-sdk-core
        ```

        **说明：** aliyun-python-sdk-core是所有阿里云官方Python SDK的公共组件。如果安装过程提示权限错误，可能是因为当前用户没有Python安装路径的写权限。此命令也可以改为`sudo pip install aliyun-python-sdk-core`。

    2.  安装ROS SDK。

        ``` {#codeblock_9dt_b86_fz2}
        pip install aliyun-python-sdk-ros
        ```

    **说明：** 

    -   示例中的命令行都使用Linux的shell，Windows/DOS用户需要根据情况修改。
    -   ROS Python SDK依赖Python 2.7以上版本。
    -   ROS Python SDK3.0.0及以上版本，支持v20150901和v20190910版API。
2.  初始化SDK。
    1.  导入相关的包。

        ``` {#codeblock_wkt_wbo_16c .language-python}
        from aliyunsdkcore.client import AcsClient
        from aliyunsdkros.request.v20190910.CreateStackRequest import CreateStackRequest
        from aliyunsdkros.request.v20190910.GetStackRequest import GetStackRequest
        from aliyunsdkros.request.v20190910.DeleteStackRequest import DeleteStackRequest
        from aliyunsdkros.request.v20190910.DescribeRegionsRequest import DescribeRegionsRequest
        from aliyunsdkros.request.v20190910.ListStacksRequest import ListStacksRequest
        ```

    2.  初始化SDK客户端对象。

        ``` {#codeblock_4ls_do3_pus .language-python}
        AK = '<Your Access Key Id>'
        SECRET = '<Your Access Key Secrect>'
        Region = '<Region Id>'
        client = AcsClient(AK, SECRET, Region) 
        ```


## 查询可用地域列表 {#section_ph2_oh4_7fe .section}

您可以使用SDK查询可用地域列表。

``` {#codeblock_e1w_gs2_2k1 .language-python}
def describe_region():
    """describe regions list """
    request = DescribeRegionsRequest()
    request.set_accept_format('json')
    response = client.do_action_with_exception(request)

    return response.decode('utf8')
```

## 创建资源栈 {#section_fyl_qv7_3l2 .section}

您可以提供自己的资源栈信息来创建资源栈。创建资源栈时必须指定以下参数：

-   StackName是将要创建的资源栈的名称，每个用户空间下的资源栈名称不能重复。
-   TimeoutInMinutes是指创建过程如果在指定的时间后不能完成则超时失败，单位为分钟。
-   TemplateBody表示创建的资源栈使用的模板内容。
-   TemplateURL表示包含模板主体的文件的位置，必须指定TemplateBody或TemplateURL，但不能同时指定两者。
-   Parameters表示创建的资源栈所需要的参数。需要在模板中定义key。

``` {#codeblock_np2_s3f_vcv .language-python}
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

``` {#codeblock_k55_anm_4kt .language-python}
def create_stack():
    """create stack"""
    request = CreateStackRequest()
    request.set_accept_format('json')
    request.set_StackName(stack_name)
    request.set_TimeoutInMinutes(timeout)
    request.set_TemplateBody(template_body)
    request.set_Parameterss(params)
    response = client.do_action_with_exception(request)

    return response.decode('utf8')
```

## 查询资源栈 {#section_4rf_xe7_nr8 .section}

您可以提供自己的资源栈信息来查询资源栈。需要提供对应资源栈的ID。

``` {#codeblock_q5g_hkw_7my .language-python}
def get_stack():
    """get descriptions of the stack"""
    request = GetStackRequest()
    request.set_accept_format('json')
    request.set_StackId(stack_id)
    response = client.do_action_with_exception(request)

    return response.decode('utf8')
```

## 删除资源栈 {#section_r2f_gdy_f54 .section}

您可以提供自己的资源栈信息来删除资源栈。需要提供对应资源栈的ID。

``` {#codeblock_c3i_j2f_ybm .language-python}
def delete_stack():
    """delete stack"""
    request = DeleteStackRequest()
    request.set_accept_format('json')
    request.set_StackId(stack_id)
    response = client.do_action_with_exception(request)

    return response.decode('utf8')
```

## 示例代码 {#section_mzq_r4w_ydp .section}

您可以提供自己的账号信息及资源栈信息进行设置。

``` {#codeblock_uma_4jx_qe1 .language-python}
import json
from time import sleep
from aliyunsdkcore.client import AcsClient
from aliyunsdkros.request.v20190910.CreateStackRequest import CreateStackRequest
from aliyunsdkros.request.v20190910.GetStackRequest import GetStackRequest
from aliyunsdkros.request.v20190910.DeleteStackRequest import DeleteStackRequest
from aliyunsdkros.request.v20190910.DescribeRegionsRequest import DescribeRegionsRequest
from aliyunsdkros.request.v20190910.ListStacksRequest import ListStacksRequest


AK = '<Your Access Key Id>'
SECRET = '<Your Access Key Secrect>'
Region = '<Region Id>'  # 如：'cn-beijing'、'cn-hangzhou'

client = AcsClient(AK, SECRET, Region)


def describe_region():
    """describe regions list """
    request = DescribeRegionsRequest()
    request.set_accept_format('json')
    response = client.do_action_with_exception(request)
    return response.decode('utf8')


def create_stack(stack_name, timeout, template_body, params=[]):
    """create stack"""
    request = CreateStackRequest()
    request.set_accept_format('json')
    request.set_StackName(stack_name)
    request.set_TimeoutInMinutes(timeout)
    request.set_TemplateBody(template_body)
    response = client.do_action_with_exception(request)
    return response.decode('utf8')


def get_stack(stack_id):
    """get descriptions of the stack"""
    request = GetStackRequest()
    request.set_accept_format('json')
    request.set_StackId(stack_id)
    response = client.do_action_with_exception(request)
    return response.decode('utf8')


def delete_stack(stack_id):
    """delete stack"""
    request = DeleteStackRequest()
    request.set_accept_format('json')
    request.set_StackId(stack_id)
    response = client.do_action_with_exception(request)
    return response.decode('utf8')


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

