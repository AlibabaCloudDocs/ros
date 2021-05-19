# Make API requests

To call the Resource Orchestration Service \(ROS\) API, you must send HTTP GET requests to the endpoint of the ROS API. You must add the request parameters that correspond to the API operation being called. After you call the API operation, the system returns a response. The request and response are both encoded in UTF-8.

## Request structure

ROS API operations use the RPC protocol. You can call ROS API operations by sending HTTP GET requests.

The following example describes the request syntax of an ROS API request:

```
http(s)://Endpoint/?Action=xx&Parameters
```

Where,

-   Endpoint
    -   Public endpoint: ros.aliyuncs.com. All regions are supported.
    -   VPC endpoint: ros.vpc-proxy.aliyuncs.com. The following table describes the supported regions.

        |Region|Region ID|
        |------|---------|
        |China \(Hangzhou\)|cn-hangzhou|
        |China \(Shanghai\)|cn-shanghai|
        |China \(Qingdao\)|cn-qingdao|
        |China \(Beijing\)|cn-beijing|
        |China \(Zhangjiakou\)|cn-zhangjiakou|
        |China \(Hohhot\)|cn-huhehaote|
        |China \(Ulanqab\)|cn-wulanchabu|
        |China \(Shenzhen\)|cn-shenzhen|
        |China \(Heyuan\)|cn-heyuan|
        |China \(Guangzhou\)|cn-guangzhou|
        |China \(Chengdu\)|cn-chengdu|
        |China \(Hong Kong\)|cn-hongkong|
        |US \(Silicon Valley\)|us-west-1|
        |US \(Virginia\)|us-east-1|
        |Singapore|ap-southeast-1|
        |Australia \(Sydney\)|ap-southeast-2|
        |Malaysia \(Kuala Lumpur\)|ap-southeast-3|
        |Indonesia \(Jakarta\)|ap-southeast-5|
        |India \(Mumbai\)|ap-south-1|
        |Japan \(Tokyo\)|ap-northeast-1|
        |Germany \(Frankfurt\)|eu-central-1|
        |UK \(London\)|eu-west-1|
        |China East 1 Finance|cn-hangzhou-finance|
        |China East 2 Finance|cn-shanghai-finance|
        |China South 1 Finance|cn-shenzhen-finance|
        |China North 2 Ali Gov 1|cn-north-2-gov-1|

-   Action

    The operation that you want to perform. For example, you can query the list of stacks by calling [ListStacks](/intl.en-US/API Reference/Stack operations/ListStacks.md).

-   Parameters

    The request parameters for the operation. Separate multiple parameters with ampersands \(&\).

    Request parameters include both common parameters and operation-specific parameters. Common parameters include information such as the API version number and authentication information. For more information, see [Common parameters](/intl.en-US/API Reference/Common parameters.md).


The following example demonstrates how to call the [ListStacks](/intl.en-US/API Reference/Stack operations/ListStacks.md) operation to query the list of stacks:

```
http(s)://ros.aliyuncs.com/?Action=ListStacks
&RegionId=cn-hangzhou
&Format=xml
&Version=2019-09-10
&Signature=Pc5WB8gokVn0xfeu%2FZV%2BiNM1dg****
&SignatureMethod=HMAC-SHA1
&SignatureNonce=1521552885****
&SignatureVersion=1.0
&AccessKeyId=LTAI4GENiH2u8MVj7Khh****
&Timestamp=2020-06-01T12:00:00Z
```

