---
title: '[!DNL Adobe Experience Manager] 桌面应用程序发行说明'
description: ' [!DNL Adobe Experience Manager] 桌面应用程序的发行详细信息、增强功能、新增功能、兼容性和下载链接。'
mini-toc-levels: 1
feature: 桌面应用程序，发行信息
exl-id: e058e7a2-fcc8-4ad1-899e-20695db6bc72
source-git-commit: 96be3f61388b7ec83bdb87d3d13a109d8cce0a1c
workflow-type: tm+mt
source-wordcount: '1687'
ht-degree: 22%

---

# [!DNL Adobe Experience Manager] 桌面应用程序发行说明 {#release-notes-v2}

以下是最新桌面应用程序版本2.1(2.1.3.3)的发行信息。 发行日期为2021年7月29日。

支持的&#x200B;**[!DNL Experience Manager]版本**&#x200B;包括：

* [!DNL Experience Manager] as a [!DNL Cloud Service]. 请参阅[发行说明](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/home.html?lang=zh-Hans)。
* [!DNL Experience Manager] 6.5.0或更高版本(在Adobe Managed Services(AMS)或内部部署中)。请参阅[Service Pack发行说明](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/service-pack/sp-release-notes.html?lang=zh-Hans)。
* [!DNL Experience Manager] 6.4.4或更高版本(在Adobe Managed Services(AMS)或内部部署中)。请参阅[Service Pack发行说明](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/sp-release-notes.html?lang=zh-Hans)。
* [!DNL Experience Manager] 6.4.0 - 6.4.3(安装了兼 [容](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/featurepack/adobe-asset-link-support) 包)，位于Adobe Managed Services(AMS)或内部部署上。
* [!DNL Experience Manager] 6.3（带有兼容包）
* [!DNL Experience Manager] 安装兼容包的6.3.3.1或更高 [版](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/featurepack/adobe-asset-link-support) 本。[!DNL Experience Manager] 6.3.3.0或更早版本不支持桌面应用程序。

[!DNL Adobe Experience Manager] 桌面应用程序适用于以下 **操作系统**:

* macOS X 10.14或更高版本，以及最新的错误修复。 [尚不支持使用](https://support.apple.com/en-us/HT211814) Apple Silion的Mac计算机。
* 带有最新Service Pack和错误修复的Windows 10。

受支持操作系统的&#x200B;**下载URL**&#x200B;包括：

| 操作系统 | [!DNL Experience Manager] as a [!DNL Cloud Service] | [!DNL Experience Manager] 6.x |
|---|---|---|
| macOS(v2.1.3.3) | [下载链接](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-desktop-app/aem-desktop-osx-2.1.3.3.dmg) | [下载链接](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/adobe/aem-desktop-app/aem-desktop-osx-2.1.3.3.dmg) |
| Windows 64位(v2.1.3.3) | [下载链接](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-desktop-app/aem-desktop-win64-2.1.3.3.exe) | [下载链接](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/adobe/aem-desktop-app/aem-desktop-win64-2.1.3.3.exe) |
| Windows 32位(v2.1.3.1) | [下载链接](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-desktop-app/aem-desktop-win32-2.1.3.1.exe) | [下载链接](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/adobe/aem-desktop-app/aem-desktop-win32-2.1.3.1.exe) |

>[!NOTE]
>
>不再支持Windows 7。 请参阅[有关Windows 7的EOL的文章](https://support.microsoft.com/en-us/help/4057281/windows-7-support-ended-on-january-14-2020)。

<!-- The version of the app you plan to install on your local machine requires a specific [!DNL Adobe Experience Manager] server version/additional server-side components (service packs, hot fixes, or feature packs). Contact your [!DNL Experience Manager] administrator for help.
-->

## 支持不同的资产和文件类型 {#support-for-file-types}

应用程序支持存储在[!DNL Experience Manager]中的资产，这些资产表示用于其基本操作的二进制文件。 在本机桌面应用程序中打开文件，取决于特定文件类型（如 PNG 或 JPG）与特定应用程序（如 Mac Preview 或 Adobe Photoshop）的操作系统关联。

一些文件类型支持将链接的资产放入二进制文件中。当使用桌面应用程序打开此类二进制文件时，如果资产存在于[!DNL Experience Manager]存储库中，则应用程序会预下载链接的资产。 当前支持的文件类型有：

* [!DNL Adobe InDesign] 文件（INDD格式）
* [!DNL Adobe Illustrator] 文件（AI格式）
* [!DNL Adobe Photoshop] 文件（PS格式）

上述应用程序的[!DNL Adobe Creative Cloud] 2018和[!DNL Adobe Creative Cloud] 2019版本支持该功能。 该应用程序使用启发式的最佳匹配方法将链接资产的本地桌面路径映射到[!DNL Experience Manager]服务器上的URL。 这是基于以下假设：

* 在本机应用程序中放置文件的路径使用全局桌面路径（从带有[!UICONTROL Reveal]选项的本地网络共享中放置）。

* 路径由本机应用程序存储在文件的 XMP 记录中.

* [!DNL Experience Manager] 已提取 XMP 记录，其中包含资产元数据记录的路径.

* 路径可以匹配到[!DNL Experience Manager]中的资产，即放置的文件也位于[!DNL Experience Manager]中的匹配路径下。

## 新增功能、增强功能和错误修复 {#what-is-new}

要了解详细信息，请参阅[v2.0](introduction.md#whats-new-v2)的新增功能。

**应用程序v2.1.3.3中的更新**

新版应用程序修复了错误。

**应用程序v2.1.3.2中的更新**

此版本的应用程序修复了错误。

**应用程序v2.1.3.1中的更新**

此版本中修复的错误是：

* 资产上传和下载速度已得到提高，即使对于大型资产也是如此。 此版本修复了在上传超大文件时，使用[!DNL desktop app]上传资产有时失败的问题。

**应用程序v2.1.2.0中的更新**

* [!UICONTROL Clear Cookies]的新选项将添加到应用程序的主菜单中。 它有助于解决潜在的登录问题，例如在将连接从服务器更改为其他服务器时。 请参阅[在连接](/help/troubleshoot.md#cannot-login-cookies-issue)之前清除Cookie。

* 添加了一个选项，该选项（如果选中）允许应用程序上传文件夹和文件，以便在[!DNL Adobe Experience Manager]中创建的节点名称与本地文件和文件夹名称相同。

   此行为与桌面应用程序版本1中的默认行为类似。 而在当前版本中，如果未启用选项，则文件夹名称中的空格和字符`% ; # , + ? ^ { } "`将在文件夹路径中替换为短划线。 此外，文件夹路径中的大写字符将转换为小写字符。 但是，在文件名中，字符`# % { } ? &`被用短划线替换；但白空和大小写仍保留。 有关更多信息，请参阅[应用程序首选项](/help/install-upgrade.md#set-preferences)和[上传和添加新资产](/help/using.md#upload-and-add-new-assets-to-aem)。

**应用程序v2.1.1.0中的更新**

* 高级设置允许应用程序在上传文件夹时模拟v1.10应用程序的行为。 在v1.10中，在存储库中创建的节点名称遵循用户提供的文件夹名称的空格和大小写。 v2.1的默认行为仍然相同，即，将文件夹名称中的多个空格替换为存储库节点名称中的连字符，然后转换为小写节点名称。 请参阅[应用程序首选项](/help/install-upgrade.md#set-preferences)。

**应用程序v2.1.0.0中的更新**

* 要上传资产，用户现在可以直接从Windows资源管理器或Mac查找器中，将文件或文件夹拖动到应用程序界面上。 除了应用程序中提供的上传选项之外，这项功能还可用。 请参阅[上传资产](/help/using.md#upload-and-add-new-assets-to-aem) <!-- CQ-4309527 -->

**应用程序v2.0.3中的更新**

此版本中修复的错误是：

* 修复了Windows上尝试访问[!DNL Adobe Experience Manager] 6.5.5.0上DAM存储库的应用程序用户的登录问题。

**应用程序v2.0.2中的更新**

错误修复和更新包括：

* 上传加速设置现已可用于提高上传性能。 打开此设置后，应用程序会使用更多本地CPU线程来更快地上传，并且会占用更多资源。

* 固定包含某些GB18030字符的文件名或路径时的资产上传。<!-- CQ-4283494 -->

* 在搜索结果中切换到其他排序类型后，可使用按相关性排序选项。<!-- CQ-4286874 -->

* 桌面应用程序现在可以列出子文件夹，而无需显式刷新。<!-- CQ-4285711 -->

* (Windows)修复了某些Windows计算机上不可用的应用程序界面的罕见问题。 用户无法单击应用程序界面，因为界面元素的点击区域会侧移，从而使其显示扭曲。<!-- CQ-4280785 -->

**应用程序v2.0.1中的更新**

错误修复和更新包括：

* 允许选项配置`%Temp%`目录以匹配`%APPDATA%`路径。<!-- CQ-4282665 -->

* 允许用户通过Okta SAML身份验证登录[!DNL Experience Manager]创作。<!-- CQ-4278134 -->

## 安装说明 {#installation-instructions-v2}

要了解如何安装和配置应用程序，请参阅[Install [!DNL Experience Manager] 桌面应用程序](install-upgrade.md)。

如果您是从以前的[!DNL Experience Manager]桌面应用程序升级，则必须按照[从以前的版本](install-upgrade.md#upgrade-from-previous-version)升级中列出的用于实现过渡的最佳实践来操作。

## 关于应用程序工作方式的重要说明 {#how-app-works}

请务必了解关于应用程序及其工作方式的以下信息。

* 该应用程序对需要与[!DNL Experience Manager]之间的资产二进制文件进行完全传输（打开、编辑、上传更改和上传资产）的操作提供完全控制。

   * 如果要在桌面上处理资产，必须明确地在文件夹中逐个或通过多选方式打开、编辑资产或将资产下载到桌面。

   * 如果要将对资产所做的本地更改上传到[!DNL Experience Manager]，您需要逐个或通过多选方式选择[!UICONTROL Upload Changes]。

   * 应用程序不是在桌面和[!DNL Experience Manager]之间同步资产的“同步客户端”。

   * 应用程序不提供将[!DNL Experience Manager]存储库映射为虚拟文件夹结构的网络共享。

* 该应用程序显示的资产列表基于 Assets 存储库的状态。对于任何下载到本地后在本地文件或缓存文件夹中重命名的文件，该应用程序不会显示或管理这些文件。

* 如果该应用程序不显示预期结果，请单击顶栏中的刷新图标。

* 使用 [!UICONTROL Reveal File] 操作时显示的本地网络共享，仅显示本地可用的文件（和文件夹）。[!UICONTROL Reveal File] 和 [!UICONTROL Reveal Folder] 会预下载资产，以帮助在本地网络共享中显示正确的资产。

* 当 Adobe Creative Cloud 应用程序读取链接/放置在 Creative Cloud 应用程序本机文件中的资产文件时，会使用 SMB (Mac)/WebDAV (Win) 本地网络共享。

下图说明了资产和文件从云到本地文件系统的流程，以及由用户操作启动的相反方式。

![[!DNL Experience Manager]资产通过桌面应用程序从 服务器流向本机桌面应用程序](assets/da20_flow_diagram.png)

## 已知问题 {#known-issues-v2}

**用户界面问题：**

* 有时，桌面应用程序的界面可能会变为空白。 右键单击并单击[!UICONTROL Refresh]以重新加载应用程序。 刷新后，您将从DAM存储库的根开始。 资产的更新或状态将会保留。<!-- CQ-4270267 -->

* 在没有跟踪板或鼠标指针的情况下，很难导航文件夹/搜索结果。 使用没有鼠标滚轮的鼠标设备时，可能不会显示滚动条。<!-- CQ-4269947 -->

* 在少数情况下，上传资产更改时，无法正确显示进度栏。

* 在应用筛选器以查找所有本地编辑的资产和删除筛选器后，应用程序不会为用户呈现搜索结果或者用户开始执行筛选时所在的文件夹视图。应用程序会显示 DAM 存储库的根文件夹。

* 有时，当您连接到未运行[!DNL Experience Manager]服务器的URL时，连接屏幕会变得无响应。 可退出应用程序后重新启动。

**CRUD（创建、读取、更新和删除）问题：**

* 在上传包含注释的资产更改时，这些注释会与资产一起存储在[!DNL Experience Manager]中，但不会显示为版本控制注释。 此问题在[!DNL Experience Manager] 6.4.5和[!DNL Experience Manager] 6.5.1中已解决。Adobe建议安装最新的Service Pack。<!-- CQ-4268990 -->

* 用户无法取消资产传输。如果意外触发了大量传输，请退出应用程序后重新启动。<!-- CQ-4278940 -->

**平台问题：**

* 有时，在 Windows 上，打开资产后其状态可能会立即变为 [!UICONTROL Edited Locally]，即使您可能没有进行任何编辑也是如此。可单击 [!UICONTROL Refresh] 进行更新。

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] as a [!DNL Cloud Service] 文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/landing/home.html)
>* [[!DNL Experience Manager] as a [!DNL Cloud Service] [!DNL Assets] 文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/home.html)
>* [如何使用 [!DNL Experience Manager] 桌面应用程序](using.md)
* [安装和升级桌面应用程序](install-upgrade.md)
* [最佳实践和故障诊断提示](troubleshoot.md)

