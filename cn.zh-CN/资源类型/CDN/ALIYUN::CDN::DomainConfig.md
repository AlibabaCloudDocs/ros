# ALIYUN::CDN::DomainConfig {#concept_rs1_3s3_fhb .concept}

ALIYUN::CDN::DomainConfig 用于域名批量配置。

## 语法 {#section_xyg_tn2_lfb .section}

```language-json
{
  "Type": "ALIYUN::CDN::DomainConfig",
  "Properties": {
    "Functions": String,
    "DomainNames": String
  }
}
```

## 属性 {#section_cgd_53n_4fb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|Functions|String|是|否|功能列表。|无。|
|DomainNames|String|是|否|您的加速域名，多个用英文半角逗号分隔。|无。|

## Functions格式 { .section}

```language-json
[{
  "functionArgs": [{
    "argName": "domain_name",
    "argValue": "api.hellodtworld.com"
  }],
  "functionName": "set_req_host_header"
}]
```

某些功能，如filetype\_based\_ttl\_set，可以设置多条记录，当需要更新其中某条记录时，可通过该条记录的configId来指定。

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

## 功能说明 { .section}

所有参数值均按照字符串类型处理。

|名称|描述|参数|
|--|--|--|
|referer\_white\_list\_set|refer白名单。| -   refer\_domain\_allow\_list：白名单列表，多个逗号分隔。
-   allow\_empty：是否允许空refer进入，取值on或off。

 |
|referer\_black\_list\_set|refer黑名单。| -   refer\_domain\_deny\_list：黑名单列表，多个逗号分隔。
-   allow\_empty：是否允许空refer进入，取值on或off。

 |
|filetype\_based\_ttl\_set|文件过期时间设置。| -   ttl：cache时间，单位：秒。
-   file\_type：文件类型，支持多个，用逗号\(英文\)隔开。如：txt,jpg。
-   weight：权重，取值范围1~199。

 |
|path\_based\_ttl\_set|目录过期时间设置。| -   ttl：cache时间，单位：秒。
-   path：目录，必须以"/"开头。
-   weight：权重，取值范围1~199。

 |
|oss\_auth|OSS鉴权Bucket。|oss\_bucket\_id：用户bucket地址。|
|ip\_black\_list\_set|IP黑名单。|ip\_list：IP列表多个用逗号隔开。|
|ip\_allow\_list\_set|IP白名单。|ip\_list：IP列表多个用逗号隔开。|
|ip\_white\_list\_set|TMD免拦截。|ip\_list：IP列表多个用逗号隔开。|
|error\_page|错误页面重定向。| -   error\_code：错误码。
-   rewrite\_page：重定向页面。

 |
|set\_req\_host\_header|修改回源自定义头。|domain\_name：回源Host头内容。|
|set\_hashkey\_args|忽略URL参数。| -   hashkey\_args：保留参数的列表，多个用逗号分隔。
-   disable：disable等于on的时候表示忽略所有参数，off不忽略。

 |
|ali\_remove\_args|忽略URL参数（删除）。| -   ali\_remove\_args：必填，删除指定的参数，多个参数之间用空格隔开，剩余参数将作为hashkey中URL args部分。
-   keep\_oss\_args：支持on/off。on表示回源保留所有参数，off表示与缓存hashkey的参数一致。

 |
|aliauth|阿里鉴权。| -   auth\_type：鉴权类型，取值范围"no\_auth","type\_a","type\_b","type\_c"。
-   auth\_key1：鉴权key1。
-   auth\_key2：鉴权key2。
-   ali\_auth\_delta：自定义鉴权缓冲时间。

 |
|set\_resp\_header|设置响应头（浏览器端可见）。| -   key：响应头。
-   value：响应头内容，删除填写null。

 |
|https\_force|强制HTTPS跳转。|enable：功能开关，取值on或off。|
|http\_force|强制HTTP跳转。|enable：功能开关，取值on或off。|
|https\_option|HTTPS基础参数。|http2：http2开关，取值on或off。|
|l2\_oss\_key|L2 OSS 回源私钥。|private\_oss\_auth：是否开启私有oss鉴权功能，取值on或off。|
|forward\_scheme|swift自适应回源。| -   enable：开关，取值on或off。
-   scheme\_origin：回源站协议，支持http、https和follow。

 |
|green\_manager|鉴黄功能。|enable：是否开启鉴黄功能，取值on或off。|
|tmd\_signature|TMD自定义规则。| -   name：规则名称，域名内不可重复。
-   path：可重复，需校验uri路径合法性。
-   pathType ：匹配规则。0 前缀匹配，1 完全匹配。
-   interval：监测时长。单位秒，参数限制必须\>=10。
-   count：单IP访问次数。
-   action：阻断类型。0：封禁，1：人机识别。
-   ttl：阻断时长，单位秒。

 |
|dynamic|全站加速相关配置。| -   enable：开关，必填，支持on/off。
-   static\_route\_type：静态加速文件后缀。
-   static\_route\_url：静态加速URI。
-   static\_route\_path：静态加速PATH。
-   dynamic\_route\_origin：回源路由 scheme，支持http/https/follow。

 |
|set\_req\_header|自定义回源HTTP头。| -   key：回源头。
-   value：回源头内容。

 |
|l2\_oss\_key|私有Buckct回源。|private\_oss\_auth：私有Bucket回源开关，支持on/off。|
|range|range回源。|enable：开关，支持on/off/force。|
|video\_seek|视频拖拽播放。|enable：开关，支持on/off|
|https\_tls\_version|TLS协议版本。| -   tls1.0：开启 TLSv1.0。默认：on，支持on/off。
-   tls1.1：开启 TLSv1.1。默认：on，支持on/off。
-   tls1.2：开启 TLSv1.2。默认：on，支持on/off。
-   tls1.3：开启 TLSv1.3。默认：on，支持on/off。

 |
|HSTS|HSTS。| -   enabled：开关，必填。默认：off，支持on/off。
-   https\_hsts\_max\_age过期时间，必填。单位：s，建议填写5184000s（60天）。
-   https\_hsts\_include\_subdomains：HSTS 头包含 **includeSubDomains** 参数，支持on/off。请谨慎开启，开启前，请确保该加速域名所有子域名都已开启 HTTPS，否则会导致子域名自动跳转到 HTTPS 后无法访问。

 |
|filetype\_force\_ttl\_code|文件状态码过期时间设置。| -   file\_type：文件类型，必填。支持多个，用逗号\(英文\)隔开，如txt,jpg。
-   code\_string：状态码，必填。例：302=0,301=0,4xx=2。

 |
|path\_force\_ttl\_code|路径状态码过期时间设置。| -   path：必填，必须以/开头，举例：/image。
-   code\_string：状态码，必填。例：302=0,301=0,4xx=2。

 |
|gzip|智能压缩。|enable：必填，功能开关，支持on/off。|
|tesla|页面优化。|enable：必填，功能开关，支持on/off。|

## 返回值 {#section_fsg_t4n_4fb .section}

**Fn::GetAtt**

无。

## 示例 {#section_klp_54n_4fb .section}

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
      "Description": "Your accelerated domain name, separated by commas in English."
    }
  },
  "Outputs": {}
}
```

