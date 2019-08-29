# ALIYUN::DNS::Domain {#concept_267984 .concept}

ALIYUN::DNS::Domain 类型用于添加域名。

## 语法 {#section_t1y_arv_ljn .section}

```language-json
{
  "Type": "ALIYUN::DNS::Domain",
  "Properties": {
    "GroupId": String,
    "DomainName": String
  }
}
```

## 属性 {#section_no2_bw5_2mb .section}

|属性名称|类型|必须|允许更新|描述|约束|
|----|--|--|----|--|--|
|GroupId|String|否|是|域名分组，默认为“默认分组”的GroupId。|无。|
|DomainName|String|是|否|域名名称。|无。|

## 返回值 {#section_y5a_2if_n88 .section}

**Fn::GetAtt**

-   DomainId：创建的跟踪名称。
-   DomainName：域名名称。
-   GroupId：域名分组ID。
-   GroupName：域名分组名称。
-   PunyCode：只针对中文域名返回punycode码。
-   DnsServers：域名在解析系统中的DNS列表。

## 示例 {#section_omv_cs6_mhg .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "Domain": {
      "Type": "ALIYUN::DNS::Domain",
      "Properties": {
        "GroupId": {
          "Ref": "GroupId"
        },
        "DomainName": {
          "Ref": "DomainName"
        }
      }
    }
  },
  "Parameters": {
    "GroupId": {
      "Type": "String",
      "Description": "Domain name grouping, the default is the \"default grouping\" GroupId"
    },
    "DomainName": {
      "Type": "String",
      "Description": "Domain name"
    }
  },
  "Outputs": {
    "DomainId": {
      "Description": "Domain ID",
      "Value": {
        "Fn::GetAtt": [
          "Domain",
          "DomainId"
        ]
      }
    },
    "DomainName": {
      "Description": "Domain name",
      "Value": {
        "Fn::GetAtt": [
          "Domain",
          "DomainName"
        ]
      }
    },
    "DnsServers": {
      "Description": "The DNS list for the domain name under resolution",
      "Value": {
        "Fn::GetAtt": [
          "Domain",
          "DnsServers"
        ]
      }
    },
    "GroupName": {
      "Description": "The name of the domain name group",
      "Value": {
        "Fn::GetAtt": [
          "Domain",
          "GroupName"
        ]
      }
    },
    "PunyCode": {
      "Description": "punycode returned only for a Chinese domain name",
      "Value": {
        "Fn::GetAtt": [
          "Domain",
          "PunyCode"
        ]
      }
    },
    "GroupId": {
      "Description": "Domain name group ID",
      "Value": {
        "Fn::GetAtt": [
          "Domain",
          "GroupId"
        ]
      }
    }
  }
}
```

