# Python SDK使用示例（旧） {#concept_wmp_3hv_vgb .task}

本文为您介绍如何使用资源编排服务（ROS）的Python SDK来创建和管理资源栈。

您除了可以在ROS控制台创建资源栈，还可以使用API代码来创建和管理资源栈。

## 准备工作 {#section_zw0_09e_agx .section}

1.  下载及安装Python SDK。 
    1.  使用pip安装aliyun-python-sdk-core。 

        ``` {#codeblock_bgb_b0j_uxi}
        pip install aliyun-python-sdk-core
        ```

        **说明：** aliyun-python-sdk-core是所有阿里云官方Python SDK的公共组件。如果安装过程提示权限错误，可能是因为您没有Python安装路径的写权限。此命令也可以改为`sudo pip install aliyun-python-sdk-core`。

    2.  安装ROS SDK。 

        ``` {#codeblock_181_u46_gss}
        pip install aliyun-python-sdk-ros
        ```

2.  初始化SDK。 
    1.  导入相关的包。 

        ``` {#codeblock_2e0_0nb_xdg .language-python}
        import json
        from aliyunsdkcore import client
        from aliyunsdkros.request.v20150901.CreateStacksRequest import CreateStacksRequest
        from aliyunsdkros.request.v20150901.DescribeStackDetailRequest import DescribeStackDetailRequest
        from aliyunsdkros.request.v20150901.DeleteStackRequest import DeleteStackRequest
        from aliyunsdkros.request.v20150901.DescribeRegionsRequest import DescribeRegionsRequest
        ```

    2.  初始化SDK客户端对象。 

        ``` {#codeblock_pog_x37_238 .language-python}
        AK = '<yourAccessKeyId>'
        SECRET = '<yourAccessKeySecrect>'
        Region = '<yourRegionId>'
        clt = client.AcsClient(AK, SECRET, Region) 
        ```


**说明：** 

-   示例中的命令行都使用Linux的shell，如果您是Windows/DOS用户，则需要根据情况修改。
-   ROS Python SDK依赖Python 2.7以上版本。
-   ROS Python SDK 3.0.0及以上版本，支持v20150901版和v20190910版API。

## 查询可用地域列表 {#section_y0m_opg_ipq .section}

您可以使用Python SDK查询可用地域列表。

``` {#codeblock_9ib_mqc_jap .language-python}
def describe_region():
    """descrbe regions list"""
    req = DescribeRegionsRequest()   # 构造请求对象
    status, headers, body = clt.get_response(req)
    if status == 200:
        regions = json.loads(body)
        return regions
    else:
        return 'Unexpected errors: status=%d, error=%s' % (status, body)
```

## 创建资源栈 {#section_ih4_qyj_w0j .section}

创建资源栈时，您必须指定以下参数：

-   Name：将要创建的资源栈的名称。每个用户空间下的资源栈名称不能重复。
-   TimeoutMins：创建过程如果在指定的时间后不能完成则超时失败。单位为分钟。
-   Template：创建的资源栈使用的模板内容。
-   Parameters：创建的资源栈所需要的参数。需要在模板中定义key。
-   status：请求的返回状态，与HTTP状态码对应。一般2xx表示成功，4xx和5xx表示出错。
-   headers：请求的返回头信息，与HTTP头对应。
-   body：请求的返回内容，与HTTP请求返回的body对应。

``` {#codeblock_301_0qe_05o .language-python}
test_template = '''
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
'''
```

``` {#codeblock_q8r_658_kgv .language-python}
def create_stack():
    """create stack"""
    global result
    req = CreateStacksRequest()
    create_stack_body = dict()   # 构造请求的消息体内容
    test_parameters = {    
        "CidrBlock": "192.168.0.0/16",    
        "VpcName": "test_vpc"
    }
    create_stack_body["Name"] = 'template-test-vpc'
    create_stack_body["Template"] = test_template
    create_stack_body["Parameters"] = test_parameters    
    create_stack_body["TimeoutMins"] = 60
    req.set_content(json.dumps(create_stack_body))
    req.set_content_type('application/json')
    status, headers, body = clt.get_response(req)
    if status == 201:   # 成功时返回状态为201
        result = json.loads(body)
        return result
    else:
        return 'Unexpected errors: status=%d, error=%s' % (status, body)
```

当创建资源栈的请求成功时，返回的body中包含被创建资源栈的ID、Name。

``` {#codeblock_85g_kol_1vc .language-python}
{'Id': '2ffcfe5d-d35c-4f35-858d-dda78922b7c6', 'Name': 'template-test-vpc'}
```

创建资源栈的请求会同步返回，但资源栈内的资源创建是由资源编排服务在后台异步执行的，创建请求返回并不表示所有资源已经创建完成。您可以通过ROS的Web控制台或者API来查询资源栈的创建状态、创建过程中的事件等。

## 查询资源栈 {#section_19l_omu_0kj .section}

您需要输入对应资源栈的ID、Name。

``` {#codeblock_xiq_t51_x22 .language-python}
def describe_stack():
    """describe stack"""
    req = DescribeStackDetailRequest()
    req.set_StackName(result['Name'])
    req.set_StackId(result['Id'])
    status, headers, body = clt.get_response(req)
    if status == 200:   # 成功时返回状态为200
        res = json.loads(body)
        if res['Status'] != 'CREATE_IN_PROGRESS':  # 资源栈的状态不是创建中时
            return res
        else:
            return describe_stack()
    else:
        return 'Unexpected errors: status=%d, error=%s' % (status, body)
```

## 删除资源栈 {#section_l5q_71n_en5 .section}

您需要输入对应资源栈的ID、Name。

``` {#codeblock_voq_yr9_79d .language-python}
def delete_stack():
    """delete stack"""
    req = DeleteStackRequest()
    req.set_StackName(result['Name'])
    req.set_StackId(result['Id'])
    status, headers, body = clt.get_response(req)
    if status == 204:   # 成功时返回状态为204
        return body
    else:
        return 'Unexpected errors: status=%d, error=%s' % (status, body)
```

``` {#codeblock_hj1_lsp_9w7 .language-python}
import json
from aliyunsdkcore import client
from aliyunsdkros.request.v20150901.CreateStacksRequest import CreateStacksRequest
from aliyunsdkros.request.v20150901.DescribeStackDetailRequest import DescribeStackDetailRequest
from aliyunsdkros.request.v20150901.DeleteStackRequest import DeleteStackRequest
from aliyunsdkros.request.v20150901.DescribeRegionsRequest import DescribeRegionsRequest

AK = '<yourAccessKeyId>'
SECRET = '<yourAccessKeySecret>'
Region = '<yourRegionId>'   # 例如：'cn-beijing'、'cn-hangzhou'


clt = client.AcsClient(AK, SECRET, Region)

test_template = '''
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
'''


def describe_region():
    """descrbe regions list """
    req = DescribeRegionsRequest()
    status, headers, body = clt.get_response(req)
    if status == 200:
        regions = json.loads(body)
        return regions
    else:
        return 'Unexpected errors: status=%d, error=%s' % (status, body)


def create_stack():
    """create stack"""
    global result
    req = CreateStacksRequest()
    create_stack_body = dict()
    test_parameters = {
        "CidrBlock": "192.168.0.0/16",
        "VpcName": "test_vpc"
    }
    create_stack_body["Name"] = 'template-test-vpc'
    create_stack_body["Template"] = test_template
    create_stack_body["Parameters"] = test_parameters
    create_stack_body["TimeoutMins"] = 60
    req.set_content(json.dumps(create_stack_body))
    req.set_content_type('application/json')
    status, headers, body = clt.get_response(req)
    if status == 201:
        result = json.loads(body)
        return result
    else:
        return 'Unexpected errors: status=%d, error=%s' % (status, body)


def describe_stack():
    """describe stack"""
    req = DescribeStackDetailRequest()
    req.set_StackName(result['Name'])
    req.set_StackId(result['Id'])
    status, headers, body = clt.get_response(req)
    if status == 200:
        res = json.loads(body)
        if res['Status'] != 'CREATE_IN_PROGRESS':
            return res
        else:
            return describe_stack()
    else:
        return 'Unexpected errors: status=%d, error=%s' % (status, body)


def delete_stack():
    """delete stack"""
    req = DeleteStackRequest()
    req.set_StackName(result['Name'])
    req.set_StackId(result['Id'])
    status, headers, body = clt.get_response(req)
    if status == 204:
        return body
    else:
        return 'Unexpected errors: status=%d, error=%s' % (status, body)


if __name__ == '__main__':
    describe_region()
    create_stack()
    describe_stack()
    delete_stack()
```

