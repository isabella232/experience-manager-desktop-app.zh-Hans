---
title: Adobe Experience Manager桌面应用程序的最佳实践和疑难解答
description: 按照最佳实践和疑难解答解决与安装、升级、配置等相关的偶发问题。
uuid: ce98a3e7-5454-41be-aaaa-4252b3e0f8dd
contentOwner: AG
products: SG_EXPERIENCEMANAGER/6.5/ASSETS, SG_EXPERIENCEMANAGER/6.4/ASSETS, SG_EXPERIENCEMANAGER/6.3/ASSETS
discoiquuid: f5eb222a-6cdf-4ae3-9cf2-755c873f397c
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 381e586077c7db63dd57a468b1c6abc60c63e34e
workflow-type: tm+mt
source-wordcount: '1537'
ht-degree: 0%

---


# Troubleshoot Adobe Experience Manager desktop app {#troubleshoot-v2}

Adobe Experience Manager(AEM)桌面应用程序连接到远程Experience Manager部署的数字资产管理(DAM)存储库。 应用程序在您的计算机上获取存储库信息和搜索结果，下载并上传文件和文件夹，并包含管理与AEM Assets用户界面冲突的功能。

阅读应用程序疑难解答、了解最佳实践并找出限制。

## Best practices {#best-practices-to-prevent-troubles}

遵循以下最佳实践，防止一些常见问题和疑难解答。

* **了解桌面应用程序的工作方式**:开始使用应用程序之前，请花些时间了解应用程序的工作方式。 了解Experience ManagerWeb界面与桌面之间的链接、存储库映射、资产缓存、本地保存以及后台上传。 了 [解工作方式](release-notes.md#how-app-works)。

* **避免文件夹名称中不支持的字符**:创建或上传文件夹时，请勿使用空格和无效字符。 在列表资产中创建文 [件夹，查看一Experience Manager字符](https://docs.adobe.com/content/help/en/experience-manager-65/assets/managing/managing-assets-touch-ui.html#Creatingfolders)。 某些Adobe Experience Manager用例可能受文件夹名称中不支持的字符影响。

* **避免冲突的最佳实践**:要避免在协作处理多个资产时发生潜在冲突，请参阅 [避免编辑冲突](using.md#adv-workflow-collaborate-avoid-conflicts)。

* **将文件夹上传用于大型分层文件夹**:使用Experience Manager桌面应用程序上传大型文件夹，而不是使用资产Web界面或其他方法。 应用程序通过记录和监视在后台上传资产。 请参阅 [批量上传资产](using.md#bulk-upload-assets)。

* **使用最新版本**:使用最新的应用程序版本，在安装新的应用程序版本或升级到较新的Adobe Experience Manager版本之前，始终检查兼容性。 See [release notes](release-notes.md).

* **使用相同的驱动器号**:在整个组织中使用相同的驱动器号映射到Adobe Experience ManagerDAM。 要查看其他用户放置的资产，路径必须相同。 使用相同的驱动器号可确保DAM资产的路径不变。 即使不同用户使用不同的驱动器盘符，资源仍会保持放置状态并且不会被删除。

* **注意网络**:网络性能对Experience Manager桌面应用程序的性能至关重要。 如果对文件传输或批量操作的响应速度较慢，请关闭可能导致大量网络流量的功能或应用程序。

* **桌面应用程序不支持的用例**:请勿将应用程序用于资产迁移（它需要规划和其他工具）;执行繁重的DAM操作（如移动大文件夹、大型上传、使用高级元数据搜索查找文件）;同步客户端(设计原则和使用模式与同步客户端(如Microsoft OneDrive或Adobe Creative Cloud桌面同步)不同。

* **超时**:当前，桌面应用程序没有可配置的超时值，该值在固定时间间隔后会断开Experience Manager服务器与桌面应用程序之间的连接。 上传大型资产时，如果连接在一段时间后超时，应用程序会重试通过增加上传超时来上传资产几次。 不推荐更改默认超时设置。

## 如何进行疑难解答 {#troubleshooting-prep}

要解决桌面应用程序问题，请注意以下信息。 此外，如果您选择寻求支持，它还会帮助您更好地向Adobe客户服务部门传达问题。

### 启用调试模式 {#enable-debug-mode}

要进行疑难解答，您可以启用调试模式并在日志中获取更多信息。

>[!NOTE]
>
>有效日志级别为DEBUG、INFO、WARN或ERROR。 在DEBUG中日志的详细程度最高，在ERROR中最低。

要在Mac上的调试模式下使用应用程序，请执行以下操作：

1. 打开终端窗口或命令提示符。

1. 通过运行 [!DNL Experience Manager] 以下命令启动桌面应用程序：

   `AEM_DESKTOP_LOG_LEVEL=DEBUG open /Applications/Adobe\ Experience\ Manager\ Desktop.app`。

要在Windows上启用调试模式：

1. 打开命令窗口。

1. 运行 [!DNL Experience Manager] 以下命令启动桌面应用程序：

`AEM_DESKTOP_LOG_LEVEL=DEBUG&"C:\Program Files\Adobe\Adobe Experience Manager Desktop.exe`。

### 日志文件的位置 {#check-log-files-v2}

[!DNL Experience Manager] 桌面应用程序根据操作系统将其日志文件存储在以下位置：

在 Windows 中：`%LocalAppData%\Adobe\AssetsCompanion\Logs`

在Mac上： `~/Library/Logs/Adobe\ Experience\ Manager\ Desktop`

上传多个资产时，如果某些文件无法上传，请查 `backend.log` 看文件以识别上传失败。

>[!NOTE]
>
>在与Adobe客户关怀团队协作处理支持请求或票证时，可要求您共享日志文件，以帮助客户关怀团队了解问题。 存档整个文 `Logs` 件夹，并与客户关怀联系人共享它。

### 清除缓存 {#clear-cache-v2}

清除AEM桌面应用程序缓存是可解决多个问题的初步故障诊断任务。 从应用程序首选项中清除缓存。 请参阅 [设置首选项](install-upgrade.md#set-preferences)。 缓存文件夹的默认位置为：

* 在 Windows 中：`%LocalAppData%\Adobe\AssetsCompanion\Cache\`

* 在Mac上： `~/Library/Group/Containers/group.com.adobe.aem.desktop/cache/`

但是，位置可能会因AEM桌面配置的AEM端点而发生更改。 该值是目标URL的编码版本。 例如，如果应用程序正在定 `http://localhost:4502`位，则目录名称为 `http%3A%2F%2Flocalhost%3A4502%2F`。 要清除缓存，请删除相应的文件夹。 清除缓存的另一个原因是当磁盘空间不足时释放磁盘空间。

>[!CAUTION]
>
>如果清除AEM桌面缓存，则不同步到AEM服务器的本地资产修改将不可撤消地丢失。

### 了解AEM桌面应用程序版本 {#know-app-version-v2}

单击 ![“应用程序](assets/do-not-localize/more_options_da2.png) ”菜单以打开应用程序菜单，然后单击 **[!UICONTROL Help]** > **[!UICONTROL About]**。

## 无法查看已放置的资产 {#placed-assets-missing}

如果您或其他创意专业人士无法在支持文件（例如INDD文件）中看到放置的资源，请检查以下各项：

* 与服务器连接。 不稳定的网络连接可能会阻止资源下载。
* 文件大小。 下载和显示大型资源需要更长的时间。
* 驱动器盘符一致性。 如果您或其他协作者在将AEM DAM映射到其他驱动器号时放置了资源，则不会显示放置的资源。
* 权限. 要检查您是否有权获取置入的资产，请与AEM管理员联系。

## 在macOS上升级时的问题 {#issues-when-upgrading-on-macos}

在macOS上升级AEM桌面应用程序时，偶尔会发生问题。 这是由于AEM桌面应用程序的旧系统文件夹阻止新版本的AEM桌面应用程序正确加载导致的。 要解决此问题，可以手动删除以下文件夹和文件。

在执行以下步骤之前，将应 `Adobe Experience Manager Desktop` 用程序从macOS Applications文件夹拖到垃圾桶。 然后打开终端，执行以下命令，并在出现提示时提供密码。

```shell
sudo rm -rf ~/Library/Application\ Support/com.adobe.aem.desktop
sudo rm -rf ~/Library/Preferences/com.adobe.aem.desktop.plist
sudo rm -rf ~/Library/Logs/Adobe\ Experience\ Manager\ Desktop

sudo find /var/folders -type d -name "com.adobe.aem.desktop" | xargs rm -rf
sudo find /var/folders -type d -name "com.adobe.aem.desktop.finderintegration-plugin" | xargs rm -rf
```

## 无法上传文件 {#upload-fails}

如果您正在将桌面应用程序与AEM 6.5.1或更高版本一起使用，请将S3或Azure连接器升级到版本1.10.4或更高版本。 它解决了与OAK-8599相关的文件 [上传失败问题](https://issues.apache.org/jira/browse/OAK-8599)。 请参 [阅安装说明](install-upgrade.md#install-v2)。

## [!DNL Experience Manager] 桌面应用程序连接问题 {#connection-issues}

### SAML登录身份验证无效 {#da-connection-issue-with-saml-aem}

如果 [!DNL Experience Manager] 桌面应用程序未连接到启用SSO(SAML)的实例 [!DNL Adobe Experience Manager] ，请阅读本节以进行疑难解答。 SSO过程多种多样，有时也很复杂，应用程序的设计尽其所能来适应这些类型的连接。 但是，某些设置需要额外的疑难解答。

有时SAML进程不会重定向回最初请求的路径，或者最终重定向到的主机与桌面应用程序中配置的主机 [!DNL Adobe Experience Manager] 不同。 要验证情况并非如此：

1. 打开Web浏览器。

1. 在地址 `<AEM host>/content/dam.json` 栏中输入URL。

   例 `<AEM host>` 如，用目标 [!DNL Adobe Experience Manager] 实例替换 `http://localhost:4502/content/dam.json`。

1. 登录到实 [!DNL Adobe Experience Manager] 例。

1. 登录完成后，在地址栏中查看浏览器的当前地址。 它应与最初输入的URL完全匹配。

1. 另外，验证之前的所 `/content/dam.json` 有内容是否 [!DNL Adobe Experience Manager] 与桌面应用 [!DNL Adobe Experience Manager] 程序设置中配置的目标值匹配。

**根据上述步骤，登录SAML进程可以正常工作，但用户仍无法登录**

显示登录 [!DNL Adobe Experience Manager] 过程的桌面应用程序内的窗口只是显示目标实例的Web [!DNL Adobe Experience Manager] 用户界面的Web浏览器：

* Mac版本使用 [WebView](https://developer.apple.com/documentation/webkit/webview)。

* Windows版本使用基于Chromium的 [CefSharp](https://cefsharp.github.io/)。

确保SAML进程支持这些浏览器。

要进一步进行疑难解答，可以视图浏览器正尝试加载的确切URL。 要查看此信息：

1. 按照在调试模式下启动应用程 [序的指示](#enable-debug-mode)。

1. 重现登录尝试。

1. 导航到应 [用程序](#check-log-files-v2) 的日志目录

1. 对于Windows:

   1. 打开“aemcompanionlog.txt”。

   1. 搜索以“登录浏览器地址已更改为”开头的消息。 这些条目还包含应用程序加载的URL。

   对于Mac:

   1. `com.adobe.aem.desktop-nnnnnnnn-nnnnnn.log`，其中 **n** 被最新文件名中的数字替换。

   1. 搜索以“已加载帧”开头的消息。 这些条目还包含应用程序加载的URL。


查看正在加载的URL序列有助于在SAML结尾进行疑难解答，以确定错误。

### SSL配置问题 {#ssl-config-v2}

AEM桌面应用程序用于HTTP通信的库采用严格的SSL强制。 有时，连接可能使用浏览器成功，但使用AEM桌面应用程序失败。 要正确配置SSL，请在Apache中安装缺少的中间证书。 请参 [阅如何在Apache中安装Intermediate CA证书](https://access.redhat.com/solutions/43575)。

## 应用程序无响应 {#unresponsive}

应用程序很少会变得无响应、只显示白屏或在界面底部显示错误，而界面上没有任何选项。 按顺序尝试以下各项：

* 右键单击应用程序界面，然后单击 **[!UICONTROL Refresh]**。
* 退出应用程序并再次打开它。

在这两种方法中，应用程序开始在根DAM文件夹。

>[!MORELIKETHIS]
>
>* [已知问题](release-notes.md#known-issues-v2)
>* [避免编辑冲突](using.md#adv-workflow-collaborate-avoid-conflicts)

