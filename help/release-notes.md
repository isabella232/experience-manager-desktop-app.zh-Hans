---
title: '[!DNL Adobe Experience Manager] 桌面应用程序发行说明'
description: ' [!DNL Adobe Experience Manager] 桌面应用程序的发行详细信息、增强功能、新增功能、兼容性和下载链接。'
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: a25c1fa13895ae9eb7268e3e01c83a5f0b9d7d1d
workflow-type: tm+mt
source-wordcount: '1346'
ht-degree: 37%

---


# [!DNL Adobe Experience Manager] 桌面应用程序发行说明  {#release-notes-v2}

| 产品 | [!DNL Adobe Experience Manager] 桌面应用程序 |
|--- |--- |
| 应用程序版本（修订版） | 2.1(2.1.0.0) |
| 支持的[!DNL Adobe Experience Manager]版本 | [!DNL Experience Manager] 作为 [!DNL Cloud Service]; [!DNL Experience Manager] 6.5; [!DNL Experience Manager] 6.4; [!DNL Experience Manager] 6.3（带兼容包） |
| 类型 | 次要版本 |
| 发布日期 | 2020年12月17日（Mac和Win） |
| 下载 URL | [macOS 64位](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/adobe/aem-desktop-app/aem-desktop-osx-2.1.0.0.dmg); [Windows 64位](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/adobe/aem-desktop-app/aem-desktop-win64-2.1.0.0.exe); [Windows 32位](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/adobe/aem-desktop-app/aem-desktop-win32-2.1.0.0.exe) |

## 系统要求和先决条件 {#system-requirements-and-prerequisites-v2}

[!DNL Adobe Experience Manager] 桌面应用程序与以下操作系统兼容：

* Mac OS X 10.14或更高版本，并修复了最新错误。

* 带有最新服务包和错误修复的Windows 10。

>[!NOTE]
>
>供应商不再支持Windows 7(https://support.microsoft.com/en-us/help/4057281/windows-7-support-ended-on-january-14-2020)。

该应用程序适用于以下[!DNL Experience Manager]版本，无论是作为[!DNL Cloud Service]部署在Adobe Managed Services(AMS)上还是部署在内部：

* [[!DNL Experience Manager] as a [!DNL Cloud Service]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/home.html).

* [[!DNL Experience Manager] 6.5.0或更](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/service-pack/sp-release-notes.html) 高版本。

* [[!DNL Experience Manager] 6.4.4或更](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/sp-release-notes.html) 高版本。

* [!DNL Experience Manager] 6.4.0 - 6.4.3，兼容 [包](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/featurepack/adobe-asset-link-support)。

>[!NOTE]
>
>[!DNL Experience Manager] 6.3桌面应用程序支持已弃用。 Adobe建议升级到较新且受支持的[!DNL Adobe Experience Manager]版本。
>[!DNL Experience Manager] 6.3.3.1或更高版本在安装[兼容性包](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/featurepack/adobe-asset-link-support)后可与桌面应用程序一起使用。 [!DNL Experience Manager] 6.3中没有此类包，因为没有计划[服务包](https://helpx.adobe.com/cn/experience-manager/maintenance-releases-roadmap.html)。

您计划在本地计算机上安装的应用程序的版本需要特定的[!DNL Adobe Experience Manager]服务器版本／其他服务器端组件（服务包、热修复或功能包）。 请与[!DNL Experience Manager]管理员联系以获取帮助。

### 支持不同的资源和文件类型{#support-for-file-types}

应用程序支持存储在[!DNL Experience Manager]中的资源，这些资源代表其基本操作的二进制文件。 在本机桌面应用程序中打开文件，取决于特定文件类型（如 PNG 或 JPG）与特定应用程序（如 Mac Preview 或 Adobe Photoshop）的操作系统关联。

一些文件类型支持将链接的资产放入二进制文件中。当使用桌面应用程序打开此类二进制文件时，如果[!DNL Experience Manager]存储库中存在资产，则应用程序将预先下载链接的资产。 当前支持的文件类型有：

* [!DNL Adobe InDesign] 文件（INDD格式）
* [!DNL Adobe Illustrator] 文件（AI格式）
* [!DNL Adobe Photoshop] 文件（PS格式）

上述应用程序的[!DNL Adobe Creative Cloud] 2018和[!DNL Adobe Creative Cloud] 2019版支持此功能。 应用程序使用启发式、最佳匹配方法将链接资源的本地桌面路径映射到[!DNL Experience Manager]服务器上的URL。 这是基于以下假设：

* 到本机应用程序中所放置文件的路径使用全局桌面路径（从本地网络共享中放置，显示[!UICONTROL Reveal]选项）。

* 路径由本机应用程序存储在文件的 XMP 记录中.

* [!DNL Experience Manager] 已提取 XMP 记录，其中包含资产元数据记录的路径.

* 路径可以与[!DNL Experience Manager]中的资产匹配，即，所放置的文件也位于[!DNL Experience Manager]中的匹配路径下。

## 新增功能和增强功能 {#whats-new-added}

要了解详细信息，请参阅[v2.0](introduction.md#whats-new-v2)中的新增功能。

**应用程序v2.1.0.0中的更新**

* 要上传资产，用户现在可以直接从Windows资源管理器或Mac Finder中拖动应用程序界面上的文件或文件夹。 除了应用程序中以前提供的上载选项外，还可以使用该选项。

**应用程序v2.0.3中的更新**

当前版本中修复的错误为：

* 修复了Windows用户尝试使用应用程序访问[!DNL Adobe Experience Manager] 6.5.5.0实例上的DAM存储库时遇到的登录问题。

**应用程序v2.0.2中的更新**

错误修复和更新包括：

* 要提高上传性能，请在[!UICONTROL Preferences]中增加上传加速。 打开此设置后，应用程序使用的本地CPU线程越多，占用的资源也越多。

* 修复了文件名或路径包含某些GB18030字符时资源上传的问题。<!-- CQ-4283494 -->

* 在搜索结果中切换到其他排序类型后，可以使用“按相关性排序”选项。<!-- CQ-4286874 -->

* 桌面应用程序现在可列表子文件夹，无需显式刷新。<!-- CQ-4285711 -->

* (Windows)修复了某些Windows计算机上不可用的应用程序界面的罕见问题。 用户无法单击应用程序界面，因为界面元素的单击区域会出现扭曲，并会侧移。<!-- CQ-4280785 -->

**应用程序v2.0.1中的更新**

错误修复和更新包括：

* 允许选项将`%Temp%`目录配置为与`%APPDATA%`路径匹配。<!-- CQ-4282665 -->

* 允许用户通过Okta SAML身份验证登录[!DNL Experience Manager]作者。<!-- CQ-4278134 -->

## 安装说明 {#installation-instructions-v2}

要了解如何安装和配置应用程序，请参阅[安装 [!DNL Experience Manager] 桌面应用程序](install-upgrade.md)。

如果您是从以前的[!DNL Experience Manager]桌面应用程序升级，则必须遵循以下转换最佳实践，这些最佳实践在从先前版本](install-upgrade.md#upgrade-from-previous-version)升级时列出。[

## 关于应用程序工作方式的重要说明 {#how-app-works}

请务必了解关于应用程序及其工作方式的以下信息。

* 该应用程序可全面控制需要从[!DNL Experience Manager]到（打开、编辑、上传更改和上传资产）完全传输资产二进制文件的操作。

   * 如果想要在桌面上处理资产，您需要明确地在某个文件夹中逐个或通过多选方式打开、编辑资产或将其下载到桌面。

   * 如果要获取对上传到[!DNL Experience Manager]的资产进行的本地更改，您需要单独或通过多选方式选择[!UICONTROL Upload Changes]。

   * 应用程序不是跨桌面和[!DNL Experience Manager]同步资源的“同步客户端”。

   * 应用程序不提供将[!DNL Experience Manager]存储库映射为虚拟文件夹结构的网络共享。

* 该应用程序显示的资产列表基于 Assets 存储库的状态。对于任何下载到本地后在本地文件或缓存文件夹中重命名的文件，该应用程序不会显示或管理这些文件。

* 如果该应用程序不显示预期结果，请单击顶栏中的刷新图标。

* 使用 [!UICONTROL Reveal File] 操作时显示的本地网络共享，仅显示本地可用的文件（和文件夹）。[!UICONTROL Reveal File] 和 [!UICONTROL Reveal Folder] 会预下载资产，以帮助在本地网络共享中显示正确的资产。

* 当 Adobe Creative Cloud 应用程序读取链接/放置在 Creative Cloud 应用程序本机文件中的资产文件时，会使用 SMB (Mac)/WebDAV (Win) 本地网络共享。

下图说明了由用户操作启动的资产和文件从云端到本地文件系统（以及从本地文件系统到云端）的流程。

![[!DNL Experience Manager]资产通过桌面应用程序从 服务器流向本机桌面应用程序](assets/da20_flow_diagram.png)

## 已知问题 {#known-issues-v2}

**用户界面问题：**

* 有时，桌面应用程序的界面可能变为空白。 右键单击并单击[!UICONTROL Refresh]以重新加载应用程序。 刷新后，您将开始到DAM存储库的根。 资产的更新或状态将保留。<!-- CQ-4270267 -->

* 无需触控板或鼠标指针，就难以导航文件夹／搜索结果。 没有鼠标滚轮，鼠标设备上可能不显示滚动条。<!-- CQ-4269947 -->

* 在少数情况下，上传资产更改时，无法正确显示进度栏。

* 在应用筛选器以查找所有本地编辑的资产和删除筛选器后，应用程序不会为用户呈现搜索结果或者用户开始执行筛选时所在的文件夹视图。应用程序会显示 DAM 存储库的根文件夹。

* 有时，当连接到未运行[!DNL Experience Manager]服务器的URL时，连接屏幕会变得不响应。 可退出应用程序后重新启动。

**CRUD（创建、读取、更新和删除）问题：**

* 应用程序尝试上传包含无效字符的文件，可能会导致服务器端上传失败。<!-- CQ-4273652 -->

* 将更改上传到包含注释的资产时，注释会与资产一起存储在[!DNL Experience Manager]中，但不会作为版本控制注释显示。 此问题已在[!DNL Experience Manager] 6.4.5和[!DNL Experience Manager] 6.5.1中解决。Adobe建议安装最新的服务包。<!-- CQ-4268990 -->

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

