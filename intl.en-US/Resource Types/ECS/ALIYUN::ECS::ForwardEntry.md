# ALIYUN::ECS::ForwardEntry {#concept_e1p_j12_lfb .concept}

ALIYUN::ECS::ForwardEntry is used to configure the DNAT table of a NAT Gateway.

## Syntax {#section_vds_412_lfb .section}

```language-json
{
  "Type": "ALIYUN::ECS::ForwardEntry",
  "Properties": {
    "ExternalIp": String,
    "ExternalPort": String,
    "ForwardTableId": String,
    "InternalIp": String,
    "IpProtocol": String,
    "InternalPort": String,
  }
}
```

## Properties {#section_pym_y12_lfb .section}

|Name|Type|Required|Editable|Description|Validity|
|----|----|--------|--------|-----------|--------|
|ExternalIp|String|Yes|No|The public IP address.|It must be an IP address that is included in the shared bandwidth package of the NAT Gateway to which the DNAT table belongs.|
|ExternalPort|String|Yes|No|The public port number.|Valid values: 1 to 65535.|
|ForwardTableId|String|Yes|No|The ID of the DNAT table.|None|
|InternalIp|String|Yes|No|The destination IP address of the forwarding request.|This address must be a private IP address.|
|IpProtocol|String|Yes|No|The protocol type.|Valid values: TCP, UDP, and Any.|
|InternalPort|String|Yes|No|The destination port number of the forwarding request.|Valid values: 1 to 65535.|

## Response parameters {#section_q1l_cb2_lfb .section}

**Fn::GetAtt**

ForwardEntryId: the ID of each entry in the DNAT table.

## Examples {#section_ax4_3b2_lfb .section}

```language-json
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "ForwardEntry": {
      "Type": "ALIYUN::ECS::ForwardEntry",
      "Properties": {
        "ForwardTableId": "my_forwardtable",
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

