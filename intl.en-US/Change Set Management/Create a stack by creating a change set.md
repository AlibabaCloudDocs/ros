# Create a stack by creating a change set

ROS allows you to create stacks by creating change sets. You can create change sets by calling an API operation or by using the Resource Orchestration Service \(ROS\) console or Alibaba Cloud CLI. You can check and modify the stacks before you execute change sets. The new stacks become valid only after the change sets are executed.

## Create a stack by using the ROS console

You can use existing resources to create a stack in the ROS console. Then, you can create a change set and execute the change set to import resources to the created stack.

For more information, see [Create a stack by importing an existing resource](/intl.en-US/Resource Import/Create a stack by importing an existing resource.md).

## Create a stack by calling an API operation

You can call the [CreateChangeSet](/intl.en-US/API Reference/API operations related to change sets/CreateChangeSet.md) operation to create a change set for a new stack and call the [PreviewStack](/intl.en-US/API Reference/Stack operations/PreviewStack.md) operation to preview the stack configuration.

If a stack is created when you create a change set, the stack is in the REVIEW\_IN\_PROGRESS state. You cannot create new change sets for a stack in this state. If the new stack does not meet the configuration requirements, you can delete the stack and create a new change set to create another stack.

## Create a stack by using Alibaba Cloud CLI

You can run the aliyun ros CreateChangeSet command to create a change set and then create a stack.

When you create a stack by creating a change set, you must set the ChangeSetType parameter to `CREATE` and specify the stack name, template, stack parameters, and change set name. In the following example, a stack named `test-create-change-set` and a change set named `test-create-change-set` are created.

```
aliyun ros CreateChangeSet --ChangeSetType CREATE --TemplateURL oss://ros-templates/test-change-set.json? RegionId=cn-hangzhou --StackName test-create-change-set --ChangeSetName test-create-change-set --Parameters.1.ParameterKey Count --Parameters.1.ParameterValue 1
```

