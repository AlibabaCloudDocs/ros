# Data structure

This topic describes the data structures of four change sets, which are Change, ResourceChange, ResourceChangeDetail, and ResourceTargetDefinition.

## Change

|Parameter|Type|Description|
|---------|----|-----------|
|ResourceChange|Structure|The resource that ROS will change and the operation that ROS will perform.|
|Type|String|The type of the object to which the changes are made. Only `Resource` is supported.|

## ResourceChange

|Parameter|Type|Description|
|---------|----|-----------|
|Action|String|The operation that you want to perform. Valid values: -   `Add`: creates resources.
-   `Modify`: modifies resources.
-   `Remove`: releases resources. |
|Details|Array|The detailed changes that are made to resources. This parameter is displayed only when the `Action` parameter is set to `Modify`.|
|LogicalResourceId|String|The logical ID of the resource as defined in the template.|
|PhysicalResourceId|String|The physical ID of the resource. When the `Action` parameter is set to `Add`, no physical ID is available because the resource has not been created.|
|Replacement|String|Specifies whether ROS replaces resources by creating new resources and deleting the original ones when the `Action` parameter is set to `Modify`. Valid values:

-   `True`: ROS replaces resources by creating new resources and deleting the original ones.
-   `False`: ROS does not replace resources by creating new resources and deleting the original ones.
-   `Conditional`: ROS may replace resources by creating new resources and deleting the original ones.

The value of this parameter depends on the `RequiresRecreation` value in the `ResourceTargetDefinition` structure. -   If the `RequiresRecreation` parameter is set to `Always` and the `Evaluation` parameter is set to `Static`, the value of the `Replacement` parameter is `True`.
-   If the `RequiresRecreation` parameter is set to `Always` and the `Evaluation` parameter is set to `Dynamic`, the value of the `Replacement` parameter is `Conditional`.
-   If there are multiple changes on a single resource and each change has a different value for the `RequiresRecreation` parameter, the value of the `Replacement` parameter depends on the change operation that has the greatest impact. The impact of change operations is in the following descending order: `Always`, `Conditional`, `Never`. |
|ResourceType|String|The type of the ROS resource.|
|Scope|String array|The parameter that triggers updates when the `Action` parameter is set to `Modify`. Valid values: -   `Properties`: The Properties parameter of the resource is updated
-   `Metadata`: The Metadata parameter of the resource is updated.
-   `DeletionPolicy`: The DeletionPolicy parameter of the resource is updated. |

## ResourceChangeDetail

|Parameter|Type|Description|
|---------|----|-----------|
|ChangeSource|String|The reason why an update is triggered. Valid values: -   `ResourceReference`: The referenced physical ID of another resource may be changed.
-   `ParameterReference`: The referenced parameter is changed.
-   `ResourceAttribute`: The referenced output attribute of another resource may be changed.
-   `DirectModification`: The template is modified.
-   `Automatic`: If the nested stack created through the `ALIYUN::ROS::Stack` resource has not been modified, ROS sets the `ChangeSource` parameter to `Automatic`. This is because the template of the nested stack may have already been changed. ROS does not update the nested stack template before you update the parent stack.
-   `System`: Specific conditions or internal mechanisms can trigger updates even if the input values for some resources have not been changed. Example: `ALIYUN::ROS::WaitConditionHandle`. |
|CausingEntity|String|The objects associated with the `ChangeSource` parameter. The mappings are as follows: -   When the ChangeSource parameter is set to `ResourceReference`, the CausingEntity value indicates the resource name.
-   When the ChangeSource parameter is set to `ParameterReference`, the CausingEntity value indicates the parameter name.
-   When the ChangeSource parameter is set to `ResourceAttribute`, the CausingEntity value indicates the `attribute name, in the "resource name.attribute name" format`.
-   When the ChangeSource parameter is set to `DirectModification`, the CausingEntity parameter is empty by default.
-   When the ChangeSource parameter is set to `Automatic`, the CausingEntity value indicates the resource name.
-   When the ChangeSource parameter is set to `System`, the CausingEntity value indicates the resource name. |
|Evaluation|String|Specifies whether ROS can determine the target values and whether original values are changed to target values before a change set is executed. Valid values: -   `Static`

When this parameter is set to `Static`, ROS can determine the target values and original values are changed to target values.

-   `Dynamic`

When this parameter is set to `Dynamic`, ROS cannot determine the target values. When ROS updates the stack, the target values depend on the results of internal functions such as `Ref` or `Fn::GetAtt`. |
|Target|Structure|The detailed information about parameters that trigger updates.|

## ResourceTargetDefinition

|Parameter|Type|Description|
|---------|----|-----------|
|Attribute|String|The parameter that triggers updates. Valid values: -   `Properties`: The Properties parameter of the resource is updated.
-   `Metadata`: The Metadata parameter of the resource is updated.
-   `DeletionPolicy`: The DeletionPolicy parameter of the resource is updated. |
|Name|String|When the `Attribute` parameter is set to `Properties`, this parameter takes effect, and the value specifies the specific attribute name. Otherwise, the value is set to `null`.|
|RequiresRecreation|String|Whether attribute changes lead to resource re-creation when the `Attribute` parameter is set to `Properties`. Valid values: -   `Never`: Attribute changes do not lead to resource re-creation.
-   `Conditionally`: Attribute changes may lead to resource re-creation.
-   `Always`: Attribute changes lead to resource re-creation. |

