---
title: 安装和配置Adobe Experience Manager桌面应用程序
description: 安装和配置Adobe Experience Manager桌面应用程序以与Adobe Experience Manager资产服务器一起使用，并将资产下载到您的本地文件系统中。
uuid: 79bc9de9-5708-41f9-ac43-68c1fd2a2129
contentOwner: AG
products: SG_EXPERIENCEMANAGER/6.3/ASSETS
discoiquuid: f6365302-1690-4719-9b8c-035719422740
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: b92e47456f9e16c24eac43d1c5fef9a582f143b5

---


# Install Adobe Experience Manager desktop app {#install-app-v2}

使用Adobe Experience Manager桌面应用程序，Experience Manager中的资产可在您的本地桌面上轻松访问，并可用于任何本机桌面应用程序。 资产可以预览、在本机桌面应用程序中打开、在Mac Finder或Windows资源管理器中显示以放置到其他文档中以及在本地更改——当您上传时，这些更改将保存回Experience Manager并在存储库中创建新版本。

这种集成允许组织中的各种角色，

* 在Experience Manager资产中集中管理资产。
* 在任何本机桌面应用程序（包括第三方应用程序）和Adobe Creative Cloud中访问资源。 同时，用户可以轻松地遵守包括品牌在内的各种标准。

要使用Experience Manager桌面应用程序，

* 确保Experience Manager桌面应用程序支持您的Experience Manager版本。 请参阅以 [下系统要求](release-notes.md#system-requirements-and-prerequisites-v2) 。
* 下载并安装应用程序。 请参阅 [下面的安装桌面应用程序](#install-v2) 。
* 使用一些资源测试连接。 了解 [如何浏览和搜索资产](using.md#browse-search-preview-assets)。

## 系统要求、先决条件和下载链接 {#tech-specs-v2}

有关详细信息，请参阅 [Experience Manager桌面应用程序发行说明](release-notes.md)。

## Upgrade from a previous version {#upgrade-from-previous-version}

如果您是v1.x桌面应用程序的用户，则了解应用程序的先前版本与最新版本之间的差异和相似性。 查看 [桌面应用程序的新增功能](introduction.md#whats-new-v2) ，以 [及应用程序的工作方式](release-notes.md#how-app-works)

>[!NOTE]
>
>一台计算机上不能共存两个版本的桌面应用程序。 安装版本之前，请卸载其他版本。

要从应用程序的先前版本升级，请按照以下说明操作：

1. 在升级之前，同步所有资产并将更改上传到Experience Manager。 这样可避免在卸载应用程序时丢失任何编辑。
1. 卸载应用程序的先前版本。 卸载时，选择清除缓存的选项。
1. 重新启动计算机。
1. [下载](release-notes.md) ，并安 [装最新](#install-v2) 的应用程序。 按照以下说明操作。

## 安装 {#install-v2}

要安装桌面应用程序，请按照以下步骤操作。 在安装最新应用程序之前，卸载任何现有的Adobe Experience Manager桌面应用程序v1.x。 有关详细信息，请参阅上文。

1. 从发行说明页面下载最 [新的安装程](release-notes.md) 序。
1. 让Experience Manager部署的URL和凭据保持便利。
1. 如果您是从应用程序的其他版本升级，请参阅升 [级桌面应用程序](#upgrade-from-previous-version)。
1. 如果您将Experience Manager用作云服务、Experience Manager 6.4.4或更高版本，或Experience Manager 6.5.0或更高版本，请跳过此步骤。 确保您的Experience Manager设置符合发行说明中所述的兼容 [性要求](release-notes.md)。 如有必要，请下载适用 [的兼容性包](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/featurepack/adobe-asset-link-support) ，并使用Experience Manager包管理器作为Experience Manager管理员安装它。 要安装包，请参阅 [如何使用包](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html)。
1. 执行安装程序二进制文件，并按照屏幕上的说明进行安装。
1. 在Windows上，安装程序可能会提示安装 `Visual Studio C++ Redistributable 2015`。 按照屏幕上的说明安装它。 如果安装失败，请手动安装。 从此处下载安 [装程序](https://www.microsoft.com/en-us/download/details.aspx?id=52685) ，并安装 `vc_redist.x64.exe` 和文 `vc_redist.x86.exe` 件。 重新运行AEM桌面应用程序安装程序。
1. 根据提示重新启动计算机。 启动和配置桌面应用程序。
1. 要将应用程序与AEM存储库连接，请单击托盘中的应用程序图标以启动应用程序。 提供AEM实例的地址。 单击 **[!UICONTROL Connect]** 并提供凭据。

   ![桌面应用程序与输入服务器地址的连接屏幕与输](assets/connect_da2.png "入服务器地址的连接屏幕")

   >[!C动作]
   >
   >确保AEM服务器地址之前或之后没有前导或尾部空格。 否则，应用程序无法连接到AEM服务器。

1. 成功连接后，您可以视图AEM DAM根文件夹中可用的文件夹和资产的列表。 您可以从应用程序内浏览文件夹。

   ![登录时，应用程序显示DAM](assets/firstview_da2.png "内容登录时，应用程序显示DAM内容")

1. （Experience Manager 6.5.1或更高版本）如果您使用的是带有Experience Manager 6.5.1或更高版本的桌面应用程序，请将S3或Azure连接器升级到版本1.10.4或更高版本。 请参 [阅Azure连接器](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/deploying/data-store-config.html#AzureDataStore) 或 [S3连接器](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/deploying/data-store-config.html#AmazonS3DataStore)。

   如果您是Adobe Managed Services(AMS)客户，请与Adobe客户关怀联系。

## 设置首选项 {#set-preferences}

要更改首选项，请单击“更 ![多选项”图标](assets/do-not-localize/more_options_da2.png) ，然 **[!UICONTROL Preference]** 后单击“首 ![选项”图标](assets/do-not-localize/preferences_icon_da2.png)。 在窗 **[!UICONTROL Preferences]** 口中，调整以下各项的值：

* [!UICONTROL Launch application on login].
* [!UICONTROL Show window when application starts].
* **[!UICONTROL Cache Directory]**:应用程序的本地缓存位置（它包含本地下载的资源）。
* **[!UICONTROL Network Drive Letter]**:用于映射到AEM DAM的驱动器号。 如果不确定，请勿更改此设置。 该应用程序可映射到Windows上的任何驱动器盘符。 如果两个用户放置不同驱动器盘符的资产，则他们看不到彼此放置的资产。 资产的路径会更改。 资源将保留在二进制文件（如INDD）中，并且不会被删除。 应用程序会列表所有可用的驱动器盘符，默认情况下会使用通常为最后可用的盘符 `Z`。
* **[!UICONTROL Maximum Cache Size]**:允许在硬盘上以GB为单位进行缓存，用于存储本地下载的资源。
* **[!UICONTROL Current cache size]**:存储本地下载的资源的大小。 仅在使用应用程序下载资产后，才会显示该信息。
* **[!UICONTROL Automatically download linked assets]**:如果您下载原始文件，则会自动获取放置在受支持的本机Creative Cloud应用程序中的资源。
* **[!UICONTROL Maximum number of downloads]**:首次下载资产时（通过“显示”、“打开”、“编辑”、“下载”或类似选项），仅当批中包含的资产小于此数时，才下载资产。 默认值为 50。如果不确定，请勿更改。 增加此值可能导致较长的等待时间，而降低此值可能不允许您一次性下载必要的资产或文件夹。
* **[!UICONTROL Upload Acceleration]**:上传资产时，应用程序可以使用并发上传来提高上传速度。 您可以通过向右移动滑块来增加上传的并发性。 最左侧的滑块表示不并发（单线程上传），中间位置对应10个并发线程，最右侧的最大限制对应20个并发线程。 较高的并发限制要求本地机器的处理器消耗更多资源。

要更新不可用的首选项，请注销AEM服务器。 更新首选项后，单击“保 ![存首选项](assets/do-not-localize/save_preferences_da2.png) ”以保存更改。

![AEM桌面应用程序首选项和设置桌](assets/preferences_da2.png "面应用程序首选项")

## 卸载应用程序 {#uninstall-the-app}

要在Windows上卸载应用程序，请执行以下步骤：

1. 将所有更改上传到AEM以避免丢失任何编辑。 请参 [阅编辑资产并将更新的资产上传到AEM](using.md#edit-assets-upload-updated-assets)。 注销并使 [!UICONTROL Exit] 用应用程序。
1. 在删除任何其他操作系统应用程序时删除该应用程序。 从“添加”中卸载它并在Windows上删除项目。
1. 要删除缓存和日志，请选中所需的复选框。
   ![用于删除日志和缓存的卸载对话框用于](assets/uninstall_da2.png "删除日志和缓存的卸载对话框用于删除日志和缓存")
1. 按照屏幕上的说明操作。 完成后，重新启动计算机。

要在Mac上卸载应用程序，请执行以下步骤：

1. 将所有更改上传到AEM以避免丢失任何编辑。 请参 [阅编辑资产并将更新的资产上传到AEM](using.md#edit-assets-upload-updated-assets)。 注销并使 [!UICONTROL Exit] 用应用程序。
1. 从中 `Adobe Experience Manager Desktop.app` 删除 `/Applications`。

或者，要清理Mac上的内部应用程序缓存并卸载该应用程序，您可以在终端中执行以下命令：
`/Applications/Adobe Experience Manager Desktop/Contents/Resources/uninstall-osx/uninstall.sh`
