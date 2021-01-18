# API概览

资源编排服务ROS（Resource Orchestration Service）提供以下API接口。

## 资源栈相关接口

|API|描述|
|---|--|
|[CancelUpdateStack](/cn.zh-CN/API参考/资源栈相关接口/CancelUpdateStack.md)|调用CancelUpdateStack接口取消更新资源栈。|
|[ContinueCreateStack](/cn.zh-CN/API参考/资源栈相关接口/ContinueCreateStack.md)|资源栈创建失败后，调用ContinueCreateStack接口重新创建资源栈。|
|[CreateStack](/cn.zh-CN/API参考/资源栈相关接口/CreateStack.md)|调用CreateStack接口创建资源栈。|
|[GetStack](/cn.zh-CN/API参考/资源栈相关接口/GetStack.md)|调用GetStack接口查询资源栈信息。|
|[DeleteStack](/cn.zh-CN/API参考/资源栈相关接口/DeleteStack.md)|调用DeleteStack接口删除资源栈。|
|[UpdateStack](/cn.zh-CN/API参考/资源栈相关接口/UpdateStack.md)|调用UpdateStack接口更新资源栈。|
|[ListStacks](/cn.zh-CN/API参考/资源栈相关接口/ListStacks.md)|调用ListStacks接口查询资源栈列表。|
|[PreviewStack](/cn.zh-CN/API参考/资源栈相关接口/PreviewStack.md)|调用PreviewStack接口预览指定模板将要创建的资源栈信息。|
|[ListStackEvents](/cn.zh-CN/API参考/资源栈相关接口/ListStackEvents.md)|调用ListStackEvents接口查询资源栈及栈内资源的事件。|

## 资源相关接口

|API|描述|
|---|--|
|[GetResourceTypeTemplate](/cn.zh-CN/API参考/资源相关接口/GetResourceTypeTemplate.md)|调用GetResourceTypeTemplate接口根据资源类型查询该资源的模板。|
|[ListStackResources](/cn.zh-CN/API参考/资源相关接口/ListStackResources.md)|调用ListStackResources接口查询某个资源栈的资源列表。|
|[GetStackResource](/cn.zh-CN/API参考/资源相关接口/GetStackResource.md)|调用GetStackResource接口查询某个资源栈的资源。|
|[GetResourceType](/cn.zh-CN/API参考/资源相关接口/GetResourceType.md)|调用GetResourceType接口查询资源类型的详细信息。|
|[ListResourceTypes](/cn.zh-CN/API参考/资源相关接口/ListResourceTypes.md)|调用ListResourceTypes接口查询支持的资源类型列表。|

## 模板相关接口

|API|描述|
|---|--|
|[GetTemplateEstimateCost](/cn.zh-CN/API参考/模板相关接口/GetTemplateEstimateCost.md)|调用GetTemplateEstimateCost接口查询模板中创建资源的预估价格。|
|[ValidateTemplate](/cn.zh-CN/API参考/模板相关接口/ValidateTemplate.md)|调用ValidateTemplate接口验证将要创建资源栈的模板。|
|[GetTemplate](/cn.zh-CN/API参考/模板相关接口/GetTemplate.md)|调用GetTemplate接口查询资源栈、更改集、自定义模板的模板详情。|
|[DeleteTemplate](/cn.zh-CN/API参考/模板相关接口/DeleteTemplate.md)|调用DeleteTemplate接口删除模板。|
|[ListTemplates](/cn.zh-CN/API参考/模板相关接口/ListTemplates.md)|调用ListTemplates接口查询模板列表。|
|[CreateTemplate](/cn.zh-CN/API参考/模板相关接口/CreateTemplate.md)|调用CreateTemplate接口创建自定义模板。|
|[UpdateTemplate](/cn.zh-CN/API参考/模板相关接口/UpdateTemplate.md)|调用UpdateTemplate接口更新模板。|
|[GetTemplateSummary](/cn.zh-CN/API参考/模板相关接口/GetTemplateSummary.md)|调用GetTemplateSummary接口获取新模板或者现有模板的信息。|
|[ListTemplateVersions](/cn.zh-CN/API参考/模板相关接口/ListTemplateVersions.md)|调用ListTemplateVersions接口查询模板的版本列表。|
|[SetTemplatePermission](/cn.zh-CN/API参考/模板相关接口/SetTemplatePermission.md)|调用SetTemplatePermission接口共享模板或取消共享模板。 |
|[GenerateTemplatePolicy](/cn.zh-CN/API参考/模板相关接口/GenerateTemplatePolicy.md)|调用GenerateTemplatePolicy接口生成模板所需的策略信息。|

## 资源栈策略相关接口

|API|描述|
|---|--|
|[SetStackPolicy](/cn.zh-CN/API参考/资源栈策略相关接口/SetStackPolicy.md)|调用SetStackPolicy接口设置资源栈策略。|
|[GetStackPolicy](/cn.zh-CN/API参考/资源栈策略相关接口/GetStackPolicy.md)|调用GetStackPolicy接口获取资源栈策略。|

## 更改集相关接口

|API|描述|
|---|--|
|[CreateChangeSet](/cn.zh-CN/API参考/更改集相关接口/CreateChangeSet.md)|调用CreateChangeSet接口创建更改集。|
|[DeleteChangeSet](/cn.zh-CN/API参考/更改集相关接口/DeleteChangeSet.md)|调用DeleteChangeSet接口删除更改集。|
|[ExecuteChangeSet](/cn.zh-CN/API参考/更改集相关接口/ExecuteChangeSet.md)|调用ExecuteChangeSet接口执行更改集。|
|[GetChangeSet](/cn.zh-CN/API参考/更改集相关接口/GetChangeSet.md)|调用GetChangeSet接口查询更改集信息。|
|[ListChangeSets](/cn.zh-CN/API参考/更改集相关接口/ListChangeSets.md)|调用ListChangeSets接口查询更改集列表。|

## 资源栈组相关接口

|API|描述|
|---|--|
|[CreateStackGroup](/cn.zh-CN/API参考/资源栈组相关接口/CreateStackGroup.md)|调用CreateStackGroup接口创建资源栈组。|
|[DeleteStackGroup](/cn.zh-CN/API参考/资源栈组相关接口/DeleteStackGroup.md)|调用DeleteStackGroup接口删除资源栈组。|
|[GetStackGroup](/cn.zh-CN/API参考/资源栈组相关接口/GetStackGroup.md)|调用GetStackGroup接口查询指定资源栈组的信息。|
|[ListStackGroups](/cn.zh-CN/API参考/资源栈组相关接口/ListStackGroups.md)|调用ListStackGroups接口查询资源栈组列表。|
|[UpdateStackGroup](/cn.zh-CN/API参考/资源栈组相关接口/UpdateStackGroup.md)|调用UpdateStackGroup接口更新资源栈组。|
|[CreateStackInstances](/cn.zh-CN/API参考/资源栈组相关接口/CreateStackInstances.md)|调用CreateStackInstances接口在指定账号和地域下创建资源栈实例。|
|[DeleteStackInstances](/cn.zh-CN/API参考/资源栈组相关接口/DeleteStackInstances.md)|调用DeleteStackInstances接口删除特定账号和地域下的资源栈实例。|
|[GetStackInstance](/cn.zh-CN/API参考/资源栈组相关接口/GetStackInstance.md)|调用GetStackInstance接口查询指定资源栈组关联的资源栈实例的详细信息。|
|[ListStackInstances](/cn.zh-CN/API参考/资源栈组相关接口/ListStackInstances.md)|调用ListStackInstances接口查询指定资源栈组关联的资源栈实例列表。|
|[UpdateStackInstances](/cn.zh-CN/API参考/资源栈组相关接口/UpdateStackInstances.md)|调用UpdateStackInstances接口在特定账号和地域下更新资源栈实例。|
|[GetStackGroupOperation](/cn.zh-CN/API参考/资源栈组相关接口/GetStackGroupOperation.md)|调用GetStackGroupOperation接口查询资源栈组操作的信息。|
|[ListStackGroupOperations](/cn.zh-CN/API参考/资源栈组相关接口/ListStackGroupOperations.md)|调用ListStackGroupOperations接口查询资源栈组操作列表。|
|[StopStackGroupOperation](/cn.zh-CN/API参考/资源栈组相关接口/StopStackGroupOperation.md)|调用StopStackGroupOperation接口停止资源栈组操作。|
|[ListStackGroupOperationResults](/cn.zh-CN/API参考/资源栈组相关接口/ListStackGroupOperationResults.md)|调用ListStackGroupOperationResults接口查询资源栈组操作结果列表。|

## 偏差检测相关接口

|API|描述|
|---|--|
|[UpdateStackTemplateByResources](/cn.zh-CN/API参考/偏差检测相关接口/UpdateStackTemplateByResources.md)|调用UpdateStackTemplateByResources接口修正资源栈模板，消除资源栈的偏差。|
|[DetectStackDrift](/cn.zh-CN/API参考/偏差检测相关接口/DetectStackDrift.md)|调用DetectStackDrift接口对资源栈进行偏差检测。|
|[DetectStackGroupDrift](/cn.zh-CN/API参考/偏差检测相关接口/DetectStackGroupDrift.md)|调用DetectStackGroupDrift接口对资源栈组进行偏差检测。|
|[DetectStackResourceDrift](/cn.zh-CN/API参考/偏差检测相关接口/DetectStackResourceDrift.md)|调用DetectStackResourceDrift接口对资源进行偏差检测。|
|[GetStackDriftDetectionStatus](/cn.zh-CN/API参考/偏差检测相关接口/GetStackDriftDetectionStatus.md)|调用GetStackDriftDetectionStatus接口查询偏差检测的状态。|
|[ListStackResourceDrifts](/cn.zh-CN/API参考/偏差检测相关接口/ListStackResourceDrifts.md)|调用ListStackResourceDrifts接口查询资源栈的资源偏差详情。|

## 标签相关接口

|API|描述|
|---|--|
|[TagResources](/cn.zh-CN/API参考/标签相关接口/TagResources.md)|调用TagResources接口为指定的ROS资源列表创建并绑定标签。|
|[UntagResources](/cn.zh-CN/API参考/标签相关接口/UntagResources.md)|调用UntagResources接口为指定的ROS资源列表统一解绑并删除标签。|
|[ListTagResources](/cn.zh-CN/API参考/标签相关接口/ListTagResources.md)|调用ListTagResources接口查询一个或多个ROS资源已经绑定的标签。|
|[ListTagKeys](/cn.zh-CN/API参考/标签相关接口/ListTagKeys.md)|调用ListTagKeys接口查询标签键。|
|[ListTagValues](/cn.zh-CN/API参考/标签相关接口/ListTagValues.md)|调用ListTagValues接口查询指定标签键对应的标签值。|

## 其他接口

|API|描述|
|---|--|
|[DescribeRegions](/cn.zh-CN/API参考/其他接口/DescribeRegions.md)|调用DescribeRegions接口查询地域列表。|
|[SignalResource](/cn.zh-CN/API参考/其他接口/SignalResource.md)|调用SignalResource接口发送信号。|
|[SetDeletionProtection](/cn.zh-CN/API参考/其他接口/SetDeletionProtection.md)|调用SetDeletionProtection接口修改资源栈的删除保护属性。|
|[ListStackOperationRisks](/cn.zh-CN/API参考/其他接口/ListStackOperationRisks.md)|调用ListStackOperationRisks接口检测删除资源栈操作可能涉及的高风险资源，并返回每个资源对应的风险原因。|

