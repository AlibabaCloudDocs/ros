# Examples of using the ROS SDK {#concept_wmp_3hv_vgb .concept}

This topic describes how to manage Resource Orchestration Services \(ROS\) resource stacks by using an SDK.

## Overview {#section_bjf_s3v_vgb .section}

You can create and manage resource stacks by using the ROS console or APIs. This topic shows how to use the Python SDK to manage ROS resource stacks, including the following operations:

-   View the list of available regions.
-   Create a resource stack.
-   View the status of a resource stack.
-   Delete a resource stack.

## Before you start {#section_vwd_mjv_vgb .section}

**Download and install the Python SDK**

**Note:** 

-   The commands in the example run in Linux Shell. Windows or DOS users need to modify the syntax accordingly.
-   The ROS Python SDK is only compatible with Python 2.7 and later versions.

Use pip to install aliyun-python-sdk-core:

`pip install aliyun-python-sdk-core`

aliyun-python-sdk-core is included in all Python SDKs of Alibaba Cloud. If the installation fails and you receive an error message, a likely reason is that the user does not have the write access permission to the Python installation path. In this case, modify the preceding command as follows. Modify the command similarly in case you receive a permission error message when you install the ROS SDK.

`sudo pip install aliyun-python-sdk-core`

Install the ROS SDK:

`pip install aliyun-python-sdk-ros`

**Initialize the SDK**

Import the required libraries:

```language-python
import json
from aliyunsdkcore import client
from aliyunsdkros.request.v20150901. CreateStacksRequest import CreateStacksRequest
from aliyunsdkros.request.v20150901. DescribeStackDetailRequest import DescribeStackDetailRequest
from aliyunsdkros.request.v20150901. DeleteStackRequest import DeleteStackRequest
from aliyunsdkros.request.v20150901. DescribeRegionsRequest import DescribeRegionsRequest
```

Initialize the SDK client: When creating the client instance, you must specify the Region ID, AccessKey ID, and AccessKey Secret parameters.

```language-python
AK = '<Your Access Key Id>'
SECRET = '<Your Access Key Secrect>'
Region = '<Region Id>'
clt = client.AcsClient(AK, SECRET, Region) 
```

## Procedure {#section_dwc_4kv_vgb .section}

**View the list of available regions**

Run the following commands to view the list of available regions.

```language-python
def describe_region():
    """descrbe regions list"""
    req = DescribeRegionsRequest()   #This line is used to construct the request object.
    status, headers, body = clt.get_response(req)
    if status == 200:
        regions = json.loads(body)
        return regions
    else:
        return 'Unexpected errors: status=%d, error=%s' % (status, body)
```

**Create a resource stack**

To create a resource stack, you must specify the stack parameters.

-   Name indicates the name of the resource stack to be created. The specified name must be unique in the same userspace.
-   TimeoutMins indicates the specified timeout for stack creation, measured in minutes. A failure will occur if the stack cannot be created within the specified time.
-   Template indicates the template based on which the stack is created.
-   status indicates the response status of the request in the form of HTTP response status code. Generally, 2xx indicates success, and 4xx or 5xx indicate errors.
-   headers indicate the HTTP response headers, which are the message headers returned in response to receiving an HTTP request.
-   body indicates the HTTP response body, which is the message body returned in response to receiving an HTTP request.

```language-python
def create_stack():
    """create stack"""
    global result
    req = CreateStacksRequest()
    create_stack_body = dict()   #This line is used to create the body of the request.
    create_stack_body["Name"] = 'empty-template-test'
    create_stack_body["Template"] = '{"ROSTemplateFormatVersion": "2015-09-01"}'
    create_stack_body["TimeoutMins"] = 60
    req.set_content(json.dumps(create_stack_body))
    req.set_content_type('application/json')
    status, headers, body = clt.get_response(req)
    if status == 201:   #The status code 201 indicates that the request has been been processed.
        token = json.loads(body)
        return result
    else:
        return 'Unexpected errors: status=%d, error=%s' % (status, body)
```

If the request for creating a stack has been processed, then the returned body includes the stack ID and name.

```language-python
{'Id': '2ffcfe5d-d35c-4f35-858d-dda78922b7c6', 'Name': 'empty-template-test'}
```

The response is returned at the same time the request is processed. However, it does not mean that the resource stack has been created because the creation progress is running in the background using ROS. You can use the ROS console or APIs to view the stack status and events.

**View the status of a resource stack**

To view the status of a resource stack, you must provide the stack ID and name. You can obtain the stack ID and name from the response after you have submitted the request for creating a stack.

```language-python
def describe_stack():
    """describe stack"""
    req = DescribeStackDetailRequest()
    req.set_StackName(result['Name'])
    req.set_StackId(result['Id'])
    status, headers, body = clt.get_response(req)
    if status == 200:   #The status code 200 indicates that the request has been received and is being processed.
        res = json.loads(body)
        if res['Status'] ! = 'CREATE_IN_PROGRESS':  #This line describes the condition that the stack status is not "CREATE_IN_PROGRESS".
            return res
        else:
            return describe_stack()
    else:
        return 'Unexpected errors: status=%d, error=%s' % (status, body)
```

**Delete a resource stack**

To delete a resource stack, you must provide the stack ID and name. You can obtain the stack ID and name from the response after you have submitted the request for creating a stack.

```language-python
def delete_stack():
    """delete stack"""
    req = DeleteStackRequest()
    req.set_StackName(result['Name'])
    req.set_StackId(result['Id'])
    status, headers, body = clt.get_response(req)
    if status == 204:   #The status code 204 indicates that the request has been fulfilled.
        return body
    else:
        return 'Unexpected errors: status=%d, error=%s' % (status, body)
```

**Sample code**

You can provide your account and stack details to perform the previous operations. The sample code is described as follows.

```language-python
import json
from aliyunsdkcore import client
from aliyunsdkros.request.v20150901. CreateStacksRequest import CreateStacksRequest
from aliyunsdkros.request.v20150901. DescribeStackDetailRequest import DescribeStackDetailRequest
from aliyunsdkros.request.v20150901. DeleteStackRequest import DeleteStackRequest
from aliyunsdkros.request.v20150901. DescribeRegionsRequest import DescribeRegionsRequest

AK = '<Your Access Key Id>'
SECRET = '<Your Access Key Secrect>'
Region = '<Region Id>'   #Specify the region parameter in the following format: "cn-beijing",  "cn-hangzhou".


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
        if res['Status'] ! = 'CREATE_IN_PROGRESS':
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

