---
title: 使用 [!DNL Experience Manager] 桌面应用程序版本1.x。
description: 了解如何使用Adobe Experience Manager桌面应用程序1.x版并优化您在桌面上使用资源的作品。
translation-type: tm+mt
source-git-commit: a25c1fa13895ae9eb7268e3e01c83a5f0b9d7d1d
workflow-type: tm+mt
source-wordcount: '2379'
ht-degree: 0%

---


# 使用[!DNL Experience Manager]桌面应用程序v1.x {#use-aem-desktop-app-v1x}

使用应用程序，可在本地桌面上轻松访问[!DNL Experience Manager]中的资源，并可用于任何桌面应用程序。 资产可以轻松地在Mac Finder或Windows资源管理器中显示，在桌面应用程序中打开，并在本地进行更改——这些更改将使用在存储库中创建的新版本保存回[!DNL Experience Manager]。

这种集成允许组织中的不同角色集中管理资产中的资产，并在Creative Cloud和其他应用程序中访问这些资产，同时使企业能够轻松遵守包括品牌在内的各种标准。

使用[!DNL Experience Manager]桌面应用程序v1所执行的关键任务包括：

1. [与服务器 [!DNL Experience Manager] 连接](#installandconnect)
1. [直接在桌面上打开资源](#openondesktop)
1. [从桌面编辑和签出资源](#workonassets)
1. [批量上传资产和文件夹](#bulkupload)

有关各种建议的dos和do&#39;ts，请参阅使用app](best-practices-for-v1.md)的[最佳实践。 如果您在使用应用程序时遇到问题，请参阅如何[解决 [!DNL Experience Manager] 桌面](troubleshoot-app-v1.md)问题。

>[!NOTE]
>
>[!DNL Experience Manager] 桌面应用程序在6. [!DNL Experience Manager] 1版本中引入，称为 [!DNL Experience Manager Assets Companion App]。

## [!DNL Experience Manager] 创意工作流程中的桌面应用程序触点  {#aem-desktop-app-touch-points-in-the-creative-workflow}

[!DNL Experience Manager] 桌面应用程序与 [!DNL Assets]您的创意工作流程相集成，并优惠以下触点。

![[!DNL Experience Manager] 桌面应用程序触点创意工作流程](assets/aem_desktopapp_workflow.png)

[!DNL Experience Manager] 桌面应用程序触点创意工作流程

## 安装应用程序并将其连接到[!DNL Experience Manager]服务器{#installandconnect}

在开始创建或编辑创意资产之前，请先将桌面应用程序与[!DNL Assets]服务器连接，以下载和上传存储库中的资产。 执行以下任务:

1. [安装应用程序](#installapp)。
1. [设置您的首](#inapppref) 选项和连接详细信息。
1. [连接到服 [!DNL Experience Manager] ](#connect) 务器，并将资产存储库作为本地驱动器装载。
1. [启用桌面](#desktopactions) 操作 [!DNL Experience Manager] 服务器。

[!DNL Experience Manager] 桌面应用程序使用HTTPS连接连接到服 [!DNL Experience Manager] 务器，以可靠、安全地传输您的资源。

>[!NOTE]
>
>对于安装和配置步骤的一部分或全部，可能需要[!DNL Experience Manager]管理员或系统管理员的帮助。

### 安装应用程序{#installapp}

要使用[!DNL Experience Manager]桌面应用程序，请确保应用程序支持您的[!DNL Experience Manager]服务器版本。 下载适合您的操作系统（Mac或Windows）的安装文件（二进制）并安装应用程序。

根据网络和系统首选项，可能需要进行详细配置。 有关详细信息，请参阅[安装和配置 [!DNL Experience Manager] 桌面应用程序](install-configure-app-v1.md)。

1. 转到[[!DNL Experience Manager] 桌面应用程序下载页面](https://helpx.adobe.com/experience-manager/kb/download-companion-app.html)并下载适用于您的操作系统的适当二进制文件。
1. 启动下载的安装文件，然后按照屏幕上的说明安装应用程序。

   >[!NOTE]
   >
   >一次只能安装[!DNL Experience Manager]桌面应用程序的一个实例并处于活动状态。

### 了解应用程序内选项和首选项{#inapppref}

应用程序允许设置连接和断开与[!DNL Experience Manager]服务器的连接、上载的视图状态、管理本地缓存等。 默认设置适用于应用程序的典型用户。 您可以调整设置，从应用程序和与[!DNL Experience Manager]服务器的集成中获得更多回报。 下文详细介绍了各种设置。

**浏** 览资产打开装载存储库 [!DNL Assets] 的本地驱动器。换言之，浏览现在在本地机器上可用的资源。

**视图资** 产状态当更改的资产上传或新资产添加到存储 [!DNL Assets] 库时，应用程序会在后台上传资产。后台上传可实现顺畅的操作，您无需等待上传完成，对于大型资产尤为如此。 您可以在本地保存更改并将其忽略。 根据可用带宽，应用程序需要一些时间将这些资源发送到服务器。 您可以检查上传的状态以及一些更基本的信息。

**选** 项在系统开始时，单击桌面应用程序托盘中的选项以访问启动应用程序的设置；在应用程序 [!DNL Experience Manager] 启动时连接到服务器；并更改安装后可用的本 [!DNL Assets] 地驱动器号。

**“高级”>“管** 理缓存”您可以控制可用于本地缓存的磁盘空间量。[!DNL Assets]服务器中的工件在本地缓存，以获得更流畅的体验。 您可以更改默认值以符合您的要求。 此外，还可以清除缓存以重新提取所有资产。 清除缓存时，它保留未保存的更改。 未签入[!DNL Experience Manager]服务器的所有资产都将保留，且不会删除。

### 连接到[!DNL Experience Manager]服务器{#connect}

该应用程序支持Mac和Windows上的代理配置。 应用程序开始时将读取配置。 如果修改代理设置，请重新启动应用程序，使更改生效。

>[!NOTE]
>
>如果修改代理设置，请重新启动应用程序，使更改生效。 否则，应用程序将继续使用之前配置的代理服务器。

1. 启动[!DNL Experience Manager]桌面应用程序。 要将[!DNL Experience Manager]实例与应用程序映射，请以`https://[aem-server-url]:[port]`格式指定[!DNL Experience Manager]服务器。

   ![在Mac上进行身份验证并提 [!DNL Experience Manager] 供服务器URL](assets/aem_desktop_app_server_url.png)

1. 在登录屏幕中，指定实例的用户名和密码。 要指定替代[!DNL Experience Manager]实例，请选择&#x200B;**[!UICONTROL Alternate Login URL]**&#x200B;选项。

   ![在桌 [!DNL Experience Manager] 面应用程序的登录屏幕上提供服 [!DNL Experience Manager] 务器凭据](assets/login_screen_v1.png)

### 在[!DNL Experience Manager] Web接口{#desktopactions}中启用桌面操作

在“资产”用户界面中，您可以浏览资产位置或签出并打开资产，以便在桌面应用程序中进行编辑。 这些选项称为桌面操作，默认情况下不启用。 请按照以下步骤启用它。

1. 在资产界面中，单击／点按工具栏右上角的用户图标。
1. 单击&#x200B;**[!UICONTROL My Preferences]**&#x200B;以显示&#x200B;**[!UICONTROL Preferences]**&#x200B;对话框。

   ![[!DNL Experience Manager] 用户首选项界面](assets/aem_ui_user_preferences.png)

1. 在“用户首选项”对话框中，选择&#x200B;**[!UICONTROL Show Desktop Actions For Assets]**。 单击 **[!UICONTROL Accept]**.

   ![选中 [!UICONTROL Show Desktop Actions For Assets] 以启用桌面操作](assets/enable_desktop_actions.png)

   *图：选中显示资产的桌面操作以启用桌面操作。*

## 在桌面上访问和打开资源{#openondesktop}

单击&#x200B;**打开**&#x200B;以在本地计算机上打开资产时，应用程序会将资产下载到其内部缓存。 该应用程序会启动与已下载资产的文件类型关联的本机桌面应用程序。

在Mac上，从上下文菜单中选择&#x200B;**打开**，以通过[!DNL Experience Manager]桌面应用程序打开资产。 在Windows上，从上下文菜单中选择“在Web上打开”以打开资产。 在资产状态窗口中，单击／点按![在桌面上打开图标](assets/do-not-localize/aemassets_icon_openondesktop.png)以打开资产。

对于Adobe InDesign(INDD)文件，从上下文菜单中选择&#x200B;**[!UICONTROL Open]**。 单击此选项时，应用程序会将链接的资源下载到您的本地文件系统，然后在Adobe InDesign打开INDD文件。 此方法确保在编辑INDD文件时，必要的资源在本地可用。

![使用桌面应用程序访问和打开资产的上下文 [!DNL Experience Manager] 菜单选项](assets/aem_desktopapp_mac_context_menu.png)

*图：使用桌面应用程序访问和打开资产的上 [!DNL Experience Manager] 下文菜单选项。*

>[!NOTE]
>
>在Windows上，[默认的Windows 7设置](https://support.microsoft.com/en-us/kb/2668751)会阻止[!DNL Experience Manager]桌面应用程序处理大于50 MB的资源。

>[!NOTE]
>
>Adobe建议您转到Mac上的Finder视图选项，并取消激活已装入[!DNL Assets]文件夹的选项&#x200B;**显示项目信息**、**显示项目预览**&#x200B;和&#x200B;**显示预览列**。 它提高了性能。

### [!DNL Experience Manager]接口{#additional-options-in-aem-assets}中的其他选项

将[!DNL Assets]存储库映射到本地驱动器后，您可以启用其他图标，并为映射的资产和文件夹显示文件夹上传功能。

1. 打开[!DNL Assets]界面，将指针悬停在文件夹或资产上，以在卡视图中将桌面操作显示为快速操作。

   ![在资产UI中，打开快速操作菜单以查看桌面操作](assets/desktop_actions_in_card_view.png)

   *图：在资产UI中，打开快速操作菜单以查看桌面操作。*

   在选择资产后或从资产页面的工具栏中单击工具栏中的&#x200B;**桌面操作**&#x200B;选项时，这些桌面操作也可用。

1. 要在与特定文件扩展名关联的桌面应用程序中打开资产，请单击&#x200B;**在桌面上打开**&#x200B;快速操作![在桌面上打开图标](assets/do-not-localize/aemassets_icon_openondesktop.png)。

   或者，从工具栏的&#x200B;**桌面操作**&#x200B;菜单中选择&#x200B;**打开**。

要在本地文件系统上找到特定资产，请单击&#x200B;**显示**&#x200B;快速操作![显示图标](assets/do-not-localize/aemassets_reveal_icon.png)。 或者，从工具栏的&#x200B;**桌面操作**&#x200B;菜单中选择&#x200B;**显示**。

## 了解资产状态{#understand-the-asset-statuses}

| ![Windows默认应用程序图标](assets/do-not-localize/win_default.png) | 应用程序已连接到服务器，且所有资产都已同步。 |
--- |--- |
| ![禁用Windows的图标](assets/do-not-localize/win_disabled.png) | 应用程序已启动，但未与服务器连接。 某些资产可能处于挂起同步状态。 |
| ![Windows文件同步图标](assets/do-not-localize/win_sync.png) | 资产正在同步。 正在上传或下载文件。 您可以从“资产状态”窗口查看确切状态并暂停转移。 |
| ![Windows重新连接图标](assets/do-not-localize/win_refresh.png) | 应用程序正在尝试重新连接。 可能是网络问题导致其断开连接。 |

## 处理您的资产{#workonassets}

### 从[!DNL Experience Manager] Web界面{#check-out-assets-from-the-aem-web-interface}中检出资源

[!DNL Assets] 允许您签出要编辑的资产，并在完成更改后重新将其签回。注销资产后，只有您才能编辑、批注、发布、移动或删除资产。 注销资产会锁定资产并阻止其他用户执行其中的任何操作。 要能够签出／登录资产，您需要对资产具有写入权限。

有两种从[!DNL Experience Manager] Web界面签出资源的方法。 有关第一种方法的详细信息，请参阅[从资产UI](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/check-out-and-submit-assets.html)签入和签出文件。 请按照以下步骤操作，获取在安装[!DNL Experience Manager]桌面应用程序时签出并打开资产的第二种方法。

1. 打开[!DNL Assets]界面，将指针悬停在文件夹或资产上，以在卡视图中将桌面操作显示为快速操作。

   ![卡视图中的属性选项](assets/desktop_actions_in_card_view.png)

   在选择资产后或从资产页面的工具栏中单击／点按工具栏中的桌面操作图标时，这些桌面操作也可用。

1. 要打开资产，请单击／点按在桌面上打开快速操作![在桌面上打开图标](assets/do-not-localize/aemassets_icon_openondesktop.png)。

   或者，从工具栏的“桌面操作”菜单中选择“打开”。

   >[!NOTE]
   >
   >当您编辑刚打开但未签出的文件时，其他用户无法知道您正在更新资产。

1. 要打开资产以在Adobe Creative Cloud应用程序中进行编辑，请单击／点按编辑桌面快速操作![编辑桌面图标](assets/do-not-localize/aemassets_icon_editdesktop.png)。 此外，还会签出资产进行编辑。 完成编辑后，请检入资产以更新[!DNL Assets]中的更改。

   或者，也可以从工具栏的“桌面操作”菜单中选择“编辑”。

1. 选择“打开”菜单选项。 此时会以预览模式打开选定的资产。
1. 要编辑资产，请选择编辑选项。 资产会在编辑模式下打开。

### 从Mac OS上的Finder中签出资产{#check-out-assets-on-mac}

该应用程序允许您签出资产文件以防止其他用户修改您正在处理的文件。

1. 从Mac上下文菜单中，选择“打开AEM Assets文件夹”选项以打开Finder。

   ![使用桌面应用程序访问和打开资产的上下文 [!DNL Experience Manager] 菜单选项](assets/aem_desktopapp_mac_context_menu.png)

   *图：使用桌面应用程序访问和打开资产的上 [!DNL Experience Manager] 下文菜单选项。*

1. 导航到要签出的资产。
1. 右键单击资产，然后从上下文菜单中选择更多资产信息。
1. 在资产信息对话框中，单击／点按签出图标以签出资产。 单击／点按签入图标后，“签出”图标将切换至该签入图标。

   ![浏览到要签出的资产](assets/browse_assets_to_checkout.png)

1. 要签入资产以便其他用户可以使用，请单击／点按资产信息对话框中的签入图标。

### 在Windows {#check-out-assets-on-windows}上检出资源

该应用程序允许您签出资产文件以防止其他用户修改您正在处理的文件。

1. 从上下文菜单中，选择浏览资产以打开资源管理器。
1. 在资源管理器中，导航到要签出的资产所在的位置。
1. 右键单击资产，然后从上下文菜单中选择“在Web上打开”。
1. 在资产信息对话框中，单击／点按签出图标。 “签出”图标切换为“签入”图标。

   ![签出图标切换](assets/checkout_icon_toggles.png)

1. 在资源管理器中审核资产。 资产![资产锁图标](assets/do-not-localize/aemassets_icon_lockcheckout.png)上的锁图标表示您已签出资产。

   >[!NOTE]
   >
   >在出现延迟后，可能会显示锁图标。 [!DNL Experience Manager] 桌面应用程序会缓存资源以进行快速访问，因此可能需要一些时间才能更新锁定状态。

1. 要签入资产以便其他用户可以使用，请单击／点按&#x200B;**资产信息**&#x200B;对话框中的签入图标。

### 使用Finder或资源管理器并使用Web界面{#check-in-an-asset-using-finder-or-explorer-and-using-web-interface}签入资产

编辑完资产后，请在桌面应用程序中保存资产。 从上下文菜单中，选择&#x200B;**更多资产信息**&#x200B;并单击签入。

资产将上传到[!DNL Experience Manager]服务器。 或者，您也可以从系统任务栏图标中选择&#x200B;**视图资产状态**&#x200B;来检查上传状态。 或者，您也可以从[!DNL Experience Manager] Web界面签入资产。 单击签出的资产或选择它。 在工具栏中，单击签入图标![签入图标](assets/do-not-localize/aemassets_icon_checkin.png)。

在本地保存任何更改后，资产会自动上传到[!DNL Experience Manager]。 该登记功能使其他[!DNL Experience Manager]用户可以编辑资产。

### 将资产和文件夹批量上传到[!DNL Experience Manager]服务器{#bulkupload}

使用[!DNL Experience Manager]桌面应用程序，您可以将包含资产的整个文件夹从本地文件目录上传到[!DNL Assets]。 这样，文件夹中的所有资产都可以批量上传，而不必一次上传一个资产。

1. 在资产UI中，单击／点按工具栏中的&#x200B;**创建**，然后从菜单中选择&#x200B;**上传文件夹**。
1. 浏览到要上传的文件夹并选择它。
1. 单击／点按确定。 资产状态对话框显示上传的状态。

   ![在“资产状态”窗口中查看上传状态](assets/aem_desktopapp_bulkupload_status.png)

   在“资产状态”窗口中查看上传状态

   >[!NOTE]
   >
   >您可以通过单击／点按相应的图标手动暂停或取消上传。

1. 文件夹上传后，请关闭对话框并导航到资产UI。 上传的文件夹显示在Web界面中。

Adobe不建议将更多文件或嵌套文件夹从本地文件系统复制粘贴或拖动到网络共享区域。 由于技术限制，应用程序无法控制上传过程，并且性能很差。

或者，在Finder或资源管理器中选择要上传到[!DNL Experience Manager]的文件／文件夹，将它们复制到系统剪贴板，导航到网络共享区域的目标文件夹，然后从[!DNL Experience Manager]桌面应用程序上下文菜单中选择&#x200B;**粘贴资产**。 这样，[!DNL Experience Manager]桌面应用程序开始上传粘贴的资产，类似于[!DNL Experience Manager] Web界面中提供的&#x200B;**上传文件夹**&#x200B;选项。

>[!MORELIKETHIS]
>
>* [桌面应 [!DNL Experience Manager] 用程序疑难解答](troubleshoot-app-v1.md)

