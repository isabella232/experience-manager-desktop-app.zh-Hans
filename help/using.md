---
title: 使用 [!DNL Experience Manager] 桌面应用程序
description: 直接从Win或Mac桌面使用 [!DNL Adobe Experience Manager] desktop app, to work with [!DNL Adobe Experience Manager] DAM资源，并用于其他应用程序。
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: caf6faf17157a0e9e3bffd40b4bdd0802a71dad7
workflow-type: tm+mt
source-wordcount: '3906'
ht-degree: 0%

---


# 使用[!DNL Adobe Experience Manager]桌面应用程序{#use-aem-desktop-app-v2}

使用[!DNL Adobe Experience Manager]桌面应用程序轻松访问存储在本地桌面上的[!DNL Adobe Experience Manager] DAM存储库中的数字资产，并将这些资产用于任何桌面应用程序。 您可以在桌面应用程序中打开资产并在本地编辑资产 — 使用版本控制将更改上传回[!DNL Experience Manager]，以与其他用户共享更新。 您还可以将新文件和文件夹层次结构上传到[!DNL Experience Manager]，创建文件夹，以及从[!DNL Experience Manager] DAM中删除资产或文件夹。

该集成允许组织中的各种角色在[!DNL Experience Manager Assets]中集中管理资产，并在Windows或Mac OS上的本机应用程序中访问本地桌面上的资产。

在注销后或第一次打开应用程序时，请以`https://[aem-server-url]:[port]/`格式提供[!DNL Experience Manager]服务器的URL。 然后选择[!UICONTROL Connect]选项。 提供凭据以将应用程序与服务器连接。

您使用[!DNL Experience Manager]桌面应用程序执行的关键任务是：

![工作流和任务，您可以使用桌面应用 [!DNL Experience Manager] 程序](assets/aem_desktop_app_usecases_v2.png "完成工作流和任务，您可以使用桌面应用程序 [!DNL Adobe Experience Manager] 完成工作")
流下载 [](assets/aem_desktop_app_usecases_print.pdf) 此可供打印的PDF文件。

## 桌面应用程序的工作方式{#how-app-works2}

在开始使用应用程序之前，请了解[应用程序的工作方式](release-notes.md#how-app-works)。 此外，请熟悉以下条款：

* **[!UICONTROL Desktop Actions]**:从资产Web界面中，您可以从浏览器中浏览资产位置或签出并打开资产，以便在本机桌面应用程序中进行编辑。这些操作可从Web界面使用桌面应用程序功能。 请参阅[如何启用桌面操作](using.md#desktopactions-v2)。

* 文件状态为&#x200B;**[!UICONTROL Cloud Only]**:此类资产不会下载到本地计算机上，并且仅在[!DNL Experience Manager]服务器上可用。

* 文件状态为&#x200B;**[!UICONTROL Available locally]**:资产会按原样下载并在本地计算机上可用。 资产不会更改。

* 文件状态为&#x200B;**[!UICONTROL Edited locally]**:此类资产将在本地修改，并且更改将保留到上传到[!DNL Experience Manager]服务器。 上传后，状态将更改为[!UICONTROL Available locally]。 请参阅[编辑资产](using.md#edit-assets-upload-updated-assets)。

* 文件状态为&#x200B;**[!UICONTROL Editing conflict]**:如果您和其他用户同时修改了资产，应用程序会指示发生了编辑冲突。 应用程序还提供保留或放弃更改的选项。 请参阅[如何避免编辑冲突](using.md#adv-workflow-collaborate-avoid-conflicts)。

* 文件状态为&#x200B;**[!UICONTROL Modified remotely]**:应用程序将指示您下载的资产是否在[!DNL Experience Manager]服务器上发生更改。 该应用程序还提供下载最新版本和更新本地副本的选项。 请参阅[如何避免编辑冲突](using.md#adv-workflow-collaborate-avoid-conflicts)。

* **[!UICONTROL Check-out]**:如果您正在编辑文件或打算编辑文件，则可以切换要签出的状态。它会在应用程序和[!DNL Experience Manager] Web界面中的资产上添加一个锁定图标。 锁定图标会向其他用户指示避免同时编辑同一资产，因为它会导致编辑冲突。

* **[!UICONTROL Check-in]**:将资源标记为安全，以便其他用户进行编辑，而不会引起编辑冲突。上传更改时，锁图标会自动删除。 切换签入状态也会删除锁定图标，但建议不要在不上传更改的情况下手动签入。 如果放弃更改，则手动切换签入。

* **[!UICONTROL Open]** 操作：只需打开资产，在本机应用程序中预览它即可。不建议使用此操作来编辑资产，因为它不会签出资产，其他用户可能会进行导致编辑冲突的编辑。

* **[!UICONTROL Edit]** 操作：使用操作可修改图像。单击[!UICONTROL Edit]操作会自动签出资产，并在资产上添加一个锁定图标。 单击编辑后，如果您不想编辑资产，请单击[!UICONTROL Toggle check-in]。 要删除、重命名或移动[!DNL Experience Manager] DAM文件夹层次结构中的资产，请使用[!DNL Experience Manager] Web界面操作，而不要使用编辑操作。

* **[!UICONTROL Download]** 操作：将资源下载到本地计算机。您可以立即下载资源并稍后进行编辑；脱机工作，稍后上传更改。 资产会下载到文件系统的缓存文件夹中。

* **[!UICONTROL Reveal File]** 或 **[!UICONTROL Reveal Folder]** 操作：当资源下载到本地缓存文件夹时，应用程序会模拟本地网络驱动器并为每个资源提供本地路径。要了解此路径，请在应用程序中使用相应的显示选项。 在Creative Cloud应用程序中放置资产时需要显示操作。 请参阅[放置资产](using.md#place-assets-in-native-documents)。

* **[!UICONTROL Open In Web]** 操作：要在Web界面中视图 [!DNL Experience Manager] 资源，请在Web中打开它。您可以从[!DNL Experience Manager]接口启动更多工作流，如更新元数据或资产发现。

* **[!UICONTROL Delete]** 操作：从DAM存储库中删 [!DNL Experience Manager] 除资产。此操作将删除Experience Manager服务器上资产的原始副本。 如果只想放弃对本地资产的修改，请参阅[放弃更改](using.md#edit-assets-upload-updated-assets)。

* **[!UICONTROL Upload Changes]**:仅当您显式上传到服务器时，桌面应用程序才会上传更新 [!DNL Experience Manager] 的资产。保存编辑时，更改将仅保存在本地计算机上。 上传资产时，系统会自动签入资产，并删除锁图标。 请参阅[编辑资产](using.md#edit-assets-upload-updated-assets)。

## 在[!DNL Experience Manager] Web界面{#desktopactions-v2}中启用桌面操作

从浏览器的“资产”用户界面中，您可以浏览资产位置或签出并打开资产，以便在桌面应用程序中进行编辑。 这些选项称为[!UICONTROL Desktop Actions]，默认情况下未启用。 要启用它，请执行以下步骤。

1. 在“资产”控制台中，单击/点按工具栏中的&#x200B;**[!UICONTROL User]**&#x200B;图标。
1. 单击/点按&#x200B;**[!UICONTROL My Preferences]**&#x200B;以显示&#x200B;**[!UICONTROL Preferences]**&#x200B;对话框。
1. 在“用户首选项”对话框中，选择&#x200B;**[!UICONTROL Show Desktop Actions For Assets]**。 单击/点按&#x200B;**[!UICONTROL Accept]**。

   ![选中显示资产的桌面操作以启用桌面操作](assets/enable_desktop_actions.png)

   选中[!UICONTROL Show Desktop Actions For Assets]以启用桌面操作

## 浏览、搜索和预览资产{#browse-search-preview-assets}

您可以浏览到、搜索和预览[!DNL Experience Manager]存储库中的可用资产，所有这些资产都可以从桌面应用程序中进行。 在应用程序中尝试以下内容：

1. 浏览到某个文件夹，查看该文件夹中可用资源的一些基本信息以及所有资源的小缩略图。

   ![浏览DAM文件和文](assets/browse_folder_da2.png "件夹浏览DAM文件和文件夹")

1. 要视图更多信息和单个资产的较大缩略图，请单击文件名。

   ![查看资产和操作的更大预览查](assets/large_preview_actions_da2.png "看资产和操作的更大预览")

1. 单击&#x200B;**[!UICONTROL Open]**&#x200B;或&#x200B;**[!UICONTROL Edit]**&#x200B;以本地下载文件，只需将其视图或分别在本机应用程序中编辑。
1. 使用关键字搜索以在[!DNL Experience Manager]存储库中查找相关资产。 使用`?`和`*`作为通配符。 这些通配符分别替换单个字符或多个字符。 根据需要过滤和排序结果。

   ![使用星号通配符的示例](assets/search_wildcard_da2.png "搜索使用星号通配符的示例搜索")

   ![使用星号通配符的另一个](assets/search_wildcard2_da2.png "示例搜索使用星号通配符的不同位置的另一个示例搜索")

>[!NOTE]
>
>应用程序会在多个元数据字段中匹配搜索条件来显示资产，而不仅仅是资产的标题或文件名。

## 下载资产 {#download-assets}

您可以将资源下载到本地文件系统中。 应用程序从[!DNL Experience Manager]服务器获取资源，并将同一副本保存到您的本地文件系统中。

单击![更多选项图标](assets/do-not-localize/more2_da2.png)获取选项，然后单击![下载图标](assets/do-not-localize/download_cloud_da2.png)进行下载。

![资产的下载选项资](assets/download_option_da2.png "产的下载选项")

>[!NOTE]
>
>下载或上传大型文件或多个文件时，应用程序会关闭对资产和文件夹的操作。 下载或上载完成后，这些操作即可用。

如果队列大小较大或您遇到某些网络问题，下载多个资源可能会导致性能降低。 此外，在下载文件夹时，您可能会在不知不觉中将许多资产排队以供下载。 为避免等待时间过长，应用程序会限制一次下载的资源数。 要了解如何配置它，请参阅[设置首选项](install-upgrade.md#set-preferences)。 即使低于此限制，应用程序也可能在下载明显较大的文件夹之前寻求确认。

![App确认下载相对大量的资](assets/download_confirmation_da2.png "产App确认下载相对大量的资产")

如果选择并下载了文件夹，则应用程序仅下载直接存储在[!DNL Experience Manager]文件夹中的资源。 它不会自动从子文件夹下载资产。

## 在桌面上打开资源{#openondesktop-v2}

您可以打开远程资源，以便在本机应用程序中进行查看。 资源将下载到本地文件夹，并在与文件格式关联的本机应用程序中启动。 您可以更改本机应用程序以在Mac或Windows中打开特定文件类型（扩展名）。

单击资产菜单中的&#x200B;**[!UICONTROL Open]**。 资产将下载到本地并在本机应用程序中打开。 在状态栏中检查大型资产的下载进度和传输速度。

<!-- ![Download progress bar for large-sized assets](assets/download_status_bar_da2.png "Download progress bar for large-sized assets")
-->

>[!NOTE]
>
>如果应用程序中未反映预期的更改，请单击刷新图标![刷新图标](assets/do-not-localize/refresh.png)，或右键单击应用程序界面，然后单击&#x200B;**[!UICONTROL Refresh]**。 当进行较大的下载或上载时，这些操作不可用。

要打开资产的本地下载文件夹，请单击![更多操作图标](assets/do-not-localize/more2_da2.png)，然后单击![显示图标](assets/do-not-localize/reveal_action2_da2.png) **[!UICONTROL Reveal File]**&#x200B;操作。

## 使用资源或将资源放入本机文档{#place-assets-in-native-documents}

在某些情况下(例如，将资产放入本机文档时)，可以在Windows资源管理器或Mac Finder中访问文件。 要获取本地下载文件的文件系统位置，请使用![显示图标](assets/do-not-localize/reveal_action2_da2.png) **[!UICONTROL Reveal File]**&#x200B;选项。

![显示资产的文件操作](assets/revealfile_action_da2.png "显示资产的文件操作")

单击文件夹上的&#x200B;**[!UICONTROL Reveal File]**&#x200B;或&#x200B;**[!UICONTROL Reveal Folder]**，打开Windows资源管理器或Mac Finder，并在本地计算机上预先选择该文件或文件夹。 此选项对于将[!DNL Experience Manager]文件放置到支持放置或链接本地文件的本机应用程序中非常有用。 要了解如何在Adobe InDesign中放置文件，请参阅[放置图形](https://helpx.adobe.com/indesign/using/placing-graphics.html)。

**[!UICONTROL Reveal File]**&#x200B;操作将打开一个本地网络共享，该共享仅显示本地可用的资源 — 即显示使用应用程序显示、下载或打开/编辑的资源。 本地网络共享不会将任何更改上载到[!DNL Experience Manager]。 要上传更改，请在应用程序中显式使用&#x200B;**[!UICONTROL Upload Changes]**&#x200B;或&#x200B;**[!UICONTROL Upload]**&#x200B;操作。

>[!NOTE]
>
>为了向后兼容[!DNL Experience Manager]桌面应用程序v1.x，显示的文件来自本地网络共享，仅公开本地可用文件。 显示文件的桌面路径与应用程序v1.x创建的路径相同。

>[!CAUTION]
>
>请勿使用&#x200B;**[!UICONTROL Reveal File]**&#x200B;选项在本机应用程序中编辑资源。 请改用&#x200B;**[!UICONTROL Edit]**&#x200B;操作。 要了解更多信息，请参阅[高级工作流：协作处理相同文件，避免编辑冲突](#adv-workflow-collaborate-avoid-conflicts)。

## 编辑资产并将更新的资产上传到[!DNL Experience Manager] {#edit-assets-upload-updated-assets}

在您要进行更改时打开要编辑的资产，并将更新的资产上传到AExperience ManagerEM服务器。 要避免与其他用户的编辑冲突，请使用应用程序启动编辑会话。 在进行开始编辑之前，请确保资产上没有锁定图标，即其他用户没有编辑资产。

要编辑资产，请搜索资产或浏览至资产所在的位置。 单击![更多图标](assets/do-not-localize/more2_da2.png)，然后单击&#x200B;**[!UICONTROL Edit]**。

在以下两种情况下，使用&#x200B;**[!UICONTROL Toggle Check-out]**&#x200B;锁定资产以防止与其他用户的编辑冲突：

* 您无需先签出资源即可开始编辑资源（例如，只需打开它）。
* 您打算尽快开始编辑资产，而不希望他人编辑。

完成编辑后，应用程序将显示已更改资产的&#x200B;**[!UICONTROL Edited Locally]**&#x200B;状态。 保存到资产的所有更改都是仅本地更改，直到您将更改上传到[!DNL Experience Manager]。 要逐个上传单个或几个资产，请单击资产选项中的&#x200B;**[!UICONTROL Upload Changes]**。 它将在[!DNL Experience Manager]中创建资产的一个版本。 使用[!DNL Assets]的Web界面，您可以在[时间轴视图](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/activity-stream.html)中查看资产历史记录。

![应用程序中的“上传更改”](assets/upload_changes_single1_da2.png "选项应用程序中的“上传更改”选项")

![查看资产的大预览时上传更改选项查看资](assets/upload_changes_single2_da2.png "产的大预览时上传更改选项")

有关协作编辑的最佳实践，请参阅[高级工作流：协作处理相同文件，避免编辑冲突](#adv-workflow-collaborate-avoid-conflicts)。

在以下情况下，您可能希望放弃对本地资产所做的更改和编辑。 单击 **[!UICONTROL Discard Changes]**.

* 如果您不想在[!DNL Experience Manager]中保存本地更改。
* 开始在保存某些更改后对原始资产进行更改。
* 不再需要资产，请停止编辑。

如有必要，切换签出。 更新的资产将从本地缓存文件夹中删除，并在您编辑或打开时再次下载。

## 将新资产上传并添加到[!DNL Experience Manager] {#upload-and-add-new-assets-to-aem}

用户可以将新资产添加到DAM存储库。 例如，您可能是代理摄影师或承包商，希望将大量照片从照片拍摄添加到[!DNL Experience Manager]存储库。 要向[!DNL Experience Manager]添加新内容，请在应用程序顶栏中选择![上载到云选项](assets/do-not-localize/upload_to_cloud_da2.png)。 浏览到本地文件系统中的资源文件，然后单击&#x200B;**[!UICONTROL Select]**。 或者，在应用程序界面上拖动文件或文件夹。 应用程序开始上传资产。 如果上传时间较长，应用程序将在底部显示一个进度栏。 创建或上载文件夹时，请勿使用空格和无效字符。 请参阅[中允许的字符列表，创建 [!DNL Assets]](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.html#creating-folders)中的文件夹。

<!-- ![Download progress bar for large-sized assets](assets/upload_status_da2.png "Download progress bar for large-sized assets")
-->

您可以从本地文件系统上载文件夹或单个文件。 上载文件夹时，将保留该文件夹的层次结构。 在批量上传资产之前，请参阅[批量上传](#bulk-upload-assets)。

要视图在给定会话中传输的资产的列表，请单击&#x200B;**[!UICONTROL View]** > **[!UICONTROL Assets transfers]**。 该列表允许您视图并快速验证当前会话的文件传输。

![列表特定会话中的已转让资](assets/assets_transfered_da2.png "产特定会话中已转让资产的列表")

您可以在&#x200B;**[!UICONTROL Preferences]** > **[!UICONTROL Upload acceleration]**&#x200B;设置中控制上载并发（加速）。 更多并发通常会提供更快的上载，但会占用大量资源，消耗本地机器的更大处理能力。 如果您遇到速度较慢的系统，请使用较低的并发值重新尝试上载。

>[!NOTE]
>
>传输列表不是永久性的，如果您退出应用程序并重新打开它，则此传输不可用。

>[!NOTE]
>
>如果文件上传失败，并且您正在连接到[!DNL Experience Manager] 6.5.1或更高版本的部署，请参阅此[疑难解答信息](troubleshoot.md#upload-fails)。

## 使用多个资产{#work-with-multiple-assets}

用户可以使用一次上传所有编辑或单击几下即可上传嵌套文件夹等操作，轻松处理和管理多个资产。

### 浏览大文件夹{#browse-large-folders}

处理包含许多资产的文件夹时，滚动以视图更多资产。 要使用键盘滚动，请按Tab键几次以选择顶部的资产。 请注意突出显示的资产，以了解其何时被选中。 现在使用向下箭头键浏览资产的列表。

### 对选定资产{#quick-actions-for-selected-assets}执行快速操作

单击几个资产的缩略图以选择资产。 要选择所有资产，请单击应用程序顶栏中的复选框。 应用程序底部的工具栏会显示适用于所有选定资产的一组操作。

![底部的工具栏显示与选定资产相关的操作底部](assets/actions_bottom_toolbar1_da2.png "的工具栏显示选定资产的常见操作")

![当没有针对所选内容的常用操作时，工具栏中没有](assets/actions_bottom_toolbar2_da2.png "任何操作当没有针对所选内容的常用操作时，工具栏中没有任何操作")

底部工具栏中的可用操作取决于所选文件的状态。 例如，如果仅选择&#x200B;**[!UICONTROL Edited Locally]**&#x200B;文件，则会显示&#x200B;**[!UICONTROL Upload Changes]**&#x200B;图标。 如果选择&#x200B;**[!UICONTROL Edited locally]**&#x200B;和&#x200B;**[!UICONTROL Cloud only]**&#x200B;的混合，则&#x200B;**[!UICONTROL Upload Changes]**&#x200B;操作不可用。

### 查找所有已编辑的图像{#find-all-edited-images}

该应用程序提供一个名为&#x200B;**[!UICONTROL Edited locally]**&#x200B;的视图，用于让您快速访问本地下载（通过[!UICONTROL Open]或[!UICONTROL Edit]操作）并随后修改的所有文件。 该应用程序允许您选择所有本地编辑的资源，并在单击几下后上传所做的更改。 此视图还显示存在编辑冲突的本地编辑的资源。

![筛选以查看所有本地编辑的资](assets/edited_locally_filter_da2.png "产筛选以查看所有本地编辑的资产，例如批量上传编辑")

### 批量上传资产{#bulk-upload-assets}

摄影师或创意公司等用户或组织可以在场景中创建大量本地资源，如照片、润饰或从[!DNL Experience Manager]外完成的较大集合中进行选择。 他们可以直接从桌面应用程序将这些大型本地文件夹上传到[!DNL Assets]。 文件夹层次结构将被保留，所有嵌套的子文件夹及包含的资产都将被上传。 上传的资产也会立即可供同一服务器的其他用户使用。 资产在后台上传，因此操作不会绑定到Web浏览器会话。

![将多个本地文件夹从桌面批量上传到 [!DNL Experience Manager]](assets/upload_local_folders_da2.png "将多个本地文件夹从桌面批量上传到Experience Manager")

上传后，如果应用程序中未反映预期更改，请单击刷新图标![刷新图标](assets/do-not-localize/refresh.png)。

>[!NOTE]
>
>请勿使用上传功能跨两个[!DNL Experience Manager]部署迁移资产。 请参阅[迁移指南](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/assets-migration-guide.html)。

### 已转让资产列表{#list-of-transferred-assets}

要视图在给定会话中传输的资产的列表，请参阅[将资产上传到 [!DNL Experience Manager]](#upload-and-add-new-assets-to-aem)。

## 高级工作流：开始来自[!DNL Assets] Web接口{#adv-workflow-start-from-aem-ui}

如有必要，请从“资产”Web界面启动您的工作流。 桌面应用程序与[!DNL Experience Manager]集成，以便在使用桌面操作进行请求时接管。

从Web界面启动工作流的一个特殊情况是资产发现。 资产用户界面中的搜索栏可优惠丰富的高级搜索体验。 您可能希望首先在Web上找到所需的资源，然后使用[!UICONTROL Desktop Actions]在应用程序中启动工作流。 某些示例案例包括使用facet筛选搜索结果、查找从Adobe Stock授权的特定资产，或您的组织实现的允许您从Web界面进行更好发现的自定义。

当您尝试在资产Web界面上执行以下操作时，将使用桌面应用程序功能：

* 允许[!UICONTROL Open]、[!UICONTROL Edit]和[!UICONTROL Reveal]的[!UICONTROL Desktop Actions]
* [!UICONTROL Upload folder]
* [!UICONTROL Check-out] 或 [!UICONTROL check-in]

例如，对于在应用程序中签出的资产，Web界面上的可用操作有[!UICONTROL Open]、[!UICONTROL Reveal]和[!UICONTROL Check-in]。

![Web界面中的桌面操 [!DNL Experience Manager] 作](assets/assets_web_actions_da2.png "Experience Manager Web界面中的桌面操作")

>[!NOTE]
>
>浏览器可能会提示您允许启动[!DNL Adobe Experience Manager]桌面。 要享受从浏览器到应用程序的不间断传输，请选中相应的复选框以始终允许应用程序接管。

您无法使用Web界面找到以下信息或工作流。 使用桌面应用程序作为Web界面不会跟踪本地更改，并且不知道以下内容：

* 在本地编辑的文件。
* 存在编辑冲突的文件以及解决冲突的方法。
* 将本地更改上载到[!DNL Experience Manager]。
* 本地可用文件的各种状态。

相反，您可以使用&#x200B;**[!UICONTROL Open In Web]**&#x200B;操作从桌面应用程序开始，在Web界面中打开资产。

## 高级工作流：协作处理同一文件，避免编辑冲突{#adv-workflow-collaborate-avoid-conflicts}

在协作环境中，多个用户可能处理同一组资产，这可能会导致版本控制冲突。 要防止冲突，请遵循以下最佳实践：

* 请勿通过单击[!UICONTROL Open]来编辑任何资产。 请勿通过从文件系统文件夹打开来编辑本地下载的资源。 其他用户不知道正在编辑资产。
* 要编辑资产，请始终单击[!UICONTROL Edit]。 它会在本机应用程序中打开资产，并在资产上添加一个锁定图标，以便其他用户知道正在编辑该资产。
* 如果您不慎开始编辑，而未单击[!UICONTROL Edit]，请单击[!UICONTROL Toggle Check-in]。 这会向资产中添加一个锁定图标。 即使您计划稍后编辑资产，但希望避免其他人编辑资产，请单击[!UICONTROL Toggle Check-in]以锁定资产。
* 在编辑资产之前，请确保其他用户没有对其进行编辑。 在资产上查找锁定图标。
* 完成编辑后，上传所有更改，然后签入资产。

![编辑冲突的状](assets/edits_conflicts_status_da2.png "态编辑冲突的状态")

如果在[!DNL Experience Manager]服务器上更新了本地下载的资产，则应用程序将显示&#x200B;**[!UICONTROL Modified remotely]**&#x200B;状态。 您可以分别单击[!UICONTROL Remove]或[!UICONTROL Update]删除本地副本或刷新本地副本。 对话框上的链接允许您视图资产的两个版本。

![用于解决资产远程修改时冲突的选项用于解](assets/modified_remotely_dialog_da2.png "决资产远程修改时冲突的选项")

如果您正在本地编辑的资源也会在服务器上更新，而您不知情，则应用程序将显示&#x200B;**[!UICONTROL Editing Conflict]**&#x200B;状态。 您可以保留一组更改 — 保留您的更新（单击&#x200B;**[!UICONTROL Keep Mine]**）并删除其他用户的编辑或尊重其他用户的更新并删除您的更新(**[!UICONTROL Overwrite Mine]**)。

![解决编辑冲突的选](assets/editing_conflict_dialog_da2.png "项解决编辑冲突的选项")

## 高级工作流：将资源放置并链接到InDesign文件{#adv-workflow-place-assets-indesign}

当您使用[!DNL Experience Manager]桌面应用程序打开包含链接资源的文件时，会预先下载资源并显示在本机应用程序中。 要使此工作流正常工作，您的本机应用程序必须支持放置指向本地资源的链接，并且[!DNL Experience Manager]必须支持解析二进制文件中指向服务器端引用的这些链接。

[!DNL Experience Manager] 桌面应用程序支持此工作流，只需选择一些Adobe Creative Cloud桌面应用程序和文件格式 — Adobe InDesign、Adobe Illustrator和Adobe Photoshop。该工作流允许您高效地处理受支持的Creative Cloud文件。 因此，如果用户A将一些资源放在InDesign文件中并将其签入[!DNL Experience Manager]，则用户B将在InDesign文件中看到资源，即使这些资源不是文件的一部分。 资源将本地下载到用户B的计算机上。

>[!NOTE]
>
>桌面应用程序可映射到Windows上的任何驱动器。 但是，对于平滑操作，不要更改默认驱动器盘符。 如果同一组织的用户使用不同的驱动器号，则他们无法看到其他人放置的资产。 路径更改时不会获取所放置的资产。 放置的资源将继续保留在二进制文件（例如INDD）中，并且不会被删除。

要了解此工作流的限制，请参阅[系统要求和支持的版本](release-notes.md)。

要尝试使用此工作流处理图像资产和InDesign，请执行以下步骤：

1. 在[!DNL Experience Manager]中放置资源的INDD文件，请务必使用它。 要了解如何创建此类INDD文件，请参阅[置入图形](https://helpx.adobe.com/indesign/using/placing-graphics.html)。
1. 从桌面应用程序中，**[!UICONTROL Edit]**&#x200B;放置资源位于[!DNL Experience Manager]的INDD文件。
1. 应用程序会同时下载InDesign文件和链接的资源。 InDesign打开文档时，链接会解析，资产会下载，资产会显示在InDesign文档中。
1. 要将新图形放入InDesign文件，请对资产使用&#x200B;**[!UICONTROL Reveal File]**&#x200B;操作。 该操作将本地下载资产，并在Windows资源管理器或Mac Finder中打开本地网络共享位置。
1. 将显示的资产放入InDesign文档。 这会在文档中创建链接。
1. 在InDesign文档中完成编辑后，请保存它，然后使用桌面应用程序将其上传到[!DNL Experience Manager]。

## 高级工作流：在本地下载资源{#adv-workflow-download-assets-locally}

在许多情况下，应用程序将从文件系统上的本地[!DNL Experience Manager]服务器下载资源。 下载会占用带宽和磁盘空间。 了解这些方案可帮助您优化等待下载完成的时间。

您可以从应用程序内按需下载资产。 请参阅[下载资产](#download-assets)。

当您使用[!UICONTROL Open]操作在本机桌面应用程序中打开资产时，如果本地尚不可用，则将本地下载该资产。 请参阅[打开资产](#openondesktop-v2)。

当您从应用程序中显示资产或文件夹的位置时，资产或文件夹首先将下载到本地，然后在您的计算机上的本地网络共享中打开。 请参阅[打开资产](#openondesktop-v2)。

当您使用[!UICONTROL Edit]操作在本机桌面应用程序中编辑资产时，如果资产尚未在本地可用，则将下载到本地。 请参阅[编辑资产并将更新的资产上传到 [!DNL Experience Manager]](#edit-assets-upload-updated-assets)。

如果已安装并允许安装该应用程序，则当您从[!DNL Experience Manager] Web界面使用[!UICONTROL Desktop Actions]时，该应用程序将完成操作。 应用程序首先下载资产，然后完成操作。
