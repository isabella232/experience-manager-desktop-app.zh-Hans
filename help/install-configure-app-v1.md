---
title: 安装和配置AEM桌面应用程序版本1.x
description: 安装和配置AEM桌面应用程序版本1.x以与AEM Assets服务器一起使用，并将资产映射为要在桌面上作为驱动器装载的资产。
uuid: 79bc9de9-5708-41f9-ac43-68c1fd2a2129
contentOwner: AG
products: SG_EXPERIENCEMANAGER/6.3/ASSETS
discoiquuid: f6365302-1690-4719-9b8c-035719422740
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: b92e47456f9e16c24eac43d1c5fef9a582f143b5

---


# 安装和配置AEM桌面应用程序v1.x {#install-and-configure-aem-desktop-app}

使用AEM桌面应用程序，AEM中的资产可在本地桌面上轻松访问，并可用于任何桌面应用程序。 资产可以在Mac Finder或Windows资源管理器中轻松显示，在桌面应用程序中打开并在本地更改——上传时更改将保存回AEM，并在存储库中创建新版本。

此类集成允许组织中的不同角色集中管理AEM资产中的资产，并在Creative Cloud和其他应用程序中访问这些资产，同时使您能轻松遵守包括品牌在内的各种标准。

要使用AEM桌面应用程序，

* 确保AEM桌面应用程序支持您的AEM服务器版本。 请参阅兼 [容性矩阵](release-notes-of-v1.md#compatibilitymatrix)。
* 下载并安装应用程序。
* 使用一些资源测试连接。 请参 [阅在桌面上访问和打开资产](use-app-v1.md#openondesktop)。

## 系统要求、先决条件和下载链接 {#system-requirements-prerequisites-and-download-links}

有关详细信息，请参阅 [AEM桌面应用程序发行说明](release-notes-of-v1.md)。

## 安装AEM桌面应用程序并将其连接到AEM服务器 {#install-and-connect-aem-desktop-app-to-aem-server}

有关详细信息，请 [参阅安装AEM桌面应用程序并将其连接到AEM服务器](use-app-v1.md#installandconnect)。

>[!NOTE]
>
>一次只能安装AEM桌面应用程序的一个实例并处于活动状态。

## 代理支持 {#proxy-support}

AEM桌面应用程序使用系统的预定义代理通过HTTPS连接到Internet。 应用程序只能使用不需要额外身份验证的网络代理进行连接。

如果为Windows配置或修改代理服务器设置（“Internet选项”>“LAN设置”），请重新启动AEM桌面应用程序，以使更改生效。

如果您的代理需要身份验证，则IT团队可以在代理服务器设置中将AEM资产URL列入白名单，以允许应用程序通信通过。

## 文件处理 {#file-handling}

当从桌面应用程序装载的网络共享位置更改文件时，文件将分两个阶段保存到该位置。 在第一阶段，文件保存在本地。 用户可以保存文件并继续处理文件，无需等待传输完成。

在第二个阶段，桌面应用程序在预定义的延迟（例如，30秒）后将更新的文件上传到AEM服务器。 此操作在后台进行。 使用“视图资产状态”选项视图上传操作的状态。

1. 将资产上传到AEM资产。
1. 单击／点按工具栏中的AEM桌面应用程序图标。
1. 从菜单中，选择视图资产状态选项。
1. 从对话框中，查看上传操作的状态。

>[!NOTE]
>
>AEM桌面应用程序最多可处理40 GB的资产。

## 连接到调度程序后面的AEM实例 {#connect-to-an-aem-instance-behind-a-dispatcher}

资产API中的复制和移动方法需要将以下附加标头传递给AEM:

* X-Destination
* X-Depth
* X覆盖

AEM Desktop使用包含默认端口的URL连接到AEM。 因此，调 `virtualhosts` 度程序配置中的设置应包括默认端口号。 有关配置的详细 `virtualhosts` 信息，请参 [阅标识虚拟主机](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#identifying-virtual-hosts-virtualhosts)。

有关配置调度程序以传递这些附加标头的其他信息，请参 [阅指定HTTP标头](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#specifying-the-http-headers-to-pass-through-clientheaders)。

## 自定义“资产信息”对话框 {#customize-the-asset-info-dialog}

您可以通过覆盖以下组件之一或两者，自定义“资产信息”对话框：

* Granite用户界面页面： `/libs/dam/gui/content/assets/moreinfo`
* 位于的HTL `/css/javascript` 组件 `/libs/dam/gui/components/admin/moreinfo`

哪个组件被覆盖，取决于自定义的性质。 要更改在“资产信息”对话框中显示的组件，请叠加Granite用户界面页面。 要更改对话框的HTML/CSS/Javascript内容，请叠加HTL组件。

## 管理缓存 {#manage-cache}

在Windows上，缓存位于 `%LOCALAPPDATA%\Adobe\AssetsCompanion\Cache\`，其中是在桌面应用程序中配置的AEM主机的编码版本。 例如， `http://localhost:4502` 显示为 `http%3A%2F%2Flocalhost%3A4502%2F`。

在Mac OS X上，类似目录位于 `~/Library/Group Containers/group.com.adobe.aem.desktop/cache`。

### 用于管理缓存的应用程序内选项 {#in-app-option-to-manage-cache}

您可以控制可用于本地缓存的磁盘空间量。 AEM资产服务器中的对象将在本地缓存，以获得更流畅的体验。 您可以更改默认值以满足您的要求。 此外，您还可以清除缓存以重新获取所有资产。 要设置所需的选项，请单击应用程序的图标，然后单击 **[!UICONTROL Advanced]** > **[!UICONTROL Manage Cache]**。****

>[!NOTE]
>
>清除缓存时，它会保留未保存的更改。 未签入AEM服务器的所有资产将保留且不会删除。

### 在Windows上更改缓存位置 {#change-location-of-cache-on-windows}

AEM桌面应用程序缓存的默认位置为：

* Windows: `%LocalAppData%\Adobe\AssetsCompanion\Cache\EncodedAEMEndpoint`
* Mac: `~/Library/Group/Containers/group.com.adobe.aem.desktop/cache/EncodedAEMEndpoint`

`EncodedAEMEndpoint` 是AEM桌面应用程序已配置的AEM端点URL。 该值是AEM服务器的目标URL的编码版本。 例如，如果应用程序是定位的， `http://localhost:4502`则目录名称为 `http%3A%2F%2Flocalhost%3A4502`。 此示例中缓存目录的Windows路径为%LocalAppData%\Adobe\AssetsCompanion\Cache\http%3A%2F%2Flocalhost%3A4502。

要将应用程序指向其他文件夹或其他驱动器，请编辑应用程序的配置文件。

1. 导航到应用程序的安装目录。 Windows上的默认位置为 `C:\Program Files (x86)\Adobe\Adobe Experience Manager Desktop`。
1. 使用文本编辑器编辑Adobe Experience Manager Desktop.exe.config文件。

   保存对此文件所做的更改需要管理员权限。

1. 搜索字符串“ProxyCacheRoot”。 您会看到它的值已设置为缓存位置“%LocalAppData%\Adobe\AssetsCompanion\Cache”。 只需将此值更改为任何有效路径。

   >[!NOTE]
   >
   >应用程序会自动创建 *&lt;Encoded AEM Endpoint>子目录* ;此行为不可配置。

## 其他资源 {#additional-resources}

* [AEM 桌面应用程序简介](https://helpx.adobe.com/customer-care-office-hours/aem/desktop-app.html)
* [使用 AEM 桌面应用程序](use-app-v1.md)

* [了解AEM桌面应用程序的登记／注销](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/collaboration/checkin-checkout-technical-video-understand.html)
* [将桌面应用程序与AEM Assets结合使用](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/collaboration/checkin-checkout-technical-video-understand.html)
* [AEM桌面应用程序疑难解答](troubleshoot-app-v1.md)
