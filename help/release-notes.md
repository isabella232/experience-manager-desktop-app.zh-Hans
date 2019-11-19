---
title: AEM桌面应用程序发行说明
description: AEM桌面应用程序的发行详细信息、增强功能、新增功能、兼容性和下载链接。
uuid: b783c3f8-aa1e-4c05-b687-5894909769f5
contentOwner: AG
products: SG_EXPERIENCEMANAGER/6.3/ASSETS
discoiquuid: 3052549b-fe75-44fb-a55e-5cc612868f54
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: f9c2347f8f17d32479207980fafba058825d986f

---


# AEM桌面应用程序发行说明 {#release-notes-v2}

| 产品 | Adobe Experience Manager(AEM)桌面应用程序 |
|---------------|--------------------------------------------------------------------|
| 应用程序版本（修订版） | 2.0 (2.0.0.4) |
| 支持的AEM版本 | AEM 6.5、AEM 6.4、AEM 6.3（带兼容包） |
| 类型 | 主要版本 |
| 发布日期 | 2019年8月30日(Mac),2019年9月9日(Win) |
| 下载URL | [MacOS 64位](https://download.macromedia.com/aem-assets-companion-app/aem-desktop-osx-2.0.0.4.dmg); [Windows 64位](https://download.macromedia.com/aem-assets-companion-app/aem-desktop-win64-2.0.0.4.exe); [Windows 32位](https://download.macromedia.com/aem-assets-companion-app/aem-desktop-win32-2.0.0.4.exe) |

## 系统要求和先决条件 {#system-requirements-and-prerequisites-v2}

AEM桌面应用程序与以下操作系统兼容：

* Mac OS X 10.10或更高版本，以及最新的错误修复。
* Windows 7和Windows 10，带有最新的Service pack和错误修复。

该应用程序适用于以下AEM版本，无论是内部部署还是在Adobe Managed Services(AMS)上部署：

* [AEM 6.5.0或更高版本](https://helpx.adobe.com/experience-manager/6-5/release-notes.html) ,
* [AEM 6.4.4或更高版本](https://helpx.adobe.com/experience-manager/6-4/release-notes/sp-release-notes.html) ,
* AEM 6.4.0 - 6.4.3，带兼容 [性包](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/featurepack/adobe-asset-link-support)
* AEM 6.3.3.1及更高版本，带有兼容 [性包](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/featurepack/adobe-asset-link-support)
* 对于AEM 6.3，不计 [划任何服务包](https://helpx.adobe.com/experience-manager/maintenance-releases-roadmap.html)。 Adobe建议升级到更高版本的AEM。

您计划在本地计算机上安装的应用程序版本需要特定的Adobe Experience manager服务器版本／其他服务器端组件（服务包、热修复或功能包）。 请与AEM管理员联系以获取帮助。

### 支持不同的资源和文件类型 {#support-for-file-types}

该应用程序支持存储在AEM中的资源，这些资源代表用于其基本操作的二进制文件。 在本机桌面应用程序中打开文件依赖于特定文件类型（如PNG或JPG）的操作系统与特定应用程序（如Mac Preview或Adobe Photoshop）的关联。

一些文件类型支持将链接的资源放入二进制文件中。 当使用桌面应用程序打开此类二进制文件时，如果AEM存储库中存在该资产，则应用程序将预下载链接的资产。 当前支持的文件类型有：

* Adobe inDesign文件（INDD格式）
* Adobe Illustrator文件（AI格式）
* Adobe Photoshop文件（PS格式）

上述应用程序的Adobe Creative Cloud 2018和Creative Cloud 2019版支持此功能。 应用程序使用启发式、最佳匹配方法将链接资产的本地桌面路径映射到AEM服务器上的URL。 它依赖于一些假设：

* 到本机应用程序中置入文件的路径使用全局桌面路径（从本地网络共享中放置，显示“显示”选项）
* 路径由本机应用程序存储在文件的XMP记录中
* AEM已提取XMP记录，其中包含资产元数据记录的路径
* 路径可以与AEM中的资产匹配（这意味着，置入的文件也位于AEM中的匹配路径下）

## 新增功能和增强功能 {#whats-new-added}

要了解详细信息，请 [参阅应用程序中的新增功能](introduction.md#whats-new-v2)。

## 安装说明 {#installation-instructions-v2}

要了解如何安装和配置应用程序，请参阅安 [装AEM桌面应用程序](install-upgrade.md)。

如果您是从以前的AEM桌面应用程序升级，则必须遵循在从先前版本升级时列出的过渡 [的这些最佳实践](install-upgrade.md#upgrade-from-previous-version)。

## 有关应用程序工作方式的重要说明 {#how-app-works}

了解以下有关应用程序及其工作方式的信息非常重要。

* 该应用程序对需要从AEM到AEM（打开、编辑、上传更改和上传资产）的资产二进制文件完全传输的操作提供完全控制。
   * 如果要在桌面上使用资产，您需要显式地打开、编辑或下载到桌面，无论是单独打开、在文件夹中，还是通过多选方式。
   * 如果要获取对上传到AEM的资产的本地更改，您需要单独选择， [!UICONTROL Upload Changes]或通过多选进行选择。
   * 应用程序不是跨桌面和AEM同步资产的“同步客户端”。
   * 应用程序不提供将AEM存储库映射为虚拟文件夹结构的网络共享。
* 应用程序显示的资产列表基于AEM资产存储库的状态。 应用程序不显示或管理本地下载并在本地文件或缓存文件夹中重命名的任何文件。
* 如果应用程序不显示预期结果，请单击顶栏中的刷新图标。
* 使用操作时显示的本地网络共 [!UICONTROL Reveal File] 享仅显示本地可用的文件（和文件夹）。 [!UICONTROL Reveal File] 预下 [!UICONTROL Reveal Folder] 载资源，帮助在本地网络共享中显示正确的资源。
* 当Adobe Creative cloud应用程序读取链接／置入Creative cloud应用程序的本机文件中的资源文件时，将使用SMB(Mac)/WebDAV(Win)本地网络共享。

下图说明了资产和文件从云到本地文件系统的流程，反之亦然，这是由用户操作启动的。

![通过桌面应用程序将资产从AEM服务器流向本机桌面应用程序](assets/da20_flow_diagram.png)

## Known issues {#known-issues-v2}

**用户界面问题：**
* 有时，桌面应用程序的界面可能为空。 右键单击并单 [!UICONTROL Refresh] 击以再次加载应用程序。 这样的刷新会重置应用程序的状态，并且您从DAM存储库根目录的欢迎屏幕开始。 <!-- CQ-4270267 -->
* 在没有触控板或鼠标滚轮的情况下，很难导航文件夹／搜索结果。 没有鼠标滚轮，滚动条可能不随鼠标设备一起显示。 <!-- CQ-4269947 -->
* 上传资产发生更改时，进度栏不会正确显示。
* 在应用和删除过滤器以查找所有本地编辑的资产后，应用程序不会将用户带到用户开始使用的搜索结果或文件夹视图。 应用程序显示DAM存储库的根文件夹。
* 有时，当您连接到未运行AEM服务器的URL时，连接屏幕会变得无响应。 退出应用程序，然后再次启动它。

**CRUD（创建、读取、更新和删除）问题：**
* 应用程序尝试上传文件，即使字符无效，也可能导致服务器端上传失败。 <!-- CQ-4273652 -->
* 在将更改上传到包含注释的资产时，这些注释会与资产一起存储在AEM中，但不会显示为版本控制注释（在AEM 6.4.5、6.5.1中解决）。 <!-- CQ-4268990 -->
* 用户无法取消资产转让。 如果触发了意外的大传输，请退出应用程序并重新启动它。 <!-- CQ-4278940 -->

**平台问题：**
* 有时，在Windows上，资产的状态可能会在打开后立即更改为， [!UICONTROL Edited Locally] 即使您可能尚未编辑该资产。 单击 [!UICONTROL Refresh] 以更新。

>[!MORELIKETHIS]
>
>* [AEM 6.5 文档](https://helpx.adobe.com/support/experience-manager/6-5.html)
>* [AEM Assets 6.5文档](https://docs.adobe.com/content/help/en/experience-manager-64/assets/home.html)
>* [使用AEM桌面应用程序](using.md)
>* [安装和升级桌面应用程序](install-upgrade.md)
>* [最佳实践和疑难解答提示](troubleshoot.md)

