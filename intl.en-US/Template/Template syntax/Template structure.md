# Template structure

A template is a UTF-8 encoded JSON or YAML file that is used to create stacks. Templates serve as the blueprint for underlying infrastructure and architecture. Templates define the configurations and dependencies of Alibaba Cloud resources.

## ROS template structure

```
{
  "ROSTemplateFormatVersion" : "2015-09-01",

  "Description" : "The description of the template, which is used to provide information such as application scenarios and template architecture.",
  "Metadata" : {
    // The template metadata that provides information such as layout for visualizations.
  },
  "Parameters" : {
    // The parameters you can specify when you create a stack.
  },

  "Mappings" : {
    // The mapping tables. Mapping tables are nested tables.
  },

  "Conditions": {
    // The conditions that are defined by using internal condition functions. These conditions determine when to create associated resources.
  },

  "Resources" : {
    // The detailed information of resources such as configurations and dependencies.
  },

  "Outputs" : {
    // The outputs that are used to provide useful information such as resource properties. You can use the ROS console or API to obtain the information.
  }
}
```

## ROSTemplateFormatVersion

Required. The template versions that are supported by ROS. Current version: 2015-09-01.

## Description

Optional. The description of the template, which is used to provide information such as the application scenarios and architecture of the template. A detailed description can help you better understand the content of the template.

## Metadata

Optional. The metadata of the template, in the JSON format.

## Parameters

Optional. The parameters you can specify when you create a stack. An ECS instance type is often defined as a parameter. Parameters have default values. Parameters can improve the flexibility and reusability of the template. When you create a stack, select appropriate specifications.

For more information, see [Parameters](/intl.en-US/Template/Template syntax/Parameters.md).

## Mappings

Optional. Mappings are defined as nested mapping tables. You can use Fn::FindInMap to match a key to a corresponding set of named values. You can also use parameter values as keys. For example, you can search the region-image mapping table for desired images by region.

For more information, see [Mappings](/intl.en-US/Template/Template syntax/Mappings.md).

## Conditions

Optional. The conditions that are defined by using Fn::And, Fn::Or, Fn::Not, and Fn::Equals. Separate multiple conditions with commas \(,\). When you create or update a stack, ROS evaluates all the conditions in your template before it creates any resources. All resources associated with true conditions are created, and all resources associated with false conditions are ignored.

For more information, see [Conditions](/intl.en-US/Template/Template syntax/Conditions.md).

## Resources

Optional. The detailed information of resources in the stack that is created based on the template. The information includes resource dependencies and configurations.

For more information, see [Resources](/intl.en-US/Template/Template syntax/Resources.md).

## Outputs

Optional. The outputs that are used to provide useful information such as resource properties. You can use the ROS console or API to obtain the information.

For more information, see [Outputs](/intl.en-US/Template/Template syntax/Outputs.md).

