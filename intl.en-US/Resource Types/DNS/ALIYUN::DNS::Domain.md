# ALIYUN::DNS::Domain

ALIYUN::DNS::Domain is used to add a domain name.

## Syntax

```
{
  "Type": "ALIYUN::DNS::Domain",
  "Properties": {
    "GroupId": String,
    "DomainName": String,
    "Tags": List
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|GroupId|String|No|Yes|The ID of the domain name group.|None|
|DomainName|String|Yes|No|The domain name.|None|
|Tags|List|No|Yes|The tags of the domain name.|A maximum of 20 tags can be specified. For more information, see [Tags properties](#section_7dm_5pp_k5j). |

## Tags syntax

```
"Tags": [
  {
    "Key": String,
    "Value": String
  }
]  
```

## Tags properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|Key|String|Yes|No|The tag key.|The tag key must be 1 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|
|Value|String|No|No|The tag value.|The tag value must be 0 to 128 characters in length and cannot contain `http://` or `https://`. It cannot start with `acs:` or `aliyun`.|

## Response parameters

Fn::GetAtt

-   DomainId: the domain name ID.
-   DomainName: the domain name.
-   GroupId: the ID of the domain name group.
-   GroupName: the name of the domain name group.
-   PunyCode: the Punycode returned only for a Chinese domain name.
-   DnsServers: the list of DNS servers used to resolve the domain name.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "DomainName": {
      "Type": "String",
      "Description": "Domain name"
    },
    "Tags": {
      "Type": "Json",
      "Description": "Tags to attach to instance. Max support 20 tags to add during create instance. Each tag with two properties Key and Value, and Key is required.",
      "MaxLength": 20
    },
    "GroupId": {
      "Type": "String",
      "Description": "Domain name grouping, the default is the \"default grouping\" GroupId"
    }
  },
  "Resources": {
    "Domain": {
      "Type": "ALIYUN::DNS::Domain",
      "Properties": {
        "DomainName": {
          "Ref": "DomainName"
        },
        "Tags": {
          "Ref": "Tags"
        },
        "GroupId": {
          "Ref": "GroupId"
        }
      }
    }
  },
  "Outputs": {
    "GroupName": {
      "Description": "The name of the domain name group",
      "Value": {
        "Fn::GetAtt": [
          "Domain",
          "GroupName"
        ]
      }
    },
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
    "PunyCode": {
      "Description": "punycode returned only for a Chinese domain name",
      "Value": {
        "Fn::GetAtt": [
          "Domain",
          "PunyCode"
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

`YAML` format

```
ROSTemplateFormatVersion: '2015-09-01'
Parameters:
  DomainName:
    Description: Domain name
    Type: String
  GroupId:
    Description: Domain name grouping, the default is the "default grouping" GroupId
    Type: String
  Tags:
    Description: Tags to attach to instance. Max support 20 tags to add during create
      instance. Each tag with two properties Key and Value, and Key is required.
    MaxLength: 20
    Type: Json
Resources:
  Domain:
    Properties:
      DomainName:
        Ref: DomainName
      GroupId:
        Ref: GroupId
      Tags:
        Ref: Tags
    Type: ALIYUN::DNS::Domain
Outputs:
  DnsServers:
    Description: The DNS list for the domain name under resolution
    Value:
      Fn::GetAtt:
      - Domain
      - DnsServers
  DomainId:
    Description: Domain ID
    Value:
      Fn::GetAtt:
      - Domain
      - DomainId
  DomainName:
    Description: Domain name
    Value:
      Fn::GetAtt:
      - Domain
      - DomainName
  GroupId:
    Description: Domain name group ID
    Value:
      Fn::GetAtt:
      - Domain
      - GroupId
  GroupName:
    Description: The name of the domain name group
    Value:
      Fn::GetAtt:
      - Domain
      - GroupName
  PunyCode:
    Description: punycode returned only for a Chinese domain name
    Value:
      Fn::GetAtt:
      - Domain
      - PunyCode
```

For more examples, visit [Domain.json](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/DNS/JSON/Domain.json) and [Domain.yml](https://github.com/aliyun/ros-templates/tree/master/ResourceTemplates/DNS/YAML/Domain.yml). In the examples, the ALIYUN::DNS::Domain and ALIYUN::DNS::DomainGroup resource types are involved.

