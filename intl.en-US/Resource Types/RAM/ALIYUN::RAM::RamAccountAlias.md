# ALIYUN::RAM::RamAccountAlias

ALIYUN::RAM::RamAccountAlias is used to create an alias for an Alibaba Cloud account.

## Syntax

```
{
  "Type": "ALIYUN::RAM::RamAccountAlias",
  "Properties": {
    "AccountAlias": String
  }
}
```

## Properties

|Property|Type|Required|Editable|Description|Constraint|
|--------|----|--------|--------|-----------|----------|
|AccountAlias|String|Yes|Yes|The alias to be created for the account.|The alias must be 3 to 32 characters in length and can contain lowercase letters, digits, and hyphens \(-\). It cannot start or end with a hyphen \(-\), and cannot contain consecutive hyphens \(-\).|

## Response parameters

Fn::GetAtt

AccountAlias: the alias of the account.

## Examples

`JSON` format

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "AccountAlias": {
      "Type": "String",
      "Description": "The alias of the Alibaba Cloud account.\nThe alias must be 3 to 32 characters in length, and can contain lowercase letters,\ndigits, and hyphens (-).\nNote It cannot start or end with a hyphen (-), and cannot contain consecutive hyphens (-).",
      "AllowedPattern": "^(?!-)([a-z0-9]+|-(?!-))+(?!-)$",
      "MinLength": 3,
      "MaxLength": 32
    }
  },
  "Resources": {
    "RamAccountAlias": {
      "Type": "ALIYUN::RAM::RamAccountAlias",
      "Properties": {
        "AccountAlias": {
          "Ref": "AccountAlias"
        }
      }
    }
  },
  "Outputs": {
    "AccountAlias": {
      "Description": "The alias of the Alibaba Cloud account.",
      "Value": {
        "Fn::GetAtt": [
          "RamAccountAlias",
          "AccountAlias"
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
  AccountAlias:
    AllowedPattern: ^(?!-)([a-z0-9]+|-(?!-))+(?!-)$
    Description: 'The alias of the Alibaba Cloud account.

      The alias must be 3 to 32 characters in length, and can contain lowercase letters,

      digits, and hyphens (-).

      Note It cannot start or end with a hyphen (-), and cannot contain consecutive
      hyphens (-).'
    MaxLength: 32
    MinLength: 3
    Type: String
Resources:
  RamAccountAlias:
    Properties:
      AccountAlias:
        Ref: AccountAlias
    Type: ALIYUN::RAM::RamAccountAlias
Outputs:
  AccountAlias:
    Description: The alias of the Alibaba Cloud account.
    Value:
      Fn::GetAtt:
      - RamAccountAlias
      - AccountAlias
```

