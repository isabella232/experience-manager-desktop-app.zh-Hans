---
title: '[!DNL Adobe Experience Manager] 桌面应用程序发行说明'
description: ' [!DNL Adobe Experience Manager] 桌面应用程序的发行详细信息、增强功能、新增功能、兼容性和下载链接。'
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 06ce2dc1c47bc1ba71b4fd1d053131d9dbdb08ba
workflow-type: tm+mt
source-wordcount: '1468'
ht-degree: 28%

---


# [!DNL Adobe Experience Manager] 桌面应用程序发行说明  {#release-notes-v2}

以下是最新桌面应用程序版本2.1(2.1.1.0)的发行信息。 发布日期为2021年3月5日。 它是一个次要版本，并且具有增强功能。

支持的&#x200B;**[!DNL Experience Manager]版本**&#x200B;为：

* [!DNL Experience Manager] as a [!DNL Cloud Service]. 请参阅[发行说明](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/home.html)。
* [!DNL Experience Manager] 6.5.0或更高版本，在Adobe Managed Services(AMS)或内部部署上提供。请参阅[ Service Pack发行说明](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/service-pack/sp-release-notes.html)。
* [!DNL Experience Manager] 6.4.4或更高版本，在Adobe Managed Services(AMS)或内部部署上提供。请参阅[ Service Pack发行说明](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/sp-release-notes.html)。
* [!DNL Experience Manager] 6.4.0 - 6.4.3，安装了 [兼](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/featurepack/adobe-asset-link-support) 容性包，位于Adobe Managed Services(AMS)或内部部署上。
* [!DNL Experience Manager] 6.3（带兼容包）
* [!DNL Experience Manager] 6.3.3.1或更高版本，并安 [装兼](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/featurepack/adobe-asset-link-support) 容包。[!DNL Experience Manager] 6.3.3.0或早期版本不支持桌面应用程序。

[!DNL Adobe Experience Manager] 桌面应用程序可用于以下 **操作系统**:

* macOS X 10.14或更高版本，并修复了最新错误。
* 带有最新服务包和错误修复的Windows 10。

支持的操作系统的&#x200B;**下载URL**&#x200B;为：

| 操作系统 | [!DNL Experience Manager] as a [!DNL Cloud Service] | [!DNL Experience Manager] 6.x |
|---|---|---|
| macOS 64位 | [下载链接](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-desktop-app/aem-desktop-osx-2.1.1.0.dmg) | [下载链接](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/adobe/aem-desktop-app/aem-desktop-osx-2.1.1.0.dmg) |
| Windows 64位 | [下载链接](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-desktop-app/aem-desktop-win64-2.1.1.0.exe) | [下载链接](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/adobe/aem-desktop-app/aem-desktop-win64-2.1.1.0.exe) |
| Windows 32位 | [下载链接](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-desktop-app/aem-desktop-win32-2.1.1.0.exe) | [下载链接](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/adobe/aem-desktop-app/aem-desktop-win32-2.1.1.0.exe) |

>[!NOTE]
>
>不再支持Windows 7。 请参阅[有关Windows 7的EOL的文章](https://support.microsoft.com/en-us/help/4057281/windows-7-support-ended-on-january-14-2020)。

<!-- The version of the app you plan to install on your local machine requires a specific [!DNL Adobe Experience Manager] server version/additional server-side components (service packs, hot fixes, or feature packs). Contact your [!DNL Experience Manager] administrator for help.
-->

## 支持不同的资源和文件类型{#support-for-file-types}

应用程序支持存储在[!DNL Experience Manager]中的资源，这些资源表示用于其基本操作的二进制文件。 在本机桌面应用程序中打开文件，取决于特定文件类型（如 PNG 或 JPG）与特定应用程序（如 Mac Preview 或 Adobe Photoshop）的操作系统关联。

一些文件类型支持将链接的资产放入二进制文件中。当使用桌面应用程序打开此类二进制文件时，如果[!DNL Experience Manager]存储库中存在该资源，则应用程序会预下载链接的资源。 当前支持的文件类型有：

* [!DNL Adobe InDesign] 文件（INDD格式）
* [!DNL Adobe Illustrator] 文件（AI格式）
* [!DNL Adobe Photoshop] 文件（PS格式）

上述应用程序的[!DNL Adobe Creative Cloud] 2018和[!DNL Adobe Creative Cloud] 2019版支持此功能。 应用程序使用启发式、最佳匹配方法将链接资源的本地桌面路径映射到[!DNL Experience Manager]服务器上的URL。 这是基于以下假设：

* 指向本机应用程序中置入文件的路径使用全局桌面路径（通过显示[!UICONTROL Reveal]选项的本地网络共享放置）。

* 路径由本机应用程序存储在文件的 XMP 记录中.

* [!DNL Experience Manager] 已提取 XMP 记录，其中包含资产元数据记录的路径.

* 路径可以与[!DNL Experience Manager]中的资产匹配，即，所放置的文件也位于[!DNL Experience Manager]中的匹配路径下。

## 新增功能、增强和错误修复{#what-is-new}

要了解详细信息，请参阅[v2.0](introduction.md#whats-new-v2)中的新增功能。

**在应用程序v2.1.1.0中更新**

* 通过高级设置，应用程序可以在上传文件夹时模拟v1.10应用程序行为。 在v1.10中，在存储库中创建的节点名称使用用户提供的文件夹名称的空格和大小写。 v2.1的默认行为仍然保持不变，即，在存储库节点名称中用连字符替换文件夹名称中的多个空格，并转换为小写节点名称。 请参阅[应用程序首选项](/help/install-upgrade.md#set-preferences)。

**在应用程序v2.1.0.0中更新**

* 要上传资产，用户现在可以直接从Windows资源管理器或Mac Finder中拖动应用程序界面上的文件或文件夹。 除了应用程序中以前提供的上载选项外，此功能还有效。<!-- CQ-4309527 -->

**在应用程序v2.0.3中更新**

当前版本中修复的错误是：

* 修复了Windows上尝试访问[!DNL Adobe Experience Manager] 6.5.5.0上的DAM存储库的应用程序用户的登录问题。

**应用程序v2.0.2中的更新**

错误修复和更新包括：

* 上载加速设置现已可用于提高上载性能。 打开此设置后，应用程序通过使用更多本地CPU线程以更快的速度上载，并且资源占用更多。

* 当文件名或包含某些GB18030字符的路径已固定时，资源上传。<!-- CQ-4283494 -->

* 在搜索结果中切换到其他排序类型后，可使用“按相关性排序”选项。<!-- CQ-4286874 -->

* 桌面应用程序现在可列表子文件夹，无需显式刷新。<!-- CQ-4285711 -->

* (Windows)修复了某些Windows计算机上不可用的应用程序界面的罕见问题。 用户无法单击应用程序界面，因为界面元素的点击区域会侧向扭曲。<!-- CQ-4280785 -->

**应用程序v2.0.1中的更新**

错误修复和更新包括：

* 允许选项将`%Temp%`目录配置为与`%APPDATA%`路径匹配。<!-- CQ-4282665 -->

* 允许用户通过Okta SAML身份验证登录[!DNL Experience Manager]作者。<!-- CQ-4278134 -->

## 安装说明 {#installation-instructions-v2}

要了解如何安装和配置应用程序，请参阅[安装 [!DNL Experience Manager] 桌面应用程序](install-upgrade.md)。

如果您是从以前的[!DNL Experience Manager]桌面应用程序升级，则必须遵循以下转换最佳实践，这些最佳实践列在从以前版本](install-upgrade.md#upgrade-from-previous-version)升级时。[

## 关于应用程序工作方式的重要说明 {#how-app-works}

请务必了解关于应用程序及其工作方式的以下信息。

* 应用程序对需要从[!DNL Experience Manager]到（打开、编辑、上传更改和上传资产）的资产二进制文件完全传输的操作提供完全控制。

   * 如果要在桌面上使用资产，您必须显式地打开、编辑或下载到桌面，无论是单独打开、在文件夹中，还是通过多选方式。

   * 如果要获取对上传到[!DNL Experience Manager]的资产的本地更改，您需要单独或通过多选选择选择[!UICONTROL Upload Changes]。

   * 应用程序不是跨桌面和[!DNL Experience Manager]同步资源的“同步客户端”。

   * 应用程序不提供将[!DNL Experience Manager]存储库映射为虚拟文件夹结构的网络共享。

* 该应用程序显示的资产列表基于 Assets 存储库的状态。对于任何下载到本地后在本地文件或缓存文件夹中重命名的文件，该应用程序不会显示或管理这些文件。

* 如果该应用程序不显示预期结果，请单击顶栏中的刷新图标。

* 使用 [!UICONTROL Reveal File] 操作时显示的本地网络共享，仅显示本地可用的文件（和文件夹）。[!UICONTROL Reveal File] 和 [!UICONTROL Reveal Folder] 会预下载资产，以帮助在本地网络共享中显示正确的资产。

* 当 Adobe Creative Cloud 应用程序读取链接/放置在 Creative Cloud 应用程序本机文件中的资产文件时，会使用 SMB (Mac)/WebDAV (Win) 本地网络共享。

下图说明了资产和文件从云到本地文件系统的流，以及由用户操作启动的相反方式。

![[!DNL Experience Manager]资产通过桌面应用程序从 服务器流向本机桌面应用程序](assets/da20_flow_diagram.png)

## 已知问题 {#known-issues-v2}

**用户界面问题：**

* 有时，桌面应用程序的界面可能变为空白。 右键单击并单击[!UICONTROL Refresh]以重新加载应用程序。 刷新后，您将开始到DAM存储库的根。 资产的更新或状态会保留。<!-- CQ-4270267 -->

* 在没有跟踪板或鼠标指针的情况下很难导航文件夹/搜索结果。 没有鼠标滚轮，滚动条可能不随鼠标设备一起显示。<!-- CQ-4269947 -->

* 在少数情况下，上传资产更改时，无法正确显示进度栏。

* 在应用筛选器以查找所有本地编辑的资产和删除筛选器后，应用程序不会为用户呈现搜索结果或者用户开始执行筛选时所在的文件夹视图。应用程序会显示 DAM 存储库的根文件夹。

* 有时，当连接到未运行[!DNL Experience Manager]服务器的URL时，连接屏幕会变得不响应。 可退出应用程序后重新启动。

**CRUD（创建、读取、更新和删除）问题：**

* 应用程序尝试上传包含无效字符的文件，可能会导致服务器端上传失败。<!-- CQ-4273652 -->

* 在将更改上传到包含注释的资产时，这些注释会与资产一起存储在[!DNL Experience Manager]中，但不会显示为版本控制注释。 此问题已在[!DNL Experience Manager] 6.4.5和[!DNL Experience Manager] 6.5.1中解决。Adobe建议安装最新的服务包。<!-- CQ-4268990 -->

* 用户无法取消资产传输。如果意外触发了大量传输，请退出应用程序后重新启动。<!-- CQ-4278940 -->

**平台问题：**

* 有时，在 Windows 上，打开资产后其状态可能会立即变为 [!UICONTROL Edited Locally]，即使您可能没有进行任何编辑也是如此。可单击 [!UICONTROL Refresh] 进行更新。

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] as a [!DNL Cloud Service] 文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/landing/home.html)
>* [[!DNL Experience Manager] as a [!DNL Cloud Service] [!DNL Assets] 文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/home.html)
>* [如何使用桌 [!DNL Experience Manager] 面应用程序](using.md)
>* [安装和升级桌面应用程序](install-upgrade.md)
>* [最佳实践和故障诊断提示](troubleshoot.md)

