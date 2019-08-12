# ALIYUN::CDN::DomainConfig {#concept_rs1_3s3_fhb .concept}

ALIYUN::CDN::DomainConfig is used to add multiple domain name settings.

## Syntax {#section_xyg_tn2_lfb .section}

```language-json
{
  "Type": "ALIYUN::CDN::DomainConfig",
  "Properties": {
    "Functions": String,
    "DomainNames": String
  }
}
```

## Properties {#section_cgd_53n_4fb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|Functions|String|Yes|No|The list of functions.|None|
|DomainNames|String|Yes|No|The accelerated domain names. Separate multiple domain names by using commas \(,\).|None|

## Functions syntax { .section}

```language-json
[{
  "functionArgs": [{
    "argName": "domain_name",
    "argValue": "api.hellodtworld.com"
  }],
  "functionName": "set_req_host_header"
}]
```

You can set certain functions, such as filetype\_based\_ttl\_set, in multiple configuration records. To update one of the configuration records, use the configId parameter to identify that record.

```language-json
[{
  "functionArgs": [{
    "argName": "file_type",
    "argValue": "jpg"
  }, {
    "argName": "ttl",
    "argValue": "18"
  }, {
    "argName": "weight",
    "argValue": "30"
  }],
  "functionName": "filetype_based_ttl_set",
  "configId": 5068995
}]
```

## Functions { .section}

All parameter values are of the string type.

|Name|Description|Parameter|
|----|-----------|---------|
|referer\_white\_list\_set|Specifies and enables the referer whitelist.| -   refer\_domain\_allow\_list: the whitelist of domain names. Multiple domain names are separated by commas \(,\).
-   allow\_empty: indicates whether an empty referer is allowed. Valid values: on and off.

 |
|referer\_black\_list\_set|Specifies and enables the referer blacklist.| -   refer\_domain\_deny\_list: the blacklist of domain names. Multiple domain names are separated by commas \(,\).
-   allow\_empty: indicates whether an empty referer is allowed. Valid values: on and off.

 |
|filetype\_based\_ttl\_set|Specifies the validity period of files.| -   ttl: the validity period of the cached content. Unit: second.
-   file\_type: the file type. You can specify multiple file types and separate them by using commas \(,\). For example, txt,jpg.
-   weight: the weight of a file in the cache. Valid values: 1 to 199.

 |
|path\_based\_ttl\_set|Specifies the validity period of a directory.| -   ttl: the validity period of the cached content. Unit: second.
-   path: the directory, which must start with a forward slash \(/\).
-   weight: the weight of a directory in the cache. Valid values: 1 to 199.

 |
|oss\_auth|Authenticates the access to an OSS bucket.|oss\_bucket\_id: the ID of your bucket.|
|ip\_black\_list\_set|Specifies the IP address blacklist.|ip\_list: the list of IP addresses. Multiple IP addresses are separated by commas \(,\).|
|ip\_allow\_list\_set|Specifies the IP address whitelist.|ip\_list: the list of IP addresses. Multiple IP addresses are separated by commas \(,\).|
|ip\_white\_list\_set|Specifies the list of IP addresses that are not blocked by the TMD system.|ip\_list: the list of IP addresses. Multiple IP addresses are separated by commas \(,\).|
|error\_page|Redirects an error page to another specified page.| -   error\_code: the error code.
-   rewrite\_page: the page to which the error page is to be redirected.

 |
|set\_req\_host\_header|Modifies the custom header of the origin host.|domain\_name: the header of the origin host.|
|set\_hashkey\_args|Ignores the specified URL parameters.| -   hashkey\_args: the list of reserved parameters. Multiple parameters are separated by commas \(,\).
-   disable: indicates whether to ignore all parameters. A value of on indicates that all parameters are ignored. A value of off indicates that none of the parameters are ignored.

 |
|ali\_remove\_args|Removes the specified URL parameters.| -   ali\_remove\_args: required. It removes the specified parameters and uses the remaining ones as the URL parameters of the hashkey. Multiple parameters are separated by spaces.
-   keep\_oss\_args: indicates whether to reserve all parameters. Valid values: on and off. A value of on indicates that all parameters are reserved during the back-to-origin process. A value of off indicates that parameters are reserved for the cache hashkey.

 |
|aliauth|Enables Alibaba authentication.| -   Auth\_type: the authentication type. Valid values: no\_auth, type\_a, type\_b, and type\_c.
-   auth\_key1: the cryptographic key 1.
-   auth\_key2: the cryptographic key 2.
-   ali\_auth\_delta: the custom buffer time of authentication.

 |
|set\_resp\_header|Specifies the response header, which is user-accessible in a browser.| -   key: the response header.
-   value: the content of the response header. Enter null if you want to delete the header.

 |
|https\_force|Forces redirection of HTTP requests to HTTPS.|Enable: indicates whether to enable the function. Valid values: on and off.|
|http\_force|Forces redirection of HTTPS requests to HTTP.|Enable: indicates whether to enable the function. Valid values: on and off.|
|https\_option|Specifies the basic parameters of HTTPS.|http2: indicates whether to enable HTTP/2 support. Valid values: on and off.|
|l2\_oss\_key|Enables private key authentication to access an OSS bucket in L2 back-to-origin requests.|private\_oss\_auth: indicates whether to authenticate the access to a private OSS bucket. Valid values: on and off.|
|forward\_scheme|Specifies the protocol of the origin.| -   enable: indicates whether to enable the function. Valid values: on and off.
-   scheme\_origin: the protocol of the origin. Valid values: http, https, and follow.

 |
|green\_manager|Enables pornographic image detection.|enable: indicates whether to enable the function. Valid values: on and off.|
|tmd\_signature|Specifies TMD custom rules.| -   name: the name of the rule. It must be unique within the domain name.
-   path: the URI path. You can specify duplicate URI paths. However, you must verify their validity.
-   pathType: the matching rule. Valid values: 0 for prefix match and 1 for exact match.
-   Interval: the interval during which the data is monitored. Unit: second. The interval must be greater than or equal to 10 seconds.
-   count: the number of visits from an IP address.
-   action: the operation to be performed after specified conditions are met. Valid values: 0 for access blocking and 1 for human-computer interaction.
-   ttl: the specified time period to block access. Unit: second.

 |
|dynamic|Specifies Dynamic Route for CDN \(DCDN\) settings.| -   enable: required. It indicates whether to enable the function. Valid values: on and off.
-   static\_route\_type: the file name extension for static content.
-   static\_route\_url: the URI of the static content.
-   static\_route\_path: the path of the static content.
-   dynamic\_route\_origin: the protocol of the origin. Valid values: http, https, and follow.

 |
|set\_req\_header|Specifies the custom HTTP header for a back-to-origin request.| -   key: the header for the back-to-origin request.
-   value: the content of the header for the back-to-origin request.

 |
|l2\_oss\_key|Specifies the private key used for the authentication of access to an OSS bucket in L2 back-to-origin requests.|private\_oss\_auth: indicates whether the authentication is required to access a private OSS bucket in back-to-origin requests. Valid values: on and off.|
|range|Enables back-to-origin based on HTTP range requests.|enable: indicates whether to enable the function. Valid values: on, off, and force.|
|video\_seek|Enables video seeking.|enable: indicates whether to enable the function. Valid values: on and off.|
|https\_tls\_version|Specifies the TLS protocol version.| -   tls1.0: enables TLSv1.0. Valid values: on and off. Default value: on.
-   tls1.1: enables TLSv1.1. Valid values: on and off. Default value: on.
-   tls1.2: enables TLSv1.2. Valid values: on and off. Default value: on.
-   tls1.3: enables TLSv1.3. Valid values: on and off. Default value: on.

 |
|HSTS|Enables the HTTP Strict Transport Security \(HSTS\).| -   Enabled: required. It indicates whether to enable the function. Valid values: on and off. Default value: off.
-   Https\_hsts\_max\_age: required. It indicates the validity period of the HSTS. Unit: second. We recommend that you set this parameter to 5,184,000 seconds \(60 days\).
-   https\_hsts\_include\_subdomains: The HSTS header contains the **IncludeSubDomains** parameter. Valid values: on and off. Ensure that HTTPS is enabled for all subdomain names of the accelerated domain. Otherwise, the subdomain names become inaccessible after they are redirected to HTTPS. Therefore, use caution when enabling this function.

 |
|filetype\_force\_ttl\_code|Specifies the validity period of the file status code.| -   file\_type: required. It indicates the file type. You can separate multiple file types by using commas \(,\). For example, txt,jpg.
-   code\_string: required. It indicates the status code. Example: 302=0,301=0,4xx=2.

 |
|path\_force\_ttl\_code|Specifies the validity period of the directory status code.| -   path: required. It indicates the directory which must start with a forward slash \(/\), such as /image.
-   code\_string: required. It indicates the status code. For example, 302=0,301=0,4xx=2.

 |
|gzip|Enables intelligent compression.|enable: required. It indicates whether to enable the function. Valid values: on and off.|
|tesla|Enables page optimization.|enable: required. It indicates whether to enable the function. Valid values: on and off.|

## Response parameters {#section_fsg_t4n_4fb .section}

**Fn::GetAtt**

None

## Examples {#section_klp_54n_4fb .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "DomainConfig": {
      "Type": "ALIYUN::CDN::DomainConfig",
      "Properties": {
        "Functions": {
          "Ref": "Functions"
        },
        "DomainNames": {
          "Ref": "DomainNames"
        }
      }
    }
  },
  "Parameters": {
    "Functions": {
      "Type": "String",
      "Description": "function list"
    },
    "DomainNames": {
      "Type": "String",
      "Description": "Your accelerated domain names, separated by commas."
    }
  },
  "Outputs": {}
}
```

