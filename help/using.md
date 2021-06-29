---
title: 使用 [!DNL Experience Manager] 桌面应用程序
description: 直接从Win或Mac桌面使用 [!DNL Adobe Experience Manager] desktop app, to work with [!DNL Adobe Experience Manager] DAM资产，并在其他应用程序中使用。
mini-toc-levels: 1
feature: 桌面应用程序，资产管理
exl-id: fa19d819-231a-4a01-bfd2-6bba6fec2f18
source-git-commit: dcd29d0bbb32004d970d334c256e659f4a4c39e1
workflow-type: tm+mt
source-wordcount: '4053'
ht-degree: 0%

---

# 使用[!DNL Adobe Experience Manager]桌面应用程序 {#use-aem-desktop-app-v2}

使用[!DNL Adobe Experience Manager]桌面应用程序，轻松访问本地桌面上[!DNL Adobe Experience Manager] DAM存储库中存储的数字资产，并在任何桌面应用程序中使用这些资产。 您可以在桌面应用程序中打开资产并在本地编辑资产 — 通过版本控制将更改上传回[!DNL Experience Manager]，以与其他用户共享更新。 您还可以将新文件和文件夹层次结构上传到[!DNL Experience Manager]、创建文件夹，以及从[!DNL Experience Manager] DAM中删除资产或文件夹。

该集成允许组织中的各种角色在[!DNL Experience Manager Assets]中集中管理资产，并在Windows或Mac OS的本机应用程序中访问本地桌面上的资产。

在注销后或首次打开应用程序时，请以`https://[aem-server-url]:[port]/`格式提供[!DNL Experience Manager]服务器的URL。 然后选择[!UICONTROL Connect]选项。 提供凭据以将应用程序与服务器连接。

使用[!DNL Experience Manager]桌面应用程序执行的关键任务包括：

![使用桌面应用程序可以完成的工作流和 [!DNL Experience Manager] 任](assets/aem_desktop_app_usecases_v2.png "务使用桌面应用程序可以完成的工作 [!DNL Adobe Experience Manager] 流")
和任务 [](assets/aem_desktop_app_usecases_print.pdf) 下载此可供打印的PDF文件。

## 桌面应用程序的工作原理 {#how-app-works2}

在开始使用应用程序之前，请了解[应用程序的工作方式](release-notes.md#how-app-works)。 此外，请熟悉以下术语：

* **[!UICONTROL Desktop Actions]**:从资产Web界面的浏览器中，您可以浏览资产位置或签出，然后打开资产，以在本机桌面应用程序中进行编辑。这些操作可从Web界面中使用，并使用桌面应用程序功能。 请参阅[如何启用Desktop Actions](using.md#desktopactions-v2)。

* 文件状态为&#x200B;**[!UICONTROL Cloud Only]**:此类资产不会下载到本地计算机，并且只能在[!DNL Experience Manager]服务器上使用。

* 文件状态为&#x200B;**[!UICONTROL Available locally]**:资产将按原样下载并在本地计算机上可用。 资产不会更改。

* 文件状态为&#x200B;**[!UICONTROL Edited locally]**:此类资产将在本地进行修改，并且更改将保留到已上传到[!DNL Experience Manager]服务器。 上传后，状态将变为[!UICONTROL Available locally]。 请参阅[编辑资产](using.md#edit-assets-upload-updated-assets)。

* 文件状态为&#x200B;**[!UICONTROL Editing conflict]**:如果您和其他用户同时修改资产，则应用程序会指示发生编辑冲突。 该应用程序还提供了用于保留或放弃更改的选项。 请参阅[如何避免编辑冲突](using.md#adv-workflow-collaborate-avoid-conflicts)。

* 文件状态为&#x200B;**[!UICONTROL Modified remotely]**:应用程序会指示您下载的资产是否在[!DNL Experience Manager]服务器上发生更改。 该应用程序还提供了用于下载最新版本和更新本地副本的选项。 请参阅[如何避免编辑冲突](using.md#adv-workflow-collaborate-avoid-conflicts)。

* **[!UICONTROL Check-out]**:如果您正在编辑文件或打算编辑文件，则可切换状态以签出。它会在应用程序和[!DNL Experience Manager] Web界面的资产上添加一个锁图标。 锁定图标指示其他用户避免同时编辑同一资产，因为这会导致编辑冲突。

* **[!UICONTROL Check-in]**:将资产标记为安全，以便其他用户在不导致编辑冲突的情况下进行编辑。上传更改时，锁图标会自动删除。 切换签入状态也会删除锁图标，不过建议在不上传更改的情况下不要手动签入。 如果放弃更改，请手动切换签入。

* **[!UICONTROL Open]** 操作：只需打开资产，即可在本机应用程序中预览资产。不建议使用此操作来编辑资产，因为它不会签出资产，并且其他用户可能会进行编辑，从而导致编辑冲突。

* **[!UICONTROL Edit]** 操作：使用操作修改图像。单击[!UICONTROL Edit]操作会自动签出资产，并在资产上添加一个锁图标。 单击编辑后，如果您不想编辑资产，请单击[!UICONTROL Toggle check-in]。 要删除、重命名或移动[!DNL Experience Manager] DAM文件夹层次结构中的资产，请使用[!DNL Experience Manager] Web界面操作，而不是编辑操作。

* **[!UICONTROL Download]** 操作：将资产下载到本地计算机。您可以立即下载资产并稍后进行编辑；脱机工作，稍后上传更改。 资产会下载到文件系统的缓存文件夹中。

* **[!UICONTROL Reveal File]** 或操 **[!UICONTROL Reveal Folder]** 作：在将资产下载到本地缓存文件夹时，应用程序会模拟本地网络驱动器并为每个资产提供本地路径。要了解此路径，请在应用程序中使用相应的显示选项。 在Creative Cloud应用程序中放置资产时，需要显示操作。 请参阅[放置资产](using.md#place-assets-in-native-documents)。

* **[!UICONTROL Open In Web]** 操作：要在Web界面中查 [!DNL Experience Manager] 看资产，请在Web中打开资产。您可以从[!DNL Experience Manager]界面启动更多工作流，如更新元数据或资产发现。

* **[!UICONTROL Delete]** 操作：从DAM存储库中删 [!DNL Experience Manager] 除资产。该操作会删除Experience Manager服务器上资产的原始副本。 如果只想放弃对本地资产的修改，请参阅[放弃更改](using.md#edit-assets-upload-updated-assets)。

* **[!UICONTROL Upload Changes]**:仅当您明确将上传到服务器时，桌面应用程序才会上传更新的 [!DNL Experience Manager] 资产。保存编辑后，更改将仅保存在本地计算机上。 上传时，资产会自动签入并删除锁定图标。 请参阅[编辑资产](using.md#edit-assets-upload-updated-assets)。

## 在[!DNL Experience Manager] Web界面中启用桌面操作 {#desktopactions-v2}

在浏览器的[!DNL Assets]用户界面中，您可以浏览资产位置或签出并打开资产，以在桌面应用程序中进行编辑。 这些选项称为[!UICONTROL Desktop Actions]，默认情况下未启用。 要启用此功能，请执行以下步骤。

1. 在[!DNL Assets]控制台中，单击工具栏中的&#x200B;**[!UICONTROL User]**&#x200B;图标。
1. 单击&#x200B;**[!UICONTROL My Preferences]**&#x200B;以显示&#x200B;**[!UICONTROL Preferences]**&#x200B;对话框。

1. 在[!UICONTROL User Preferences]对话框中，选择&#x200B;**[!UICONTROL Show Desktop Actions For Assets]**，然后单击&#x200B;**[!UICONTROL Accept]**。


   ![选择显示资产的桌面操作以启用桌面操作](assets/enable_desktop_actions.png)

   *图：选择 [!UICONTROL Show Desktop Actions For Assets] 以启用桌面操作。*

## 浏览、搜索和预览资产 {#browse-search-preview-assets}

您可以浏览、搜索和预览[!DNL Experience Manager]存储库中可用的资产，所有这些资产都可以从桌面应用程序中进行。 在应用程序中尝试以下操作：

1. 浏览到文件夹，并查看文件夹中可用资产的一些基本信息，以及所有资产的小缩略图。

   ![浏览DAM文件和文](assets/browse_folder_da2.png "件夹浏览DAM文件和文件夹")

1. 要查看更多信息和单个资产的较大缩略图，请单击文件名。

   ![查看资产和操作的更大预览](assets/large_preview_actions_da2.png "查看资产和操作的更大预览")

1. 单击&#x200B;**[!UICONTROL Open]**&#x200B;或&#x200B;**[!UICONTROL Edit]**&#x200B;以在本地下载文件，只需在本机应用程序中查看或编辑该文件即可。
1. 使用关键字搜索可在[!DNL Experience Manager]存储库中查找相关资产。 使用`?`和`*`作为通配符。 这些通配符分别用于替换单个字符或多个字符。 根据需要筛选和排序结果。

   ![使用星号通配符的示](assets/search_wildcard_da2.png "例搜索使用星号通配符的示例搜索")

   ![使用星号通配符的另一](assets/search_wildcard2_da2.png "个示例搜索使用星号通配符的不同位置的另一个示例搜索")

>[!NOTE]
>
>该应用程序通过在多个元数据字段中匹配搜索条件来显示资产，而不只是通过资产的标题或文件名来显示。

## 下载资产 {#download-assets}

您可以在本地文件系统上下载资产。 应用程序从[!DNL Experience Manager]服务器获取资产，并在本地文件系统上保存相同的副本。

单击![更多选项图标](assets/do-not-localize/more2_da2.png)以获取选项，然后单击![下载图标](assets/do-not-localize/download_cloud_da2.png)下载。

![资产的下载选项](assets/download_option_da2.png "资产的下载选项")

>[!NOTE]
>
>下载或上传一个或多个文件时，应用程序会关闭对资产和文件夹的操作。 下载或上载完成后，即可执行这些操作。

如果队列大小较大或您遇到某些网络问题，下载多个资产可能会导致性能不佳。 此外，在下载文件夹时，您可能会无意中将许多资产排入队列进行下载。 为避免等待时间过长，应用程序会限制一次下载的资产数量。 要了解如何配置它，请参阅[设置首选项](install-upgrade.md#set-preferences)。 即使低于此限制，应用程序有时也可能会在下载明显较大的文件夹之前寻求确认。

![应用程序确认下载相对大量的](assets/download_confirmation_da2.png "资产应用程序确认下载相对大量的资产")

如果选择并下载了文件夹，则应用程序将仅下载直接存储在[!DNL Experience Manager]文件夹中的资产。 它不会自动从子文件夹下载资产。

## 在桌面上打开资产 {#openondesktop-v2}

您可以打开远程资产，以在本机应用程序中查看。 资产会下载到本地文件夹，并在与该文件格式关联的本机应用程序中启动。 您可以更改本机应用程序，以在Mac或Windows中打开特定文件类型（扩展名）。

从资产菜单中单击&#x200B;**[!UICONTROL Open]**。 资产将在本地下载并在本机应用程序中打开。 在状态栏中查看大型资产的下载进度和传输速度。

<!-- ![Download progress bar for large-sized assets](assets/download_status_bar_da2.png "Download progress bar for large-sized assets")
-->

>[!NOTE]
>
>如果应用程序中未反映预期的更改，请单击刷新图标![刷新图标](assets/do-not-localize/refresh.png)，或在应用程序界面中右键单击，然后单击&#x200B;**[!UICONTROL Refresh]**。 当进行较大的下载或上载时，这些操作将不可用。

要打开资产的本地下载文件夹，请单击![更多操作图标](assets/do-not-localize/more2_da2.png)，然后单击![显示图标](assets/do-not-localize/reveal_action2_da2.png) **[!UICONTROL Reveal File]**&#x200B;操作。

## 使用资产或将资产放入本机文档中 {#place-assets-in-native-documents}

在某些情况下，例如，将资产放入本机文档时，您可以在Windows资源管理器或Mac Finder中访问文件。 要转到本地下载文件的文件系统位置，请使用![显示图标](assets/do-not-localize/reveal_action2_da2.png) **[!UICONTROL Reveal File]**&#x200B;选项。

![显示资产的文件操](assets/revealfile_action_da2.png "作显示资产的文件操作")

单击文件夹上的&#x200B;**[!UICONTROL Reveal File]**&#x200B;或&#x200B;**[!UICONTROL Reveal Folder]**，打开Windows资源管理器或Mac查找器，并在本地计算机上预先选择该文件或文件夹。 例如，将[!DNL Experience Manager]文件放置在支持放置或链接本地文件的本机应用程序中时，此选项非常有用。 要了解如何在Adobe InDesign中放置文件，请参阅[放置图形](https://helpx.adobe.com/indesign/using/placing-graphics.html)。

**[!UICONTROL Reveal File]**&#x200B;操作会打开一个本地网络共享，该共享仅显示本地可用的资产，即显示使用应用程序显示、下载或打开/编辑的资产。 本地网络共享不会将任何更改上载到[!DNL Experience Manager]。 要上传更改，请在应用程序中明确使用&#x200B;**[!UICONTROL Upload Changes]**&#x200B;或&#x200B;**[!UICONTROL Upload]**&#x200B;操作。

>[!NOTE]
>
>为了向后兼容[!DNL Experience Manager]桌面应用程序v1.x，显示的文件来自本地网络共享，仅公开本地可用的文件。 显示文件的桌面路径与应用程序v1.x创建的路径相同。

>[!CAUTION]
>
>请勿使用&#x200B;**[!UICONTROL Reveal File]**&#x200B;选项编辑本机应用程序中的资产。 请改用&#x200B;**[!UICONTROL Edit]**&#x200B;操作。 要了解更多信息，请参阅[高级工作流：协作处理相同的文件，避免编辑冲突](#adv-workflow-collaborate-avoid-conflicts)。

## 编辑资产并将更新的资产上传到[!DNL Experience Manager] {#edit-assets-upload-updated-assets}

打开资产以在您要进行更改时进行编辑，并将更新的资产上传到AEM Experience ManagerEM服务器。 为避免与其他用户编辑的冲突，请使用应用程序启动编辑会话。 在开始编辑之前，请确保资产上没有锁图标，也就是说，其他用户没有编辑资产。

要编辑资产，请搜索资产或浏览到资产的位置。 单击![更多图标](assets/do-not-localize/more2_da2.png)并单击&#x200B;**[!UICONTROL Edit]**。

在以下两种情况下，使用&#x200B;**[!UICONTROL Toggle Check-out]**&#x200B;锁定资产，以防止与其他用户编辑的资产冲突：

* 您已开始编辑资产，但未先将其签出（例如，通过打开资产）。
* 您计划尽快开始编辑资产，而不希望其他人进行编辑。

完成编辑后，应用程序会显示已更改资产的&#x200B;**[!UICONTROL Edited Locally]**&#x200B;状态。 保存到资产的所有更改都仅在本地，直到您将更改上传到[!DNL Experience Manager]为止。 要逐个上传单个或多个资产，请单击资产选项中的&#x200B;**[!UICONTROL Upload Changes]**。 它会在[!DNL Experience Manager]中创建资产的版本。 使用[!DNL Assets]的Web界面，您可以在[时间轴视图](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/activity-stream.html)中查看资产历史记录。

![应用程序中appUpload更改选](assets/upload_changes_single1_da2.png "项中的“上传更改”选项")

![查看资产的大型预览时上传更改选](assets/upload_changes_single2_da2.png "项查看资产的大型预览时上传更改选项")

有关协作编辑的最佳实践，请参阅[高级工作流：协作处理相同的文件，避免编辑冲突](#adv-workflow-collaborate-avoid-conflicts)。

在以下情况下，您可能希望放弃对本地资产所做的更改和编辑。 单击 **[!UICONTROL Discard Changes]**.

* 如果您不想在[!DNL Experience Manager]中保存本地更改。
* 保存某些更改后，开始对原始资产进行更改。
* 由于不再需要资产，请停止编辑该资产。

如有必要，请切换签出。 更新的资产将从本地缓存文件夹中删除，并在您编辑或打开时再次下载。

## 将新资产上传并添加到[!DNL Experience Manager] {#upload-and-add-new-assets-to-aem}

用户可以将新资产添加到DAM存储库。 例如，您可能是代理摄影师或承包商，希望将照片拍摄中的大量照片添加到[!DNL Experience Manager]存储库。 要向[!DNL Experience Manager]添加新内容，请选择应用程序顶栏中的![上传到云选项](assets/do-not-localize/upload_to_cloud_da2.png)。 浏览到本地文件系统中的资产文件，然后单击&#x200B;**[!UICONTROL Select]**。 或者，要上传资产，请将文件或文件夹拖动到应用程序界面上。 在Windows上，如果您将资产拖动到应用程序内的文件夹中，则资产会上传到该文件夹中。 如果上传时间较长，应用程序会显示一个进度栏。

<!-- ![Download progress bar for large-sized assets](assets/upload_status_da2.png "Download progress bar for large-sized assets")
-->

您可以从本地文件系统上载文件夹或单个文件。 上传文件夹后，文件夹的层次结构会保留下来。 在批量上传资产之前，请参阅[批量上传](#bulk-upload-assets)。

要查看在给定会话中转移的资产列表，请单击&#x200B;**[!UICONTROL View]** > **[!UICONTROL Assets transfers]**。 利用列表，可查看并快速验证当前会话的文件传输。

![特定会话中已转移资产列](assets/assets_transfered_da2.png "表特定会话中已转移资产列表")

您可以在&#x200B;**[!UICONTROL Preferences]** > **[!UICONTROL Upload acceleration]**&#x200B;设置中控制上传并发（加速）。 更多并发通常提供更快的上传速度，但可能会占用大量资源，消耗本地计算机的更大处理能力。 如果您遇到系统运行缓慢的情况，请使用较低的并发值重新尝试上传。

>[!NOTE]
>
>传输列表不是永久性的，如果您退出应用程序并将其重新打开，则该列表将不可用。

### 管理资产名称中的特殊字符 {#special-characters-in-filename}

在旧版应用程序中，在存储库中创建的节点名称会保留用户提供的文件夹名称的空格和大小写。 要使当前应用程序模拟v1.10应用程序的节点命名规则，请在[!UICONTROL Preferences]中启用[!UICONTROL Use legacy conventions when creating nodes for assets and folders]。 请参阅[应用程序首选项](/help/install-upgrade.md#set-preferences)。 默认情况下，此旧版首选项处于禁用状态。

>[!NOTE]
>
>应用程序仅使用以下命名约定更改存储库中的节点名称。 应用程序会原样保留资产的`Title`。

<!-- TBD: Do NOT use this table.

| Where do characters occur | Characters | Legacy preference | Renaming convention | Example |
|---|---|---|---|---|
| In file name extension | `.` | Enabled or disabled | Retained as is | NA |
| File or folder name | `. / : [ ] | *` | Enabled or disabled | Replaced with a `-` (hyphen) | `myimage.jpg` remains as is and `my.image.jpg` changes to `my-image.jpg`. |
| Folder name | `% ; # , + ? ^ { } "` | Disabled | Replaced with a `-` (hyphen) | tbd |
| File name | `% # ? { } &` | Disabled | Replaced with a `-` (hyphen) | tbd |
| File name | Whitespaces | Enabled or disabled | Retained as is | NA |
| Folder name | Whitespaces | Disabled | Replaced with a `-` (hyphen) | tbd |
| File name | Uppercase characters | Disabled | Retained as is | tbd |
| Folder name | Uppercase characters | Disabled | Replaced with a `-` (hyphen) | tbd |
-->

| 字符数 ‡ | 应用程序中的旧版首选项 | 在文件名中出现时 | 在文件夹名称中出现时 | 示例 |
|---|---|---|---|---|
| `. / : [ ] | *` | 启用或禁用 | 替换为`-`（连字符）。 文件扩展名中的`.`（圆点）将保持原样。 | 替换为`-`（连字符）。 | `myimage.jpg` 保持不变，并 `my.image.jpg` 更改 `my-image.jpg`为。 |
| `% ; # , + ? ^ { } "` 和空格 | ![取消选择](assets/do-not-localize/deselect-icon.png) iconDisabled | 保留空格 | 替换为`-`（连字符）。 | `My Folder.` 更改为 `my-folder-`。 |
| `# % { } ? & .` | ![取消选择](assets/do-not-localize/deselect-icon.png) iconDisabled | 替换为`-`（连字符）。 | NA. | `#My New File.` 更改为 `-My New File-`。 |
| 大写字母 | ![取消选择](assets/do-not-localize/deselect-icon.png) iconDisabled | 外壳保持原样。 | 已更改为小写字符。 | `My New Folder` 更改为 `my-new-folder`。 |
| 大写字母 | ![selection checked ](assets/do-not-localize/selection-checked-icon.png) iconEnabled | 外壳保持原样。 | 外壳保持原样。 | 不。 |

字符列表以空格分隔。

<!-- TBD: Check if the following is to be included in the footnote.

Do not use &#92;&#92; in the names of files and &#92;&#116; &#38; in the names of folders. 
-->


<!-- TBD: Securing the below presentation of the same content in a comment.

**File names**

| Characters | Replaced by |
|---|---|
| &#35; &#37; &#123; &#63; &#125; &#38; &#46; &#47; &#58; &#91; &#124; &#93; &#42; | hyphen (-) |
| whitespaces | whitespaces are retained |
| capital case | casing is retained |

>[!CAUTION]
>
>Avoid using &#92;&#92; in file names.

**Folder names**

| Characters | Replaced by |
|---|---|
| Characters | Replaced by |
| &#37; &#59; &#35; &#44; &#43; &#63; &#94; &#123; &#123; &#34; &#46; &#47; &#59; &#91; &#93; &#124; &#42; | hyphen (-) |
| whitespaces | hyphen (-) |
| capital case | lower case |

>[!CAUTION]
>
>Avoid using &#92;&#92; &#92;&#116; &#38; in folder names.

>[!NOTE]
>
>If you enable [!UICONTROL Use legacy conventions when creating nodes for assets and folders] in app [!UICONTROL Preferences], then the app emulates v1.10 app behavior when uploading folders. In v1.10, the node names created in the repository respect spaces and casing of the folder names provided by the user. For more information, see [app Preferences](/help/install-upgrade.md#set-preferences).

-->

## 使用多个资产 {#work-with-multiple-assets}

用户可以使用一次性上传所有编辑或单击几次后上传嵌套文件夹等操作，轻松处理和管理多个资产。

### 浏览大型文件夹 {#browse-large-folders}

使用包含多个资产的文件夹时，滚动以查看更多资产。 要使用键盘滚动，请按Tab键几次以选择顶部的资产。 请注意突出显示的资产，以了解其选择的时间。 现在，使用向下箭头键在资产列表中移动。

### 对选定资产执行快速操作 {#quick-actions-for-selected-assets}

单击几个资产的缩略图以选择资产。 要选择所有资产，请单击应用程序顶部栏中的复选框。 应用程序底部的工具栏中会显示一组操作，这些操作集体适用于所有选定的资产。

![底部的工具栏显示与选定资产相关的操](assets/actions_bottom_toolbar1_da2.png "作底部的工具栏显示选定资产的常见操作")

![没有选定内容的常见操作时工具栏中没有](assets/actions_bottom_toolbar2_da2.png "操作没有选定内容的常用操作时工具栏中没有操作")

底部工具栏中可用的操作取决于选定文件的状态。 例如，如果仅选择&#x200B;**[!UICONTROL Edited Locally]**&#x200B;文件，则会看到&#x200B;**[!UICONTROL Upload Changes]**&#x200B;图标。 如果选择&#x200B;**[!UICONTROL Edited locally]**&#x200B;和&#x200B;**[!UICONTROL Cloud only]**&#x200B;的组合，则&#x200B;**[!UICONTROL Upload Changes]**&#x200B;操作不可用。

### 查找所有编辑的图像 {#find-all-edited-images}

该应用程序提供了一个名为&#x200B;**[!UICONTROL Edited locally]**&#x200B;的视图，用于快速访问您在本地下载（通过[!UICONTROL Open]或[!UICONTROL Edit]操作）并修改的所有文件。 该应用程序允许您选择所有本地编辑的资产，并在单击几下后上传更改。 此视图还显示本地编辑的具有编辑冲突的资产。

![过滤以查看所有本地编辑的资](assets/edited_locally_filter_da2.png "产过滤器查看所有本地编辑的资产，例如批量上传编辑的资产")

### 批量上传资产 {#bulk-upload-assets}

用户或组织（如摄影师或创意机构）可以在场景中创建大量本地资产，如照片、润饰或从[!DNL Experience Manager]以外完成的较大集合中进行选择。 他们可以直接从桌面应用程序将这些大型本地文件夹上传到[!DNL Assets]。 文件夹层次结构将保留，并上传所有嵌套的子文件夹和包含的资产。 上传的资产也可立即供同一服务器的其他用户使用。 资产在后台上传，因此该操作不会绑定到Web浏览器会话。

![将多个本地文件夹从桌面批量上传到 [!DNL Experience Manager]](assets/upload_local_folders_da2.png "将多个本地文件夹从桌面批量上传到Experience Manager")

上传后，如果应用程序中未反映预期的更改，请单击刷新图标![刷新图标](assets/do-not-localize/refresh.png)。

>[!NOTE]
>
>请勿使用上传功能跨两个[!DNL Experience Manager]部署迁移资产。 请改为参阅[迁移指南](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/assets-migration-guide.html)。

### 已转让资产列表 {#list-of-transferred-assets}

要查看在给定会话中转移的资产列表，请参阅[将资产上传到 [!DNL Experience Manager]](#upload-and-add-new-assets-to-aem)。

## 高级工作流：从[!DNL Assets] web界面开始 {#adv-workflow-start-from-aem-ui}

如有必要，请从Assets Web界面启动您的工作流。 该桌面应用程序与[!DNL Experience Manager]集成，以在使用桌面操作请求时接管。

从Web界面启动工作流的一个特殊案例是资产发现。 资产用户界面中的Omnisearch栏提供了丰富而高级的搜索体验。 您可能需要先在Web上找到所需的资产，然后使用[!UICONTROL Desktop Actions]在应用程序中启动工作流。 某些示例案例包括使用Facet筛选搜索结果、查找从Adobe Stock授权的特定资产，或者由您的组织实施的自定义设置，该设置允许您从Web界面更好地发现。

当您尝试在Assets Web界面上执行以下操作时，将使用桌面应用程序功能：

* 允许[!UICONTROL Open]、[!UICONTROL Edit]和[!UICONTROL Reveal]的[!UICONTROL Desktop Actions]
* [!UICONTROL Upload folder]
* [!UICONTROL Check-out] 或 [!UICONTROL check-in]

例如，Web界面上可用于在应用程序中签出的资产的操作包括[!UICONTROL Open]、[!UICONTROL Reveal]和[!UICONTROL Check-in]。

![Web界面中的桌面操 [!DNL Experience Manager] 作](assets/assets_web_actions_da2.png "Experience ManagerWeb界面中的桌面操作")

>[!NOTE]
>
>浏览器可能会提示您允许启动[!DNL Adobe Experience Manager]桌面。 要不间断地从浏览器传输到应用程序，请选中相应的复选框，以始终允许应用程序接管。

您无法使用Web界面找到以下信息或工作流。 使用桌面应用程序，因为Web界面不会跟踪本地更改，并且不知道以下内容：

* 本地编辑的文件。
* 存在编辑冲突的文件以及解决该冲突的方法。
* 将本地更改上载到[!DNL Experience Manager]。
* 本地可用文件的各种状态。

相反，您可以从桌面应用程序开始，通过&#x200B;**[!UICONTROL Open In Web]**&#x200B;操作，在Web界面中打开资产。

## 高级工作流：在同一文件上协作，避免编辑冲突 {#adv-workflow-collaborate-avoid-conflicts}

在协作环境中，多个用户可能会处理同一组资产，这可能会导致版本控制冲突。 要防止冲突，请遵循以下最佳实践：

* 请勿通过单击[!UICONTROL Open]来编辑任何资产。 请勿通过从文件系统文件夹中打开来编辑本地下载的资产。 其他用户不知道正在编辑资产。
* 要编辑资产，请始终单击[!UICONTROL Edit]。 它会在本机应用程序中打开资产，并在资产上添加一个锁图标，以便其他用户知道正在编辑资产。
* 如果意外开始编辑而未单击[!UICONTROL Edit]，请单击[!UICONTROL Toggle Check-in]。 这会向资产添加一个锁图标。 即使您计划稍后编辑资产，但是希望避免其他人编辑资产，单击[!UICONTROL Toggle Check-in]可锁定资产。
* 在编辑资产之前，请确保其他用户未对其进行编辑。 在资产上查找锁图标。
* 完成编辑后，上传所有更改，然后签入资产。

![编辑冲突的](assets/edits_conflicts_status_da2.png "状态编辑冲突的状态")

如果在[!DNL Experience Manager]服务器上更新了本地下载的资产，则应用程序会显示&#x200B;**[!UICONTROL Modified remotely]**&#x200B;状态。 您可以分别单击[!UICONTROL Remove]或[!UICONTROL Update]，以删除本地副本或刷新本地副本。 利用对话框中的链接，可查看资产的两个版本。

![用于解决资产远程修改时冲突的选项用于](assets/modified_remotely_dialog_da2.png "解决资产远程修改时冲突的选项")

如果您在本地编辑的资产也会在服务器上更新，且您不知情，则应用程序会显示&#x200B;**[!UICONTROL Editing Conflict]**&#x200B;状态。 您可以保留一组更改 — 保留您的更新（单击&#x200B;**[!UICONTROL Keep Mine]**）并删除其他用户的编辑或尊重其他用户的更新并删除您的更新(**[!UICONTROL Overwrite Mine]**)。

![用于解决编辑冲突的选](assets/editing_conflict_dialog_da2.png "项用于解决编辑冲突的选项")

## 高级工作流：在InDesign文件中放置和链接资产 {#adv-workflow-place-assets-indesign}

当您使用[!DNL Experience Manager]桌面应用程序打开包含链接资产的文件时，系统会预先下载资产，并将其放置在本机应用程序中。 要使此工作流正常工作，您的本机应用程序必须支持将链接放置到本地资产，并且[!DNL Experience Manager]必须支持在二进制文件中解析这些链接以指向服务器端引用。

[!DNL Experience Manager] 桌面应用程序通过几种精选的Adobe Creative Cloud桌面应用程序和文件格式(Adobe InDesign、Adobe Illustrator和Adobe Photoshop)支持此工作流。利用工作流，可高效处理支持的Creative Cloud文件。 因此，如果用户A在InDesign文件中放置一些资产并将其签入[!DNL Experience Manager]，则用户B将看到InDesign文件中的资产，即使这些资产不在文件中。 资产将在用户B的计算机上本地下载。

>[!NOTE]
>
>该桌面应用程序可以映射到Windows上的任何驱动器。 但是，为了顺利操作，请不要更改默认驱动器号。 如果同一组织的用户使用不同的驱动器号，则他们看不到其他人放置的资产。 路径更改时，不会获取放置的资产。 置入的资产将继续保留在二进制文件（如INDD）中，并且不会被删除。

要了解此工作流的限制，请参阅[系统要求和支持的版本](release-notes.md)。

要尝试使用此工作流处理图像资产和InDesign，请执行以下步骤：

1. 在[!DNL Experience Manager]中放置资产的INDD文件中，请务必保持方便。 要了解如何创建此类INDD文件，请参阅[放置图形](https://helpx.adobe.com/indesign/using/placing-graphics.html)。
1. 在桌面应用程序内，**[!UICONTROL Edit]**&#x200B;包含[!DNL Experience Manager]中已放置资产的INDD文件。
1. 应用程序会同时下载InDesign文件和链接的资产。 InDesign打开文档时，将解析链接，下载资产，并在InDesign文档中显示资产。
1. 要在InDesign文件中放置新图形，请对资产执行&#x200B;**[!UICONTROL Reveal File]**&#x200B;操作。 操作会在本地下载资产，并在Windows资源管理器或Mac Finder中打开本地网络共享位置。
1. 将显示的资产放入InDesign文档中。 这会在文档中创建一个链接。
1. 在InDesign文档中完成编辑后，请保存该文档并使用桌面应用程序将其上传到[!DNL Experience Manager]。

## 高级工作流：从本地下载资产 {#adv-workflow-download-assets-locally}

在许多情况下，应用程序会从文件系统上的本地[!DNL Experience Manager]服务器下载资产。 下载占用带宽和磁盘空间。 了解这些方案可帮助您优化下载完成的等待时间。

您可以从应用程序中（按需）下载资产。 请参阅[下载资产](#download-assets)。

当您使用[!UICONTROL Open]操作在本机桌面应用程序中打开资产时，如果该资产尚未在本地可用，则会在本地下载该资产。 请参阅[打开资产](#openondesktop-v2)。

当您从应用程序中显示资产或文件夹的位置时，首先会在本地下载资产或文件夹，然后在本地网络共享中在您的计算机上打开该资产或文件夹。 请参阅[打开资产](#openondesktop-v2)。

当您使用[!UICONTROL Edit]操作在本机桌面应用程序中编辑资产时，如果该资产尚未在本地可用，则会在本地下载该资产。 请参阅[编辑资产并将更新的资产上传到 [!DNL Experience Manager]](#edit-assets-upload-updated-assets)。

如果安装并允许使用该应用程序，则当您从[!DNL Experience Manager] Web界面使用[!UICONTROL Desktop Actions]时，该应用程序将完成操作。 应用程序先下载资产，然后完成操作。
