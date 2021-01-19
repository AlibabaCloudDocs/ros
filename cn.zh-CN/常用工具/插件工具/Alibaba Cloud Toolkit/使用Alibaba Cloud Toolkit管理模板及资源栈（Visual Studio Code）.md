# 使用Alibaba Cloud Toolkit管理模板及资源栈（Visual Studio Code）

在Visual Studio Code中安装和配置Alibaba Cloud Toolkit（以下简称Cloud Toolkit）后，您可以实现对ROS模板及资源栈便捷、高效的管理。

-   下载并安装[Visual Studio Code](https://code.visualstudio.com/)。
-   已在Visual Studio Code中安装和配置Cloud Toolkit，详情请参见[在Visual Studio Code中安装和配置Cloud Toolkit]()。

Cloud Toolkit是一个插件工具，可以帮助开发者更高效地部署、测试、开发和诊断应用。Cloud Toolkit详情，请参见[什么是Alibaba Cloud Toolkit]()。

ROS已经与Cloud Toolkit集成，当您在Visual Studio Code中安装和配置Cloud Toolkit后，可以管理模板和资源栈。

## 管理模板

Cloud Toolkit通过ROS LOCAL TEMPLATES模块管理本地模板，ROS REMOTE TEMPLATES模块管理远端模板。本地模板通过资源配置文件（.ros.config.yml）帮助您管理模板文件。

1.  在Visual Studio Code中打开工作文件夹。

2.  创建模板。

    1.  左侧菜单栏，单击![模板](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9590610061/p166656.png)。

    2.  单击**ROS LOCAL TEMPLATES**。

    3.  单击**+**，创建JSON或YAML格式的模板。

3.  编辑模板。

    -   **AlibabaCloud ROS YAML Template**示例

        ![yaml](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8590610061/p166659.gif)

    -   **AlibabaCloud ROS JSON Template**示例

        ![json](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8590610061/p166660.gif)

    **说明：**

    -   在Resources下输入资源类型关键字即可提示所有相关资源类型。
    -   模板语法错误时，Cloud Toolkit会自动提示。
4.  管理本地模板。

    1.  鼠标悬停在ROS LOCAL TEMPLATES，单击对应图标管理模板。

        ![本地模板-1](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1121420061/p166907.png)

        功能操作如下表所示：

        |功能|说明|
        |--|--|
        |**Open Folder**|打开文件夹。|
        |**Refresh**|刷新本地或远端目录。|
        |**Create**|创建本地模板。首次使用此插件创建模板默认会创建.ros.config.yml文件及JSON和YAML文件夹。|
        |**Upload**|上传本地模板至远端。|

    2.  右键单击本地模板，根据需求进行操作。

        ![本地模板](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8590610061/p166666.png)

        功能操作如下表所示：

        |功能|说明|
        |--|--|
        |**Delete**|删除本地模板。|
        |**Rename**|重命名本地模板名称。|
        |**Upload**|上传本地模板。**说明：** 上传模板后，本地模板将显示在ROS REMOTE TEMPLATES（远端模板列表）中。 |

    **说明：** 选中.ros.json或者.ros.yaml的本地模板后，您可以在模板编辑区单击鼠标右键，单击**Alibaba Cloud Ros - Create Stack**跳转到资源编排控制台**创建资源栈**页面，快速创建资源栈。

5.  管理远端模板。

    1.  鼠标悬停在ROS REMOTE TEMPLATES，单击对应图标管理模板。

        ![远端模板](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1121420061/p166917.png)

        功能操作如下表所示：

        |功能|说明|
        |--|--|
        |**Refresh**|刷新远端模板。|
        |**Update**|更新远端模板。|
        |**Download**|下载远端模板。|

    2.  右键单击远端模板，根据需求进行操作。

        ![远端模板](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1121420061/p166919.png)

        功能操作如下表所示：

        |功能|说明|
        |--|--|
        |**Delete**|删除远端模板。|
        |**Download**|下载远端模板。|
        |**Rename**|重命名远端模板。|
        |**Update**|更新远端模板。        1.  单击**Update**打开远端模板对比框。
        2.  编辑右侧模板。

**说明：** 左侧模板不可编辑。

        3.  单击鼠标右键，在弹出的对话框单击**Alibaba Cloud Ros - Update Template**。

![上传模板](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8937230061/p167239.png) |

        **说明：**

        -   单击远端模板，默认打开一个临时文件，您可以查看模板信息。
        -   鼠标悬浮至远端模板上显示模板属性信息。

## 管理资源栈

Alibaba Cloud Toolkit通过ALIBABA CLOUD VIEW模块帮助您便捷地管理远端资源栈（资源编排控制台的资源栈）。

1.  在Visual Studio Code中打开您的工程。

2.  单击左侧菜单栏![资源栈图标](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8590610061/p166692.png)。

3.  选择**Alibaba Cloud View** \> **ROS VIEW**，根据需求进行操作。

    ![stack](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9590610061/p166695.png)

    功能操作如下表所示：

    |功能|说明|
    |--|--|
    |**地域**|选择资源栈所在地域。|
    |**Search**|在当前地域下，搜索资源栈ID或资源栈名称；若未输入，则刷新当前地域资源栈列表。|
    |**Create Stack**|创建资源栈 ，自动跳转至ROS控制台创建资源栈页面。|
    |**Stack ID/Name**|单击名称，显示该资源栈属性信息。|
    |**Status**|显示该资源栈当前状态。|
    |**Create at**|显示该资源栈创建时间。|
    |**Outputs**|显示该资源栈的输出值信息。|
    |**Delete**|删除该资源栈。|
    |**More**|    -   **Properties**：显示该资源栈的属性信息。
    -   **Resources**：显示该资源栈内的所有资源信息。
    -   **Parameters**：显示该资源栈的参数信息。 |


## 联系我们

如您需要进一步的帮助或反馈相关需求，请添加客户支持群联系阿里云，钉钉群号为11783495。

![客户支持群](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2192649951/p96978.png)

