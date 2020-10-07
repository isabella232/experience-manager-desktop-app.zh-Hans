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
source-git-commit: a7a334df5eaa2b8a8d0412bff1ed2a47d39ca1a2
workflow-type: tm+mt
source-wordcount: '2230'
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

### 日志文件的位置 {#check-log-files-v2}

[!DNL Experience Manager] 桌面应用程序根据操作系统将其日志文件存储在以下位置：

在 Windows 中：`%LocalAppData%\Adobe\AssetsCompanion\Logs`

在Mac上： `~/Library/Logs/Adobe\ Experience\ Manager\ Desktop`

上传多个资产时，如果某些文件无法上传，请查 `backend.log` 看文件以识别上传失败。

>[!NOTE]
>
>在与Adobe客户关怀团队协作处理支持请求或票证时，可要求您共享日志文件，以帮助客户关怀团队了解问题。 存档整个文 `Logs` 件夹，并与客户关怀联系人共享它。

### 更改日志文件中的详细信息级别 {#level-of-details-in-log}

要更改日志文件中的详细信息级别：

1. 确保应用程序未运行。

1. 在Windows系统上：

   1. 打开命令窗口。

   1. 通过 [!DNL Adobe Experience Manager] 运行以下命令启动桌面应用程序：

   ```shell
   set AEM_DESKTOP_LOG_LEVEL=DEBUG&"C:\Program Files\Adobe\Adobe Experience Manager Desktop.exe
   ```

   在Mac系统上：

   1. 打开终端窗口。

   1. 通过 [!DNL Adobe Experience Manager] 运行以下命令启动桌面应用程序：

   ```shell
   AEM_DESKTOP_LOG_LEVEL=DEBUG open /Applications/Adobe\ Experience\ Manager\ Desktop.app
   ```

有效日志级别为DEBUG、INFO、WARN或ERROR。 在DEBUG中日志的详细程度最高，在ERROR中最低。

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

### 清除缓存 {#clear-cache-v2}

执行以下步骤：

1. 开始应用程序并连接AEM实例。

1. 单击右上角的省略号并选择，打开应用程序的首选项 [!UICONTROL Preferences]。

1. 找到显示的条目 [!UICONTROL Current Cache Size]。 单击此元素旁边的垃圾桶图标。

要手动清除缓存，请继续执行以下步骤。

>[!CAUTION]
>
>这可能是破坏性操作。 如果有未上载到的本地文件更改， [!DNL Adobe Experience Manager]则这些更改将通过继续操作丢失。

通过删除应用程序的缓存目录清除缓存，该目录位于应用程序的首选项中。

1. 开始应用程序。

1. 通过选择右上角的省略号并选择，打开应用程序的首选项 [!UICONTROL Preferences]。

1. 记下该 [!UICONTROL Cache Directory] 值。

   在此目录中，有以编码端点命名的子 [!DNL Adobe Experience Manager] 目录。 名称是目标URL的编码版 [!DNL Adobe Experience Manager] 本。 例如，如果应用程序正在定 `localhost:4502` 位，则目录名称将 `localhost_4502`为。

要清除缓存，请删除所需的“已编码端点” [!DNL Adobe Experience Manager] 目录。 或者，删除首选项中指定的整个目录将清除应用程序已使用的所有实例的缓存。

清除 [!DNL Adobe Experience Manager]]桌面应用程序的缓存是可解决多个问题的初步疑难解答任务。 从应用程序首选项中清除缓存。 请参阅 [设置首选项](install-upgrade.md#set-preferences)。 缓存文件夹的默认位置为：

### 了解桌面应 [!DNL Adobe Experience Manager] 用程序版本 {#know-app-version-v2}

要查看版本号：

1. 开始应用程序。

1. 单击右上角的椭圆，将指针悬停在上 [!UICONTROL Help]方，然后单击 [!UICONTROL About]。

   版本号列在此屏幕上。

### 无法查看已放置的资产 {#placed-assets-missing}

如果您或其他创意专业人士无法在支持文件（例如INDD文件）中看到放置的资源，请检查以下各项：

* 与服务器连接。 不稳定的网络连接可能会阻止资源下载。

* 文件大小。 下载和显示大型资源需要更长的时间。

* 驱动器盘符一致性。 如果您或其他协作者在将AEM DAM映射到其他驱动器号时放置了资源，则不会显示放置的资源。

* 权限. 要检查您是否有权获取置入的资产，请与AEM管理员联系。

### 对桌面应用程序用户界面上的文件所做的编辑不会立即反映 [!DNL Adobe Experience Manager] 在 {#changes-on-da-not-visible-on-aem}

[!DNL Adobe Experience Manager] 桌面应用程序将由用户决定何时完成对文件的所有编辑。 根据文件的大小和复杂性，将新版本的文件传输回文件需要花费大量时间 [!DNL Adobe Experience Manager]。 应用程序的设计要求最大限度地减少文件来回传输的次数，而不是猜测文件编辑何时完成并自动上传。 建议用户选择上传文件的更改， [!DNL Adobe Experience Manager] 以启动将文件传回的过程。

### 在macOS上升级时的问题 {#issues-when-upgrading-on-macos}

在macOS上升级AEM桌面应用程序时，偶尔会发生问题。 这是由于AEM桌面应用程序的旧系统文件夹阻止新版本的AEM桌面应用程序正确加载导致的。 要解决此问题，可以手动删除以下文件夹和文件。

在执行以下步骤之前，将应 `Adobe Experience Manager Desktop` 用程序从macOS Applications文件夹拖到垃圾桶。 然后打开终端，执行以下命令，并在出现提示时提供密码。

```shell
sudo rm -rf ~/Library/Application\ Support/com.adobe.aem.desktop
sudo rm -rf ~/Library/Preferences/com.adobe.aem.desktop.plist
sudo rm -rf ~/Library/Logs/Adobe\ Experience\ Manager\ Desktop

sudo find /var/folders -type d -name "com.adobe.aem.desktop" | xargs rm -rf
sudo find /var/folders -type d -name "com.adobe.aem.desktop.finderintegration-plugin" | xargs rm -rf
```

### 无法上传文件 {#upload-fails}

如果您正在将桌面应用程序与AEM 6.5.1或更高版本一起使用，请将S3或Azure连接器升级到版本1.10.4或更高版本。 它解决了与OAK-8599相关的文件 [上传失败问题](https://issues.apache.org/jira/browse/OAK-8599)。 请参 [阅安装说明](install-upgrade.md#install-v2)。

### [!DNL Experience Manager] 桌面应用程序连接问题 {#connection-issues}

如果您遇到一般连接问题，请通过以下一些方法进一步了解桌面应 [!DNL Experience Manager] 用程序的用途。

**检查请求日志**

[!DNL Experience Manager] 桌面应用程序将其发送的所有请求以及每个请求的响应代码记录在专用日志文件中。

1. 在应 `request.log` 用程序的日志目录中打开以查看这些请求。

1. 日志中的每一行表示请求或响应。 请求后面将 `>` 有一个字符，后面跟有请求的URL。 响应后面将 `<` 有一个字符，后跟响应代码和请求的URL。 可以使用每行的GUID匹配请求和响应。

**检查应用程序的嵌入式浏览器加载的请求**

大多数应用程序请求都位于请求日志中。 但是，如果那里没有有用的信息，那么查看应用程序的嵌入式浏览器发送的请求可能会很有用。
有关如 [何视图这](#da-connection-issue-with-saml-aem) 些请求的说明，请参阅SAML部分。

#### SAML登录身份验证无效 {#da-connection-issue-with-saml-aem}

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

#### SSL配置问题 {#ssl-config-v2}

AEM桌面应用程序用于HTTP通信的库采用严格的SSL强制。 有时，连接可能使用浏览器成功，但使用AEM桌面应用程序失败。 要正确配置SSL，请在Apache中安装缺少的中间证书。 请参 [阅如何在Apache中安装Intermediate CA证书](https://access.redhat.com/solutions/43575)。


AEM Desktop用于HTTP通信的库采用严格的SSL强制。 因此，在某些情况下，通过浏览器成功的SSL连接会因桌面应用程序 [!DNL Adobe Experience Manager] 失败而失败。 这很好，因为它鼓励正确配置SSL并提高安全性，但当应用程序无法连接时，这可能会令人沮丧。

在这种情况下，建议使用一种工具来分析服务器的SSL证书并识别问题，以便更正它们。 有一些网站在提供服务器的URL时检查服务器的证书。

作为一项临时措施，可以在桌面应用程序中禁用严格的SSL [!DNL Adobe Experience Manager] 强制实施。 这不是推荐的长期解决方案，因为它通过隐藏配置不正确的SSL的根本原因来降低安全性。 禁用严格强制：

1. 使用您选择的编辑器编辑应用程序的JavaScript配置文件，该文件（默认情况下）位于以下位置（取决于操作系统）:

   在Mac上： `/Applications/Adobe Experience Manager Desktop.app/Contents/Resources/javascript/lib-smb/config.json`

   在 Windows 中：`C:\Program Files (x86)\Adobe\Adobe Experience Manager Desktop\javascript\config.json`

1. 在文件中找到以下部分：

   ```shell
   ...
   "assetRepository": {
       "options": {
   ...
   ```

1. 通过按如下方式添加来 `"strictSSL": false` 修改节：

   ```shell
   ...
   "assetRepository": {
       "options": {
           "strictSSL": false,
   ...
   ```

1. 保存文件并重新启动桌 [!DNL Adobe Experience Manager] 面应用程序。

### 应用程序无响应 {#unresponsive}

应用程序很少会变得无响应、只显示白屏或在界面底部显示错误，而界面上没有任何选项。 按顺序尝试以下各项：

* 右键单击应用程序界面，然后单击 **[!UICONTROL Refresh]**。
* 退出应用程序并再次打开它。

在这两种方法中，应用程序开始在根DAM文件夹。

### 需要有关桌面应用程序的其 [!DNL Experience Manager] 他帮助 {#additional-help}

创建包含以下信息的Jira票证：

* 用 `DAM - Companion App` 作 [!UICONTROL Component]。

* 在中重述问题的详细步骤 [!UICONTROL Description]。

* 重放问题时捕获的调试级别日志。

* 目标AEM版本。

* 操作系统版本。

* [!DNL Adobe Experience Manager] 桌面应用程序版本。 要了解您的应用程序版本，请参 [阅查找桌面应用程序版本](#know-app-version-v2)。

>[!MORELIKETHIS]
>
>* [已知问题](release-notes.md#known-issues-v2)
>* [避免编辑冲突](using.md#adv-workflow-collaborate-avoid-conflicts)

