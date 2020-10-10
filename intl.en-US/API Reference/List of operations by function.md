# List of operations by function

The following tables list API operations available for use in Resource Orchestration Service \(ROS\).

## Stack operations

|Operation|Description|
|---------|-----------|
|[CancelUpdateStack](/intl.en-US/API Reference/Stack operations/CancelUpdateStack.md)|Cancels the update of a stack.|
|[ContinueCreateStack](/intl.en-US/API Reference/Stack operations/ContinueCreateStack.md)|Creates a new stack based on the template of the previous stack that fails to be created.|
|[CreateStack](/intl.en-US/API Reference/Stack operations/CreateStack.md)|Creates a stack.|
|[GetStack](/intl.en-US/API Reference/Stack operations/GetStack.md)|Queries information about stacks.|
|[DeleteStack](/intl.en-US/API Reference/Stack operations/DeleteStack.md)|Deletes a stack and all of its resources.|
|[UpdateStack](/intl.en-US/API Reference/Stack operations/UpdateStack.md)|Updates a stack.|
|[ListStacks](/intl.en-US/API Reference/Stack operations/ListStacks.md)|Queries the list of stacks.|
|[PreviewStack](/intl.en-US/API Reference/Stack operations/PreviewStack.md)|Previews the stack to be created by using a specified template.|
|[ListStackEvents](/intl.en-US/API Reference/Stack operations/ListStackEvents.md)|Queries stacks and their resource events.|

## Resource operations

|Operation|Description|
|---------|-----------|
|[GetResourceTypeTemplate](/intl.en-US/API Reference/Resource operations/GetResourceTypeTemplate.md)|Queries the template of a resource by resource type.|
|[ListStackResources](/intl.en-US/API Reference/Resource operations/ListStackResources.md)|Queries the resource list of a specific stack.|
|[GetStackResource](/intl.en-US/API Reference/Resource operations/GetStackResource.md)|Queries information about a resource in a specific stack.|
|[GetResourceType](/intl.en-US/API Reference/Resource operations/GetResourceType.md)|Queries detailed information about a resource type.|
|[ListResourceTypes](/intl.en-US/API Reference/Resource operations/ListResourceTypes.md)|Queries the list of supported resource types.|

## Template operations

|Operation|Description|
|---------|-----------|
|[GetTemplateEstimateCost](/intl.en-US/API Reference/Template operations/GetTemplateEstimateCost.md)|Queries estimated prices of resources to be created based on a template.|
|[ValidateTemplate](/intl.en-US/API Reference/Template operations/ValidateTemplate.md)|Validates the template that is used to create stacks.|
|[GetTemplate](/intl.en-US/API Reference/Template operations/GetTemplate.md)|Queries detailed information about a template, including stacks and change sets associated with the template.|
|[DeleteTemplate](/intl.en-US/API Reference/Template operations/DeleteTemplate.md)|Deletes a template.|
|[ListTemplates](/intl.en-US/API Reference/Template operations/ListTemplates.md)|Queries the list of templates.|
|[CreateTemplate](/intl.en-US/API Reference/Template operations/CreateTemplate.md)|Creates a template.|
|[UpdateTemplate](/intl.en-US/API Reference/Template operations/UpdateTemplate.md)|Updates a template.|
|[GetTemplateSummary](/intl.en-US/API Reference/Template operations/GetTemplateSummary.md)|Queries information about a new or existing template.|

## Stack policy operations

|Operation|Description|
|---------|-----------|
|[SetStackPolicy](/intl.en-US/API Reference/Stack policy operations/SetStackPolicy.md)|Configures a stack policy.|
|[GetStackPolicy](/intl.en-US/API Reference/Stack policy operations/GetStackPolicy.md)|Queries information about a stack policy.|

## Change set operations

|Operation|Description|
|---------|-----------|
|[CreateChangeSet](/intl.en-US/API Reference/API operations related to change sets/CreateChangeSet.md)|Creates a change set.|
|[DeleteChangeSet](/intl.en-US/API Reference/API operations related to change sets/DeleteChangeSet.md)|Deletes a change set.|
|[ExecuteChangeSet](/intl.en-US/API Reference/API operations related to change sets/ExecuteChangeSet.md)|Executes a change set.|
|[GetChangeSet](/intl.en-US/API Reference/API operations related to change sets/GetChangeSet.md)|Queries information about a change set.|
|[ListChangeSets](/intl.en-US/API Reference/API operations related to change sets/ListChangeSets.md)|Queries the list of change sets.|

## Stack group operations

|Operation|Description|
|---------|-----------|
|[CreateStackGroup](/intl.en-US/API Reference/Stack group operations/CreateStackGroup.md)|Creates a stack group.|
|[DeleteStackGroup](/intl.en-US/API Reference/Stack group operations/DeleteStackGroup.md)|Deletes a stack group.|
|[GetStackGroup](/intl.en-US/API Reference/Stack group operations/GetStackGroup.md)|Queries information about a stack group.|
|[ListStackGroups](/intl.en-US/API Reference/Stack group operations/ListStackGroups.md)|Queries the list of stack groups.|
|[UpdateStackGroup](/intl.en-US/API Reference/Stack group operations/UpdateStackGroup.md)|Updates a stack group.|
|[CreateStackInstances](/intl.en-US/API Reference/Stack group operations/CreateStackInstances.md)|Creates stack instances in a specified account and region.|
|[DeleteStackInstances](/intl.en-US/API Reference/Stack group operations/DeleteStackInstances.md)|Deletes stack instances in a specified account and region.|
|[GetStackInstance](/intl.en-US/API Reference/Stack group operations/GetStackInstance.md)|Queries details about a stack instance associated with a stack group.|
|[ListStackInstances](/intl.en-US/API Reference/Stack group operations/ListStackInstances.md)|Queries the list of stack instances associated with a stack group.|
|[UpdateStackInstances](/intl.en-US/API Reference/Stack group operations/UpdateStackInstances.md)|Updates stack instances in a specified account and region.|
|[GetStackGroupOperation](/intl.en-US/API Reference/Stack group operations/GetStackGroupOperation.md)|Queries information about a stack group operation.|
|[ListStackGroupOperations](/intl.en-US/API Reference/Stack group operations/ListStackGroupOperations.md)|Queries the list of stack group operations.|
|[StopStackGroupOperation](/intl.en-US/API Reference/Stack group operations/StopStackGroupOperation.md)|Stops a stack group operation.|
|[ListStackGroupOperationResults](/intl.en-US/API Reference/Stack group operations/ListStackGroupOperationResults.md)|Queries the result list of stack group operations.|

## Drift detection operations

|Operation|Description|
|---------|-----------|
|[UpdateStackTemplateByResources](/intl.en-US/API Reference/Drift detection operations/UpdateStackTemplateByResources.md)|Corrects a template to eliminate stack drift.|
|[DetectStackDrift](/intl.en-US/API Reference/Drift detection operations/DetectStackDrift.md)|Detects drift on all supported resources for a stack.|
|[DetectStackGroupDrift](/intl.en-US/API Reference/Drift detection operations/DetectStackGroupDrift.md)|Detects drift on a stack group.|
|[DetectStackResourceDrift](/intl.en-US/API Reference/Drift detection operations/DetectStackResourceDrift.md)|Detects drift on individual resources in a stack.|
|[GetStackDriftDetectionStatus](/intl.en-US/API Reference/Drift detection operations/GetStackDriftDetectionStatus.md)|Queries the drift detection status of a stack.|
|[ListStackResourceDrifts](/intl.en-US/API Reference/Drift detection operations/ListStackResourceDrifts.md)|Queries the drift information of resources in a specified stack.|

## Tag operations

|Operation|Description|
|---------|-----------|
|[TagResources](/intl.en-US/API Reference/Tag operations/TagResources.md)|Creates and binds tags to a specified ROS resource list.|
|[UntagResources](/intl.en-US/API Reference/Tag operations/UntagResources.md)|Unbinds and deletes tags from a specified ROS resource list.|
|[ListTagResources](/intl.en-US/API Reference/Tag operations/ListTagResources.md)|Queries the tags that are bound to one or more ROS resources.|
|[ListTagKeys](/intl.en-US/API Reference/Tag operations/ListTagKeys.md)|Queries tag keys.|
|[ListTagValues](/intl.en-US/API Reference/Tag operations/ListTagValues.md)|Queries the values of specified tag keys.|

## Other operations

|Operation|Description|
|---------|-----------|
|[DescribeRegions](/intl.en-US/API Reference/Other operations/DescribeRegions.md)|Queries available regions.|
|[SignalResource](/intl.en-US/API Reference/Other operations/SignalResource.md)|Sends signals.|
|[SetDeletionProtection](/intl.en-US/API Reference/Other operations/SetDeletionProtection.md)|Configures deletion protection for a stack.|
|[t1919298.md\#]()|Detects the resources that may face high risks caused by a stack deletion operation, and queries the reason for each risk.|

