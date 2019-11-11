---
title: AEM桌面应用程序简介
seo-title: Adobe Experience manager桌面应用程序技术文档和自助
description: 技术文档和自助，了解AEM桌面应用程序如何在直接从其桌面使用企业资产时优化创意用户的工作流程。
seo-description: 了解AEM桌面应用程序在直接从其桌面使用企业资产时如何优化创意用户的工作流程。
contentOwner: asgupa
products: SG_EXPERIENCEMANAGER/6.3/ASSETS
discoiquuid: 39d7bcad-d7b0-4978-a790-4cb68b8a7d6a
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: b74a3ff5c9a25ee1433dd661a1bce677271a5ebe

---


# AEM桌面应用程序概述 {#overview-v2}

Adobe在其解决方案中提供互联的工作流程，为业务线用户和创意专业人士提供更高的工作效率。 Adobe Experience manager桌面应用程序连接存储库和桌面应用程序（包括Adobe和第三方应用程序），以便更快地访问资源并简化工作流程。 这种省时省力的方式提高了用户的效率，这些用户在桌面工作流程中使用Adobe Experience manager的资产。

使用该应用程序，AEM资产中的资产可在本地桌面上轻松访问，并可用于任何桌面应用程序。 您可以在您选择的桌面应用程序中打开和编辑资产。 仅当您选择上传更改时，本地编辑才会在AEM中作为资产的新版本可用，这允许您在桌面上以有效方式处理资产的进行中编辑。 该应用程序支持将资产和嵌套文件夹上传到AEM，从而简化了向存储库添加新内容的过程。

这种集成允许组织中的各种角色在AEM资产中集中管理资产。 营销人员和商业用户可以确保符合各种标准，包括品牌和许可。 创意用户还拥有专用的 [Adobe Asset Link](https://www.adobe.com/marketing/experience-manager-assets/adobe-asset-link.html) （Adobe Photoshop、Illustrator和InDesign中的资源）工具，可以通过Creative cloud和其他本机应用程序访问桌面上的资源。

>[!NOTE]
>
>Adobe Experience manager桌面应用程序在AEM 6.1版本中引入，之前称为AEM Assets Companion应用程序。 有关应用程序版本1.x的帮助，请参阅左侧提要栏中的目录。 Adobe建议升级到最新版本2。

桌面应用程序文档包含以下角色和用例的信息。

| 所需信息 | 帮助内容 |
|-------------------------------------------------------------------------------------------------------|------------------------------------------------------------|
| 想快速了解最新版本中的新增功能和增强功能吗？ | [应用程序中的新增功能](#whats-new-v2) |
| 想了解入门项目和技术规范吗？ 想要下载链接？ | [发行说明](release-notes.md) |
| 不是桌面应用程序的新增功能？ 升级并希望顺利过渡？ | [从先前版本升级](install-upgrade.md#upgrade-from-previous-version) |
| 快起来。 是否要调整默认首选项？ | [安装和配置应用程序](install-upgrade.md) |
| 了解如何使用浏览、发现、编辑、上传、解决冲突、执行批量操作等。 | [使用AEM桌面应用程序](using.md) |
| 遇到问题了？ 是否需要帮助进行疑难解答？ | [AEM桌面应用程序疑难解答](troubleshoot.md) |

## 应用程序中的新增功能 {#whats-new-v2}

该应用程序的版本2.0是从头开始创建的，与先前版本相比，它提供了许多改进。 新应用程序更为用户友好，并提供专用的桌面体验和新的应用程序UI。 用户可以通过搜索或浏览、打开、编辑和上传更改来发现资产，以及上传新资产——无需用户使用AEM界面。 此版本还支持从AEM界面打开文件。

新应用程序为用户体验带来了重大改进，同时满足了与以前相同的使用案例。 以下是顶级改进。

* 用户通过在内置浏览器中浏览和搜索应用程序内的资源来发现资源，而不是依赖Mac finder或Windows资源管理器来显示虚拟网络共享。
* 明确指导用户可执行的操作。
* 通过减少带宽使用来改进性能。 仅在必要时才下载原始二进制文件。 对于浏览和搜索资产，只传输小缩略图。
* 针对批量操作（如批量上传）进行了优化。

新应用程序的主要使用案例和增强功能与客户旅程进行了映射，如下图所示。

![AEM桌面应用程序的新增功能](assets/do-not-localize/whats-new-desktop-app-v2.png)

桌面应用程序允许用户直接从应用程序内完成上述所有用例。 如有必要，您还可以选择在Web界面中执行资产搜索，然后将控件传递给应用程序以打开和编辑资产。
