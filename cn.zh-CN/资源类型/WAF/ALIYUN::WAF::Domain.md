# ALIYUN::WAF::Domain

ALIYUN::WAF::Domain类型用于添加域名配置信息，将您的域名接入WAF实例进行防护。

## 语法

```
{
  "Type": "ALIYUN::WAF::Domain",
  "Properties": {
    "HttpToUserIp": String,
    "HttpPort": List,
    "IsAccessProduct": String,
    "ResourceGroupId": String,
    "DomainName": String,
    "InstanceId": String,
    "SourceIps": List,
    "ReadTime": Integer,
    "ClusterType": String,
    "LoadBalancing": String,
    "LogHeaders": List,
    "WriteTime": Integer,
    "Http2Port": List,
    "ConnectionTime": Integer,
    "HttpsRedirect": String,
    "HttpsPort": List
  }
}
```

## 属性

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|HttpToUserIp|String|否|是|是否开启HTTP回源功能。开启后HTTPS访问请求将通过HTTP协议转发回源站，默认回源端口为80端口。|取值：-   0（默认）：关闭。
-   1：开启。

**说明：** 如果您的网站不支持HTTPS回源，开启HTTP回源功能可通过WAF支持HTTPS访问。 |
|HttpPort|List|否|是|HTTP协议配置的端口。|指定多个HTTP端口时，使用英文逗号（,）分隔。**说明：** 填写该参数值即表示使用HTTP访问协议，且HttpPort与HttpsPort两个请求参数至少需要填写一个。 |
|IsAccessProduct|String|是|是|该域名在WAF前是否配置有七层代理（例如：高防、CDN等），即客户端访问流量到WAF前是否有经过其它七层代理转发。|取值： -   0：否。
-   1：是。 |
|ResourceGroupId|String|否|否|域名在资源管理产品中所属的资源组ID。|无|
|DomainName|String|是|否|域名名称。|无|
|InstanceId|String|是|否|WAF实例ID。|无|
|SourceIps|List|是|是|域名对应的源站服务器IP或服务器回源域名。|您只能选择填写源站服务器IP或服务器回源域名中的一种。-   填写源站服务器IP时，最多支持添加20个源站服务器IP实现负载均衡，IP间以英文逗号（,）分隔。
-   填写服务器回源域名时，只能填写一个域名地址。 |
|ReadTime|Integer|否|是|WAF独享集群读连接超时时长。|使用独享集群防护资源时，可以配置该参数。单位：秒。 |
|ClusterType|String|否|是|WAF实例的集群类别。|取值：-   0（默认值）：物理集群。
-   1：虚拟集群，即WAF独享集群。 |
|LoadBalancing|String|否|是|回源时采用的负载均衡算法。|取值：-   0：IP Hash方式。
-   1：轮询方式。 |
|LogHeaders|List|否|是|域名的流量标记字段和值，用于标记经过WAF的流量。

该参数值的样式为`[{"k":"_key_","v":"_value_"}]`。其中，`_key_`表示自定义请求头部字段，`_value_`表示为该字段设定的值。

通过指定自定义请求头部字段和对应的值，当域名的访问流量经过WAF时，系统将自动在请求头部中添加设定的自定义字段值作为流量标记，便于后端服务统计相关信息。

|如果请求中已存在该自定义头部字段，系统将用设定的流量标记值覆盖请求中该自定义字段的值。|
|WriteTime|Integer|否|是|WAF独享集群写连接超时时长。|使用独享集群防护资源时，可以配置该参数。单位：秒。 |
|Http2Port|List|否|是|HTTP 2.0协议配置的端口。|指定多个HTTP 2.0端口时，使用英文逗号（,）分隔。|
|ConnectionTime|Integer|否|是|WAF独享集群连接超时时长。|使用独享集群防护资源时，可以配置该参数。单位：秒。 |
|HttpsRedirect|String|否|是|是否开启HTTPS强制跳转。|取值：-   0（默认值）：关闭。
-   1：开启。

只有当域名使用HTTPS访问协议时，需填写该请求参数。开启强制跳转后HTTP请求将显示为HTTPS，默认跳转至443端口。|
|HttpsPort|List|否|是|HTTPS协议配置的端口。|指定多个HTTPS端口时，使用英文逗号（,）分隔。填写该参数值即表示使用HTTPS访问协议，且HttpPort与HttpsPort两个请求参数至少需要填写一个。 |

## 返回值

Fn::GetAtt

-   HttpToUserIp：是否开启HTTP回源功能。
-   HttpPort：HTTP协议配置的端口。
-   IsAccessProduct：域名在WAF前是否配置有七层代理。
-   ResourceGroupId：域名所属资源组ID。
-   DomainName：域名。
-   InstanceId：WAF实例ID。
-   SourceIps：域名对应的源站服务器IP或服务器回源域名。
-   ReadTime：WAF独享集群读连接超时时长。
-   ClusterType：WAF实例的集群类别。
-   Cname：WAF实例为该域名配置记录所分配的CNAME。
-   LoadBalancing：回源时采用的负载均衡算法。
-   LogHeaders：域名的流量标记字段和值，用于标记经过WAF的流量。
-   WriteTime：WAF独享集群写连接超时时长。
-   Http2Port：HTTP 2.0协议配置的端口。
-   Version：乐观锁版本。
-   ConnectionTime：WAF独享集群连接超时时长。
-   HttpsRedirect：是否开启HTTPS强制跳转。
-   HttpsPort：HTTPS协议配置的端口。

## 示例

`JSON`格式

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "HttpToUserIp": {
      "Type": "String",
      "Description": "Http back to source"
    },
    "HttpPort": {
      "Type": "Json",
      "Description": "Http port configuration"
    },
    "IsAccessProduct": {
      "Type": "String",
      "Description": "Is there a seven-layer agency before WAF"
    },
    "ResourceGroupId": {
      "Type": "String",
      "Description": "Resource group Id"
    },
    "DomainName": {
      "Type": "String",
      "Description": "Domain name"
    },
    "InstanceId": {
      "Type": "String",
      "Description": "Instance id"
    },
    "SourceIps": {
      "Type": "Json",
      "Description": "Back to source IP configuration"
    },
    "ReadTime": {
      "Type": "Number",
      "Description": "Read connection timeout period"
    },
    "ClusterType": {
      "Type": "String",
      "Description": "Cluster type"
    },
    "LoadBalancing": {
      "Type": "String",
      "Description": "Load balancing configuration"
    },
    "LogHeaders": {
      "Type": "Json",
      "Description": "Domain traffic tagging"
    },
    "WriteTime": {
      "Type": "Number",
      "Description": "Write connection timeout period"
    },
    "Http2Port": {
      "Type": "Json",
      "Description": "Http2 port configuration"
    },
    "ConnectionTime": {
      "Type": "Number",
      "Description": "Connection timeout"
    },
    "HttpsRedirect": {
      "Type": "String",
      "Description": "Https forced redirect configuration"
    },
    "HttpsPort": {
      "Type": "Json",
      "Description": "Https port configuration"
    }
  },
  "Resources": {
    "WAFDomain": {
      "Type": "ALIYUN::WAF::Domain",
      "Properties": {
        "HttpToUserIp": {
          "Ref": "HttpToUserIp"
        },
        "HttpPort": {
          "Ref": "HttpPort"
        },
        "IsAccessProduct": {
          "Ref": "IsAccessProduct"
        },
        "ResourceGroupId": {
          "Ref": "ResourceGroupId"
        },
        "DomainName": {
          "Ref": "DomainName"
        },
        "InstanceId": {
          "Ref": "InstanceId"
        },
        "SourceIps": {
          "Ref": "SourceIps"
        },
        "ReadTime": {
          "Ref": "ReadTime"
        },
        "ClusterType": {
          "Ref": "ClusterType"
        },
        "LoadBalancing": {
          "Ref": "LoadBalancing"
        },
        "LogHeaders": {
          "Ref": "LogHeaders"
        },
        "WriteTime": {
          "Ref": "WriteTime"
        },
        "Http2Port": {
          "Ref": "Http2Port"
        },
        "ConnectionTime": {
          "Ref": "ConnectionTime"
        },
        "HttpsRedirect": {
          "Ref": "HttpsRedirect"
        },
        "HttpsPort": {
          "Ref": "HttpsPort"
        }
      }
    }
  },
  "Outputs": {
    "HttpToUserIp": {
      "Description": "Http back to source",
      "Value": {
        "Fn::GetAtt": [
          "WAFDomain",
          "HttpToUserIp"
        ]
      }
    },
    "HttpPort": {
      "Description": "Http port configuration",
      "Value": {
        "Fn::GetAtt": [
          "WAFDomain",
          "HttpPort"
        ]
      }
    },
    "IsAccessProduct": {
      "Description": "Is there a seven-layer agency before WAF",
      "Value": {
        "Fn::GetAtt": [
          "WAFDomain",
          "IsAccessProduct"
        ]
      }
    },
    "ResourceGroupId": {
      "Description": "Resource group Id",
      "Value": {
        "Fn::GetAtt": [
          "WAFDomain",
          "ResourceGroupId"
        ]
      }
    },
    "DomainName": {
      "Description": "Domain name",
      "Value": {
        "Fn::GetAtt": [
          "WAFDomain",
          "DomainName"
        ]
      }
    },
    "InstanceId": {
      "Description": "Instance id",
      "Value": {
        "Fn::GetAtt": [
          "WAFDomain",
          "InstanceId"
        ]
      }
    },
    "SourceIps": {
      "Description": "Back to source IP configuration",
      "Value": {
        "Fn::GetAtt": [
          "WAFDomain",
          "SourceIps"
        ]
      }
    },
    "ReadTime": {
      "Description": "Read connection timeout period",
      "Value": {
        "Fn::GetAtt": [
          "WAFDomain",
          "ReadTime"
        ]
      }
    },
    "ClusterType": {
      "Description": "Cluster type",
      "Value": {
        "Fn::GetAtt": [
          "WAFDomain",
          "ClusterType"
        ]
      }
    },
    "Cname": {
      "Description": "CNAME assigned by WAF instance",
      "Value": {
        "Fn::GetAtt": [
          "WAFDomain",
          "Cname"
        ]
      }
    },
    "LoadBalancing": {
      "Description": "Load balancing configuration",
      "Value": {
        "Fn::GetAtt": [
          "WAFDomain",
          "LoadBalancing"
        ]
      }
    },
    "LogHeaders": {
      "Description": "Domain traffic tagging",
      "Value": {
        "Fn::GetAtt": [
          "WAFDomain",
          "LogHeaders"
        ]
      }
    },
    "WriteTime": {
      "Description": "Write connection timeout period",
      "Value": {
        "Fn::GetAtt": [
          "WAFDomain",
          "WriteTime"
        ]
      }
    },
    "Http2Port": {
      "Description": "Http2 port configuration",
      "Value": {
        "Fn::GetAtt": [
          "WAFDomain",
          "Http2Port"
        ]
      }
    },
    "Version": {
      "Description": "Optimistic lock version",
      "Value": {
        "Fn::GetAtt": [
          "WAFDomain",
          "Version"
        ]
      }
    },
    "ConnectionTime": {
      "Description": "Connection timeout",
      "Value": {
        "Fn::GetAtt": [
          "WAFDomain",
          "ConnectionTime"
        ]
      }
    },
    "HttpsRedirect": {
      "Description": "Https forced redirect configuration",
      "Value": {
        "Fn::GetAtt": [
          "WAFDomain",
          "HttpsRedirect"
        ]
      }
    },
    "HttpsPort": {
      "Description": "Https port configuration",
      "Value": {
        "Fn::GetAtt": [
          "WAFDomain",
          "HttpsPort"
        ]
      }
    }
  }
}
```

`YAML`格式

```
ROSTemplateFormatVersion: '2015-09-01'
Parameters:
  HttpToUserIp:
    Type: String
    Description: Http back to source
  HttpPort:
    Type: Json
    Description: Http port configuration
  IsAccessProduct:
    Type: String
    Description: Is there a seven-layer agency before WAF
  ResourceGroupId:
    Type: String
    Description: Resource group Id
  DomainName:
    Type: String
    Description: Domain name
  InstanceId:
    Type: String
    Description: Instance id
  SourceIps:
    Type: Json
    Description: Back to source IP configuration
  ReadTime:
    Type: Number
    Description: Read connection timeout period
  ClusterType:
    Type: String
    Description: Cluster type
  LoadBalancing:
    Type: String
    Description: Load balancing configuration
  LogHeaders:
    Type: Json
    Description: Domain traffic tagging
  WriteTime:
    Type: Number
    Description: Write connection timeout period
  Http2Port:
    Type: Json
    Description: Http2 port configuration
  ConnectionTime:
    Type: Number
    Description: Connection timeout
  HttpsRedirect:
    Type: String
    Description: Https forced redirect configuration
  HttpsPort:
    Type: Json
    Description: Https port configuration
Resources:
  WAFDomain:
    Type: 'ALIYUN::WAF::Domain'
    Properties:
      HttpToUserIp:
        Ref: HttpToUserIp
      HttpPort:
        Ref: HttpPort
      IsAccessProduct:
        Ref: IsAccessProduct
      ResourceGroupId:
        Ref: ResourceGroupId
      DomainName:
        Ref: DomainName
      InstanceId:
        Ref: InstanceId
      SourceIps:
        Ref: SourceIps
      ReadTime:
        Ref: ReadTime
      ClusterType:
        Ref: ClusterType
      LoadBalancing:
        Ref: LoadBalancing
      LogHeaders:
        Ref: LogHeaders
      WriteTime:
        Ref: WriteTime
      Http2Port:
        Ref: Http2Port
      ConnectionTime:
        Ref: ConnectionTime
      HttpsRedirect:
        Ref: HttpsRedirect
      HttpsPort:
        Ref: HttpsPort
Outputs:
  HttpToUserIp:
    Description: Http back to source
    Value:
      'Fn::GetAtt':
        - WAFDomain
        - HttpToUserIp
  HttpPort:
    Description: Http port configuration
    Value:
      'Fn::GetAtt':
        - WAFDomain
        - HttpPort
  IsAccessProduct:
    Description: Is there a seven-layer agency before WAF
    Value:
      'Fn::GetAtt':
        - WAFDomain
        - IsAccessProduct
  ResourceGroupId:
    Description: Resource group Id
    Value:
      'Fn::GetAtt':
        - WAFDomain
        - ResourceGroupId
  DomainName:
    Description: Domain name
    Value:
      'Fn::GetAtt':
        - WAFDomain
        - DomainName
  InstanceId:
    Description: Instance id
    Value:
      'Fn::GetAtt':
        - WAFDomain
        - InstanceId
  SourceIps:
    Description: Back to source IP configuration
    Value:
      'Fn::GetAtt':
        - WAFDomain
        - SourceIps
  ReadTime:
    Description: Read connection timeout period
    Value:
      'Fn::GetAtt':
        - WAFDomain
        - ReadTime
  ClusterType:
    Description: Cluster type
    Value:
      'Fn::GetAtt':
        - WAFDomain
        - ClusterType
  Cname:
    Description: CNAME assigned by WAF instance
    Value:
      'Fn::GetAtt':
        - WAFDomain
        - Cname
  LoadBalancing:
    Description: Load balancing configuration
    Value:
      'Fn::GetAtt':
        - WAFDomain
        - LoadBalancing
  LogHeaders:
    Description: Domain traffic tagging
    Value:
      'Fn::GetAtt':
        - WAFDomain
        - LogHeaders
  WriteTime:
    Description: Write connection timeout period
    Value:
      'Fn::GetAtt':
        - WAFDomain
        - WriteTime
  Http2Port:
    Description: Http2 port configuration
    Value:
      'Fn::GetAtt':
        - WAFDomain
        - Http2Port
  Version:
    Description: Optimistic lock version
    Value:
      'Fn::GetAtt':
        - WAFDomain
        - Version
  ConnectionTime:
    Description: Connection timeout
    Value:
      'Fn::GetAtt':
        - WAFDomain
        - ConnectionTime
  HttpsRedirect:
    Description: Https forced redirect configuration
    Value:
      'Fn::GetAtt':
        - WAFDomain
        - HttpsRedirect
  HttpsPort:
    Description: Https port configuration
    Value:
      'Fn::GetAtt':
        - WAFDomain
        - HttpsPort
```

