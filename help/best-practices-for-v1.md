---
title: AEM桌面应用程序版本1.x最佳实践
description: Adobe Experience Manager桌面应用程序版本1.x的主要功能和建议使用。
uuid: ba8fbc74-e1ad-4085-a031-ffd317628ba6
contentOwner: AG
products: SG_EXPERIENCEMANAGER/6.3/ASSETS
discoiquuid: 57d5cd78-abce-4ede-a50e-7c161ddb43ae
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: b92e47456f9e16c24eac43d1c5fef9a582f143b5

---


# AEM桌面应用程序v1.x最佳做法 {#aem-desktop-app-best-practices}

## 概述 {#overview}

Adobe Experience Manager(AEM)桌面应用程序将您的数字资产管理(DAM)解决方案与您的桌面相链接，这样您就可以直接在桌面上打开AEM Web UI中提供的文件。 如果从桌面保存资产，则资产会上传到AEM的相应位置。

AEM桌面应用程序使您不必在AEM中更新错误的本地副本或更新错误资产。 桌面应用程序的简单易用的工作流程是使用桌面操作系统提供的网络共享技术实现的。

桌面应用程序将AEM资产存储库作为网络共享装载到桌面上。 因此，文件夹和文件看起来就像是本地的。 但是，不建议在Finder或资源管理器中从桌面直接执行数字资产管理操作。 相反，Adobe建议您使用AEM Assets Web UI执行操作，如复制或移动大量资产。

>[!NOTE]
>
>在阅读本文档之前，您可以查看整体 [AEM和Creative Cloud集成最佳实践](https://docs.adobe.com/content/help/en/experience-manager-64/assets/administer/aem-cc-integration-best-practices.html) ，以获得主题的更高级别概述。

## AEM desktop app architecture {#aem-desktop-app-architecture}

AEM桌面应用程序使用WebDAV(Windows)或SMB(Mac)网络共享来装载网络共享。 安装的网络共享仅是本地共享。 AEM桌面应用程序会截取调用（打开、读取、写入）并提供其他本地缓存。 它将远程调用转换到AEM Assets服务器以优化AEM HTTP请求。 下图描述了AEM桌面应用程序架构。

![AEM桌面应用程序架构](assets/chlimage_1.png)

保存文件时的写入时附加缓存会导致文件首先保存在本地（这样用户就不会等待网络传输）。 然后，在预定义的延迟（30秒）后，文件将在后台上传到AEM，然后资产将上传到AEM。 AEM桌面应用程序提供了用于监视后台文件上传状态的UI。

## 建议使用AEM桌面应用程序 {#recommended-use-of-aem-desktop-app}

AEM桌面应用程序的主要功能包括：

* 从桌面上的AEM Assets Web UI打开文件：在Web UI中，您可以在桌面上显示资产（在Finder、资源管理器中），或使用桌面应用程序打开资产。
* 结帐和结帐：资产可以签出进行编辑，在AEM资产中，这些资产被标记为用户已锁定。 编辑后，可以签入资产以将其解锁。
* 保存对文件所做的更改：您保存到网络共享中文件的任何更改都会自动上传到AEM，并且会创建新版本。
* 将链接的资产放在其他文档中：在Creative Cloud（PS、ID、AI等）等应用程序中，可以将外部文件作为链接放置(例如，可以将图像放入InDesign文档中)。 在这种情况下，网络共享装载允许您从AEM中浏览和选择资产以放置。 放置链接的文件在某些非Adobe应用程序（如MS Office）中也有效。
* AEM中的参考分辨率：如果已放置的文件和具有链接的主文件都存储在AEM中，它可以自动提供有关资产引用的服务器端信息。
* 从桌面访问资产：在挂载的网络共享中，上下文菜单提供“更多信息”对话框(较大的预览、关键元数据)，以及在AEM UI中打开资产的功能。
* 批量上传大型分层文件夹：如果您在AEM UI中使用“创建”>“文件夹上传”选项来上传资产，则AEM桌面应用程序会在后台将选定的文件夹层次结构上传到AEM。 上传进度可在桌面应用程序中使用专用UI进行监视。

## AEM桌面应用程序的使用不当 {#inappropriate-use-of-aem-desktop-app}

* 请勿使用AEM桌面应用程序从桌面管理资产。 AEM桌面应用程序未构建为网络驱动器的替换。 请改用以下功能：
   * 用于数字资产管理（查找／共享资产、元数据、复制／移动等）的AEM Assets Web UI
   * AEM桌面应用程序文件夹上传以上传大型、分层的文件夹

* 请勿将AEM桌面应用程序视为AEM资产的“桌面同步”客户端。 此处AEM桌面应用程序的主要优点是它提供对整个存储库的“虚拟”访问，并且桌面同步应用程序通常仅同步属于一个用户的资产。 AEM桌面应用程序提供一定级别的缓存和后台上传；但是，它的工作方式与典型的“同步”应用程序（如Adobe Creative Cloud桌面应用程序或Microsoft OneDrive）截然不同。
* 请勿频繁使用AEM桌面应用程序网络驱动器保存资产。 所有保存操作都会传输到AEM资产。 因此，直接在已装载的AEM资产存储库中执行密集编辑操作是不现实的。 直接在已装载的存储库中编辑资产会使用不相关的版本创建资产的时间线，并在服务器上施加额外的间接费用。
* 请勿使用AEM桌面应用程序将大量数据从一个AEM实例迁移到另一个AEM实例。 请参阅迁移 [指南](https://docs.adobe.com/content/help/en/experience-manager-65/assets/administer/assets-migration-guide.html) ，以规划和执行资产迁移。 相反，桌面应用程 [序支持在](use-app-v1.md#bulkupload) AEM中首次批量上传大量资产。

## 针对选定用例的建议 {#recommendations-for-selected-use-cases}

### 对创意用户的资源的访问权限 {#access-to-assets-for-creative-users}

AEM桌面应用程序提供对整个DAM存储库的虚拟访问，而桌面上的创意用户在桌面上查找和访问正确的资源可能会很复杂。 使用这些最佳实践为他们简化操作。

* 使用AEM Assets Web UI中的协作功能，为创意用户提供对正确资产的更直接的访问。 其中包括共享文件夹或收藏集、提供智能收藏集（保存的搜索）或发送通知以及指向正确资产的指针。 创意用户随后可以在Web UI中使用桌面操作来快速访问其桌面上的这些资产。
* 考虑资产(访问控制)的适当权限，以简化创意用户在DAM存储库中的视图，基本上限制他们仅访问他们需要／感兴趣的资产：

   * 某些与创意用户无关的区域可能会被拒绝加入其用户组，以从其视图中删除，同时也会在桌面上删除
   * DAM中的大多数资源都是最终的，不是用于更改的——这些资源对于创意用户应为只读
   * 只有需要更改／润饰的资源才应为创意用户启用写入功能。 某些组织使用AEM Projects及其创建的文件夹来托管仍受更改影响的资产。

### 搜索资产 {#searching-assets}

要搜索要在桌面上打开的文件，请执行以下操作：

* 使用AEM Assets Web UI查找资产。 不仅AEM资产中的搜索功能强大（搜索彩块化、保存的搜索），它还提供了查找正确资产的其他功能。 这些过滤器包括其他任务，如根据状态（批准、到期）、收藏集、、通知以及与其他用户／组共享文件夹／收藏集的功能。
* 在您找到资产后，请在AEM UI中使用桌面操作以访问桌面上的资产。

### 更新使用AEM桌面应用程序打开的资产 {#updating-assets-opened-using-aem-desktop-app}

如果您直接在从AEM资产映射到本地网络共享的位置编辑资产，则每次在桌面上保存资产时，该资产都会上传到AEM。 此外，AEM还会创建版本并生成再现。

如果存储在AEM中的资产需要更新：

* 对于 **次要更新**，如批准流程中的次要润饰请求：

   * 取出文件并在桌面上打开它
   * 更新文件
   * 保存更新的版本。 此时会更新资产，并且时间轴会显示要进行比较的原始版本

* 对于 **主要更新**，如需要较小创意WIP周期的更改请求：

   * 使用“显示”选项在桌面上打开相应的文件夹
   * 将文件复制到映射的AEM资产共享之外的WIP文件夹（例如，将文件复制到与Adobe Creative Cloud桌面应用程序同步的文件夹中）
   * 处理文件并间歇性地保存它。 更改不会保存到AEM资产
   * 完成编辑后，移动、复制或保存从AEM映射的文件，以将其上传为新版本

## 网络性能 {#network-performance}

对于使用AEM桌面应用程序的用户来说，良好的体验很大程度上取决于其桌面与AEM服务器之间良好、稳定的网络连接，以及为获得良好性能而调整的服务器，尤其是在上传和更新资产方面。 这些建议针对组织中的网络/IT团队。

### 网络注意事项 {#network-considerations}

要了解有关AEM Assets网络配置的最佳实践，请参阅 [AEM Assets网络注意事项文档](https://docs.adobe.com/content/help/en/experience-manager-64/assets/administer/assets-migration-guide.html) 。 帮助为用户优化AEM桌面应用程序体验的一些重要方面包括：

* **使用正确配置的Dispatcher:** 使用AEM Dispatcher实现更多安全性，并确保已将其配置为 [AEM桌面应用程序连接到调度程序后面的AEM](using.md)

* **节省带宽：** 在Mac上的Finder中，当使用Finder浏览已装载的存储库时，请考虑关闭图标预览。 Finder请求每个文件生成一个预览，并使桌面应用程序在本地下载和缓存资产。 请注意，在节省带宽的同时，它也会降低桌面用户的用户体验，因此在使用具有大资产和／或有限带宽的存储库时应该这样做。

>[!NOTE]
>
>要关闭图标预览，请在Finder中转至视图，选择视图选项，然后取消选中“显示图标预览”选项。 这仅适用于当前文件夹——要使其成为默认文件夹，请在同一窗口中单击“用作默认文件夹”按钮。

### 优化服务器性能 {#optimizing-server-performance}

要了解如何优化AEM Assets服务器以获得性能，请参阅《 [AEM Assets性能调整指南》](https://docs.adobe.com/content/help/en/experience-manager-65/assets/administer/performance-tuning-guidelines.html)。 AEM桌面应用程序服务器性能的一些重要方面围绕优化工作流配置，以便它在资产上传方面表现良好：

* **更高性能的资产上传：** 将 [AEM资产更新工作流模型配置为临时](https://docs.adobe.com/content/help/en/experience-manager-65/assets/administer/performance-tuning-guidelines.html#Workflows)。

* **限制上传的服务器CPU:** 确保正确设置最大的并行工作流作业参数，这样上传不会耗尽所有CPU。
