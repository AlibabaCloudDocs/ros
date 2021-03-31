# Parameters

The Parameters section improves the flexibility and reusability of a template. When you create a stack, you can replace parameter values in the template.

For example, you want to create a stack in a web application, and the stack needs to contain one SLB instance, two ECS instances, and one ApsaraDB RDS instance. If the web application is under heavy workload, you can select an ECS instance that has high specifications when you create the stack. If the web application is not under heavy workload, you can select an ECS instance that has lower specifications. The following example shows how to define the InstanceType parameter for an ECS instance:

```
"Parameters" : {
  "InstanceType" : {
    "Type" : "String",
    "AllowedValues":["ecs.t1.small","ecs.s1.medium", "ecs.m1.medium", "ecs.c1.large"],
    "Default": "ecs.t1.small",
    "Label": "The ECS instance type",
    "Description" : "The instance type of the ECS instance you want to create. Default value: ecs.t1.small. Valid values: ecs.t1.small, ecs.s1.medium, ecs.m1.medium, and ecs.c1.large."
  }
}
```

You can specify the value of the InstanceType parameter when you create stacks based on the template. If you do not specify the parameter, the default value `ecs.t1.small` is used.

The following example shows how to reference the InstanceType parameter when you define a resource:

```
"Webserver" : {
  "Type" : "ALIYUN::ECS::Instance",
  "InstanceType": {
    "Ref": "InstanceType"
  }
}
```

## Syntax

Each parameter consists of a name and properties. The parameter name can contain only letters and digits, and must be unique within the template. You can use the Label field to define the alias of a parameter.

The following table describes the parameter properties.

|Parameter property|Required|Description|
|------------------|--------|-----------|
|Type|Yes|The data type of the parameter. Valid values:

-   `String`: a string value. Example: `"ecs.s1.medium"`.
-   `Number`: an integer or a floating-point number. Example: 3.14.
-   CommaDelimitedList: a set of strings separated by commas \(,\), which can be indexed by using the Fn::Select function. Example: `"80, foo, bar"`.
-   `Json`: a JSON string. Example: `{ "foo": "bar" }`, `[1, 2, 3]`.
-   `Boolean`: a Boolean value. Example: `true` or `false`.
-   `ALIYUN::OOS::Parameter::Value`: a common parameter stored in an OOS data warehouse. Example: `my_image`.
-   `ALIYUN::OOS::SecretParameter::Value`: an encryption parameter stored in an OOS data warehouse. Example: `my_password`. |
|Default|No|The default value of the parameter. If you do not specify a value for the parameter when you create a stack, ROS checks whether a default value is defined in the template. If a default value is found, ROS uses the default value. Otherwise, an error is returned.**Note:** The default value can be set to `null`, which indicates that this parameter is an empty string and the parameter verification is skipped. |
|AllowedValues|No|The list of one or more valid parameter values.|
|AllowedPattern|No|The regular expression that is used to check whether the specified parameter value is a string. If the input is not a string, an error is returned. If you use the following special characters, add two backslashes \(\\\\\) immediately before the characters to escape:

```
*.? +-$^[ ]( ){ }|\/
```

**Note:** A hyphen \(-\) does not need to be escaped if it is the first or last character in the range. For example, \[a-z-\]. |
|MaxLength|No|The integer value that determines the longest string allowed for a String-type parameter.|
|MinLength|No|The integer value that determines the shortest string allowed for a String-type parameter.|
|MaxValue|No|The numeric value that determines the maximum value allowed for a Number-type parameter.|
|MinValue|No|The numeric value that determines the minimum value allowed for a Number-type parameter.|
|NoEcho|No|Specifies whether to mask the parameter value when the GetStack operation is called. If you set this parameter property to `true`, only asterisks \(\*\) are returned.|
|Description|No|The string that describes the parameter.|
|ConstraintDescription|No|The string that explains the parameter constraint.|
|Label|No|The alias of the parameter, encoded in UTF-8. When you create a web form based on a template, `label` can be mapped to the parameter name.|
|AssociationProperty|No|The associated resource property. If you specify this parameter property, ROS checks whether the specified parameter value is valid and provides a list of valid values based on the associated resource property. Valid values:

-   `ALIYUN::ECS::Instance::ImageId`: the ID of the image.
-   `ALIYUN::ECS::Instance::ZoneId`: The zone ID of the ECS instance.
-   `ALIYUN::ECS::VPC::VPCId`: the ID of the VPC.
-   `ALIYUN::ECS::VSwitch::VSwitchId`: the ID of the vSwitch.
-   `ALIYUN::ECS::Instance::InstanceType`: the instance type of the ECS instance.
-   `ALIYUN::ECS::SecurityGroup::SecurityGroupId`: the ID of the security group.
-   `ALIYUN::RAM::Role`: the RAM role.
-   `ALIYUN::RAM::User`: the RAM user.
-   `ALIYUN::ECS::KeyPair::KeyPairName`: the key pair.

For example, if you set the AssociationProperty parameter property to `ALIYUN::ECS::Instance::ImageId`, the ROS console verifies whether the specified image ID is valid and lists other valid values in a drop-down list. For more information, see [Example 1: the UserName, PassWord, and ImageId parameters](#section_i5w_x3v_kfb). |
|AssociationPropertyMetadata|No|The metadata map that explains the constraint of the AssociationProperty parameter property.Valid values:

-   `ZoneId`: the ID of the zone. If you set the parameter property to ZoneId, ROS queries the resources in the specified zone.

Applicable value of the AssociationProperty parameter property: `ALIYUN::ECS::VSwitch::VSwitchId`.

-   `VpcId`: the ID of the VPC. If you set the parameter property to VpcId, ROS queries the resources in the specified VPC.

Applicable values of the AssociationProperty parameter property:

    -   `ALIYUN::ECS::VSwitch::VSwitchId`
    -   `ALIYUN::ECS::SecurityGroup::SecurityGroupId`

For more information, see [Example 2: the vSwitchId parameter that uses the AssociationPropertyMetadata parameter property](#section_dbf_br8_mh1).|
|Confirm|No|Specifies whether to enter the parameter value for a second time if the NoEcho parameter property is set to `true`. Default value: `false`. **Note:** The Confirm parameter property can be set to `true` only when it is used with a String-type parameter and when the NoEcho parameter is set to `true`. |

## Example 1: the UserName, PassWord, and ImageId parameters

In the following example, three parameters are defined in the Parameters section.

-   UserName: a String-type parameter whose value must be 6 to 12 characters in length. Default value: anonymous. Valid values:

    -   `anonymous`
    -   `user-one`
    -   `user-two`
    **Note:** The default value `anonymous` must also meet the length and valid value requirements.

-   PassWord: a String-type parameter that does not have a default value. If you set the NoEcho parameter property to `true`, the GetStack operation does not return any parameter values. The parameter value must be 1 to 41 characters in length and can contain uppercase letters, lowercase letters, and digits.
-   ImageId: a String-type parameter. You can use the AssociationProperty parameter property to query the list of all available images and check whether the default value is valid.

```
"Parameters": {
  "UserName": {
    "Label": "Username",
    "Description": "Enter the username",
    "Default": "anonymous",
    "Type": "String",
    "MinLength": "6",
    "MaxLength": "12",
    "AllowedValues": [
      "anonymous",
      "user-one",
      "user-two"
    ]
  },
  "PassWord": {
    "Label": "Password",
    "NoEcho": "True",
    "Description": "Enter the password",
    "Type": "String",
    "MinLength": "1",
    "MaxLength": "41",
    "AllowedPattern": "[a-zA-Z0-9]*"
  },
  "ImageId": {
    "Label": "Image",
    "Type": "String",
    "Description": "Select an image",
    "AssociationProperty": "ALIYUN::ECS::Instance::ImageId",
    "Default": "centos_7_7_x64_20G_alibase_2020****.vhd"
  }
}
```

## Example 2: the vSwitchId parameter that uses the AssociationPropertyMetadata parameter property

If you specify the AssociationPropertyMetadata parameter property, the ROS console lists available vSwitches in a drop-down list that are located in the specified zone and VPC. If you do not specify the AssociationPropertyMetadata parameter property, the ROS console lists all vSwitches in the current region.

```
{
  "ROSTemplateFormatVersion": "2015-09-01",
  "Parameters": {
    "VpcId": {
      "Type": "String",
      "AssociationProperty": "ALIYUN::ECS::VPC::VPCId"
    },
    "EcsZone": {
      "Type": "String",
      "AssociationProperty": "ALIYUN::ECS::Instance::ZoneId"
    },
    "VSwitchId": {
      "Type": "String",
      "AssociationProperty": "ALIYUN::ECS::VSwitch::VSwitchId",
      "AssociationPropertyMetadata": {
        "VpcId": "VpcId",
        "ZoneId": "EcsZone"
      }
    }
  }
}
```

