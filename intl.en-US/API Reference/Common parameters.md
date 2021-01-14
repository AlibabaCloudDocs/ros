# Common parameters

This topic describes the common request and response parameters.

## Common request parameters

The following table describes common request parameters that must be used when you call ROS API operations by sending GET requests over URLs.

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. For more information about valid values of this parameter, see [List of operations by function](/intl.en-US/API Reference/List of operations by function.md).|
|AccessKeyId|String|Yes|The AccessKey ID provided to you by Alibaba Cloud.|
|Signature|String|Yes|The signature string of the current request. For more information about how signatures are calculated, see [Request signatures](/intl.en-US/API Reference/Request signatures.md).|
|SignatureMethod|String|Yes|The encryption method of the signature string. Set the value to HMAC-SHA1.|
|SignatureVersion|String|Yes|The version of the signature encryption algorithm. Set the value to 1.0.|
|SignatureNonce|String|Yes|A unique, random number used to prevent replay attacks. You must use different numbers for different requests.|
|Timestamp|String|Yes|The timestamp of the request. Specify the time in the ISO 8601 standard in the yyyy-MM-ddTHH:mm:ssZ format. The time must be in UTC.|
|Version|String|Yes|The version number of the API. The value must be in the YYYY-MM-DD format. Set the value to 2019-09-10.|
|Format|String|No|The format in which to return the response. Default value: xml. Valid values: -   json
-   xml |

## Common response parameters

|Parameter|Type|Description|
|:--------|:---|:----------|
|RequestId|String|The ID of the request. **Note:** Every response returns a unique RequestID regardless of whether the call is successful. |

## Sample success responses

`XML` format

```
<XXXXXXResponse>
        <RequestId type="string">BA4C8BF3-482E-4B03-A1E3-C60DB7A95DE0</RequestId>
</XXXXXXResponse>
```

`JSON` format

```
{
   "RequestId": "BA4C8BF3-482E-4B03-A1E3-C60DB7A95DE0",
}
```

