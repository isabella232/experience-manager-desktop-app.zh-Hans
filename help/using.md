---
title: 使用Adobe Experience Manager桌面应用程序
description: 了解如何安装和使用Adobe Experience Manager桌面应用程序，如何直接从Win或Mac桌面处理Adobe Experience ManagerDAM资产。 了解最佳实践和疑难解答信息。
uuid: 55057617-89de-43cd-8419-1252a42ab2fb
contentOwner: AG
products: SG_EXPERIENCEMANAGER/6.3/ASSETS
discoiquuid: 39d7bcad-d7b0-4978-a790-4cb68b8a7d6a
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 27cc0ba26622016ce82b758fb0607652176f6992
workflow-type: tm+mt
source-wordcount: '3995'
ht-degree: 0%

---


# Use Adobe Experience Manager desktop app {#use-aem-desktop-app-v2}

使用Adobe Experience Manager(AEM)桌面应用程序轻松访问本地桌面上的Adobe Experience ManagerDAM资产，并将这些资产用于任何桌面应用程序。 您可以在桌面应用程序中打开资产并在本地编辑资产——使用版本控制将更改上传回Experience Manager，以与其他用户共享更新。 您还可以将新文件和文件夹层次结构上传到Experience Manager，创建文件夹，以及从Experience ManagerDAM中删除资产或文件夹。

该集成允许组织中的各种角色在Experience Manager资产中集中管理资产，并在Windows或Mac OS上的本机应用程序中访问本地桌面上的资产。

在注销后或首次打开应用程序时，请提供Experience Manager服务器的URL。 单击“连接”。 提供凭据以将应用程序与服务器连接。

您使用Experience Manager桌面应用程序执行的关键任务包括：

![工作流和任务，您可以使用桌面 [!DNL Experience Manager] 应用](assets/aem_desktop_app_usecases_v2.png "程序完成工作流和任务，您可以使用Adobe Experience Manager桌面应用程序")完 [成工作](assets/aem_desktop_app_usecases_print.pdf) 流下载此可打印的PDF文件。

## 桌面应用程序的工作方式 {#how-app-works2}

在开始使用应用程序之前，请了解 [应用程序的工作方式](release-notes.md#how-app-works)。 另外，请熟悉以下术语：

* **[!UICONTROL Desktop Actions]**: 从资产Web界面中，您可以在浏览器中浏览资产位置或签出并打开资产，以便在本机桌面应用程序中进行编辑。 这些操作可从Web界面使用桌面应用程序功能。 了解 [如何启用桌面操作](using.md#desktopactions-v2)。

* 文件状态 **[!UICONTROL Cloud Only]**&#x200B;为： 此类资产不会下载到本地计算机上，并且仅在Experience Manager服务器上可用。

* 文件状态 **[!UICONTROL Available locally]**&#x200B;为： 资产会按原样下载并在本地计算机上可用。 资产不会更改。

* 文件状态 **[!UICONTROL Edited locally]**&#x200B;为： 此类资产将在本地进行修改，更改将保留到上传到Experience Manager服务器。 上传后，状态将变为 [!UICONTROL Available locally]。 请参阅 [编辑资产](using.md#edit-assets-upload-updated-assets)。

* 文件状态 **[!UICONTROL Editing conflict]**&#x200B;为： 如果您和其他用户同时修改资产，则应用程序会指示发生编辑冲突。 应用程序还提供保留或放弃更改的选项。 了解 [如何避免编辑冲突](using.md#adv-workflow-collaborate-avoid-conflicts)。

* 文件状态 **[!UICONTROL Modified remotely]**&#x200B;为： 应用程序会指示您下载的资产是否在Experience Manager服务器上发生更改。 应用程序还提供下载最新版本和更新本地副本的选项。 了解 [如何避免编辑冲突](using.md#adv-workflow-collaborate-avoid-conflicts)。

* **[!UICONTROL Check-out]**: 如果您正在编辑文件或打算编辑文件，则可以切换状态以签出。 它会在应用程序和AEM Web界面中为资产添加一个锁图标。 锁定图标会向其他用户指示避免同时编辑同一资产，因为它会导致编辑冲突。

* **[!UICONTROL Check-in]**: 将资产标记为安全，以便其他用户进行编辑，而不会造成编辑冲突。 上传更改时，锁图标会自动删除。 切换签入状态也会删除锁定图标，但建议不要在不上传更改的情况下手动签入。 如果放弃更改，则手动切换签入。

* **[!UICONTROL Open]** 操作： 只需打开资产，在本机应用程序中预览它即可。 不建议使用此操作来编辑资产，因为它不会签出资产，并且其他用户可能会进行编辑，从而导致编辑冲突。

* **[!UICONTROL Edit]** 操作： 使用操作修改图像。 单击 [!UICONTROL Edit] 操作会自动签出资产，并在资产上添加一个锁图标。 单击编辑后，如果您不想编辑资产，请单击 [!UICONTROL Toggle check-in]。 要删除、重命名或移动AEM DAM文件夹层次结构中的资产，请使用AEM Web界面操作，而不要使用编辑操作。

* **[!UICONTROL Download]** 操作： 将资源下载到本地计算机。 您可以立即下载资源并稍后进行编辑； 脱机工作，稍后上传更改。 资产会下载到文件系统的缓存文件夹中。

* **[!UICONTROL Reveal File]** 或 **[!UICONTROL Reveal Folder]** 操作： 当资源下载到本地缓存文件夹时，应用程序将模拟本地网络驱动器并为每个资源提供本地路径。 要了解此路径，请在应用程序中使用相应的显示选项。 在Creative Cloud应用程序中放置资产时，需要显示操作。 请参 [阅放置资产](using.md#place-assets-in-native-documents)。

* **[!UICONTROL Open In Web]** 操作： 要在AEM Web界面中视图资产，请在Web中打开它。 您可以从AEM界面启动更多工作流，如更新元数据或资产发现。

* **[!UICONTROL Delete]** 操作： 从AEM DAM存储库中删除资产。 此操作将删除AEM服务器上资产的原始副本。 如果只想放弃对本地资产的修改，请参阅放弃 [更改](using.md#edit-assets-upload-updated-assets)。

* **[!UICONTROL Upload Changes]**: 仅当您显式上传到AEM服务器时，桌面应用程序才会上传更新的资产。 保存编辑时，更改将仅保存在本地计算机上。 上传资产时，资产会自动签入，并删除锁图标。 请参阅 [编辑资产](using.md#edit-assets-upload-updated-assets)。

## 在AEM Web界面中启用桌面操作 {#desktopactions-v2}

从浏览器的“资产”用户界面中，您可以浏览资产位置或签出并打开资产，以便在桌面应用程序中进行编辑。 这些选项被调 [!UICONTROL Desktop Actions] 用，默认情况下不启用。 要启用它，请按照以下步骤操作。

1. 在“资产”控制台中，单击／点 **[!UICONTROL User]** 按工具栏中的图标。
1. 单击／点按 **[!UICONTROL My Preferences]** 以显示对 **[!UICONTROL Preferences]** 话框。
1. 在“用户首选项”对话框中，选择 **[!UICONTROL Show Desktop Actions For Assets]**。 单击／点按 **[!UICONTROL Accept]**。

   ![选中“显示资产的桌面操作”以启用桌面操作](assets/chlimage_1-3.png)

   检查 [!UICONTROL Show Desktop Actions For Assets] 以启用桌面操作

## 浏览、搜索和预览资产 {#browse-search-preview-assets}

您可以从桌面应用程序中浏览到、搜索和预览AEM存储库中的可用资产。 在应用程序中尝试以下内容：

1. 浏览到文件夹，查看该文件夹中可用资产的一些基本信息以及所有资产的小缩略图。

   ![浏览DAM文件和文](assets/browse_folder_da2.png "件夹浏览DAM文件和文件夹")

1. 要视图更多信息和单个资产的较大缩略图，请单击文件名。

   ![查看资产和操作的更大预览](assets/large_preview_actions_da2.png "查看资产和操作的更大预览")

1. 单 **[!UICONTROL Open]** 击或 **[!UICONTROL Edit]** 以本地下载文件，只需分别将其视图或在本机应用程序中编辑。
1. 使用关键字搜索以在AEM存储库中查找相关资产。 使用 `?` 和 `*` 作为通配符。 这些通配符分别替换单个字符或多个字符。 根据需要过滤结果并对结果进行排序。

   ![使用星号通配符的示例](assets/search_wildcard_da2.png "搜索使用星号通配符的示例搜索")

   ![使用星号通配符的另一](assets/search_wildcard2_da2.png "个示例搜索使用星号通配符的不同位置的另一个示例搜索")

>[!NOTE]
>
>该应用程序通过在多个元数据字段中匹配搜索条件来显示资产，而不仅仅是资产的标题或文件名。

## 下载资产 {#download-assets}

您可以在本地文件系统上下载资源。 应用程序从AEM服务器获取资产，并将同一副本保存到您的本地文件系统。

单击 ![更多选项图标](assets/do-not-localize/more2_da2.png) ，然后单击 ![下载图标](assets/do-not-localize/download_cloud_da2.png) 以下载选项。

![资产的下载选](assets/download_option_da2.png "项资产的下载选项")

>[!NOTE]
>
>下载或上传大型文件或多个文件时，应用程序会关闭对资产和文件夹的操作。 下载或上传完成后，这些操作即可用。

如果队列大或遇到某些网络问题，下载多个资源可能会导致性能降低。 此外，在下载文件夹时，您可能会在不知不觉中将许多资产排队下载。 为避免等待时间过长，应用程序一次性限制下载的资源数。 要了解如何配置它，请参阅设 [置首选项](install-upgrade.md#set-preferences)。 即使低于此限制，应用程序有时也会在下载明显较大的文件夹之前寻求确认。

![应用程序确认下载相对大量的资](assets/download_confirmation_da2.png "产应用程序确认下载相对大量的资产")

如果选择并下载了文件夹，则应用程序只下载直接存储在AEM文件夹中的资产。 它不会自动从子文件夹下载资产。

## 在桌面上打开资源 {#openondesktop-v2}

您可以打开远程资源，以便在本机应用程序中进行查看。 资源将下载到本地文件夹，并在与文件格式关联的本机应用程序中启动。 您可以更改本机应用程序以在Mac或Windows中打开特定文件类型（扩展名）。

从资 **[!UICONTROL Open]** 产菜单中单击。 资产将下载到本地并在本机应用程序中打开。 在状态栏中检查大型资产的下载进度和传输速度。

<!-- ![Download progress bar for large-sized assets](assets/download_status_bar_da2.png "Download progress bar for large-sized assets")
-->

>[!NOTE]
>
>如果应用程序中未反映预期的更改，请单击刷新图标 ![刷新图标](assets/do-not-localize/refresh.png) ，或在应用程序界面中右键单击并单击 **[!UICONTROL Refresh]**。 当进行较大的下载或上传时，这些操作不可用。

要打开资产的本地下载文件夹，请单击“更 ![多操作”图标](assets/do-not-localize/more2_da2.png) ，然后单 ![击“显示”图标](assets/do-not-localize/reveal_action2_da2.png)**[!UICONTROL Reveal File]** 操作。

## 将资源使用或放入本机文档 {#place-assets-in-native-documents}

在某些情况下，例如将资产置入本机文档时，您可以在Windows资源管理器或Mac Finder中访问文件。 要获取本地下载文件的文件系统位置，请使用“显 ![示”图标](assets/do-not-localize/reveal_action2_da2.png)**[!UICONTROL Reveal File]** 选项。

![显示资产的文件操](assets/revealfile_action_da2.png "作显示资产的文件操作")

单击 **[!UICONTROL Reveal File]**&#x200B;或在文 **[!UICONTROL Reveal Folder]** 件夹上，打开Windows资源管理器或Mac Finder，并在本地计算机上预先选择文件或文件夹。 此选项对于（例如）将AEM文件放入支持置入或链接本地文件的本机应用程序非常有用。 要了解如何在Adobe InDesign中放置文件，请参阅 [置入图形](https://helpx.adobe.com/indesign/using/placing-graphics.html)。

该操 **[!UICONTROL Reveal File]** 作会打开一个本地网络共享，该共享仅显示本地可用的资产——即显示使用应用程序显示、下载或打开／编辑的资产。 本地网络共享不会将任何更改上传到AEM。 要上传更改，请在应用程序 **[!UICONTROL Upload Changes]** 中显 **[!UICONTROL Upload]** 式使用或执行操作。

>[!NOTE]
>
>为了向后兼容AEM桌面应用程序v1.x，显示的文件通过本地网络共享提供，仅公开本地可用文件。 显示文件的桌面路径与应用程序v1.x创建的路径相同。

>[!CAUTION]
>
>请勿使用选 **[!UICONTROL Reveal File]** 项在本机应用程序中编辑资源。 而是使用操 **[!UICONTROL Edit]** 作。 要了解更多信息，请参阅高 [级工作流： 协作处理同一文件并避免编辑冲突](#adv-workflow-collaborate-avoid-conflicts)。

## 编辑资产并将更新的资产上传到AEM {#edit-assets-upload-updated-assets}

在您要进行更改时打开要编辑的资产，并将更新的资产上传到AEM服务器。 要避免与其他用户的编辑冲突，请使用应用程序启动编辑会话。 在进行开始编辑之前，请确保资产上没有锁定图标，即其他用户没有编辑资产。

要编辑资产，请搜索资产或浏览至资产所在的位置。 单击“ ![更多”图](assets/do-not-localize/more2_da2.png) 标，然后单 **[!UICONTROL Edit]**&#x200B;击。

在以 **[!UICONTROL Toggle Check-out]** 下两种情况下，均可使用锁定资产以防止与其他用户的编辑冲突：

* 您已开始编辑资产，但无需先签出（例如，只打开它）。
* 您打算尽快开始编辑资产，但不希望其他人进行编辑。

完成编辑后，应用程序将显示已更 **[!UICONTROL Edited Locally]** 改资产的状态。 在将更改上传到AEM之前，保存到资产的所有更改均仅限本地。 要逐个上传单个或几个资产，请从资 **[!UICONTROL Upload Changes]** 产的选项中单击。 它会在AEM中创建资产的某个版本。 使用AEM Assets的Web界面，您可以在时间轴视图中查看资产 [历史记录](https://docs.adobe.com/content/help/en/experience-manager-65/assets/using/activity-stream.html)。

![应用程序中的“上传更改”](assets/upload_changes_single1_da2.png "选项中的“上传更改”选项")

![查看资产的大预览时上传更改选项查看资](assets/upload_changes_single2_da2.png "产的大预览时上传更改选项")

有关协作编辑的最佳实践，请参阅高 [级工作流： 协作处理同一文件并避免编辑冲突](#adv-workflow-collaborate-avoid-conflicts)。

在以下情况下，您可能希望放弃对本地资产所做的更改和编辑。 单击 **[!UICONTROL Discard Changes]**.

* 如果您不想在AEM中保存本地更改。
* 开始在保存某些更改后对原始资产进行更改。
* 不再需要资产，请停止编辑该资产。

如有必要，可切换签出。 更新的资产将从本地缓存文件夹删除，并在您编辑或打开时再次下载。

## 将新资产上传并添加到AEM {#upload-and-add-new-assets-to-aem}

用户可以将新资产添加到DAM存储库。 例如，您可能是代理摄影师或承包商，希望将大量照片从照片拍摄添加到AEM存储库。 要向AEM添加新内容，请单 ![击应用程序顶栏](assets/do-not-localize/upload_to_cloud_da2.png) 中的“上传到云”图标。 浏览到本地文件系统中的资产文件，然后单击 **[!UICONTROL Select]**。 如果资产上传时间较长，则应用程序开始会上传资产并在底部显示进度栏。 创建或上传文件夹时，请勿使用空格和无效字符。 请参阅在列表中创建 [文件夹中的AEM Assets字符](https://docs.adobe.com/content/help/en/experience-manager-65/assets/managing/managing-assets-touch-ui.html#Creatingfolders)。

<!-- ![Download progress bar for large-sized assets](assets/upload_status_da2.png "Download progress bar for large-sized assets")
-->

您可以从本地文件系统上载文件夹或单个文件。 上传文件夹时，会保留其层次结构。 在批量上传资产之前，请参阅 [批量上传](#bulk-upload-assets)。

要视图在给定会话中转移的资产的列表，请单击 **[!UICONTROL View]** > **[!UICONTROL Assets transfers]**。 列表允许您视图并快速验证当前会话的文件传输。

![特定会话中已转让资产](assets/assets_transfered_da2.png "的列表特定会话中已转让资产的列表")

您可以在>设置中控制上传并发( **[!UICONTROL Preferences]** 加速 **[!UICONTROL Upload acceleration]** )。 更多并发通常提供更快的上传，但可能会占用大量资源，消耗本地机器的更大处理能力。 如果您遇到系统速度较慢的问题，请使用较低的并发值重新尝试上载。

>[!NOTE]
>
>传输列表不是永久的，如果退出应用程序并重新打开它，则此转换不可用。

>[!NOTE]
>
>如果文件无法上传，并且您正在连接到AEM 6.5.1或更高版本的部署，请参阅此疑难 [解答信息](troubleshoot.md#upload-fails)。

## 使用多个资源 {#work-with-multiple-assets}

用户可以使用一次上传所有编辑或单击几下即可上传嵌套文件夹等操作，轻松处理和管理多个资产。

### 浏览大型文件夹 {#browse-large-folders}

处理包含许多资产的文件夹时，滚动以视图更多资产。 要使用键盘滚动，请多按Tab键，以选择顶部的资产。 请注意突出显示的资产，以了解其何时被选择。 现在使用向下箭头键浏览资产列表。

### 对选定资产执行快速操作 {#quick-actions-for-selected-assets}

单击几个资产的缩略图以选择资产。 要选择所有资产，请单击应用程序顶栏中的复选框。 应用程序底部的工具栏中会显示适用于所有选定资产的一组操作。

![底部的工具栏显示与选定资产相关的](assets/actions_bottom_toolbar1_da2.png "操作底部的工具栏显示选定资产的常见操作")

![没有选择的常用操作时工具栏中没有操](assets/actions_bottom_toolbar2_da2.png "作没有选择的常用操作时工具栏中没有操作")

底部工具栏中的可用操作取决于所选文件的状态。 例如，如果仅选择文 **[!UICONTROL Edited Locally]** 件，您将看到 **[!UICONTROL Upload Changes]** 图标。 如果您选择了和的 **[!UICONTROL Edited locally]** 组合 **[!UICONTROL Cloud only]**，则 **[!UICONTROL Upload Changes]** 该操作不可用。

### 查找所有已编辑的图像 {#find-all-edited-images}

该应用程序提供一个视图, **[!UICONTROL Edited locally]**&#x200B;称为，允许您快速访问您本地下载（通过或操作）并 [!UICONTROL Open] 进行修 [!UICONTROL Edit] 改的所有文件。 该应用程序允许您选择所有本地编辑的资产，并只需单击几下即可上传所做的更改。 此视图还显示存在编辑冲突的本地编辑的资产。

![筛选以查看所有本地编辑的资](assets/edited_locally_filter_da2.png "产筛选以查看所有本地编辑的资产，例如批量上传编辑")

### 批量上传资产 {#bulk-upload-assets}

用户或组织（如摄影师或创意公司）可以在场景中创建大量本地资源，如照片、润饰或从AEM外完成的较大集合中进行选择。 他们可以直接从桌面应用程序将这些大型本地文件夹上传到AEM Assets。 文件夹层次结构将被保留，并且所有嵌套的子文件夹和包含的资产都会被上传。 上传的资产也会立即提供给同一服务器的其他用户使用。 资产在后台上传，因此操作不会绑定到Web浏览器会话。

![将多个本地文件夹从桌面批量上传到AEM](assets/upload_local_folders_da2.png "将多个本地文件夹从桌面上传到AEM")

上传后，如果应用程序中未反映预期的更改，请单击刷新图标刷 ![新图标](assets/do-not-localize/refresh.png)。

>[!NOTE]
>
>请勿使用上传功能跨两个AEM部署迁移资产。 相反，请参阅迁 [移指南](https://docs.adobe.com/content/help/en/experience-manager-65/assets/administer/assets-migration-guide.html)。

### 列表已转让资产 {#list-of-transferred-assets}

要视图在给定会话中转移的资产的列表，请参 [阅将资产上传到AEM](#upload-and-add-new-assets-to-aem)。

## 高级工作流： 开始自AEM AssetsWeb界面 {#adv-workflow-start-from-aem-ui}

如有必要，从AEM AssetsWeb界面启动您的工作流。 桌面应用程序与AEM集成，可在使用桌面操作进行请求时接管。

从Web界面启动工作流的一个特殊情况是资产发现。 资产用户界面中的Omnisearch栏可优惠丰富的高级搜索体验。 您可能希望首先在Web上找到所需的资产，然后使用启动应用程序中的工作流 [!UICONTROL Desktop Actions]。 某些示例包括使用彩块化筛选搜索结果、查找从Adobe Stock授权的特定资产，或您的组织实施的允许您从Web界面更好地发现的自定义。

当您尝试在Assets Web界面上执行以下操作时，将使用桌面应用程序功能：

* 允 [!UICONTROL Desktop Actions] 许 [!UICONTROL Open]、 [!UICONTROL Edit]和 [!UICONTROL Reveal]
* [!UICONTROL Upload folder]
* [!UICONTROL Check-out] 或 [!UICONTROL check-in]

例如，对于在应用程序中签出的资产，Web界面上的可用操作 [!UICONTROL Open]有 [!UICONTROL Reveal]、和 [!UICONTROL Check-in]。

![AEM Web界面中的桌面操](assets/assets_web_actions_da2.png "作AEM Web界面中的桌面操作")

>[!NOTE]
>
>浏览器可能会提示您允许启动Adobe Experience Manager桌面。 要享受从浏览器到应用程序的不间断传输，请选中相应的复选框，始终允许应用程序接管。

使用Web界面找不到以下信息或工作流。 使用桌面应用程序，因为Web界面不跟踪本地更改，并且不知道以下内容：

* 在本地编辑的文件。
* 存在编辑冲突的文件以及解决该冲突的方法。
* 将本地更改上传到AEM。
* 本地可用文件的各种状态。

相反，您可以使用操作在从桌面应用程序开始的Web界面中打开资 **[!UICONTROL Open In Web]** 产。

## 高级工作流： 协作处理同一文件，避免编辑冲突 {#adv-workflow-collaborate-avoid-conflicts}

在协作环境中，多个用户可能使用同一组资产，这会导致版本控制冲突。 要防止冲突，请遵循以下最佳实践：

* 请勿通过单击来编辑任何资 [!UICONTROL Open]产。 请勿通过从文件系统文件夹打开来编辑本地下载的资源。 其他用户不知道正在编辑资产。
* 要编辑资产，请始终单击 [!UICONTROL Edit]。 它会在本机应用程序中打开资产并在资产上添加一个锁定图标，以便其他用户知道正在编辑该资产。
* 如果您 [!UICONTROL Toggle Check-in] 意外开始编辑，请单击，而不 [!UICONTROL Edit]单击。 这会向资产添加一个锁图标。 即使您计划稍后编辑资产，但希望避免其他人编辑资产，也可以单 [!UICONTROL Toggle Check-in] 击以锁定资产。
* 在编辑资产之前，请确保其他用户没有对其进行编辑。 在资产上查找锁定图标。
* 完成编辑后，请上传所有更改，然后签入资产。

![编辑冲突的状](assets/edits_conflicts_status_da2.png "态编辑冲突的状态")

如果本地下载的资产在AEM服务器上更新，则应用程序将显示状 **[!UICONTROL Modified remotely]** 态。 您可以通过单击或分别单击来删除本地副本或刷 [!UICONTROL Remove] 新本地 [!UICONTROL Update] 副本。 对话框上的链接允许您视图资产的两个版本。

![用于解决资产远程修改时冲突的选](assets/modified_remotely_dialog_da2.png "项用于解决资产远程修改时冲突的选项")

如果您在本地编辑的资产也会在服务器上更新，而您并不知道该资产，则应用程序会显示一个 **[!UICONTROL Editing Conflict]** 状态。 您可以保留一组更改——保留您的更新(单击 **[!UICONTROL Keep Mine]**)并删除其他用户的编辑，或保留其他用户的更新并删除您的更新(**[!UICONTROL Overwrite Mine]**)。

![解决编辑冲突的选](assets/editing_conflict_dialog_da2.png "项解决编辑冲突的选项")

## 高级工作流： 在InDesign文件中放置和链接资源 {#adv-workflow-place-assets-indesign}

当您使用AEM桌面应用程序打开包含链接资产的文件时，会预先下载资产并显示在本机应用程序中。 要使此工作流正常工作，您的本机应用程序必须支持放置指向本地资产的链接，并且AEM必须支持在指向服务器端引用的二进制文件中解析这些链接。

AEM桌面应用程序通过几种精选的Adobe Creative Cloud桌面应用程序和文件格式（Adobe InDesign、Adobe Illustrator和Adobe Photoshop）支持此工作流程。 该工作流程允许您高效地处理受支持的Creative Cloud文件。 因此，如果用户A将一些资源放入InDesign文件并将其签入AEM，则用户B将在InDesign文件中看到这些资源，即使这些资源不是文件的一部分。 资源将本地下载到用户B的计算机上。

>[!NOTE]
>
>桌面应用程序可映射到Windows上的任何驱动器。 但是，对于平滑操作，不要更改默认驱动器盘符。 如果同一组织的用户使用不同的驱动器号，则他们看不到其他人放置的资产。 路径更改时不会获取已放置的资产。 置入的资源继续保留在二进制文件（如INDD）中，并且不会删除。

要了解此工作流程的限制，请参阅系 [统要求和支持的版本](release-notes.md#system-requirements-and-prerequisites-v2)。

要尝试使用图像资源和InDesign的此工作流程，请执行以下步骤：

1. 在AEM中为置入的资产准备好INDD文件。 要了解如何创建此类INDD文件，请参阅 [置入图形](https://helpx.adobe.com/indesign/using/placing-graphics.html)。
1. 从桌面应用程序 **[!UICONTROL Edit]** 中，在AEM中包含已放置资产的INDD文件。
1. 应用程序同时下载InDesign文件和链接的资源。 当InDesign打开文档时，链接会解析，资产会下载，资产会显示在InDesign文档中。
1. 要将新图形放入InDesign文件，请对资 **[!UICONTROL Reveal File]** 产使用操作。 此操作将本地下载资产，并在Windows资源管理器或Mac Finder中打开本地网络共享位置。
1. 将显示的资源放入InDesign文档。 这会在文档中创建链接。
1. 在InDesign文档中完成编辑后，请保存它，然后使用桌面应用程序将其上传到AEM。

## 高级工作流： 本地下载资源 {#adv-workflow-download-assets-locally}

在许多情况下，应用程序会从文件系统的本地AEM服务器下载资产。 下载会占用带宽和磁盘空间。 了解这些方案有助于您优化等待下载完成的时间。

您可以从应用程序按需下载资产。 请参 [阅下载资产](#download-assets)。

当您使用操作 [!UICONTROL Open] 在本机桌面应用程序中打开资产时，该资产将下载到本地（如果本地尚不可用）。 请参阅 [打开资产](#openondesktop-v2)。

当您从应用程序中显示资产或文件夹的位置时，首先在本地下载资产或文件夹，然后在本地网络共享中在您的计算机上打开。 请参阅 [打开资产](#openondesktop-v2)。

当您使用操作 [!UICONTROL Edit] 在本机桌面应用程序中编辑资产时，如果资产不在本地可用，则将下载到本地。 请参 [阅编辑资产并将更新的资产上传到AEM](#edit-assets-upload-updated-assets)。

如果应用程序已安装并获准，则在您从AEM Web界面使用时，该应用程 [!UICONTROL Desktop Actions] 序将完成操作。 应用程序首先下载资产，然后完成操作。
