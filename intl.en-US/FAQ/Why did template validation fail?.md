# Why did template validation fail?

This topic describes why template validation fails.

## Format

Make sure that the template is a valid JSON or YAML file with UTF-8 encoding. The files are valid if their content can be correctly interpreted as JSON or YAML.

## Version \(ROSTemplateFormatVersion\)

Make sure that ROSTemplateFormatVersion is correctly spelled and the value is 2015-09-01.

## Mappings

Make sure that mapping definitions meet the Resource Orchestration Service \(ROS\) requirements.

**Note:** Functions cannot be used in mappings.

## Parameters

Make sure that parameter definitions meet the ROS requirements.

**Note:** Functions cannot be used in parameters. If the parameter definition contains a constraint and a default value, the default value must also conform to the parameter constraint.

## Resources

Resource IDs cannot contain forward slashes \(/\).

A resource definition must contain a Type property whose value is of the String type.

A resource definition can only contain values of the Type, Properties, Metadata, DependsOn, DeletionPolicy, and Description properties.

## Outputs

A value must be defined in an output.

## Unsupported resource types

If the template contains unsupported resources, validation fails.

## Others

Make sure that the size of the template file is no larger than 512 KB.

Make sure that the template contains only the following top-level objects: ROSTemplateFormatVersion, Description, Mappings, Parameters, Resources, and Outputs.

