---
title: 使用 AEM 桌面应用程序
description: 了解如何安装和使用Adobe Experience manager桌面应用程序，直接从Win或Mac桌面处理AEM资产。 了解最佳实践和疑难解答信息。
uuid: 55057617-89de-43cd-8419-1252a42ab2fb
contentOwner: AG
products: SG_EXPERIENCEMANAGER/6.3/ASSETS
discoiquuid: 39d7bcad-d7b0-4978-a790-4cb68b8a7d6a
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: ad5337c8e1697d0a37d3020d25802dc1d732f320

---


# 使用 AEM 桌面应用程序 {#use-aem-desktop-app-v2}

使用Adobe Experience Manager(AEM)桌面应用程序轻松访问本地桌面上的AEM资产，并在任何桌面应用程序中使用这些资产。 您可以在桌面应用程序中打开资产并在本地编辑资产——使用版本控制将更改上传回AEM，以与其他用户共享更新。 您还可以将新文件和文件夹层次结构上传到AEM，创建文件夹，以及从AEM中删除资产或文件夹。

该集成允许组织中的各种角色在AEM资产中集中管理资产，并在Windows或Mac OS上的本机应用程序中访问本地桌面上的资产。

在注销后或首次打开应用程序时，请提供AEM服务器的URL。 单击“连接”。 提供凭据以将应用程序与服务器连接。

使用AEM桌面应用程序执行的主要任务有：

![可使用AEM桌面应用程序完成的工作流和任](assets/aem_desktop_app_usecases_v2.png "务可使用AEM桌面应用程序完成的工作流和")任 [务下载此可打印](assets/aem_desktop_app_usecases_print.pdf) 的PDF文件。

## 桌面应用程序的工作原理 {#how-app-works2}

在开始使用应用程序之前，请了解 [应用程序的工作方式](release-notes.md#how-app-works)。 此外，请熟悉以下条款：

* **[!UICONTROL Desktop Actions]**:从资产Web界面中，您可以在浏览器中浏览资产位置或注销，然后打开资产以在本机桌面应用程序中进行编辑。 这些操作可从Web界面使用桌面应用程序功能。 了解 [如何启用桌面操作](using.md#desktopactions-v2)。

* 文件状态 **[!UICONTROL Cloud Only]**&#x200B;为：此类资产不会下载到本地计算机上，并且仅在AEM服务器上可用。

* 文件状态 **[!UICONTROL Available locally]**&#x200B;为：资产会按原样下载并在本地计算机上可用。 资产不会更改。

* 文件状态 **[!UICONTROL Edited locally]**&#x200B;为：此类资产将在本地进行修改，并且更改将保留到上传到AEM服务器。 上传后，状态将更改为 [!UICONTROL Available locally]。 请参阅 [编辑资产](using.md#edit-assets-upload-updated-assets)。

* 文件状态 **[!UICONTROL Editing conflict]**&#x200B;为：如果您和其他用户同时修改了资产，则应用程序会指示发生了编辑冲突。 应用程序还提供保留或放弃更改的选项。 了解 [如何避免编辑冲突](using.md#adv-workflow-collaborate-avoid-conflicts)。

* 文件状态 **[!UICONTROL Modified remotely]**&#x200B;为：应用程序将指示您下载的资产是否在AEM服务器上发生更改。 应用程序还提供下载最新版本和更新本地副本的选项。 了解 [如何避免编辑冲突](using.md#adv-workflow-collaborate-avoid-conflicts)。

* **[!UICONTROL Check-out]**:如果您正在编辑文件或打算编辑文件，则可以切换状态以注销。 它会在应用程序和AEM web界面中的资产上添加一个锁图标。 锁定图标会向其他用户指示避免同时编辑同一资产，因为这会导致编辑冲突。

* **[!UICONTROL Check-in]**:将资产标记为安全，以便其他用户进行编辑而不会引起编辑冲突。 上传更改时，锁图标会自动删除。 切换登记状态也会删除锁定图标，但建议不要在不上传更改的情况下手动登记。 如果放弃更改，请手动切换登记。

* **[!UICONTROL Open]** 操作：只需打开资产，即可在本机应用程序中预览它。 不建议使用此操作来编辑资产，因为它不会签出资产，并且其他用户可能会进行编辑而导致编辑冲突。

* **[!UICONTROL Edit]** 操作：使用动作修改图像。 单击 [!UICONTROL Edit] 操作会自动签出资产，并在资产上添加一个锁图标。 单击编辑后，如果您不想编辑资产，请单击 [!UICONTROL Toggle check-in]。 要删除、重命名或移动AEM DAM文件夹层次结构中的资产，请使用AEM web界面操作，而不要使用编辑操作。

* **[!UICONTROL Download]** 操作：将资产下载到本地计算机。 您可以立即下载资产并稍后进行编辑；脱机工作，稍后上传更改。 资产会下载到文件系统上的缓存文件夹中。

* **[!UICONTROL Reveal File]** 或操 **[!UICONTROL Reveal Folder]** 作：当资产下载到本地缓存文件夹时，应用程序将模拟本地网络驱动器并为每个资产提供本地路径。 要了解此路径，请在应用程序中使用相应的显示选项。 在Creative cloud应用程序中放置资源时，需要显示操作。 请参阅 [放置资产](using.md#place-assets-in-native-documents)。

* **[!UICONTROL Open In Web]** 操作：要在AEM web界面中查看资产，请在Web中打开它。 您可以从AEM界面启动更多工作流，如更新元数据或资产发现。

* **[!UICONTROL Delete]** 操作：从AEM DAM存储库中删除资产。 此操作将删除AEM服务器上资产的原始副本。 如果只想放弃对本地资产的修改，请参阅放 [弃更改](using.md#edit-assets-upload-updated-assets)。

* **[!UICONTROL Upload Changes]**:桌面应用程序仅在您显式上传到AEM服务器时才会上传更新的资产。 保存编辑后，更改将仅保存在本地计算机上。 上传时，资产会自动登记并删除锁定图标。 请参阅 [编辑资产](using.md#edit-assets-upload-updated-assets)。

## 在AEM web界面中启用桌面操作 {#desktopactions-v2}

从浏览器的“资产”用户界面中，您可以浏览资产位置或注销并打开资产，以便在桌面应用程序中进行编辑。 这些选项被调 [!UICONTROL Desktop Actions] 用，默认情况下不启用。 要启用它，请按照以下步骤操作。

1. 在“资产”控制台中，单击／点按工 **[!UICONTROL User]** 具栏中的图标。
1. 单击／点按 **[!UICONTROL My Preferences]** 以显示对 **[!UICONTROL Preferences]** 话框。
1. 在“用户首选项”对话框中，选择 **[!UICONTROL Show Desktop Actions For Assets]**。 单击／点按 **[!UICONTROL Accept]**。

   ![选中显示资产的桌面操作以启用桌面操作](assets/chlimage_1-3.png)

   选中 [!UICONTROL Show Desktop Actions For Assets] 以启用桌面操作

## 浏览、搜索和预览资产 {#browse-search-preview-assets}

您可以从桌面应用程序中浏览到、搜索和预览AEM存储库中的可用资产。 在应用程序中尝试以下操作：

1. 浏览到某个文件夹，查看该文件夹中可用资产的一些基本信息以及所有资产的小缩略图。

   ![浏览DAM文件和文件夹浏](assets/browse_folder_da2.png "览DAM文件和文件夹")

1. 要查看详细信息以及单个资产的较大缩略图，请单击文件名。

   ![查看资产和操作的更大预览](assets/large_preview_actions_da2.png "查看资产和操作的更大预览")

1. 单击 **[!UICONTROL Open]** 或以 **[!UICONTROL Edit]** 在本地下载文件，只需查看该文件或在本机应用程序中编辑它即可。
1. 使用关键字搜索以在AEM存储库中查找相关资产。 使用 `?` 和 `*` 作为通配符。 这些通配符分别替换单个字符或多个字符。 根据需要过滤结果并排序。

   ![使用星号通配符的示例搜](assets/search_wildcard_da2.png "索使用星号通配符的示例搜索")

   ![使用星号通配符的另一个示例](assets/search_wildcard2_da2.png "搜索使用星号通配符的不同位置的另一个示例搜索")

>[!NOTE]
>
>该应用程序通过在多个元数据字段中匹配搜索条件来显示资产，而不仅仅是资产的标题或文件名。

## 下载资产 {#download-assets}

您可以将资源下载到本地文件系统。 应用程序从AEM服务器获取资产，并将同一副本保存到您的本地文件系统中。

单击“ ![更多选项”图标](assets/do-not-localize/more2_da2.png) ，获取选项，然后单 ![击“下载”图标](assets/do-not-localize/download_cloud_da2.png) 以下载。

![资产的下载选项](assets/download_option_da2.png "资产的下载选项")

>[!NOTE]
>
>下载或上传大型文件或多个文件时，应用程序会关闭对资产和文件夹的操作。 下载或上传完成后，这些操作将可用。

如果队列大或您遇到某些网络问题，下载多个资源可能会导致性能降低。 此外，在下载文件夹时，您可能会在不知不觉中将许多资产排队下载。 为避免等待时间过长，应用程序会限制一次下载的资产数量。 要了解如何配置它，请参阅设 [置首选项](install-upgrade.md#set-preferences)。 即使低于此限制，应用程序有时也可能在下载明显较大的文件夹之前寻求确认。

![应用程序确认下载相对大量的资](assets/download_confirmation_da2.png "产应用程序确认下载相对大量的资产")

如果选择并下载了文件夹，则应用程序仅下载直接存储在AEM中文件夹中的资产。 它不会自动从子文件夹下载资产。

## 在桌面上打开资源 {#openondesktop-v2}

您可以打开远程资源，以便在本机应用程序中查看。 资产将下载到本地文件夹，并在与文件格式关联的本机应用程序中启动。 您可以更改本机应用程序以在Mac或Windows中打开特定文件类型（扩展）。

从资 **[!UICONTROL Open]** 产菜单中单击。 资产将下载到本地，并在本机应用程序中打开。 在状态栏中检查大型资产的下载进度和传输速度。
<!-- ![Download progress bar for large-sized assets](assets/download_status_bar_da2.png "Download progress bar for large-sized assets")

-->

>[!NOTE]
>
>如果应用程序中未反映预期的更改，请单击刷新图标刷新图 ![标](assets/do-not-localize/refresh.png) ，或右键单击应用程序界面并单击 **[!UICONTROL Refresh]**。 当进行较大的下载或上传时，这些操作不可用。

要打开资产的本地下载文件夹，请单击“更多操 ![作”图标](assets/do-not-localize/more2_da2.png) ，然后单击“ ![显示”图标](assets/do-not-localize/reveal_action2_da2.png)**[!UICONTROL Reveal File]** 操作。

## 使用资源或将其置入本机文档 {#place-assets-in-native-documents}

在某些情况下，例如，将资产置入本机文档时，您可以在Windows资源管理器或Mac finder中访问文件。 要获取本地下载文件的文件系统位置，请使用“显示” ![图标](assets/do-not-localize/reveal_action2_da2.png)**[!UICONTROL Reveal File]** 选项。

![显示资产的文件操作](assets/revealfile_action_da2.png "显示资产的文件操作")

单击 **[!UICONTROL Reveal File]**&#x200B;或在文 **[!UICONTROL Reveal Folder]** 件夹上，打开Windows资源管理器或Mac Finder，并在本地计算机上预先选择文件或文件夹。 此选项对于（例如）将AEM文件放入支持放置或链接本地文件的本机应用程序非常有用。 要了解如何在Adobe inDesign中放置文件，请参阅 [置入图形](https://helpx.adobe.com/indesign/using/placing-graphics.html)。

该操 **[!UICONTROL Reveal File]** 作会打开一个本地网络共享，该共享仅显示本地可用的资产——即显示使用应用程序显示、下载或打开／编辑的资产。 本地网络共享不会将任何更改上传到AEM。 要上传更改，请在应用程序 **[!UICONTROL Upload Changes]** 中显 **[!UICONTROL Upload]** 式使用或操作。

>[!NOTE]
>
>为了向后兼容AEM桌面应用程序v1.x，显示的文件通过本地网络共享提供，仅公开本地可用的文件。 显示文件的桌面路径与应用程序v1.x创建的路径相同。

>[!CAUTION]
>
>请勿使用选 **[!UICONTROL Reveal File]** 项在本机应用程序中编辑资源。 请改用操 **[!UICONTROL Edit]** 作。 要了解更多信息，请参阅 [高级工作流：协作处理同一文件，避免编辑冲突](#adv-workflow-collaborate-avoid-conflicts)。

## 编辑资产并将更新的资产上传到AEM {#edit-assets-upload-updated-assets}

在您要进行更改时打开资产进行编辑，并将更新的资产上传到AEM服务器。 要避免与其他用户的编辑冲突，请使用应用程序启动编辑会话。 在开始编辑之前，请确保资产上没有锁定图标，即其他用户没有编辑资产。

要编辑资产，请搜索资产或浏览至资产所在的位置。 单击“ ![更多”图标](assets/do-not-localize/more2_da2.png) ，然后单击 **[!UICONTROL Edit]**。

在以 **[!UICONTROL Toggle Check-out]** 下两种情况下，使用锁定资产以防止与其他用户的编辑发生冲突：

* 您已开始编辑资产，而无需先注销（例如，只打开它）。
* 您打算很快开始编辑资产，但不希望其他人编辑。

完成编辑后，应用程序将显示已更 **[!UICONTROL Edited Locally]** 改资产的状态。 在将更改上传到AEM之前，保存到资产的所有更改都是仅本地更改。 要逐个上传个人或几个资产，请从资产 **[!UICONTROL Upload Changes]** 的选项中单击。 它会在AEM中创建资产的一个版本。 使用AEM资产的Web界面，您可以在时间轴视图中查看资产 [历史记录](https://helpx.adobe.com/experience-manager/6-5/assets/using/activity-stream.html)。

![应用程序中的“上传更改”选](assets/upload_changes_single1_da2.png "项中的“上传更改”选项")

![查看资产的大预览时上传更改选项查看资产的](assets/upload_changes_single2_da2.png "大预览时上传更改选项")

有关协作编辑的最佳实践，请参阅高 [级工作流：协作处理同一文件，避免编辑冲突](#adv-workflow-collaborate-avoid-conflicts)。

在以下情况下，您可能希望放弃对本地资产所做的更改和编辑。 Click **[!UICONTROL Discard Changes]**.

* 如果您不想在AEM中保存本地更改。
* 在保存某些更改后，开始对原始资产进行更改。
* 停止编辑资产，因为不再需要它。

如有必要，可切换注销。 更新的资产将从本地缓存文件夹中删除，并在您编辑或打开时再次下载。

## 将新资产上传并添加到AEM {#upload-and-add-new-assets-to-aem}

用户可以将新资产添加到DAM存储库。 例如，您可能是要将大量照片从照片拍摄添加到AEM存储库的代理摄影师或承包商。 要向AEM添加新内容，请单 ![击应用程序顶栏中的](assets/do-not-localize/upload_to_cloud_da2.png) “上传到云”图标。 浏览到本地文件系统中的资产文件，然后单击 **[!UICONTROL Select]**。 如果资产上传时间较长，则应用程序会开始上传资产并在底部显示进度栏。 创建或上传文件夹时，请勿使用空格和无效字符。 请参阅在AEM资产中创建 [文件夹中的字符列表](https://helpx.adobe.com/experience-manager/6-5/assets/using/managing-assets-touch-ui.html#Creatingfolders)。

<!-- ![Download progress bar for large-sized assets](assets/upload_status_da2.png "Download progress bar for large-sized assets")
-->

您可以从本地文件系统上载文件夹或单个文件。 上传文件夹时，会保留该文件夹的层次结构。 在批量上传资产之前，请参阅 [批量上传](#bulk-upload-assets)。

要查看在给定会话中传输的资产列表，请单击 **[!UICONTROL View]** &gt; **[!UICONTROL Assets transfers]**。 该列表允许您查看并快速验证当前会话的文件传输。

![特定会话中的已转让资产列表特](assets/assets_transfered_da2.png "定会话中已转让资产的列表")

>[!NOTE]
>
>传输列表不是永久的，如果您退出应用程序并重新打开它，则该列表不可用。

>[!NOTE]
>
>如果文件上传失败，并且您要连接到AEM 6.5.1或更高版本的部署，请参阅此疑难解 [答信息](troubleshoot.md#upload-fails)。

## 使用多个资产 {#work-with-multiple-assets}

用户可以使用一次上传所有编辑或单击几下即可上传嵌套文件夹等操作轻松处理和管理多个资产。

### 浏览大型文件夹 {#browse-large-folders}

使用包含许多资产的文件夹时，滚动可查看更多资产。 要使用键盘滚动，请按Tab键几次以选择顶部的资产。 请注意高亮显示的资产，以了解其何时被选中。 现在，使用向下箭头键在资产列表中移动。

### 对选定资产执行快速操作 {#quick-actions-for-selected-assets}

单击几个资产的缩略图以选择资产。 要选择所有资产，请单击应用程序顶栏中的复选框。 适用于所有选定资产的一组操作将一起显示在应用程序底部的工具栏中。

![底部的工具栏显示与选定资产相关的操](assets/actions_bottom_toolbar1_da2.png "作底部的工具栏显示选定资产的常见操作")

![没有选定内容的常用操作时工具栏中没有任](assets/actions_bottom_toolbar2_da2.png "何操作没有选定内容的常用操作时工具栏中没有任何操作")

底部的工具栏中的可用操作取决于所选文件的状态。 例如，如果仅选择文 **[!UICONTROL Edited Locally]** 件，您会看到图 **[!UICONTROL Upload Changes]** 标。 如果您选择了和的 **[!UICONTROL Edited locally]** 组合 **[!UICONTROL Cloud only]**，则 **[!UICONTROL Upload Changes]** 该操作不可用。

### 查找所有已编辑的图像 {#find-all-edited-images}

应用程序提供一个名为的视 **[!UICONTROL Edited locally]**&#x200B;图，让您能够快速访问您本地下载（通过或操作）并进行修 [!UICONTROL Open] 改的 [!UICONTROL Edit] 所有文件。 该应用程序允许您选择所有本地编辑的资产，并单击几下即可上传更改。 此视图还显示存在编辑冲突的本地编辑的资产。

![筛选以查看所有本地编辑的资](assets/edited_locally_filter_da2.png "产筛选以查看所有本地编辑的资产，例如批量上传编辑")

### 批量上传资产 {#bulk-upload-assets}

用户或组织（如摄影师或创意公司）可以在照片、润饰或从AEM外完成的较大集合中进行选择等场景中创建大量本地资源。 他们可以直接从桌面应用程序将这些大型本地文件夹上传到AEM资产。 将保留文件夹层次结构，并上传所有嵌套的子文件夹和包含的资产。 上传的资产也会立即可供同一服务器的其他用户使用。 资产在后台上传，因此操作不会绑定到Web浏览器会话。

![将多个本地文件夹从桌面批量上传到](assets/upload_local_folders_da2.png "AEM将多个本地文件夹从桌面上传到AEM")

上传后，如果应用程序中未反映预期的更改，请单击刷新图标刷 ![新图标](assets/do-not-localize/refresh.png)。

>[!NOTE]
>
>请勿使用上传功能跨两个AEM部署迁移资产。 相反，请参阅迁 [移指南](https://helpx.adobe.com/experience-manager/6-5/assets/using/assets-migration-guide.html)。

### 已转让资产列表 {#list-of-transferred-assets}

要查看在给定会话中传输的资产列表，请参阅将 [资产上传到AEM](#upload-and-add-new-assets-to-aem)。

## 高级工作流：从AEM Assets web界面开始 {#adv-workflow-start-from-aem-ui}

如有必要，请从AEM Assets web界面启动您的工作流。 桌面应用程序与AEM集成，在使用桌面操作进行请求时接管。

资产发现是从Web界面启动工作流的一个特殊情况。 资产用户界面中的Omnisearch栏提供丰富的高级搜索体验。 您可能希望首先在Web上找到所需的资产，然后使用在应用程序中启动工作流 [!UICONTROL Desktop Actions]。 某些示例包括使用facet筛选搜索结果、查找从Adobe Stock授权的特定资产，或您的组织实现的允许您从Web界面更好地发现的自定义。

当您尝试在资产Web界面上执行以下操作时，将使用桌面应用程序功能：

* 允 [!UICONTROL Desktop Actions] 许、 [!UICONTROL Open]和 [!UICONTROL Edit]允许 [!UICONTROL Reveal]
* [!UICONTROL Upload folder]
* [!UICONTROL Check-out] 或 [!UICONTROL check-in]

例如，对于在应用程序中签出的资产，Web界面上的可用操作有 [!UICONTROL Open]、 [!UICONTROL Reveal]和 [!UICONTROL Check-in]。

![AEM web界面中的桌面操作AEM web](assets/assets_web_actions_da2.png "界面中的桌面操作")

>[!NOTE]
>
>浏览器可能会提示您允许启动Adobe Experience Manager Desktop。 要享受从浏览器到应用程序的无中断传输，请选中相应的复选框，始终允许应用程序接管。

使用Web界面时，您找不到以下信息或工作流。 使用桌面应用程序，因为Web界面不跟踪本地更改，并且不知道以下内容：

* 在本地编辑的文件。
* 存在编辑冲突的文件以及解决该冲突的方法。
* 将本地更改上传到AEM。
* 本地可用文件的各种状态。

相反，您可以从桌面应用程序开始使用操作在Web界面中打开资 **[!UICONTROL Open In Web]** 产。

## 高级工作流：协作处理同一文件，避免编辑冲突 {#adv-workflow-collaborate-avoid-conflicts}

在协作环境中，多个用户可能使用同一组资产，这会导致版本控制冲突。 要防止冲突，请遵循以下最佳实践：

* 请勿通过单击来编辑任何资产 [!UICONTROL Open]。 请勿通过从文件系统文件夹打开来编辑本地下载的资源。 其他用户不知道正在编辑资产。
* 要编辑资产，请始终单击 [!UICONTROL Edit]。 它会在本机应用程序中打开资产，并在资产上添加一个锁定图标，以便其他用户知道正在编辑该资产。
* 如果 [!UICONTROL Toggle Check-in] 您意外开始编辑时未单击，请单击 [!UICONTROL Edit]。 这会向资产添加一个锁图标。 即使您计划稍后编辑资产，但是希望避免他人编辑资产，单击可 [!UICONTROL Toggle Check-in] 锁定资产。
* 在编辑资产之前，请确保其他用户未编辑该资产。 在资产上查找锁定图标。
* 完成编辑后，上传所有更改，然后登记资产。

![编辑冲突的状态](assets/edits_conflicts_status_da2.png "编辑冲突的状态")

如果更新了AEM服务器上本地下载的资产，则应用程序会显示状 **[!UICONTROL Modified remotely]** 态。 您可以分别单击或刷新本地副本，从而删除本 [!UICONTROL Remove] 地副 [!UICONTROL Update] 本。 对话框上的链接允许您查看资产的两个版本。

![用于解决资产远程修改时冲突的选项用于解](assets/modified_remotely_dialog_da2.png "决资产远程修改时冲突的选项")

如果您正在本地编辑的资产也会在服务器上更新，而您不知情，则应用程序会显示状 **[!UICONTROL Editing Conflict]** 态。 您可以保留一组更改——保留您的更新(单击 **[!UICONTROL Keep Mine]**)并删除其他用户的编辑，或保留其他用户的更新并删除您的更新(**[!UICONTROL Overwrite Mine]**)。

![解决编辑冲突的选](assets/editing_conflict_dialog_da2.png "项解决编辑冲突的选项")

## 高级工作流：在InDesign文件中放置和链接资源 {#adv-workflow-place-assets-indesign}

当您使用AEM桌面应用程序打开包含链接资产的文件时，会预先下载资产并显示在本机应用程序中。 要使此工作流正常工作，您的本机应用程序必须支持放置指向本地资产的链接，并且AEM必须支持在指向服务器端引用的二进制文件中解析这些链接。

AEM桌面应用程序支持此工作流程，只需选择几种Adobe Creative cloud桌面应用程序和文件格式- Adobe inDesign、Adobe Illustrator和Adobe Photoshop。 该工作流程允许您高效地处理受支持的Creative cloud文件。 因此，如果用户A将一些资源放入InDesign文件中并将其签入AEM，则用户B将在InDesign文件中看到这些资源，即使这些资源不是文件的一部分。 资源将本地下载到用户B的机器上。

>[!NOTE]
>
>桌面应用程序可映射到Windows上的任何驱动器。 但是，对于平滑操作，不要更改默认驱动器盘符。 如果同一组织的用户使用不同的驱动器号，则他们看不到其他人放置的资产。 随着路径的更改，不会获取已放置的资产。 放置的资源将继续保留在二进制文件（如INDD）中，并且不会删除。

要了解此工作流程的限制，请参阅系 [统要求和支持的版本](release-notes.md#system-requirements-and-prerequisites-v2)。

要使用图像资源和InDesign尝试此工作流程，请执行以下步骤：

1. 在AEM中保持INDD文件的便利性。 要了解如何创建此类INDD文件，请参阅 [置入图形](https://helpx.adobe.com/indesign/using/placing-graphics.html)。
1. 从桌面应用程序中， **[!UICONTROL Edit]** AEM中包含已置入资产的INDD文件。
1. 应用程序会下载InDesign文件和链接的资源。 当InDesign打开文档时，将解析链接，下载资源，并在InDesign文档中显示资源。
1. 要将新图形放入InDesign文件中，请对资 **[!UICONTROL Reveal File]** 产使用操作。 该操作将本地下载资产，并在Windows资源管理器或Mac finder中打开本地网络共享位置。
1. 将显示的资源放在InDesign文档中。 这会在文档中创建链接。
1. 在InDesign文档中完成编辑后，请保存该文档，然后使用桌面应用程序将其上传到AEM。

## 高级工作流：本地下载资源 {#adv-workflow-download-assets-locally}

在许多情况下，应用程序会从文件系统上的本地AEM服务器下载资产。 下载会消耗带宽和磁盘空间。 了解这些方案有助于优化下载的等待时间。

您可以从应用程序内按需下载资产。 请参阅 [下载资产](#download-assets)。

当您使用操作在 [!UICONTROL Open] 本机桌面应用程序中打开资产时，如果资产不在本地可用，则会在本地下载该资产。 请参阅 [打开资产](#openondesktop-v2)。

当您从应用程序中显示资产或文件夹的位置时，资产或文件夹首先下载到本地，然后在本地网络共享中在您的计算机上打开。 请参阅 [打开资产](#openondesktop-v2)。

当您使用该操 [!UICONTROL Edit] 作在本机桌面应用程序中编辑资产时，如果该资产尚未在本地可用，则会在本地下载该资产。 请参 [阅编辑资产并将更新的资产上传到AEM](#edit-assets-upload-updated-assets)。

如果已安装并允许应用程序，则在您从AEM web界面使用时，应用程序将 [!UICONTROL Desktop Actions] 完成这些操作。 应用程序首先下载资产，然后完成操作。