# Query regions {#concept_50086_zh .concept}

Call /regions by GET method to query the region list of Alibaba Cloud.

## Request parameters {#section_sxw_zdb_mfb .section}

None.

## Response parameters {#section_ffk_b2b_mfb .section}

The system returns the region list.

|Name|Type|Description|
|----|----|-----------|
|Regions|List|List of all regions.|

## Error codes {#section_umq_d2b_mfb .section}

|Error code|Description|HTTP status code|Meaning|
|----------|-----------|----------------|-------|
|InternalError|Server error|500|Server-side unknown exception.|

## Example {#section_mn3_g2b_mfb .section}

**Request example**

```language-json
GET http://ros.aliyuncs.com/regions HTTP/1.1
x-acs-signature-method: HMAC-SHA1
Authorization: acs ACSTQDkNtSMrZtwL:8xKxVMy4xi2zgXUNLERRiZbgapg=
Date: Fri, 11 Sep 2015 05:30:11 GMT
x-acs-signature-version: 1.0
x-sdk-client: Java/2.0.0
Accept: application/octet-stream
x-acs-version: 2015-09-01
Cache-Control: no-cache
Pragma: no-cache
User-Agent: Java/1.6.0_27
Host: ros.aliyuncs.com
Connection: keep-alive




```

**Response example**

```language-json
HTTP/1.1 200 OK
Date: Fri, 11 Sep 2015 05:30:12 GMT
Content-Type: application/json; charset=UTF-8
Content-Length: 1694
Connection: close
Vary: Accept-Encoding
Access-Control-Allow-Origin: *
Access-Control-Allow-Methods: POST, GET, OPTIONS
Access-Control-Allow-Headers: X-Requested-With, X-Sequence, _aop_secret, _aop_signature
Access-Control-Max-Age: 172800
X-Acs-Request-Id: A21A4B12-CCD7-42F0-9A62-DE8347D88385
Server: Jetty(7.2.2.v20101205)

{
    "Regions":[
        {
            "LocalName":"China South 1 (Shenzhen)",
            "RegionId":"cn-shenzhen"
        },
        {
            "LocalName":"Singapore",
            "RegionId":"ap-southeast-1"
        },
        {
            "LocalName":"China North 1 (Qingdao)",
            "RegionId":"cn-qingdao"
        },
        {
            "LocalName": "China North 2 (Beijing)"
            "RegionId":"cn-beijing"
        },
        {
            "LocalName":"China East 2 (Shanghai)",
            "RegionId":"cn-shanghai"
        },
        {
            "LocalName":"US East 1 (Virginia)",
            "RegionId":"us-east-1"
        },
        {
            "LocalName":"Hong Kong",
            "RegionId":"cn-hongkong"
        },
        {
            "LocalName":"Middle East 1 (Dubai)",
            "RegionId":"me-east-1"
        },
        {
            "LocalName": "Asia Pacific SE 2 (Sydney)"
            "RegionId":"ap-southeast-2"
        },
        {
            "LocalName":"China East 1 (Hangzhou)",
            "RegionId":"cn-hangzhou"
        },
        {
            "LocalName":"Germany 1 (Frankfurt)",
            "RegionId":"eu-central-1"
        },
        {
            "LocalName":"Asia Pacific NE 1 (Tokyo)",
            "RegionId":"ap-northeast-1"
        },
        {
            "LocalName":"US West 1 (Silicon Valley)",
            "RegionId":"us-west-1"
        }
    ]
}


```

