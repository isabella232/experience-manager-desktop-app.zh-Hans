---
title: 安装和配置AEM桌面应用程序版本1.x
description: 安装并配置AEM桌面应用程序版本1.x以与AEM Assets服务器配合使用，并将资产映射为要作为驱动器装载到桌面上。
uuid: 79bc9de9-5708-41f9-ac43-68c1fd2a2129
contentOwner: AG
products: SG_EXPERIENCEMANAGER/6.5/ASSETS, SG_EXPERIENCEMANAGER/6.4/ASSETS,SG_EXPERIENCEMANAGER/6.3/ASSETS
discoiquuid: f6365302-1690-4719-9b8c-035719422740
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 0820ad90cc89e2d2571c9f6c43c1e60734b7ade0
workflow-type: tm+mt
source-wordcount: '957'
ht-degree: 0%

---


# 安装和配置AEM桌面应用程序v1.x {#install-and-configure-aem-desktop-app}

使用AEM桌面应用程序，AEM中的资源可在您的本地桌面上轻松访问，并可用于任何桌面应用程序。 资产可以轻松地在Mac Finder或Windows资源管理器中显示，在桌面应用程序中打开，并在本地进行更改——上传时，更改将保存回AEM，并在存储库中创建新版本。

这种集成允许组织中的不同角色集中管理AEM Assets的资产，并在Creative Cloud和其他应用程序中访问这些资产，同时使企业能够轻松遵守包括品牌在内的各种标准。

要使用AEM桌面应用程序，

* 确保AEM桌面应用程序支持AEM服务器版本。 请参阅兼 [容性矩阵](release-notes-of-v1.md#compatibilitymatrix)。

* 下载并安装应用程序。

* 使用一些资源测试连接。 请参 [阅在桌面上访问和打开资产](use-app-v1.md#openondesktop)。

## 系统要求、先决条件和下载链接 {#system-requirements-prerequisites-and-download-links}

有关详细信息，请参阅AEM [桌面应用程序发行说明](release-notes-of-v1.md)。

## 安装AEM桌面应用程序并将其连接到AEM服务器 {#install-and-connect-aem-desktop-app-to-aem-server}

有关详细信息，请参 [阅安装AEM桌面应用程序并将其连接到AEM服务器](use-app-v1.md#installandconnect)。

>[!NOTE]
>
>一次只能安装AEM桌面应用程序的一个实例并处于活动状态。

## 文件处理 {#file-handling}

当从桌面应用程序装载的网络共享位置更改文件时，文件将分两个阶段保存到该位置。 在第一阶段，文件保存在本地。 用户可以保存文件并继续处理文件，无需等待传输完成。

在第二阶段，桌面应用程序在预定义的延迟（例如30秒）后将更新的文件上载到AEM服务器。 此操作在后台进行。 使用视图资产状态选项来视图上传操作的状态。

1. 将资产上传到AEM Assets。

1. 单击／点按工具栏中的AEM桌面应用程序图标。

1. 从菜单中，选择视图资产状态选项。

1. 在对话框中，查看上传操作的状态。

>[!NOTE]
>
>AEM桌面应用程序可处理高达40 GB的资源。

## 连接到调度程序后面的AEM实例 {#connect-to-an-aem-instance-behind-a-dispatcher}

资产API中的复制和移动方法需要将以下附加标头传递到AEM::

* X-目标
* X深度
* X覆盖

AEM desktop使用包含默认端口的URL连接到AEM。 因此，调 `virtualhosts` 度程序配置中的设置应包括默认端口号。 有关配置的更 `virtualhosts` 多信息，请 [参阅标识虚拟主机](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#identifying-virtual-hosts-virtualhosts)。

有关配置调度程序以传递这些附加标头的其他信息，请参 [阅指定HTTP标头](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#specifying-the-http-headers-to-pass-through-clientheaders)。

### 代理支持 {#proxy-support}

AEM桌面应用程序使用系统的预定义代理通过HTTPS连接到Internet。 应用程序只能使用不需要额外身份验证的网络代理进行连接。

如果为Windows配置或修改代理服务器设置（“Internet选项”>“LAN设置”），请重新启动AEM桌面应用程序以使更改生效。

>[!NOTE]
>
>仅在开始桌面应用程序时才应用代理配置。 关闭并重新启动应用程序，以使任何更改生效。

如果您的代理需要身份验证，则IT团队可以允许代理服务器设置中的Experience Manager资产URL允许应用程序通信通过。

## 自定义资产信息对话框 {#customize-the-asset-info-dialog}

您可以通过覆盖以下一个或两个组件来自定义资产信息对话框：

* 位于的Granite用户界面页 `/libs/dam/gui/content/assets/moreinfo`面。

* 位于的 `/css/javascript` HTL组 `/libs/dam/gui/components/admin/moreinfo`件。

哪个组件会被覆盖，具体取决于自定义的性质。 要更改作为“资产信息”对话框一部分显示的组件，请叠加Granite用户界面页。 要更改对话框的HTML、CSS或Javascript内容，请叠加HTL组件。

## 管理缓存 {#manage-cache}

在Windows上，缓存位于， `%LOCALAPPDATA%\Adobe\AssetsCompanion\Cache\`其中是在桌面应用程序中配置的AEM主机的编码版本。 例如， `http://localhost:4502` 显示 `http%3A%2F%2Flocalhost%3A4502%2F`为。

在Mac OS X上，类似的目录位于 `~/Library/Group Containers/group.com.adobe.aem.desktop/cache`。

### 用于管理缓存的应用程序内选项 {#in-app-option-to-manage-cache}

您可以控制可用于本地缓存的磁盘空间量。 来自AEM Assets服务器的工件在本地缓存，以获得更流畅的体验。 您可以更改默认值以符合您的要求。 此外，还可以清除缓存以重新提取所有资产。 要设置所需的选项，请单击应用程序的图标，然 **[!UICONTROL Advanced]** 后单 **[!UICONTROL Manage Cache]**&#x200B;击>。 ****

>[!NOTE]
>
>清除缓存时，它保留未保存的更改。 未签入AEM服务器的所有资产都将保留且不会删除。

### 更改Windows上缓存的位置 {#change-location-of-cache-on-windows}

AEM桌面应用程序的缓存的默认位置如下：

* 在Windows中 `%LocalAppData%\Adobe\AssetsCompanion\Cache\EncodedAEMEndpoint`。

* 在Mac中 `~/Library/Group/Containers/group.com.adobe.aem.desktop/cache/EncodedAEMEndpoint`。

`EncodedAEMEndpoint` 是AEM桌面应用程序配置的AEM端点URL。 该值是AEM服务器的目标URL的编码版本。 例如，如果应用程序正在定 `http://localhost:4502`位，则目录名称为 `http%3A%2F%2Flocalhost%3A4502`。 此示例中缓存目录的Windows路径为 `%LocalAppData%\Adobe\AssetsCompanion\Cache\http%3A%2F%2Flocalhost%3A4502`。

要将应用程序指向其他文件夹或其他驱动器，请编辑应用程序的配置文件。

1. 导航到应用程序的安装目录。 Windows上的默认位置为 `C:\Program Files (x86)\Adobe\Adobe Experience Manager Desktop`。

1. 使用文本编辑器编辑Adobe Experience ManagerDesktop.exe.config文件。

   需要管理员权限才能保存对此文件所做的更改。

1. 搜索字符串“ProxyCacheRoot”。 您将看到其值设置为缓存位置 `%LocalAppData%\Adobe\AssetsCompanion\Cache`。 只需将此值更改为任何有效路径。

   >[!NOTE]
   >
   >应用程序会自动创建 *&lt;已编码的AEM端点>* 子目录。 此行为不可配置。

>[!MORELIKETHIS]
* [AEM 桌面应用程序简介](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/creative-workflows/aem-desktop-app.html).
* [使用 AEM 桌面应用程序](use-app-v1.md).
* [AEM桌面应用程序疑难解答](troubleshoot-app-v1.md)。

