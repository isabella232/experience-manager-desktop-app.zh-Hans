---
title: 安装和配置桌面应用程序v1.10
description: 安装和配置 [!DNL Experience Manager] desktop app version 1.10 to work with [!DNL Assets] 服务器，并将要作为驱动器装载的资源映射到桌面。
translation-type: tm+mt
source-git-commit: cc4ce762ad1d7f4c5a54ab6bac9d1a872e3d18c9
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 0%

---


# 安装和配置[!DNL Experience Manager]桌面应用程序v1.10 {#install-and-configure-aem-desktop-app}

使用[!DNL Experience Manager]桌面应用程序，可在本地桌面上轻松访问[!DNL Experience Manager]中的资源，并可在任何桌面应用程序中使用。 资产可以在Mac Finder或Windows资源管理器中轻松显示，在桌面应用程序中打开，并在本地进行更改 — 当您上传时，更改将保存回[!DNL Experience Manager]并在存储库中创建新版本。

此类集成允许组织中的不同角色集中管理资产中的资产，并在Creative Cloud和其他应用程序中访问这些资产，同时使组织能轻松遵守包括品牌在内的各种标准。

要使用[!DNL Experience Manager]桌面应用程序，

* 确保[!DNL Experience Manager]桌面应用程序支持[!DNL Experience Manager]服务器版本。 请参见[兼容性矩阵](release-notes-of-v1.md#compatibilitymatrix)。

* 下载并安装应用程序。

* 使用一些资源测试连接。 请参阅[在桌面上访问和打开资源](use-app-v1.md#openondesktop)。

## 系统要求、先决条件和下载链接{#system-requirements-prerequisites-and-download-links}

有关详细信息，请参阅[[!DNL Experience Manager] 桌面应用程序发行说明](release-notes-of-v1.md)。

## 安装应用程序并将其连接到[!DNL Experience Manager]服务器{#install-and-connect-aem-desktop-app-to-aem-server}

有关详细信息，请参阅[安装并连接 [!DNL Experience Manager] desktop app to [!DNL Experience Manager] server](use-app-v1.md#installandconnect)。

>[!NOTE]
>
>一次只能安装[!DNL Experience Manager]桌面应用程序的一个实例并处于活动状态。

## 文件处理{#file-handling}

从桌面应用程序装载的网络共享位置更改文件时，文件将分两个阶段保存到该位置。 在第一阶段，文件保存在本地。 用户可以保存文件并继续处理文件，无需等待传输完成。

在第二阶段，桌面应用程序在预定义的延迟（例如30s）后将更新后的文件上载到[!DNL Experience Manager]服务器。 此操作在后台进行。 使用“视图资产状态”选项视图上传操作的状态。

1. 将资产上传到资产。

1. 单击工具栏中的[!DNL Experience Manager]桌面应用程序图标。

1. 从菜单中，选择视图资产状态选项。

1. 在对话框中，查看上载操作的状态。

>[!NOTE]
>
>[!DNL Experience Manager] 桌面应用程序可处理高达40 GB的资源。

## 连接到调度程序{#connect-to-an-aem-instance-behind-a-dispatcher}后面的[!DNL Experience Manager]实例

资产API中的复制和移动方法需要将以下附加标头传递给[!DNL Experience Manager]:

* X — 目标
* X深
* X覆盖

[!DNL Experience Manager] desktop使用包 [!DNL Experience Manager] 含默认端口的URL连接到。因此，调度程序配置中的`virtualhosts`设置应包括默认端口号。 有关`virtualhosts`配置的详细信息，请参阅[标识虚拟主机](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#identifying-virtual-hosts-virtualhosts)。

有关配置调度程序以传递这些附加标头的其他信息，请参阅[指定HTTP标头](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#specifying-the-http-headers-to-pass-through-clientheaders)。

### 代理支持{#proxy-support}

[!DNL Experience Manager] 桌面应用程序使用系统的预定义代理通过HTTPS连接到Internet。应用程序只能使用不需要额外身份验证的网络代理进行连接。

如果配置或修改Windows的代理服务器设置（“Internet选项”>“LAN设置”），请重新启动[!DNL Experience Manager]桌面应用程序，以使更改生效。

>[!NOTE]
>
>仅当开始桌面应用程序时才应用代理配置。 关闭并重新启动应用程序，以使任何更改生效。

如果您的代理需要身份验证，则IT团队可以允许代理服务器设置中的Experience Manager资产URL允许应用程序通信通过。

## 自定义“资产信息”对话框{#customize-the-asset-info-dialog}

您可以通过覆盖以下一个或两个组件来自定义“资产信息”对话框：

* 位于`/libs/dam/gui/content/assets/moreinfo`的Granite用户界面页。

* 位于`/libs/dam/gui/components/admin/moreinfo`的HTL `/css/javascript`组件。

哪个组件会被覆盖，具体取决于自定义的性质。 要更改在“资产信息”对话框中显示的组件，请叠加Granite用户界面页。 要更改对话框的HTML、CSS或JavaScript内容，请覆盖HTL组件。

## 管理缓存{#manage-cache}

在Windows上，缓存位于`%LOCALAPPDATA%\Adobe\AssetsCompanion\Cache\`，其中是在桌面应用程序中配置的[!DNL Experience Manager]主机的编码版本。 例如，`http://localhost:4502`显示为`http%3A%2F%2Flocalhost%3A4502%2F`。

在Mac OS X上，类似的目录位于`~/Library/Group Containers/group.com.adobe.aem.desktop/cache`。

### 用于管理缓存{#in-app-option-to-manage-cache}的应用程序内选项

您可以控制可用于本地缓存的磁盘空间量。 资产服务器中的对象将在本地缓存，以获得更流畅的体验。 您可以更改默认值以符合您的要求。 此外，您还可以清除缓存，重新提取所有资产。 要设置所需的选项，请单击应用程序图标，然后单击&#x200B;**[!UICONTROL Advanced]** > **[!UICONTROL Manage Cache]**。 ****

>[!NOTE]
>
>清除缓存时，会保留未保存的更改。 未签入[!DNL Experience Manager]服务器的所有资产都将保留，而不会删除。

### 更改Windows {#change-location-of-cache-on-windows}上缓存的位置

[!DNL Experience Manager]桌面应用程序的缓存的默认位置如下所示：

* 在Windows中，`%LocalAppData%\Adobe\AssetsCompanion\Cache\EncodedAEMEndpoint`。

* 在Mac中，`~/Library/Group/Containers/group.com.adobe.aem.desktop/cache/EncodedAEMEndpoint`。

`EncodedAEMEndpoint` 是应用程序配置 [!DNL Experience Manager] 的终结点URL。该值是[!DNL Experience Manager]服务器的目标URL的编码版本。 例如，如果应用程序针对`http://localhost:4502`，则目录名为`http%3A%2F%2Flocalhost%3A4502`。 此示例中缓存目录的Windows路径为`%LocalAppData%\Adobe\AssetsCompanion\Cache\http%3A%2F%2Flocalhost%3A4502`。

要将应用程序指向其他文件夹或其他驱动器，请编辑应用程序的配置文件。

1. 导航到应用程序的安装目录。 Windows上的默认位置为`C:\Program Files (x86)\Adobe\Adobe Experience Manager Desktop`。

1. 使用文本编辑器编辑Adobe Experience Manager Desktop.exe.config文件。

   需要管理员权限才能保存对此文件所做的更改。

1. 搜索字符串&quot;ProxyCacheRoot&quot;。 您会看到它的值设置为缓存位置`%LocalAppData%\Adobe\AssetsCompanion\Cache`。 只需将此值更改为任何有效路径。

   >[!NOTE]
   >
   >应用程序会自动创建&#x200B;*&lt;Encoded AEM Endpoint>*&#x200B;子目录。 不能配置此行为。

>[!MORELIKETHIS]
* [桌面应 [!DNL Experience Manager] 用程序简介](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/creative-workflows/aem-desktop-app.html)。
* [使 [!DNL Experience Manager] 用桌面应用程序](use-app-v1.md)。
* [桌面 [!DNL Experience Manager] 应用程序疑难解答](troubleshoot-app-v1.md)。

