---
title: 安装和配置桌面应用程序
description: 安装和配置 [!DNL Adobe Experience Manager] desktop app to work with [!DNL Adobe Experience Manager Assets] 服务器，并下载本地文件系统上的资源。
feature: Experience Manager桌面应用程序，发行信息
translation-type: tm+mt
source-git-commit: 7204e3afb6d3a0908c076cf042072e3157572797
workflow-type: tm+mt
source-wordcount: '1405'
ht-degree: 1%

---


# 安装[!DNL Adobe Experience Manager]桌面应用程序{#install-app-v2}

使用[!DNL Adobe Experience Manager]桌面应用程序，[!DNL Experience Manager]中的资源可在您的本地桌面上轻松使用，并可用于任何本机桌面应用程序。 资产可以预览、在本机桌面应用程序中打开、在Mac Finder或Windows资源管理器中显示以放置到其他文档中并在本地进行更改 — 当您上传时，更改将保存回[!DNL Experience Manager]并在存储库中创建新版本。

这种集成允许组织中的各种角色，

* 在[!DNL Experience Manager Assets]中集中管理资产。

* 在任何本机桌面应用程序（包括第三方应用程序）和Adobe Creative Cloud中访问资源。 同时，用户可以轻松遵守包括品牌在内的各种标准。

要使用[!DNL Experience Manager]桌面应用程序，

* 确保[!DNL Experience Manager]桌面应用程序支持您的[!DNL Experience Manager]版本。 请参阅[系统要求](release-notes.md)。

* 下载并安装应用程序。 请参阅下面的[安装桌面应用程序](#install-v2)。

* 使用一些资源测试连接。 请参阅[如何浏览和搜索资产](using.md#browse-search-preview-assets)。

## 系统要求、先决条件和下载链接{#tech-specs-v2}

有关详细信息，请参阅[[!DNL Experience Manager] 桌面应用程序发行说明](release-notes.md)。

## 从先前版本{#upgrade-from-previous-version}升级

如果您是v1.x桌面应用程序的用户，请了解该应用程序的先前版本和最新版本之间的差异和相似性。 请参阅[桌面应用程序](introduction.md#whats-new-v2)中的新增功能和[应用程序的工作方式](release-notes.md#how-app-works)

>[!NOTE]
>
>一台计算机上不能共存两个版本的桌面应用程序。 安装版本前，请卸载其他版本。

要从应用程序的先前版本进行升级，请按照以下说明操作：

1. 在升级之前，同步所有资产并将更改上传到[!DNL Experience Manager]。 这样可避免在卸载应用程序时丢失任何编辑。

1. 卸载应用程序的先前版本。 卸载时，选择清除缓存的选项。

1. 重新启动计算机。

1. [下载](release-notes.md) 并安 [](#install-v2) 装最新的应用程序。按照以下说明操作。

## 安装 {#install-v2}

要安装桌面应用程序，请按照以下步骤操作。 在安装最新的Adobe之前，请卸载任何现有的桌面应用程序[!DNL Experience Manager] v1.x。 有关详细信息，请参阅上文。

1. 从[发行说明](release-notes.md)页面下载最新的安装程序。

1. 请准备好[!DNL Experience Manager]部署的URL和凭据。

1. 如果您是从另一个版本的应用程序升级，请参阅[升级桌面应用程序](#upgrade-from-previous-version)。

1. 如果您使用[!DNL Experience Manager]作为[!DNL Cloud Service]、[!DNL Experience Manager] 6.4.4或更高版本或[!DNL Experience Manager] 6.5.0或更高版本，请跳过此步骤。 确保您的[!DNL Experience Manager]设置符合[发行说明](release-notes.md)中提到的兼容性要求。 如有必要，请下载适用的[兼容性包](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/featurepack/adobe-asset-link-support)，并使用[!DNL Experience Manager]包管理器作为[!DNL Experience Manager]管理员安装它。 要安装包，请参阅[如何使用包](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)。

1. 执行安装程序二进制文件，并按照屏幕上的说明进行安装。

1. 在Windows上，安装程序可能会提示安装`Visual Studio C++ Redistributable 2015`。 按照屏幕说明安装它。 如果安装失败，请手动安装。 从[此处](https://www.microsoft.com/en-us/download/details.aspx?id=52685)下载安装程序，并安装`vc_redist.x64.exe`和`vc_redist.x86.exe`文件。 重新运行[!DNL Experience Manager]桌面应用程序安装程序。

1. 按提示重新启动计算机。 启动和配置桌面应用程序。

1. 要将应用程序与[!DNL Experience Manager]存储库连接，请单击任务栏中的应用程序图标，然后启动应用程序。 以`https://[aem_server]:[port]/`格式提供[!DNL Experience Manager]服务器的地址。

   单击&#x200B;**[!UICONTROL Connect]**&#x200B;并提供凭据。

   ![桌面应用程序与输入服务器地址的连接屏幕](assets/connect_da2.png)

   *图：连接屏幕到输入服务器地址。*

   >[!CAUTION]
   >
   >确保[!DNL Experience Manager]服务器地址之前或之后没有前导或尾部空格。 否则，应用程序无法连接到[!DNL Experience Manager]服务器。

1. 成功连接后，您可以视图[!DNL Experience Manager] DAM根文件夹中可用的文件夹和资产的列表。 您可以从应用程序中浏览文件夹。

   ![登录后，应用程序将显示DAM内容](assets/firstview_da2.png)

   *图：应用程序在登录后显示DAM内容*

1. （[!DNL Experience Manager] 6.5.1或更高版本）如果您使用带有[!DNL Experience Manager] 6.5.1或更高版本的桌面应用程序，请将S3或Azure连接器升级到版本1.10.4或更高版本。 请参阅[Azure连接器](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html#azure-data-store)或[S3连接器](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html#amazon-s-data-store)。

   如果您是Adobe Managed Services(AMS)客户，请与Adobe客户服务联系。

## 设置首选项{#set-preferences}

要更改首选项，请单击![更多选项图标](assets/do-not-localize/more_options_da2.png)和&#x200B;**[!UICONTROL Preference]** ![首选项图标](assets/do-not-localize/preferences_icon_da2.png)。 在&#x200B;**[!UICONTROL Preferences]**&#x200B;窗口中，调整以下值：

* [!UICONTROL Launch application on login]。

* [!UICONTROL Show window when application starts]。

* **[!UICONTROL Cache Directory]**:应用程序的本地缓存位置（它包含本地下载的资源）。

* **[!UICONTROL Network Drive Letter]**:用于映射到DAM的驱动 [!DNL Experience Manager] 器号。如果您不确定，请不要更改此项。 该应用程序可映射到Windows上的任何驱动器号。 如果两个用户放置不同驱动器盘符中的资源，则他们无法看到彼此放置的资源。 资产的路径会更改。 资源将保留在二进制文件（例如INDD）中，并且不会被删除。 应用程序会列表所有可用的驱动器盘符，默认情况下使用最后可用的盘符，通常为`Z`。

* **[!UICONTROL Maximum Cache Size]**:允许在硬盘上缓存(GB)，用于存储本地下载的资源。

* **[!UICONTROL Current cache size]**:存储本地下载资源的大小。仅当使用应用程序下载资产后，才会显示该信息。

* **[!UICONTROL Automatically download linked assets]**:如果您下载原始文件，将自动获取放置在受支持的本机Creative Cloud应用程序中的资源。

* **[!UICONTROL Maximum number of downloads]**: ![警告](assets/do-not-localize/caution-icon.png) 图标谨慎更改。首次下载资产时（通过“显示”、“打开”、“编辑”、“下载”或类似选项），仅当批中包含的资产少于此数时，才下载资产。 默认值为 50。如果不确定，请勿更改。 增加此值可能会延长等待时间，而减少此值可能不允许您一次性下载必要的资产或文件夹。

* **[!UICONTROL Use legacy conventions when creating nodes for assets and folders]**: ![警告](assets/do-not-localize/caution-icon.png) 图标谨慎更改。通过此设置，应用程序在上传文件夹时可模拟v1.10应用程序行为。 在v1.10中，在存储库中创建的节点名称会保留用户提供的文件夹名称的空格和大小写。 但是，在应用程序的v2.1中，文件夹名称中的额外空格将转换为虚线。 例如，如果未选择该选项，并保留v2.1中的默认行为，则上传`New Folder`或`new   folder`将在存储库中创建相同的节点。 如果选择此选项，则在存储库中为上述两个文件夹创建不同的节点，并且它与v1.10应用程序的行为相匹配。

   v2.1的默认行为仍保持不变，即，将存储库节点名称中文件夹名称中的多个空格替换为虚线，并转换为小写节点名称。

* **[!UICONTROL Upload Acceleration]**: ![警告](assets/do-not-localize/caution-icon.png) 图标谨慎更改。上传资产时，应用程序可以使用并发上传来提高上传速度。 您可以通过向右移动滑块来增加上载的并发性。 最左侧的滑块表示不并发（单线程上传），中间位置对应10个并发线程，最右侧的最大限制对应20个并发线程。 更高的并发限制会占用更多资源。

要更新不可用的首选项，请注销[!DNL Experience Manager]服务器，然后进行更新。 更新首选项后，单击![保存首选项](assets/do-not-localize/save_preferences_da2.png)。

![桌面应用程序首选项和设置](assets/preferences_da2.png)

*图：桌面应用程序首选项。*

### 代理支持{#proxy-support}

[!DNL Experience Manager] 桌面应用程序使用系统的预定义代理通过HTTPS连接到Internet。应用程序只能使用不需要额外身份验证的网络代理进行连接。

如果配置或修改Windows的代理服务器设置（“Internet选项”>“LAN设置”），请重新启动[!DNL Experience Manager]桌面应用程序，以使更改生效。 开始桌面应用程序时，将应用代理配置。 关闭并重新启动应用程序，以使任何更改生效。

如果您的代理需要身份验证，则IT团队可以允许代理服务器设置中的[!DNL Experience Manager Assets] URL允许应用程序通信通过。

## 卸载应用程序{#uninstall-the-app}

要在Windows上卸载应用程序，请执行以下步骤：

1. 将所有更改上传到[!DNL Experience Manager]以避免丢失任何编辑。 请参阅[编辑资产并将更新的资产上传到 [!DNL Experience Manager]](using.md#edit-assets-upload-updated-assets)。 注销并[!UICONTROL Exit]应用程序。

1. 删除应用程序，就像删除任何其他操作系统应用程序一样。 在Windows上从“添加”和“删除项目”中卸载它。

1. 要删除缓存和日志，请选中所需的复选框。

   ![用于删除日志和缓存的卸载对话框](assets/uninstall_da2.png)

1. 按照屏幕上的说明操作。 完成后，重新启动计算机。

要在Mac上卸载应用程序，请执行以下步骤：

1. 将所有更改上传到[!DNL Experience Manager]以避免丢失任何编辑。 请参阅[编辑资产并将更新的资产上传到 [!DNL Experience Manager]](using.md#edit-assets-upload-updated-assets)。 注销并[!UICONTROL Exit]应用程序。

1. 从`/Applications`中删除`Adobe Experience Manager Desktop.app`。

或者，要清理Mac上的内部应用程序缓存并卸载该应用程序，可以在终端中执行以下命令：

```shell
/Applications/Adobe Experience Manager Desktop/Contents/Resources/uninstall-osx/uninstall.sh
```
