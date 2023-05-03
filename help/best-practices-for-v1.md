---
title: 桌面应用程序v1.10最佳实践
description: 的主要功能和建议使用 [!DNL Adobe Experience Manager] 桌面应用程序版本1.10。
exl-id: 5de06b33-c05c-47eb-b884-408b6f9afc94
source-git-commit: 7a7236c36f615e97e9d040e6139368a931eb579e
workflow-type: tm+mt
source-wordcount: '1676'
ht-degree: 0%

---

# AEM桌面应用程序v1.10最佳实践 {#aem-desktop-app-best-practices}

## 概述 {#overview}

[!DNL Adobe Experience Manager] 桌面应用程序将您的数字资产管理(DAM)解决方案与桌面链接，以便您能够直接在桌面上打开AEM web UI中可用的文件。 如果您从桌面保存资产，则资产会上传到相应位置的AEM。

AEM桌面应用程序消除了您在AEM中更新错误的本地副本或更新错误资产的可能性。 桌面应用程序的易于使用的工作流程通过使用桌面操作系统提供的网络共享技术来实现。

桌面应用程序将AEM Assets存储库作为网络共享装载到桌面上。 因此，文件夹和文件会像本地文件夹和文件一样显示。 但是，不建议在Finder或Explorer中的已挂载网络共享中直接从桌面执行数字资产管理操作。 相反，Adobe建议您使用AEM Assets Web UI来执行操作，例如复制或移动大量资产。

>[!NOTE]
>
>在阅读本文档之前，您可以查看 [AEM和Creative Cloud集成最佳实践](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/aem-cc-integration-best-practices.html) ，以获取主题的更高级概述。

## AEM桌面应用程序架构 {#aem-desktop-app-architecture}

AEM桌面应用程序使用WebDAV(Windows)或SMB(Mac)网络共享来装载网络共享。 挂载的网络共享仅是本地的。 AEM桌面应用程序会截取调用（打开、读取、写入）并提供其他本地缓存。 它会将远程调用转换到AEM Assets服务器，以优化AEM HTTP请求。 下图描述了AEM桌面应用程序架构。

![AEM桌面应用程序架构](assets/arch_v1.png)

*图：桌面应用程序架构*

保存文件时的写缓存会导致文件首先保存在本地（这样用户就不会等待网络传输）。 然后，在经过预定义的延迟（30秒）后，文件会在后台上传到AEM，然后资产会上传到AEM。 AEM桌面应用程序提供了用于监控后台文件上传状态的UI。

## 建议使用AEM桌面应用程序 {#recommended-use-of-aem-desktop-app}

AEM桌面应用程序的主要功能包括：

* **在桌面上从AEM Assets Web UI打开文件**. 从Web UI中，您可以在桌面上显示资产（在“访达”、“资源管理器”中），或使用桌面应用程序打开资产。

* **签出和签入**. 资产可签出以进行编辑，但在AEM Assets中，这些资产会被标记为用户已锁定。 编辑后，可以签入资产以解锁资产。

* **保存对文件所做的更改**. 您保存到网络共享中文件的任何更改都会自动上传到AEM，并创建一个新版本。

* **将链接的资产放在其他文档中**. 在应用程序中，例如Creative Cloud([!DNL Adobe Photoshop], [!DNL Adobe InDesign]和 [!DNL Adobe Illustrator])，则可以将外部文件作为链接放置。 例如，您可以将图像放入InDesign文档中。 在这种情况下，网络共享装载允许您从AEM中浏览和选择资产以进行放置。 在某些非Adobe应用程序（如MS Office）中，也可以放置链接的文件。

* **AEM中的参考解析**. 如果已放置的文件和具有链接的主文件都存储在AEM中，则它可以自动提供有关资产引用的服务器端信息。

* **从桌面访问资产**. 在挂载的网络共享中，上下文菜单提供 [!UICONTROL More Info] 对话框（更大的预览、关键元数据），以及在AEM UI中打开资产的功能。

* **批量上传大型分层文件夹**. 如果您使用AEM UI中的创建>文件夹上传选项来上传资产，AEM桌面应用程序会将选定的文件夹层次结构上传到后台的AEM。 可以在桌面应用程序中使用专用UI监控上传进度。

## 不当使用AEM桌面应用程序 {#inappropriate-use-of-aem-desktop-app}

* 请勿使用AEM桌面应用程序从桌面管理资产。 AEM桌面应用程序未作为网络驱动器的替代品而构建。 请改用以下功能：

   * AEM Assets Web UI，用于数字资产管理（查找或共享资产、元数据，以及复制或移动）。

   * AEM桌面应用程序 [!UICONTROL Folder Upload] 上传大型分层文件夹。

* 请勿将AEM桌面应用程序视为AEM Assets的“桌面同步”客户端。 此处AEM桌面应用程序的主要优势在于它提供了对整个存储库的“虚拟”访问，而桌面同步应用程序通常只同步属于一个用户的资产。 AEM桌面应用程序提供一定程度的缓存和后台上传；但是，它的工作方式与典型的“同步”应用程序(如Adobe Creative Cloud桌面应用程序或Microsoft OneDrive)非常不同。

* 请勿经常使用AEM桌面应用程序网络驱动器来保存资产。 所有保存操作都会传输到AEM Assets。 因此，直接在已装载的AEM Assets存储库中执行密集的编辑操作是不切实际的。 直接在已装载的存储库中编辑资产会使用不相关的版本创建资产的时间轴，并在服务器上施加额外的开销。

* 请勿使用AEM桌面应用程序将大量数据从一个AEM实例迁移到另一个实例。 请参阅 [迁移指南](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/assets-migration-guide.html) 来规划和执行资产迁移。 相反，桌面应用程序 [支持批量上传](use-app-v1.md#bulkupload) 在 [!DNL Adobe Experience Manager].

## Recommendations（针对选定用例） {#recommendations-for-selected-use-cases}

### 为创意用户访问资产 {#access-to-assets-for-creative-users}

AEM桌面应用程序提供了对整个DAM存储库的虚拟访问权限，而桌面上的创意用户在其桌面上查找和访问正确的资产可能会非常复杂。 使用这些最佳实践为他们简化操作。

* 使用AEM Assets Web UI中的协作功能，为创意用户提供更直接的正确资产访问权限。 其中包括共享文件夹或收藏集、提供智能收藏集（保存的搜索）或发送通知以及向正确资产发送指针。 然后，创意用户可以在Web UI中使用桌面操作，快速访问桌面上的这些资产。

* 考虑资产的正确权限（访问控制），以便为创意用户简化DAM存储库的视图，基本上限制他们仅访问他们需要或感兴趣的资产：

   * 某些与创意用户无关的区域可能会被拒绝用于其用户组，以便从他们的视图中（在桌面上）删除它们。

   * DAM中的大多数资产是最终资产，并且不是为了进行更改，因此这些资产对于创意用户应为只读。

   * 只有需要更改或润饰的资产才应为创意用户启用写入功能。 某些组织使用AEM项目及其创建的文件夹来托管仍受更改影响的资产。

### 搜索资源 {#searching-assets}

要搜索要在桌面上打开的文件，请执行以下操作：

* 使用AEM Assets Web UI找到资产。 AEM Assets中的搜索不仅功能强大（搜索彩块化、保存的搜索），还提供其他功能来查找正确的资产。 这些过滤器包括其他过滤器，例如，根据状态（批准、到期）、收藏集、任务、通知以及与其他用户/组共享文件夹/收藏集的功能搜索资产。

* 找到资产后，在AEM UI中使用桌面操作在桌面上访问资产。

### 更新使用AEM桌面应用程序打开的资产 {#updating-assets-opened-using-aem-desktop-app}

如果您直接在从AEM Assets映射到本地网络共享的位置编辑资产，则每次在桌面上保存资产时，该资产都会上传到AEM。 此外，AEM还会创建一个版本并生成演绎版。

如果存储在AEM中的资产需要更新：

* 对于 **次要更新**，例如批准流程中的次要润饰请求：

   * 签出文件并在桌面上将其打开。

   * 更新文件。

   * 保存更新版本。 资产会更新，时间轴会显示要比较的原始版本。

* 对于 **主要更新**，例如需要较短创意WIP周期的更改请求：

   * 使用显示选项在桌面上打开相应的文件夹。

   * 将文件复制到映射的AEM Assets共享之外的WIP文件夹(例如，将文件复制到与Adobe Creative Cloud桌面应用程序同步的文件夹中)。

   * 处理文件并间歇性地保存它。 更改未保存到AEM Assets。

   * 编辑完成后，移动、复制或保存从AEM映射的文件，以将其上传为新版本。

## 网络性能 {#network-performance}

对于使用AEM桌面应用程序的用户而言，其良好体验很大程度上取决于其台式机与AEM服务器之间良好且稳定的网络连接，以及针对性能而调整的服务器，特别是有关上传和更新资产的连接。 这些建议适用于组织中的网络/IT团队。

### 网络注意事项 {#network-considerations}

要了解有关AEM Assets网络配置的最佳实践，请参阅 [如何批量迁移资产](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/assets-migration-guide.html) 文档。 有助于为用户优化AEM桌面应用程序体验的一些重要方面包括：

* **使用正确配置的Dispatcher**. 使用AEM Dispatcher提高安全性，并确保已为 [AEM桌面应用程序与调度程序后面的AEM的连接](install-configure-app-v1.md#connect-to-an-aem-instance-behind-a-dispatcher)

* **节省带宽**. 在使用Finder浏览已装载的存储库时，请考虑在Mac的Finder中关闭图标预览。 “查找器”请求每个文件生成一个预览，并导致桌面应用程序在本地下载和缓存资产。 请注意，在节省带宽的同时，也会减少桌面用户的用户体验，因此在使用具有大资产和/或有限带宽的存储库时，应该这样做。

>[!NOTE]
>
>要关闭图标预览，请在“查找器”中转到 [!UICONTROL View]，选择 [!UICONTROL View Options]，然后取消选中 [!UICONTROL Show icon preview] 选项。 此操作仅适用于当前文件夹 — 若要使其成为默认文件夹，请单击 [!UICONTROL Use as default] 选项。

### 优化服务器性能 {#optimizing-server-performance}

要了解如何优化AEM Assets服务器的性能，请参阅 [AEM Assets性能调整指南](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/performance-tuning-guidelines.html). AEM桌面应用程序服务器性能的一些重要方面是围绕优化工作流配置，以便其在资产上传方面表现良好：

* **性能更高的资产上传**. 配置 [AEM资产更新工作流模型为临时模型](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/performance-tuning-guidelines.html).

* **限制上载的服务器CPU**. 确保正确设置最大并行工作流作业参数，以便上传不会耗尽所有CPU。
