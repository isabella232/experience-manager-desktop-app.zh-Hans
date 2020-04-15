---
title: Adobe Experience Manager桌面应用程序发行说明
description: Adobe Experience Manager桌面应用程序的发行详细信息、增强功能、新增功能、兼容性和下载链接。
uuid: b783c3f8-aa1e-4c05-b687-5894909769f5
contentOwner: AG
products: SG_EXPERIENCEMANAGER/6.3/ASSETS
discoiquuid: 3052549b-fe75-44fb-a55e-5cc612868f54
index: y
internal: n
snippet: y
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: aca68b0c2eb363e33c8a6edec2370758124a4b9e

---


# Adobe Experience Manager桌面应用程序发行说明 {#release-notes-v2}

| 产品 | Adobe Experience Manager 桌面应用程序 |
|----|----|
| 应用程序版本（修订版） | 2.0 (2.0.2.0) |
| 支持的 AEM 版本 | AEM作为云服务；AEM 6.5;AEM 6.4;AEM 6.3（带有兼容性包） |
| 类型 | 次要版本 |
| 发布日期 | 2020年4月15日（Mac和Win） |
| 下载 URL | [macOS 64位](https://download.macromedia.com/aem-assets-companion-app/aem-desktop-osx-2.0.2.0.dmg); [Windows 64位](https://download.macromedia.com/aem-assets-companion-app/aem-desktop-win64-2.0.2.0.exe); [Windows 32位](https://download.macromedia.com/aem-assets-companion-app/aem-desktop-win32-2.0.2.0.exe) |

## 系统要求和先决条件 {#system-requirements-and-prerequisites-v2}

Adobe Experience Manager桌面应用程序与以下操作系统兼容：

* Mac OS X 10.10 或更高版本（带有最新的错误修复）。
* Windows 7 和 Windows 10（带有最新的 Service Pack 和错误修复）。

该应用程序适用于以下Experience Manager版本，无论是作为云服务部署在Adobe Managed Services(AMS)上还是内部部署：

* [Experience Manager 云服务](https://docs.adobe.com/content/help/zh-Hans/experience-manager-cloud-service/release-notes/home.html)
* [Experience Manager 6.5.0+或更高版本](https://docs.adobe.com/content/help/en/experience-manager-65/release-notes/release-notes.html)
* [Experience Manager 6.4.4+](https://docs.adobe.com/content/help/en/experience-manager-64/release-notes/release-notes.html) 或更高版本
* Experience Manager 6.4.0 - 6.4.3兼容 [包](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/featurepack/adobe-asset-link-support)

>[!NOTE]
>
>已弃用Experience Manager 6.3桌面应用程序支持。 Adobe建议升级到更新且受支持的Adobe Experience Manager版本。
>Experience Manager 6.3.3.1或更高版本可在安装兼容性包后与桌面应用程 [序一起使用](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/featurepack/adobe-asset-link-support)。 Experience Manager 6.3没有此类包，因为计划中没 [有服务包](https://helpx.adobe.com/cn/experience-manager/maintenance-releases-roadmap.html)。

您计划在本地计算机上安装的应用程序版本，需要特定的 Adobe Experience Manager 服务器版本/其他服务器端组件（服务包、修补程序或功能包）。请与Adobe Experience Manager管理员联系以获取帮助。

### Support for different assets and file types {#support-for-file-types}

该应用程序支持存储在Adobe Experience Manager中的资源，这些资源代表用于其基本操作的二进制文件。 在本机桌面应用程序中打开文件，取决于特定文件类型（如 PNG 或 JPG）与特定应用程序（如 Mac Preview 或 Adobe Photoshop）的操作系统关联。

一些文件类型支持将链接的资产放入二进制文件中。当使用桌面应用程序打开此类二进制文件时，如果资产存在于Experience Manager存储库中，则应用程序会预下载链接的资产。 当前支持的文件类型有：

* Adobe InDesign 文件（INDD 格式）
* Adobe Illustrator 文件（AI 格式）
* Adobe Photoshop 文件（PS 格式）

上述应用程序的Adobe Creative Cloud 2018和Adobe Creative Cloud 2019版支持此功能。 应用程序使用启发式、最佳匹配方法将链接资产的本地桌面路径映射到Experience Manager服务器上的URL。 这是基于以下假设：

* Paths to placed files in the native application use a global desktop path (placed from the local network share shown with [!UICONTROL Reveal] option).
* 路径由本机应用程序存储在文件的 XMP 记录中.
* Experience Manager已提取XMP记录，其中包含资产的元数据记录路径。
* 路径可以与Experience Manager中的资产匹配，即，置入的文件也位于Experience Manager中的匹配路径下。

## 新增功能和增强功能 {#whats-new-added}

To know the details, see [What&#39;s new in v2.0](introduction.md#whats-new-v2).

**应用程序v2.0.2中的更新**

错误修复和更新包括：

* 要提高上传性能，请在中增加上传加速 [!UICONTROL Preferences]。 打开此设置后，应用程序使用的本地CPU线程越多，占用的资源也越多。
* 修复了文件名或路径包含某些GB18030字符时资产上传的问题。 <!-- CQ-4283494 -->
* 在搜索结果中切换到其他排序类型后，“按相关性排序”选项可用。 <!-- CQ-4286874 -->
* 桌面应用程序现在可列表子文件夹，无需显式刷新。 <!-- CQ-4285711 -->
* (Windows)修复了某些Windows计算机上应用程序界面不可用的罕见问题。 用户无法单击应用程序界面，因为界面元素的单击区域会“偏移”，该界面看起来会失真。 <!-- CQ-4280785 -->

**应用程序v2.0.1中的更新**

错误修复和更新包括：

* 允许选项将目 `%Temp%` 录配置为匹配 `%APPDATA%` 路径。 <!-- CQ-4282665 -->
* 允许用户通过Okta SAML身份验证登录AEM作者。 <!-- CQ-4278134 -->

## 安装说明 {#installation-instructions-v2}

To know how to install and configure the app, see [Install Experience Manager desktop app](install-upgrade.md).

If you are upgrading from a previous Experience Manager desktop app, you must follow these best practices for transitioning that are listed at [upgrade from previous version](install-upgrade.md#upgrade-from-previous-version).

## 关于应用程序工作方式的重要说明 {#how-app-works}

请务必了解关于应用程序及其工作方式的以下信息。

* 对于需要与 AEM 来回完全传输资产二进制文件的操作（打开、编辑、上传更改和上传资产），该应用程序会提供完全控制权。
   * 如果想要在桌面上处理资产，您需要明确地在某个文件夹中逐个或通过多选方式打开、编辑资产或将其下载到桌面。
   * 如果想要将对资产所做的本地更改上传到 AEM，您需要逐个或通过多选方式选择 [!UICONTROL Upload Changes]。
   * 该应用程序不是在桌面和 AEM 之间同步资产的“同步客户端”。
   * 该应用程序不提供将 AEM 存储库映射为虚拟文件夹结构的网络共享。
* 该应用程序显示的资产列表基于 AEM Assets 存储库的状态。对于任何下载到本地后在本地文件或缓存文件夹中重命名的文件，该应用程序不会显示或管理这些文件。
* 如果该应用程序不显示预期结果，请单击顶栏中的刷新图标。
* 使用 [!UICONTROL Reveal File] 操作时显示的本地网络共享，仅显示本地可用的文件（和文件夹）。[!UICONTROL Reveal File] 和 [!UICONTROL Reveal Folder] 会预下载资产，以帮助在本地网络共享中显示正确的资产。
* 当 Adobe Creative Cloud 应用程序读取链接/放置在 Creative Cloud 应用程序本机文件中的资产文件时，会使用 SMB (Mac)/WebDAV (Win) 本地网络共享。

下图说明了由用户操作启动的资产和文件从云端到本地文件系统（以及从本地文件系统到云端）的流程。

![资产通过桌面应用程序从 AEM 服务器流向本机桌面应用程序](assets/da20_flow_diagram.png)

## 已知问题 {#known-issues-v2}

**用户界面问题：**

* 有时，桌面应用程序的界面可能变为空白。 Right-click and click [!UICONTROL Refresh] to re-load the application. 刷新后，您将开始到DAM存储库的根。 资产的更新或状态会保留。 <!-- CQ-4270267 -->
* 在没有跟踪板或鼠标指针的情况下，很难导航文件夹／搜索结果。 The scroll-bar might not appear with mouse devices without mouse wheel. <!-- CQ-4269947 -->
* 在少数情况下，上传资产更改时，无法正确显示进度栏。
* 在应用筛选器以查找所有本地编辑的资产和删除筛选器后，应用程序不会为用户呈现搜索结果或者用户开始执行筛选时所在的文件夹视图。应用程序会显示 DAM 存储库的根文件夹。
* 有时，在连接到未运行 AEM 服务器的 URL 时，连接屏幕会变得无响应。可退出应用程序后重新启动。

**CRUD（创建、读取、更新和删除）问题：**

* 应用程序尝试上传包含无效字符的文件，可能会导致服务器端上传失败。<!-- CQ-4273652 -->
* 在将更改上传到包含注释的资产时，这些注释会与资产一起存储在AEM中，但不会显示为版本控制注释。 在AEM 6.4.5和AEM 6.5.1中解决了此问题。Adobe强烈建议安装最新的服务包。 <!-- CQ-4268990 -->
* 用户无法取消资产传输。如果意外触发了大量传输，请退出应用程序后重新启动。<!-- CQ-4278940 -->

**平台问题：**

* 有时，在 Windows 上，打开资产后其状态可能会立即变为 [!UICONTROL Edited Locally]，即使您可能没有进行任何编辑也是如此。可单击 [!UICONTROL Refresh] 进行更新。

>[!MORELIKETHIS]
>
>* [AEM as Cloud Service文档](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/landing/home.html)
>* [AEM as Cloud Service Assets文档](https://docs.adobe.com/content/help/zh-Hans/experience-manager-cloud-service/assets/home.html)
>* [如何使用Experience Manager桌面应用程序](using.md)
>* [安装和升级桌面应用程序](install-upgrade.md)
>* [最佳实践和故障诊断提示](troubleshoot.md)

