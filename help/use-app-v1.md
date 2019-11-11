---
title: 使用AEM桌面应用程序版本1.x
seo-title: 使用Adobe Experience manager桌面应用程序版本1.x
description: 了解如何使用Adobe Experience manager桌面应用程序版本1.x并优化您在桌面上使用资产的作品。
seo-description: 了解如何使用Adobe Experience manager桌面应用程序版本1.x，以及如何通过桌面和创意工作流程优化您的资产。
uuid: 55057617-89de-43cd-8419-1252a42ab2fb
contentOwner: asgupa
products: SG_EXPERIENCEMANAGER/6.3/ASSETS
discoiquuid: 39d7bcad-d7b0-4978-a790-4cb68b8a7d6a
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: c305f57b8ad874bcffc250689d917e31820225e4

---


# 使用AEM桌面应用程序v1.x {#use-aem-desktop-app-v1x}

使用应用程序，AEM中的资产可在您的本地桌面上轻松访问，并可用于任何桌面应用程序。 资产可以在Mac finder或Windows资源管理器中轻松显示，在桌面应用程序中打开并在本地更改——更改将保存回AEM，并在存储库中创建新版本。

此类集成允许组织中的不同角色集中管理AEM资产中的资产，并在Creative cloud和其他应用程序中访问这些资产，同时使您能轻松遵守包括品牌在内的各种标准。

您使用AEM桌面应用程序v1执行的主要任务包括：

* [与AEM服务器连接](#installandconnect)

* [直接在桌面上打开资源](#openondesktop)
* [从桌面编辑和签出资源](#workonassets)

* [批量上传资产和文件夹](#bulkupload)

有关各种建议的dos和don't，请参阅使用 [应用程序的最佳实践](best-practices-for-v1.md)。 如果您使用应用程序时遇到问题，请参阅如何对AEM Desktop [进行疑难解答](troubleshoot-app-v1.md)。

>[!NOTE]
>AEM桌面应用程序在AEM 6.1版本中引入，称为AEM Assets Companion应用程序。

## 创意工作流程中的AEM Desktop应用程序触点 {#aem-desktop-app-touch-points-in-the-creative-workflow}

AEM Desktop应用程序与AEM Assets集成在您的创意工作流程中，并提供以下接触点。

![AEM desktop应用程序触点创意工作流程](assets/aem_desktopapp_workflow.png)

AEM desktop应用程序触点创意工作流程

## 安装AEM桌面应用程序并将其连接到AEM服务器 {#installandconnect}

在开始创建或编辑创意资产之前，请先将桌面应用程序与AEM资产服务器连接，以下载和上传存储库中的资产。 执行以下任务：

1. [安装应用程序](#installapp)。
1. [设置您的首选项](#inapppref) 和连接详细信息。
1. [连接到AEM服务器](#connect) ，并将资产存储库作为本地驱动器装载。
1. [在AEM服务器上启用桌面操作](#desktopactions) 。

AEM桌面应用程序使用HTTPS连接连接到AEM服务器，以强健而安全地传输您的资产。

>[!NOTE]
>对于部分或全部安装和配置步骤，您可能需要AEM管理员或系统管理员的帮助。

### 安装应用程序 {#installapp}

要使用AEM桌面应用程序，请确保AEM桌面应用程序支持您的AEM服务器版本。 下载适合您的操作系统（Mac或Windows）的安装文件（二进制）并安装应用程序。

根据网络和系统首选项，可能需要进行详细配置。 有关更 [多详细信息，请参阅安装和配置AEM桌面应用程序](install-configure-app-v1.md) 。

1. 转到 [AEM Desktop应用程序下载页面](https://helpx.adobe.com/experience-manager/kb/download-companion-app.html) ，下载适用于您的操作系统的相应二进制文件。
1. 启动下载的安装文件，然后按照屏幕上的说明安装应用程序。

   >[!NOTE]
   >一次只能安装AEM桌面应用程序的一个实例并处于活动状态。

### 了解应用程序内选项和首选项 {#inapppref}

该应用程序允许设置连接AEM服务器和从AEM服务器断开连接、查看上传状态、管理本地缓存等。 默认设置适用于应用程序的典型用户。 您可以调整设置，以从应用程序和AEM服务器集成中获得更多好处。 下面详细介绍了各种设置。

**浏览资产** 打开装载AEM资产存储库的本地驱动器。 换句话说，浏览现在在本地机器上可用的资源。

**查看资产状态** ：当更改的资产上传或新资产添加到AEM资产存储库时，应用程序会在后台上传资产。 后台上传允许顺畅操作，您无需等待上传完成，对于大型资产尤为如此。 您可以将更改保存在本地并将其忽略。 应用程序需要一些时间将这些资源发送到服务器，具体取决于可用带宽。 您可以检查上传的状态以及一些更基本的信息。

**选项** 单击／点按AEM桌面应用程序托盘中的选项，以访问在系统启动时启动应用程序的设置；在启动应用程序时连接到AEM服务器；并更改安装后AEM资产可用的本地驱动器盘符。

**“高级”&gt;“管理缓存** ”您可以控制可用于本地缓存的磁盘空间量。 AEM资产服务器中的对象将在本地缓存，以获得更流畅的体验。 您可以更改默认值以满足您的要求。 此外，您还可以清除缓存以重新获取所有资产。 清除缓存时，它会保留未保存的更改。 未签入AEM服务器的所有资产将保留且不会删除。

### 连接到AEM服务器 {#connect}

应用程序支持Mac和Windows上的代理配置。 应用程序启动时将读取配置。 如果修改代理设置，请重新启动应用程序，使更改生效。

>[!NOTE]
>
>如果修改了代理设置，请重新启动应用程序，使更改生效。 否则，应用程序将继续使用之前配置的代理服务器。

1. 启动AEM Desktop应用程序。 要将AEM实例与应用程序映射，请以格式指定AEM服务器 `https://[aem-server-url]:[port]`。

   ![在Mac上进行身份验证并提供AEM服务器URL](assets/aem_desktop_app_server_url.png)

1. 在登录屏幕中，指定实例的用户名和密码。 要指定替代AEM实例，请选择该 **[!UICONTROL Alternate Login URL]** 选项。

   ![在AEM Desktop的登录屏幕上提供AEM服务器凭据](assets/chlimage_1-2.png)

### 在AEM web界面中启用桌面操作 {#desktopactions}

从浏览器中的资产UI中，您可以浏览资产位置或注销并打开资产以在桌面应用程序中进行编辑。 这些选项称为“桌面操作”，默认情况下不启用。 请按照以下步骤启用它。

1. 在“资产”控制台中，单击／点按工 **具栏中的** “用户”图标。
1. 单击／点按 **[!UICONTROL My Preferences]** 以显示对 **[!UICONTROL Preferences]** 话框。
1. 在“用户首选项”对话框中，选择 **[!UICONTROL Show Desktop Actions For Assets]**。 单击／点按 **[!UICONTROL Accept]**。

   ![选中显示资产的桌面操作以启用桌面操作](assets/chlimage_1-3.png)

   选中显示资产的桌面操作以启用桌面操作

## 在桌面上访问和打开资源 {#openondesktop}

>[!NOTE]
>在Windows上，默 [认的Windows 7设置会阻止](https://support.microsoft.com/en-us/kb/2668751) AEM桌面应用程序处理大于50 MB的资产。

### 从AEM web界面显示映射资产的位置 {#reveal-the-location-of-mapped-assets-from-aem-web-interface}

将AEM资产存储库映射到本地驱动器后，您可以启用其他图标，并为映射的资产和文件夹显示文件夹上传功能。

1. 打开AEM资产界面，将指针悬停在文件夹或资产上，以在卡片视图中将桌面操作显示为快速操作。

   ![在资产UI中，打开快速操作菜单以查看桌面操作](assets/chlimage_1-4.png)

   在资产UI中，打开快速操作菜单以查看桌面操作

   在选择资产后或从资产页面的工具栏中单击／点按工具栏中的 **桌面操作** ，也可以执行这些桌面操作。

1. 要在与特定文件扩展名关联的桌面应用程序中打开资产，请单击／点按在桌面上打开快速操作 **** 在桌面上打开图标 ![](assets/aemassets_icon_openondesktop.png)。

   或者，从工 **具栏的** “桌面 **操作** ”菜单中选择“打开”。

1. 单击／点按显 **示** 快速操作 ![显示图标](assets/aemassets_reveal_icon.png) ，以在本地文件系统上查找特定资产。

   或者，从工 **具栏的** “桌面 **操作** ”菜单中选择“显示”。

### 从Finder或资源管理器中打开AEM资产 {#open-aem-assets-from-the-finder-or-the-explorer}

在Mac上，从上下文菜单中选择打开，以通过AEM Desktop打开资产。

对于Adobe inDesign(INDD)文件，从上下文 **[!UICONTROL Open]** 菜单中选择。 单击此选项后，应用程序会将链接的资源下载到您的本地文件系统，然后在Adobe inDesign中打开INDD文件。 此方法确保在编辑INDD文件时，必要的资源在本地可用。

在Windows上，从上下文菜单中选择“在Web上打开”以打开资产。 在资产状态窗口中，单击／点按在桌 ![面上打开图标](assets/aemassets_icon_openondesktop.png) ，以打开资产。

![使用AEM Desktop应用程序访问和打开资产的上下文菜单选项](assets/aem_desktopapp_mac_context_menu.png)

使用AEM Desktop应用程序访问和打开资产的上下文菜单选项

### 了解资产状态 {#understand-the-asset-statuses}

| ![Windows默认应用程序图标](assets/win_default.png) | 应用程序已连接到服务器，并且所有资产都已同步。 |
|------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| ![Windows禁用图标](assets/win_disabled.png) | 应用程序已启动，但未与服务器连接。 某些资产可能处于挂起同步状态。 |
| ![Windows文件同步图标](assets/win_sync.png) | 资产正在同步。 正在上传或下载文件。 您可以查看确切状态，并从“资产状态”窗口暂停转移。 |
| ![Windows重新连接图标](assets/win_refresh.png) | 应用程序正在尝试重新连接。 可能是网络问题导致其断开连接。 |

## 处理您的资产 {#workonassets}

### 从AEM web界面中签出资产 {#check-out-assets-from-the-aem-web-interface}

通过AEM资产，您可以注销要编辑的资产，并在完成更改后重新登记。 注销资产后，只有您才能编辑、批注、发布、移动或删除资产。 注销资产会锁定资产，并阻止其他用户执行任何这些操作。 要能够注销／登录资产，您需要对资产具有写入权限。

有两种方法可从AEM web界面注销资产。 有关第一种方法的详细信息，请参 [阅从资产UI签入和签出文件](https://helpx.adobe.com/in/experience-manager/6-4/assets/using/check-out-and-submit-assets.html)。 请按照以下步骤操作，以获取在安装AEM Desktop应用程序时注销并打开资产的第二种方法。

1. 打开AEM资产界面，将指针悬停在文件夹或资产上，以在卡片视图中将桌面操作显示为快速操作。

   ![卡片视图中的属性选项](assets/chlimage_1-4.png)

   在选择资产后或从资产页面的工具栏中单击／点按工具栏中的桌面操作图标时，这些桌面操作也可用。

1. 要打开资产，请单击／点按在桌面上打开快速操作在桌 ![面上打开图标](assets/aemassets_icon_openondesktop.png)。

   或者，也可以从工具栏的“桌面操作”菜单中选择“打开”。

   >[!NOTE]
   >当您编辑刚打开但未签出的文件时，其他用户不会知道您正在更新资产。

1. 要打开资产以在Adobe Creative cloud应用程序中进行编辑，请单击／点按编辑桌面快速操作编辑桌 ![面图标](assets/aemassets_icon_editdesktop.png)。 此操作还会检出要编辑的资产。 完成编辑后，请登记资产以更新AEM资产中的更改。

   或者，也可以从工具栏的“桌面操作”菜单中选择“编辑”。

1. 选择“打开”菜单选项。 此时会以预览模式打开选定的资产。
1. 要编辑资产，请选择编辑选项。 资产会在编辑模式下打开。

### 在Mac上查看资源 {#check-out-assets-on-mac}

该应用程序允许您签出资产文件，以防止其他用户修改您正在处理的文件。

1. 从Mac上下文菜单中，选择打开AEM资产文件夹以打开Finder。

   ![使用AEM Desktop应用程序访问和打开资产的上下文菜单选项](assets/aem_desktopapp_mac_context_menu.png)

   使用AEM Desktop应用程序访问和打开资产的上下文菜单选项

1. 导航到要注销的资产。

   ![在Mac上的AEM Assets上下文菜单中打开](assets/chlimage_1-5.png)

1. 右键单击资产，然后从上下文菜单中选择更多资产信息。
1. 在资产信息对话框中，单击／点按结帐图标以注销资产。 单击／点按后，“检出”(Checkout)图标将切换到“签入”(Checkin)图标。

   ![浏览到资产以结帐](assets/chlimage_1-6.png)

1. 要签入资产以便其他用户可以使用它，请单击／点按资产信息对话框中的签入图标。

### 在Windows上签出资源 {#check-out-assets-on-windows}

该应用程序允许您签出资产文件，以防止其他用户修改您正在处理的文件。

1. 从上下文菜单中，选择浏览资产以打开资源管理器。
1. 在资源管理器中，导航到要注销的资产所在的位置。

   ![签出图标切换](assets/chlimage_1-7.png)

1. 右键单击资产，然后从上下文菜单中选择在Web上打开。
1. 在资产信息对话框中，单击／点按结帐图标。 “检出”(Checkout)图标切换为“检入”(Checkin)图标。

   ![签出图标切换](assets/chlimage_1-8.png)

1. 在资源管理器中审核资产。 资产锁定图标上的锁 ![定图标](assets/aemassets_icon_lockcheckout.png) ，表示您已注销资产。

   >[!NOTE]
   >在延迟几分钟后，可能会显示锁图标。 AEM desktop应用程序缓存资产以便快速访问，因此可能需要片刻时间才能更新锁定状态。

1. 要签入资产以便其他用户可以使用它，请单击／点按资产信息对话框中的签 **入图标** 。

### 使用Finder或资源管理器以及Web界面登记资产 {#check-in-an-asset-using-finder-or-explorer-and-using-web-interface}

编辑完资产后，将资产保存到桌面应用程序中。 从上下文菜单中，选择更多资产信息，然后单击／点按签入。

资产会上传到AEM服务器。 或者，您也可以选择从任务栏图标中选择查看资产状态来检查上传状态。

![AEM桌面应用程序文件传输和上传状态窗口](assets/aem_desktopapp_upload_status.png)

或者，您也可以从AEM web界面签入资产。 单击／点按已签出的资产或选择它。 在工具栏中，单击／点按签入图标签 ![入图标](assets/aemassets_icon_checkin.png)。

### 将资产和文件夹批量上传到AEM服务器 {#bulkupload}

使用AEM Desktop，您可以将包含资产的整个文件夹从本地文件目录上传到AEM资产。 这样，文件夹中的所有资产都会批量上传，而不必一次上传一个。

1. 在资产UI中，单击／点按工 **具栏中的创建** ，然后从菜单中 **选择上传文件夹** 。
1. 浏览到要上传的文件夹，然后选择它。
1. 单击／点按确定。 资产状态对话框显示上传的状态。

   ![在“资产状态”窗口中查看上传状态](assets/aem_desktopapp_bulkupload_status.png)

   在“资产状态”窗口中查看上传状态

   >[!NOTE]
   >您可以通过单击／点按相应的图标手动暂停或取消上传。

1. 文件夹上传后，关闭对话框并导航到资产UI。 上传的文件夹显示在Web界面中。

请注意，不建议 *在Finder或资源管理器中复制并粘贴* ，或将更多文件／嵌套文件夹从本地磁盘拖放到AEM桌面应用程序映射的网络共享区域。 与上述“上传文件夹”功能相比，它更不可靠。

如果您希望在桌面上工作，还可以选择要在Finder或资源管理器中选择要上传到AEM的文件／文件夹，将它们复制到系统剪贴板，然后导航到网络共享区域中的目标文件夹，并从AEM桌面应用程序上下文菜单中选择“粘贴资产”。 这样，AEM桌面应用程序就会开始上传粘贴的资产，这与上述上传文件夹类似。

>[!MORELIKETHIS]
>
>* [AEM桌面应用程序简介](https://helpx.adobe.com/experience-manager/kt/eseminars/ccoo-aem-desktop-app.html)
>* [了解AEM桌面应用程序的登记／注销](https://helpx.adobe.com/experience-manager/kt/assets/using/checkin-checkout-technical-video-understand.html)
>* [AEM Desktop应用程序疑难解答](troubleshoot-app-v1.md)

