---
title: AEM桌面应用程序版本1.x最佳实践
description: Adobe Experience Manager桌面应用程序1.x版的主要功能和推荐使用。
uuid: ba8fbc74-e1ad-4085-a031-ffd317628ba6
contentOwner: AG
products: SG_EXPERIENCEMANAGER/6.5/ASSETS, SG_EXPERIENCEMANAGER/6.4/ASSETS, SG_EXPERIENCEMANAGER/6.3/ASSETS
discoiquuid: 57d5cd78-abce-4ede-a50e-7c161ddb43ae
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: e6e184d36cb7d78177384d919c74d048e46a1c95
workflow-type: tm+mt
source-wordcount: '1705'
ht-degree: 0%

---


# AEM桌面应用程序v1.x最佳实践 {#aem-desktop-app-best-practices}

## 概述 {#overview}

Adobe Experience Manager(AEM)桌面应用程序将您的数字资产管理(DAM)解决方案与桌面链接，这样您就可以直接在桌面上打开AEM web UI中提供的文件。 如果您从桌面保存资产，则资产会上传到AEM的适当位置。

AEM桌面应用程序消除了您在AEM中更新错误的本地副本或更新错误资产的可能性。 桌面应用程序易于使用的工作流通过桌面操作系统提供的网络共享技术实现。

桌面应用程序将AEM Assets存储库作为网络共享装载到桌面上。 因此，文件夹和文件看起来就像是本地文件。 但是，不建议在Finder或资源管理器中从安装的网络共享中直接从桌面执行数字资产管理操作。 相反，Adobe建议您使用AEM AssetsWeb UI执行操作，如复制或移动大量资源。

>[!NOTE]
>
>在阅读此文档之前，您可以查阅AEM和 [Creative Cloud集成的整体最佳实践](https://docs.adobe.com/content/help/en/experience-manager-64/assets/administer/aem-cc-integration-best-practices.html) ，以获得主题的更高级别概述。

## AEM desktop app architecture {#aem-desktop-app-architecture}

AEM桌面应用程序使用WebDAV(Windows)或SMB(Mac)网络共享来装载网络共享。 挂载的网络共享仅是本地共享。 AEM桌面应用程序会拦截调用（打开、读取、写入）并提供额外的本地缓存。 它将远程调用转换到AEM Assets服务器，以优化AEM HTTP请求。 下图描述了AEM桌面应用程序架构。

![AEM桌面应用程序架构](assets/arch_v1.png)

*图：桌面应用程序架构*

保存文件时的额外写缓存会导致文件首先保存在本地（这样用户就不会等待网络传输）。 然后，在预定义的延迟（30秒）后，文件在后台上传到AEM，然后资产上传到AEM。 AEM桌面应用程序提供用于监视后台文件上传状态的UI。

## 建议使用AEM桌面应用程序 {#recommended-use-of-aem-desktop-app}

AEM桌面应用程序的主要功能包括：

* **在桌面上从AEM AssetsWeb UI打开文件**。 在Web UI中，您可以在桌面上显示资产（在Finder、资源管理器中），或使用桌面应用程序打开资产。

* **结帐和结帐**。 资源可以签出进行编辑，在AEM Assets被标记为用户已锁定。 编辑后，可以检入资产以将其解锁。

* **保存对文件所做的更改**。 您保存到网络共享中文件的任何更改都会自动上传到AEM，并创建一个新版本。

* **将链接的资源放置到其他文档**。 在Creative Cloud（、和）[!DNL Adobe Photoshop]等应 [!DNL Adobe InDesign]用程 [!DNL Adobe Illustrator]序中，可以将外部文件作为链接放置。 例如，可以将图像放入InDesign文档。 在这种情况下，网络共享装载允许您浏览并选择AEM中的资产以放置。 放置链接的文件在某些非Adobe应用程序（如MS Office）中也有效。

* **AEM中的参考解析**。 如果已放置的文件和具有链接的主文件都存储在AEM中，则它可以自动提供有关资产引用的服务器端信息。

* **从桌面访问资产**。 在挂载的网络共享中，上下文菜单提 [!UICONTROL More Info] 供对话框(较大的预览、关键元数据)以及在AEM UI中打开资产的功能。

* **批量上传大型分层文件夹**。 如果您在AEM UI中使用创建>文件夹上传选项来上传资产，AEM桌面应用程序会将选定的文件夹层次结构上传到后台的AEM。 上传进度可在桌面应用程序中使用专用UI进行监视。

## AEM桌面应用程序的使用不当 {#inappropriate-use-of-aem-desktop-app}

* 请勿使用AEM桌面应用程序从桌面管理资产。 AEM桌面应用程序未构建为网络驱动器的替换。 请改用以下功能：

   * AEM Assets数字资产管理（查找或共享资产、元数据以及复制或移动）的Web UI。

   * AEM桌面应 [!UICONTROL Folder Upload] 用程序上传大型分层文件夹。

* 请勿将AEM桌面应用程序视为AEM Assets的“桌面同步”客户端。 此处AEM桌面应用程序的主要优点是它提供对整个存储库的“虚拟”访问，桌面同步应用程序通常仅同步属于一个用户的资产。 AEM桌面应用程序提供一定级别的缓存和后台上传；但是，它的工作方式与典型的“同步”应用程序(如Adobe Creative Cloud桌面应用程序或Microsoft OneDrive)截然不同。

* 请勿频繁使用AEM桌面应用程序网络驱动器来保存资源。 所有保存操作都传送到AEM Assets。 因此，直接在已装载的AEM Assets存储库中执行密集编辑操作是不现实的。 直接在已装载的存储库中编辑资产会使用不相关的版本来创建资产的时间轴，并在服务器上施加额外的间接费用。

* 请勿使用AEM桌面应用程序将大量数据从一个AEM实例迁移到另一个实例。 请参阅迁 [移指南](https://docs.adobe.com/content/help/en/experience-manager-65/assets/administer/assets-migration-guide.html) ，以规划和执行资产迁移。 相比之下，桌面应 [用程序支持](use-app-v1.md#bulkupload) ，首次批量上传大量资源 [!DNL Adobe Experience Manager]。

## Recommendations公司为特定用例 {#recommendations-for-selected-use-cases}

### 对创意用户的资源的访问权限 {#access-to-assets-for-creative-users}

AEM桌面应用程序提供对整个DAM存储库的虚拟访问——桌面上的创意用户在桌面上查找和访问正确的资源可能非常复杂。 使用这些最佳实践为他们简化这些操作。

* 使用AEM AssetsWeb UI中的协作功能，为创意用户提供更直接的资源访问权限。 其中包括共享文件夹或收藏集、提供智能收藏集（保存的搜索）或发送通知以及将指针指向正确资产等。 创意用户随后可以在Web UI中使用桌面操作快速访问桌面上的这些资产。

* 考虑资产(访问控制)的适当权限，以简化创意用户在DAM存储库中的视图，基本上仅限于他们需要或感兴趣的资产：

   * 某些与创意用户无关的区域可能会被拒绝用于其用户组，以从其视图（也在桌面上）删除它们。

   * DAM中的大多数资产都是最终资产，并非用于更改——创意用户应该只读。

   * 只有需要更改或润饰的资源才应为创意用户启用写入功能。 一些组织使用AEM Projects及其创建的文件夹来托管仍受更改影响的资产。

### 搜索资产 {#searching-assets}

要搜索要在桌面上打开的文件：

* 使用AEM AssetsWeb UI查找资产。 AEM Assets的搜索功能不仅强大（搜索彩块化、保存的搜索），还提供了额外的功能来查找正确的资产。 这些过滤器包括其他任务，如根据状态（批准、到期）、收藏集、、通知以及与其他用户／组共享文件夹／收藏集的功能。

* 找到资产后，在AEM UI中使用桌面操作以访问桌面上的资产。

### 更新使用AEM桌面应用程序打开的资源 {#updating-assets-opened-using-aem-desktop-app}

如果您直接在从AEM Assets映射到本地网络共享的位置编辑资产，则每次在桌面上保存资产时，资产都会上传到AEM。 此外，AEM还创建一个版本并生成再现。

如果存储在AEM中的资产需要更新：

* 对于 **次要更新**，如批准流程中的次要润饰请求：

   * 签出文件并在桌面上将其打开。

   * 更新文件。

   * 保存更新的版本。 资产会更新，时间轴会显示原始版本进行比较。

* 对于 **重要更新**，如需要较小创意WIP周期的更改请求：

   * 使用“显示”选项在桌面上打开相应的文件夹。

   * 将文件复制到映射的AEM Assets共享外的WIP文件夹(例如，将文件复制到与Adobe Creative Cloud桌面应用程序同步的文件夹中)。

   * 处理文件并间歇性地保存它。 更改不会保存到AEM Assets。

   * 编辑完成后，移动、复制或保存从AEM映射的文件，以将其上传为新版本。

## 网络性能 {#network-performance}

对于使用AEM桌面应用程序的用户来说，良好的体验很大程度上取决于其桌面与AEM服务器之间良好、稳定的网络连接，以及为获得良好性能而调整的服务器，特别是在上传和更新资产方面。 这些建议针对组织中的网络/IT团队。

### 网络注意事项 {#network-considerations}

要了解有关AEM Assets网络配置的最佳实践，请参阅AEM Assets [网络考虑事项](https://docs.adobe.com/content/help/en/experience-manager-64/assets/administer/assets-migration-guide.html) 文档。 帮助用户优化AEM桌面应用程序体验的一些重要方面包括：

* **使用正确配置的Dispatcher**。 使用AEM Dispatcher实现更多安全性，并确保将它配置为 [AEM桌面应用程序连接到调度程序后的AEM](install-configure-app-v1.md#connect-to-an-aem-instance-behind-a-dispatcher)

* **节省带宽**。 在使用Finder浏览已装载的存储库时，请考虑在Mac上的Finder中关闭图标预览。 Finder请求每个文件生成预览，并导致桌面应用程序在本地下载和缓存资产。 请注意，在节省带宽的同时，也会降低桌面用户的用户体验，因此在使用具有大资源和／或有限带宽的存储库时应该这样做。

>[!NOTE]
>
>要关闭图标预览，请在Finder中转至视图，选择视图选项，然后取消选中“显示图标预览”选项。 此操作仅适用于当前文件夹——要将其设为默认文件夹，请在同一窗口中单击“用作默认文件夹”按钮。

### 优化服务器性能 {#optimizing-server-performance}

要了解如何优化AEM Assets服务器的性能，请参阅《AEM Assets [性能调整指南》](https://docs.adobe.com/content/help/en/experience-manager-65/assets/administer/performance-tuning-guidelines.html)。 AEM桌面应用程序服务器性能的一些重要方面是围绕优化工作流配置，以便它能够很好地用于资产上传：

* **更高效的资产上传**。 将AEM资产 [更新工作流模型配置为临时模型](https://docs.adobe.com/content/help/en/experience-manager-65/assets/administer/performance-tuning-guidelines.html#Workflows)。

* **限制上载的服务器CPU**。 确保正确设置最大并行工作流作业参数，这样上载不会耗尽所有CPU。
