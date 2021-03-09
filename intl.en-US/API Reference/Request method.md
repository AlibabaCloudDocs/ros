# Request method

This topic describes how to make API requests and is intended for users who initiate HTTP or HTTPS GET requests by calling API operations based on URLs.

If you use [SDKs](https://github.com/aliyun?spm=a2c4g.11186623.2.7.7ac73290vjdB7q), Alibaba Cloud CLI \(see [What is Alibaba Cloud CLI?]()\) or [OpenAPI Developer Portal](https://next.api.aliyun.com/api/ROS/2019-09-10), skip this topic.

ROS API operations are called by sending HTTP or HTTPS requests to the ROS API endpoint. The request URL consists of multiple parameters with a fixed [Request syntax](#section_ow0_qmi_l2m). The URL consists of [Common parameters](/intl.en-US/API Reference/Common parameters.md), your signature \(see [Request signatures](/intl.en-US/API Reference/Request signatures.md)\) and parameters of a specific API. Unencoded sample URL requests for every operation are provided for your reference. You must encode your URL before submitting a request. After the authentication process is complete based on your signature, the results are returned to you. Response parameters are displayed if the call is successful, and an error message is displayed if the call fails. You can troubleshoot issues based on the common error codes and API operation-specific error codes.

## Endpoint

The endpoint of the ROS API is ros.aliyuncs.com.

## Protocols

You can send requests over HTTP or HTTPS. We recommend that you send requests over HTTPS to enhance security.

## Request syntax

You can call ROS API operations by sending HTTP or HTTPS GET requests based on URLs. Each URL must include request parameters. This topic explains the structure of HTTP or HTTPS GET requests and provides the endpoint of ROS.

The following example demonstrates an unencoded URL request to call the [ListStacks](/intl.en-US/API Reference/Stack operations/ListStacks.md) operation:

```
http(s)://ros.aliyuncs.com/? Action=ListStacks
&RegionId=cn-hangzhou
&<Common request parameters>
```

where:

-   `http(s)` specifies the protocol used for the request.
-   `ros.aliyuncs.com` specifies the endpoint of ROS.
-   `Action=ListStacks` specifies the operation to be called. `RegionId=cn-hangzhou` is specific to [ListStacks](/intl.en-US/API Reference/Stack operations/ListStacks.md).
-   `<Common request parameters>` are common parameters defined in the system.

## Request encoding

The request and response are encoded in UTF-8.

