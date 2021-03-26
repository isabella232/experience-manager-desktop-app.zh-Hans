---
title: ' [!DNL Adobe Experience Manager] 桌面应用程序的最佳实践和疑难解答'
description: 按照最佳实践和疑难解答解决与安装、升级、配置等相关的偶发问题。
translation-type: tm+mt
source-git-commit: 9d90bdcab79604e03d1ad3f30ed2aca2eb03e1c5
workflow-type: tm+mt
source-wordcount: '2110'
ht-degree: 0%

---


# [!DNL Adobe Experience Manager]桌面应用程序{#troubleshoot-v2}疑难解答

[!DNL Adobe Experience Manager] 桌面应用程序连 [!DNL Experience Manager] 接到部署的数字资产管理(DAM)存储库。应用程序会在您的计算机上获取存储库信息和搜索结果，并下载和上传文件和文件夹，并包含管理与资产用户界面冲突的功能。

阅读应用程序疑难解答、了解最佳实践并找出其限制。

## 最佳实践{#best-practices-to-prevent-troubles}

遵循以下最佳做法，防止出现一些常见问题和疑难解答。

* **了解桌面应用程序的工作方式**:开始使用应用程序之前，请花些时间了解应用程序的工作方式。了解[!DNL Experience Manager] Web界面与桌面、存储库映射、资产缓存、本地保存和后台上传之间的链接。 请参见[其工作方式](release-notes.md#how-app-works)。

* **避免文件夹名称中不支持的字符**:创建或上载文件夹时，请勿使用空格和无效字符。请参阅[ [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.html#creating-folders)中创建文件夹的列表。 某些[!DNL Experience Manager]用例可能会受到文件夹名称中不受支持的字符的影响。

* **避免冲突的最佳实践**:要避免在协作处理多个资产时发生潜在冲突，请参阅 [避免编辑冲突](using.md#adv-workflow-collaborate-avoid-conflicts)。

* **将文件夹上传用于大型分层文件夹**:使用桌面应用程序上传大型文件夹，而不是使 [!DNL Experience Manager] 用资产Web界面或其他方法。应用程序通过日志记录和监视功能在后台上传资产。 请参阅[批量上传资产](using.md#bulk-upload-assets)。

* **使用最新版本**:使用最新的应用程序版本，在安装新应用程序版本或升级到较新版本之前，请始终检查是否 [!DNL Experience Manager] 兼容。请参阅[发行说明](release-notes.md)。

* **使用相同的驱动器号**:在整个组织中使用相同的驱动器盘符映射 [!DNL Experience Manager] 到DAM。要查看其他用户放置的资产，路径必须相同。 使用相同的驱动器盘符可确保DAM资产的路径一致。 即使不同用户使用不同的驱动器号，资源仍会保持放置状态且不会被删除。

* **注意网络**:网络性能是桌面应 [!DNL Experience Manager] 用程序性能的关键。如果您遇到文件传输或批量操作响应较慢的问题，请关闭可能导致大量网络流量的功能或应用程序。

* **桌面应用程序不支持的用例**:请勿将应用程序用于资产迁移（需要规划和其他工具）；（如移动大文件夹、大型上传、使用高级元数据搜索查找文件）；作为同步客户端(设计原则和使用模式不同于同步客户端，如Microsoft OneDrive或Adobe Creative Cloud桌面同步)。

* **超时**:目前，桌面应用程序没有可配置的超时值，该值会在固定时间间隔后断开服 [!DNL Experience Manager] 务器与桌面应用程序之间的连接。上传大型资产时，如果连接在一段时间后超时，应用程序会重试通过增加上传超时次数来上传资产。 不推荐更改默认超时设置。

## 如何对{#troubleshooting-prep}进行疑难解答

要解决桌面应用程序问题，请注意以下信息。 此外，如果您选择寻求支持，它还会帮助您更好地向Adobe客户服务部门传达问题。

### 日志文件{#check-log-files-v2}的位置

[!DNL Experience Manager] 桌面应用程序会根据操作系统将其日志文件存储在以下位置：

在 Windows 中：`%LocalAppData%\Adobe\AssetsCompanion\Logs`

在Mac上：`~/Library/Logs/Adobe\ Experience\ Manager\ Desktop`

上传多个资产时，如果某些文件无法上传，请参阅`backend.log`文件以标识失败的上传。

>[!NOTE]
>
>与Adobe客户关怀团队协作处理支持请求或票证时，可能会要求您共享日志文件以帮助客户关怀团队了解问题。 将整个`Logs`文件夹存档，并与客户关怀联系人共享。

### 更改日志文件{#level-of-details-in-log}中的详细信息级别

要更改日志文件中的详细信息级别：

1. 确保应用程序未运行。

1. 在Windows系统上：

   1. 打开命令窗口。

   1. 通过运行以下命令启动[!DNL Adobe Experience Manager]桌面应用程序：

   ```shell
   set AEM_DESKTOP_LOG_LEVEL=DEBUG&"C:\Program Files\Adobe\Adobe Experience Manager Desktop.exe
   ```

   在Mac系统上：

   1. 打开终端窗口。

   1. 通过运行以下命令启动[!DNL Adobe Experience Manager]桌面应用程序：

   ```shell
   AEM_DESKTOP_LOG_LEVEL=DEBUG open /Applications/Adobe\ Experience\ Manager\ Desktop.app
   ```

有效的日志级别为DEBUG、INFO、WARN或ERROR。 在DEBUG中日志的详细程度最高，在ERROR中最低。

### 启用调试模式{#enable-debug-mode}

要进行疑难解答，您可以启用调试模式并在日志中获取更多信息。

>[!NOTE]
>
>有效日志级别为DEBUG、INFO、WARN或ERROR。 在DEBUG中日志的详细程度最高，在ERROR中最低。

要在Mac上的调试模式下使用应用程序，请执行以下操作：

1. 打开终端窗口或命令提示符。

1. 运行以下命令启动[!DNL Experience Manager]桌面应用程序：

   `AEM_DESKTOP_LOG_LEVEL=DEBUG open /Applications/Adobe\ Experience\ Manager\ Desktop.app`。

要在Windows上启用调试模式，请执行以下操作：

1. 打开命令窗口。

1. 运行以下命令启动[!DNL Experience Manager]桌面应用程序：

`AEM_DESKTOP_LOG_LEVEL=DEBUG&"C:\Program Files\Adobe\Adobe Experience Manager Desktop.exe`。

### 清除缓存 {#clear-cache-v2}

执行以下步骤：

1. 开始应用程序并连接[!DNL Experience Manager]实例。

1. 单击右上角的省略号并选择[!UICONTROL Preferences]，打开应用程序的首选项。

1. 找到显示[!UICONTROL Current Cache Size]的条目。 单击此元素旁边的垃圾桶图标。

要手动清除缓存，请继续执行以下步骤。

>[!CAUTION]
>
>这是一个潜在的破坏性操作。 如果有未上载到[!DNL Adobe Experience Manager]的本地文件更改，则继续操作将丢失这些更改。

通过删除应用程序的缓存目录清除缓存，该目录位于应用程序的首选项中。

1. 开始应用程序。

1. 选择右上角的省略号并选择[!UICONTROL Preferences]，打开应用程序的首选项。

1. 记下[!UICONTROL Cache Directory]值。

   在此目录中，有以编码[!DNL Adobe Experience Manager]终结点命名的子目录。 名称是目标[!DNL Adobe Experience Manager] URL的编码版本。 例如，如果应用程序针对`localhost:4502`，则目录名称将为`localhost_4502`。

要清除缓存，请删除所需的Encoded [!DNL Adobe Experience Manager] Endpoint目录。 或者，删除首选项中指定的整个目录将清除应用程序已使用的所有实例的缓存。

清除[!DNL Adobe Experience Manager]桌面应用程序缓存是可解决多个问题的初步疑难解答任务。 从应用程序首选项中清除缓存。 请参阅[设置首选项](install-upgrade.md#set-preferences)。 缓存文件夹的默认位置为：

### 了解[!DNL Adobe Experience Manager]桌面应用程序版本{#know-app-version-v2}

要查看版本号：

1. 开始应用程序。

1. 单击右上角的省略号，将指针悬停在[!UICONTROL Help]上，然后单击[!UICONTROL About]。

   版本号列在此屏幕上。

### 无法查看已放置的资源{#placed-assets-missing}

如果您或其他创意专业人士无法在支持文件（例如INDD文件）中看到放置的资源，请检查以下内容：

* 连接到服务器。 不稳定的网络连接可能会阻止资源下载。

* 文件大小。 下载和显示大型资源需要更长时间。

* 驱动字母一致性。 如果您或其他协作者在将[!DNL Experience Manager] DAM映射到其他驱动器盘符时放置了资源，则不会显示放置的资源。

* 权限. 要检查您是否具有获取已放置资产的权限，请与[!DNL Experience Manager]管理员联系。

### 对桌面应用程序用户界面上的文件所做的编辑不会立即反映在[!DNL Adobe Experience Manager]中{#changes-on-da-not-visible-on-aem}

[!DNL Adobe Experience Manager] 桌面应用程序留给用户决定何时完成对文件的所有编辑。根据文件的大小和复杂性，将新版本文件传输回[!DNL Adobe Experience Manager]需要大量时间。 应用程序的设计要求最大限度地减少文件来回传输的次数，而不是猜测文件编辑何时完成并自动上传。 建议用户选择上载文件的更改，以启动将文件传回[!DNL Adobe Experience Manager]的过程。

### 在macOS {#issues-when-upgrading-on-macos}上升级时的问题

在macOS上升级[!DNL Experience Manager]桌面应用程序时，偶尔会出现问题。 这是由于[!DNL Experience Manager]桌面应用程序的旧系统文件夹阻止正确加载新版本的[!DNL Experience Manager]桌面应用程序而导致的。 要解决此问题，可以手动删除以下文件夹和文件。

在执行以下步骤之前，将`Adobe Experience Manager Desktop`应用程序从macOS Applications文件夹拖到垃圾桶。 然后打开终端，执行以下命令，并在出现提示时提供您的密码。

```shell
sudo rm -rf ~/Library/Application\ Support/com.adobe.aem.desktop
sudo rm -rf ~/Library/Preferences/com.adobe.aem.desktop.plist
sudo rm -rf ~/Library/Logs/Adobe\ Experience\ Manager\ Desktop

sudo find /var/folders -type d -name "com.adobe.aem.desktop" | xargs rm -rf
sudo find /var/folders -type d -name "com.adobe.aem.desktop.finderintegration-plugin" | xargs rm -rf
```

### 无法上载文件{#upload-fails}

如果您使用的桌面应用程序具有[!DNL Experience Manager] 6.5.1或更高版本，请将S3或Azure连接器升级到版本1.10.4或更高版本。 它解决了与[OAK-8599](https://issues.apache.org/jira/browse/OAK-8599)相关的文件上载失败问题。 请参阅[安装说明](install-upgrade.md#install-v2)。

### [!DNL Experience Manager] 桌面应用程序连接问题  {#connection-issues}

如果您遇到一般连接问题，请通过以下方式获取有关[!DNL Experience Manager]桌面应用程序正在执行的操作的更多信息。

**检查请求日志**

[!DNL Experience Manager] 桌面应用程序将其发送的所有请求以及每个请求的响应代码记录在一个专用日志文件中。

1. 打开应用程序日志目录中的`request.log`以查看这些请求。

1. 日志中的每一行都表示请求或响应。 请求将具有`>`字符，后跟请求的URL。 响应后面将有一个`<`字符，后跟响应代码和请求的URL。 可以使用每行的GUID匹配请求和响应。

**检查应用程序的嵌入式浏览器加载的请求**

应用程序的大多数请求都位于请求日志中。 但是，如果那里没有有用的信息，那么查看应用程序的嵌入式浏览器发送的请求可能会很有用。
有关如何视图这些请求的说明，请参阅[ SAML部分](#da-connection-issue-with-saml-aem)。

#### SAML登录身份验证无法运行{#da-connection-issue-with-saml-aem}

[!DNL Experience Manager] 桌面应用程序无法连接到您的启用SSO(SAML)的 [!DNL Adobe Experience Manager] 部署。应用程序的设计尝试适应SSO连接和进程的不同和复杂性。 但是，安装程序可能需要其他疑难解答。

有时，SAML进程不会重定向回最初请求的路径，或最终重定向到与[!DNL Adobe Experience Manager]桌面应用程序中配置的主机不同的主机。 要验证情况并非如此：

1. 打开Web浏览器。 访问`https://[aem_server]:[port]/content/dam.json` URL。

1. 登录到[!DNL Adobe Experience Manager]部署。

1. 登录完成后，查看地址栏中浏览器的当前地址。 它应与最初输入的URL完全匹配。

1. 另外，请验证`/content/dam.json`之前的所有项是否与[!DNL Adobe Experience Manager]桌面应用程序设置中配置的目标[!DNL Adobe Experience Manager]值相匹配。

**根据上述步骤，登录SAML进程可以正确工作，但用户仍无法登录**

显示登录过程的[!DNL Adobe Experience Manager]桌面应用程序中的窗口只是显示目标[!DNL Adobe Experience Manager]实例的Web用户界面的Web浏览器：

* Mac版本使用[WebView](https://developer.apple.com/documentation/webkit/webview)。

* Windows版本使用基于Chromium的[CefSharp](https://cefsharp.github.io/)。

确保SAML进程支持这些浏览器。

要进一步排除故障，可以视图浏览器正尝试加载的确切URL。 要查看此信息：

1. 按照[调试模式](#enable-debug-mode)中启动应用程序的说明操作。

1. 重制登录尝试。

1. 导航到应用程序的[日志目录](#check-log-files-v2)

1. 对于Windows:

   1. 打开“aemcompanionlog.txt”。

   1. 搜索以“登录浏览器地址已更改为”开头的消息。 这些条目还包含应用程序加载的URL。

   对于Mac:

   1. `com.adobe.aem.desktop-nnnnnnnn-nnnnnn.log`，其中， **** n将替换为最新文件名中的任何数字。

   1. 搜索以“已加载帧”开头的消息。 这些条目还包含应用程序加载的URL。


查看正在加载的URL序列有助于在SAML末尾进行疑难解答，以确定错误内容。

#### SSL配置问题{#ssl-config-v2}

[!DNL Experience Manager]桌面应用程序用于HTTP通信的库采用严格的SSL强制。 有时，连接可能使用浏览器成功，但使用[!DNL Experience Manager]桌面应用程序失败。 要正确配置SSL，请在Apache中安装缺少的中间证书。 请参阅[如何在Apache](https://access.redhat.com/solutions/43575)中安装Intermediate CA证书。

[!DNL Experience Manager]桌面应用程序用于HTTP通信的库利用严格的SSL强制。 因此，在某些情况下，通过浏览器成功的SSL连接在[!DNL Adobe Experience Manager]桌面应用程序中失败。 这很好，因为它鼓励正确配置SSL并提高安全性，但当应用程序无法连接时，这会令人沮丧。

在这种情况下，建议使用一种工具来分析服务器的SSL证书并识别问题，以便更正它们。 有些网站会检查服务器证书的URL。

作为一项临时措施，可以在[!DNL Adobe Experience Manager]桌面应用程序中禁用严格的SSL强制。 这不是推荐的长期解决方案，因为它通过隐藏SSL配置不正确的根本原因来降低安全性。 禁用严格强制：

1. 使用您选择的编辑器编辑应用程序的JavaScript配置文件，该文件（默认情况下）位于以下位置（取决于操作系统）：

   在Mac上：`/Applications/Adobe Experience Manager Desktop.app/Contents/Resources/javascript/lib-smb/config.json`

   在 Windows 中：`C:\Program Files (x86)\Adobe\Adobe Experience Manager Desktop\javascript\config.json`

1. 在文件中找到以下部分：

   ```shell
   ...
   "assetRepository": {
       "options": {
   ...
   ```

1. 通过添加`"strictSSL": false`修改节，如下所示：

   ```shell
   ...
   "assetRepository": {
       "options": {
           "strictSSL": false,
   ...
   ```

1. 保存文件并重新启动[!DNL Adobe Experience Manager]桌面应用程序。

### 应用程序无响应{#unresponsive}

应用程序很少会变得无响应、只显示白屏或在界面底部显示错误，而界面上没有任何选项。 请按顺序尝试以下各项：

* 右键单击应用程序接口，然后单击&#x200B;**[!UICONTROL Refresh]**。
* 退出应用程序并再次打开它。

在这两种方法中，应用程序将开始根DAM文件夹。

<!--
### Need additional help with [!DNL Experience Manager] desktop app {#additional-help}

Create Jira ticket with the following information:

* Use `DAM - Companion App` as the [!UICONTROL Component].

* Detailed steps to reproduce the issue in [!UICONTROL Description].

* DEBUG level logs that were captured while reproducing the issue.

* Target Experience Manager version.

* Operating system version.

* [!DNL Adobe Experience Manager] desktop app version. To know your app version, see [finding the desktop app version](#know-app-version-v2).
-->

>[!MORELIKETHIS]
>
>* [已知问题](release-notes.md#known-issues-v2)
>* [避免编辑冲突](using.md#adv-workflow-collaborate-avoid-conflicts)

