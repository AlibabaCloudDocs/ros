# ALIYUN::DNS::Domain {#concept_267984 .concept}

ALIYUN::DNS::Domain is used to add a domain name.

## Syntax {#section_t1y_arv_ljn .section}

```language-json
{
  "Type": "ALIYUN::DNS::Domain",
  "Properties": {
    "GroupId": String,
    "DomainName": String
  }
}
```

## Properties {#section_no2_bw5_2mb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|GroupId|String|No|Yes|The ID of the group to which the domain name will belong. The default value is the ID of the default group.|None|
|DomainName|String|Yes|No|The domain name to be added.|None|

## Response parameters {#section_y5a_2if_n88 .section}

 **Fn::GetAtt** 

-   DomainId: the ID of the domain used to create the tracking link.
-   DomainName: the domain name.
-   GroupId: the ID of the domain name group.
-   GroupName: the name of the domain name group.
-   PunyCode: the Punycode returned only for a Chinese domain name.
-   DnsServers: the list of DNS servers used to resolve the domain name.

## Examples {#section_omv_cs6_mhg .section}

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
      "Description": "The ID of the domain name group. The default value is the \"ID of the default group \" GroupId"
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
      "Description": "Punycode returned only for a Chinese domain name",
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

