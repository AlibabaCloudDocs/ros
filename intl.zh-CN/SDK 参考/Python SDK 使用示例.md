# Python SDK 使用示例 {#concept_wmp_3hv_vgb .concept}

本文为您介绍ROS如何使用Python SDK 管理资源栈。

## 背景信息 {#section_bjf_s3v_vgb .section}

您除了可以在 ROS控制台创建资源栈外，还可以使用 API 代码来创建和管理资源栈。接下来介绍ROS如何使用Python SDK 管理资源栈。

-   查询可用地域列表
-   创建资源栈
-   查询资源栈
-   删除资源栈

## 使用SDK管理资源栈的准备工作 {#section_vwd_mjv_vgb .section}

**下载及安装Python SDK**

**说明：** 

-   示例中的命令行都使用Linux的shell，Windows/DOS用户需要根据情况修改。
-   ROS Python SDK依赖Python 2.7以上版本。

首先，使用pip安装aliyun-python-sdk-core：

 `pip install aliyun-python-sdk-core` 

aliyun-python-sdk-core是所有阿里云官方Python SDK的公共组件。如果安装过程提示权限错误，可能是因为当前用户没有Python安装路径的写权限，上面的命令可以改成下面这样，后面的例子类似：

 `sudo pip install aliyun-python-sdk-core` 

接下来，安装ROS SDK：

 `pip install aliyun-python-sdk-ros` 

**初始化SDK**

导入必要的库：

``` {#codeblock_9dz_daj_ni9 .language-python}
import json
from aliyunsdkcore import client
from aliyunsdkros.request.v20150901.CreateStacksRequest import CreateStacksRequest
from aliyunsdkros.request.v20150901.DescribeStackDetailRequest import DescribeStackDetailRequest
from aliyunsdkros.request.v20150901.DeleteStackRequest import DeleteStackRequest
from aliyunsdkros.request.v20150901.DescribeRegionsRequest import DescribeRegionsRequest
```

初始化SDK客户端对象：在创建Client实例时，您需要获取Region ID、AccessKey ID和AccessKey Secret。

``` {#codeblock_3v8_61p_i5k .language-python}
AK = '<Your Access Key Id>'
SECRET = '<Your Access Key Secrect>'
Region = '<Region Id>'
clt = client.AcsClient(AK, SECRET, Region) 
```

## 使用SDK管理资源栈的实施步骤 {#section_dwc_4kv_vgb .section}

**查询可用地域列表**

可用于查询可用地域列表。

``` {#codeblock_6t1_pme_aeh .language-python}
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

**创建资源栈**

创建资源栈，您可提供自己的资源栈信息来创建资源栈。

-   Name是将要创建的资源栈的名称，每个用户空间下的资源栈名称不能重复。
-   TimeoutMins是指创建过程如果在指定的时间后不能完成则超时失败，单位为分钟。
-   Template表示创建的资源栈使用的模板内容。
-   status表示请求的返回状态，与HTTP状态码对应，一般2xx表示成功，4xx和5xx表示出错。
-   headers表示请求的返回头信息，与HTTP头对应。
-   body表示请求的返回内容，与HTTP请求返回的body对应。

``` {#codeblock_emd_1vr_crc .language-python}
def create_stack():
    """create stack"""
    global result
    req = CreateStacksRequest()
    create_stack_body = dict()   # 构造请求的消息体内容
    create_stack_body["Name"] = 'empty-template-test'
    create_stack_body["Template"] = '{"ROSTemplateFormatVersion": "2015-09-01"}'
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

当创建资源栈的请求成功时，返回的body中包含被创建资源栈的ID、Name，如下所示:

``` {#codeblock_v51_h2s_mom .language-python}
{'Id': '2ffcfe5d-d35c-4f35-858d-dda78922b7c6', 'Name': 'empty-template-test'}
```

创建资源栈的请求会同步返回，但资源栈内的资源创建是由资源编排服务在后台异步执行的，所以到创建请求返回，并不表示所有资源已经创建完成。我们可以通过ROS的Web控制台或者API来查询堆栈的创建状态、创建过程中的事件等等。

**查询资源栈**

查询资源栈，您可提供自己的资源栈信息来查询资源栈。需要提供创建资源栈返回的资源栈ID、 Name。

``` {#codeblock_5j4_73l_d83 .language-python}
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

**删除资源栈**

删除资源栈，您可提供自己的资源栈信息来删除资源栈。需要提供创建资源栈返回的资源栈ID、 Name。

``` {#codeblock_72d_cwy_u9k .language-python}
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

**完整的代码**

完整的代码如下，您可提供自己的账号信息及资源栈信息进行设置。

``` {#codeblock_vap_ath_xgq .language-python}
import json
from aliyunsdkcore import client
from aliyunsdkros.request.v20150901.CreateStacksRequest import CreateStacksRequest
from aliyunsdkros.request.v20150901.DescribeStackDetailRequest import DescribeStackDetailRequest
from aliyunsdkros.request.v20150901.DeleteStackRequest import DeleteStackRequest
from aliyunsdkros.request.v20150901.DescribeRegionsRequest import DescribeRegionsRequest

AK = '<Your Access Key Id>'
SECRET = '<Your Access Key Secrect>'
Region = '<Region Id>'   # 如：'cn-beijing'、'cn-hangzhou'


clt = client.AcsClient(AK, SECRET, Region)


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
    create_stack_body["Name"] = 'empty-template-test000000'
    create_stack_body["Template"] = '{"ROSTemplateFormatVersion": "2015-09-01"}'
    create_stack_body["Parameters"] = dict()
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

