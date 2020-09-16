# ALIYUN::ECS::SSHKeyPairAttachment

ALIYUN::ECS::SSHKeyPairAttachment is used to attach an SSH key pair to specified ECS instances.

## Syntax

```
{
  "Type": "ALIYUN::ECS::SSHKeyPairAttachment",
  "Properties": {
    "InstanceIds": List,
    "KeyPairName": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|InstanceIds|List|Yes|Yes|The IDs of the ECS instances to which the SSH key pair is attached.|Separate IDs with commas \(,\). Only Linux instances are supported.|
|KeyPairName|String|Yes|No|The name of the SSH key pair.|None|

## Response parameters

Fn::GetAtt

None.

## Examples

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Resources": {
    "SSHKeyPairAttachment": {
      "Type": "ALIYUN::ECS::SSHKeyPairAttachment",
      "Properties": {
        "KeyPairName": "ssh_key_pai****",
        "InstanceIds": [
          'i-2zeiofnh20hj8fej****',
          'i-2zebt3kfvxm28y9o****'
        ]
      }
    }
  }
}
```

