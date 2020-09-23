# ALIYUN::ECS::ForwardEntry

ALIYUN::ECS::ForwardEntry is used to configure the Destination Network Address Translation \(DNAT\) table of a Network Address Translation \(NAT\) gateway.

## Syntax

```
{
  "Type": "ALIYUN::ECS::ForwardEntry",
  "Properties": {
    "ExternalIp": String,
    "ExternalPort": String,
    "ForwardTableId": String,
    "InternalIp": String,
    "IpProtocol": String,
    "InternalPort": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|ExternalIp|String|Yes|No|The public IP address.|It must be an IP address that is included in the shared service plan of the NAT gateway to which the DNAT table belongs.|
|ExternalPort|String|Yes|No|The public port number.|Valid values: 1 to 65535.|
|ForwardTableId|String|Yes|No|The ID of the DNAT table.|None|
|InternalIp|String|Yes|No|The destination IP address to which the request will be forwarded.|This address must be a private IP address.|
|IpProtocol|String|Yes|No|The protocol type.|Valid values: -   TCP
-   UDP
-   Any |
|InternalPort|String|Yes|No|The port number of the private network.|Valid values: 1 to 65535.|

## Response parameters

Fn::GetAtt

ForwardEntryId: the ID of each entry in the DNAT table.

## Examples

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "ForwardEntry": {
      "Type": "ALIYUN::ECS::ForwardEntry",
      "Properties": {
        "ForwardTableId": "my_forwardt****",
        "ExternalIp": "101.201.XX.XX",
        "ExternalPort": "8080",
        "IpProtocol": "TCP",
        "InternalIp": "10.2.XX.XX",
        "InternalPort": "80"
      }
    }
  },
  "Outputs": {
    "ForwardEntryId": {
      "Value" : {"Fn::GetAttr": ["ForwardEntry","ForwardEntryId"]}
    }
  }
}
```

