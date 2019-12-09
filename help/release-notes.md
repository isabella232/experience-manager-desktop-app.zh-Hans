---
title: AEM 桌面应用程序发行说明
description: AEM桌面应用程序的发行详细信息、增强功能、新增功能、兼容性和下载链接。
uuid: b783c3f8-aa1e-4c05-b687-5894909769f5
contentOwner: AG
products: SG_EXPERIENCEMANAGER/6.3/ASSETS
discoiquuid: 3052549b-fe75-44fb-a55e-5cc612868f54
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: ad5337c8e1697d0a37d3020d25802dc1d732f320

---


# AEM 桌面应用程序发行说明 {#release-notes-v2}

| 产品 | Adobe Experience Manager (AEM) 桌面应用程序 |
|---------------|--------------------------------------------------------------------|
| 应用程序版本（修订版） | 2.0 (2.0.0.4) |
| 支持的 AEM 版本 | AEM 6.5、AEM 6.4、AEM 6.3（带有兼容包） |
| 类型 | 主要版本 |
| 发布日期 | 2019 年 8 月 30 日 (Mac)，2019 年 9 月 9 日 (Win) |
| 下载 URL | [MacOS 64 位](https://download.macromedia.com/aem-assets-companion-app/aem-desktop-osx-2.0.0.4.dmg)；[Windows 64 位](https://download.macromedia.com/aem-assets-companion-app/aem-desktop-win64-2.0.0.4.exe)；[Windows 32 位](https://download.macromedia.com/aem-assets-companion-app/aem-desktop-win32-2.0.0.4.exe) |

## 系统要求和先决条件 {#system-requirements-and-prerequisites-v2}

AEM 桌面应用程序与以下操作系统兼容：

* Mac OS X 10.10 或更高版本（带有最新的错误修复）。
* Windows 7 和 Windows 10（带有最新的 Service Pack 和错误修复）。

该应用程序可与以下 AEM 版本配合使用，无论 AEM 是部署在本地还是 Adobe Managed Services (AMS) 上：

* [AEM 6.5.0](https://helpx.adobe.com/experience-manager/6-5/release-notes.html) 或更高版本
* [AEM 6.4.4](https://helpx.adobe.com/experience-manager/6-4/release-notes/sp-release-notes.html) 或更高版本
* AEM 6.4.0 - 6.4.3，带有[兼容包](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/featurepack/adobe-asset-link-support)
* AEM 6.3.3.1 及更高版本，带有[兼容包](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/featurepack/adobe-asset-link-support)
* 对于 AEM 6.3，没有[计划发布 Service Pack](https://helpx.adobe.com/experience-manager/maintenance-releases-roadmap.html)。Adobe 建议升级到更高的 AEM 版本。

您计划在本地计算机上安装的应用程序版本，需要特定的 Adobe Experience Manager 服务器版本/其他服务器端组件（服务包、修补程序或功能包）。如需帮助，请与 AEM 管理员联系。

### 支持不同的资产和文件类型 {#support-for-file-types}

该应用程序支持 AEM 中存储的资产，这些资产代表用于执行其基本操作的二进制文件。在本机桌面应用程序中打开文件，取决于特定文件类型（如 PNG 或 JPG）与特定应用程序（如 Mac Preview 或 Adobe Photoshop）的操作系统关联。

一些文件类型支持将链接的资产放入二进制文件中。当使用该桌面应用程序打开此类二进制文件时，如果资产存在于 AEM 存储库中，则应用程序会预下载链接的资产。当前支持的文件类型有：

* Adobe InDesign 文件（INDD 格式）
* Adobe Illustrator 文件（AI 格式）
* Adobe Photoshop 文件（PS 格式）

以上应用程序的 Adobe Creative Cloud 2018 和 Creative Cloud 2019 版本均支持该功能。该应用程序使用启发式的最佳匹配方法，将链接资产的本地桌面路径映射到 AEM 服务器上的 URL。这是基于以下假设：

* 在本机应用程序中放置文件的路径，使用的是全局桌面路径（从带有“显示”选项的本地网络共享放置）
* 路径由本机应用程序存储在文件的 XMP 记录中
* AEM 已提取 XMP 记录，其中包含资产元数据记录的路径
* 路径可以与 AEM 中的资产匹配（这意味着，放置的文件也位于 AEM 中的匹配路径下）

## 新增功能和增强功能 {#whats-new-added}

要了解详细信息，请参阅[应用程序的新增功能](introduction.md#whats-new-v2)。

## 安装说明 {#installation-instructions-v2}

要了解如何安装和配置应用程序，请参阅[安装 AEM 桌面应用程序](install-upgrade.md)。

如果您是从以前的 AEM 桌面应用程序升级，则必须按照[从以前的版本升级](install-upgrade.md#upgrade-from-previous-version)中列出的用于实现过渡的最佳实践来操作。

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
* 有时，桌面应用程序的界面可能变为空白。 Right-click and click [!UICONTROL Refresh] to re-load the application. 刷新后，您将从DAM存储库的根位置开始。 资产的更新或状态会保留。 <!-- CQ-4270267 -->
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
>* [AEM 6.5 文档](https://helpx.adobe.com/support/experience-manager/6-5.html)
>* [AEM Assets 6.5 文档](https://docs.adobe.com/content/help/en/experience-manager-64/assets/home.html)
>* [使用 AEM 桌面应用程序](using.md)
>* [安装和升级桌面应用程序](install-upgrade.md)
>* [最佳实践和故障诊断提示](troubleshoot.md)

