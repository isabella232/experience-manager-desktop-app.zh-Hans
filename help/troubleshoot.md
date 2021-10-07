---
title: ' [!DNL Adobe Experience Manager] 桌面应用程序的最佳实践和疑难解答'
description: 按照最佳实践和疑难解答，解决与安装、升级、配置等相关的偶发问题。
exl-id: f388e4ac-907d-4093-ba6f-86ecdafeb015
source-git-commit: 2c846fb9cd82691f6439e93429dffcca8127ba68
workflow-type: tm+mt
source-wordcount: '2260'
ht-degree: 0%

---

# 对[!DNL Adobe Experience Manager]桌面应用程序进行故障诊断 {#troubleshoot-v2}

[!DNL Adobe Experience Manager] 桌面应用程序可连 [!DNL Experience Manager] 接到部署的数字资产管理(DAM)存储库。该应用程序会在您的计算机上获取存储库信息和搜索结果，并下载和上传文件和文件夹，同时还包含用于管理与Assets用户界面冲突的功能。

请阅读并排查应用程序问题，了解最佳实践，并找出限制。

## 最佳实践 {#best-practices-to-prevent-troubles}

遵循以下最佳实践，以防止出现一些常见问题和疑难解答。

* **了解桌面应用程序的工作方式**:在开始使用应用程序之前，请花些时间了解应用程序的工作方式。了解[!DNL Experience Manager] Web界面与桌面之间的链接、存储库映射、资产缓存、本地保存以及后台上传。 请参阅[其工作方式](release-notes.md#how-app-works)。

* **避免文件夹名称中不支持的字符**:创建或上载文件夹时，请勿使用空格和无效字符。请参阅[在 [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.html#creating-folders)中创建文件夹中的字符列表。 某些[!DNL Experience Manager]用例可能会受到文件夹名称中不支持的字符的影响。

* **避免冲突的最佳实践**:要避免在协作处理多个资产时出现潜在冲突，请参阅 [避免编辑冲突](using.md#adv-workflow-collaborate-avoid-conflicts)。

* **对大型分层文件夹使用文件夹上传**:使用桌面应用程序上传大型文件夹，而不是使用资产Web界 [!DNL Experience Manager] 面或其他方法。应用程序会通过日志记录和监控在后台上传资产。 请参阅[批量上传资产](using.md#bulk-upload-assets)。

* **使用最新版本**:在安装新应用程序版本之前或升级到新版本之前，请使用最新版本并始终检查兼容性 [!DNL Experience Manager] 。请参阅[发行说明](release-notes.md)。

* **使用相同的驱动器号**:在组织内使用相同的驱动器号来映射到 [!DNL Experience Manager] DAM。要查看其他用户放置的资产，路径必须相同。 使用相同的驱动器号可确保DAM资产的常量路径。 即使不同用户使用不同的驱动器号，资产仍会保持放置状态，并且不会被删除。

* **注意网络**:网络性能对桌面应用 [!DNL Experience Manager] 程序的性能至关重要。如果文件传输或批量操作响应速度减慢，请关闭可能导致大量网络流量的功能或应用程序。

* **桌面应用程序不支持的用例**:请勿将应用程序用于资产迁移（需要规划和其他工具）；（例如，移动大文件夹、大上传、使用高级元数据搜索查找文件）；和作为同步客户端(设计原则和使用模式与Microsoft OneDrive或Adobe Creative Cloud桌面同步等同步客户端不同)。

* **超时**:目前，桌面应用程序没有可配置的超时值，该值会在固定时间间隔后断开服 [!DNL Experience Manager] 务器与桌面应用程序之间的连接。在上传大型资产时，如果连接在一段时间后超时，应用程序会重试几次，以增加上传超时时间，从而上传资产。 没有建议的方法来更改默认超时设置。

## 如何进行故障诊断 {#troubleshooting-prep}

要解决桌面应用程序问题，请注意以下信息。 此外，如果您选择寻求支持，它还可以让您更好地将问题传达给Adobe客户支持。

### 日志文件的位置 {#check-log-files-v2}

[!DNL Experience Manager] 桌面应用程序会根据操作系统将其日志文件存储在以下位置：

在 Windows 中：`%LocalAppData%\Adobe\AssetsCompanion\Logs`

在Mac:`~/Library/Logs/Adobe\ Experience\ Manager\ Desktop`

在上传多个资产时，如果某些文件无法上传，请参阅`backend.log`文件以识别上传失败的内容。

>[!NOTE]
>
>在与Adobe客户支持部门就支持请求或票证合作时，可能会要求您共享日志文件，以帮助客户支持团队了解问题。 存档整个`Logs`文件夹，并将其与您的客户支持联系人共享。

### 更改日志文件中的详细信息级别 {#level-of-details-in-log}

要更改日志文件中的详细信息级别，请执行以下操作：

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

有效的日志级别为“调试”、“信息”、“警告”或“错误”。 日志的详细程度在DEBUG中最高，在ERROR中最低。

### 启用调试模式 {#enable-debug-mode}

要进行故障诊断，您可以启用调试模式并在日志中获取更多信息。

>[!NOTE]
>
>有效的日志级别为“调试”、“信息”、“警告”或“错误”。 日志的详细程度在DEBUG中最高，在ERROR中最低。

要在Mac的调试模式下使用应用程序，请执行以下操作：

1. 打开终端窗口或命令提示符。

1. 通过运行以下命令启动[!DNL Experience Manager]桌面应用程序：

   `AEM_DESKTOP_LOG_LEVEL=DEBUG open /Applications/Adobe\ Experience\ Manager\ Desktop.app`。

要在Windows上启用调试模式，请执行以下操作：

1. 打开命令窗口。

1. 通过运行以下命令启动[!DNL Experience Manager]桌面应用程序：

`AEM_DESKTOP_LOG_LEVEL=DEBUG&"C:\Program Files\Adobe\Adobe Experience Manager Desktop.exe`。

### 了解[!DNL Adobe Experience Manager]桌面应用程序版本 {#know-app-version-v2}

要查看版本号，请执行以下操作：

1. 启动应用程序。

1. 单击右上角的省略号，将鼠标悬停在[!UICONTROL Help]上，然后单击[!UICONTROL About]。

   此屏幕上列出了版本号。

### 清除缓存 {#clear-cache-v2}

执行以下步骤：

1. 启动应用程序并连接[!DNL Experience Manager]实例。

1. 单击右上角的省略号并选择[!UICONTROL Preferences]以打开应用程序的首选项。

1. 找到显示[!UICONTROL Current Cache Size]的条目。 单击此元素旁边的垃圾桶图标。

要手动清除缓存，请继续执行以下步骤。

>[!CAUTION]
>
>这是一项潜在的破坏性操作。 如果存在未上传到[!DNL Adobe Experience Manager]的本地文件更改，则继续操作会丢失这些更改。

通过删除应用程序的缓存目录清除缓存，该目录可在应用程序的首选项中找到。

1. 启动应用程序。

1. 选择右上角的省略号，然后选择[!UICONTROL Preferences]，打开应用程序的首选项。

1. 记下[!UICONTROL Cache Directory]值。

   在此目录中，有以编码的[!DNL Adobe Experience Manager]端点命名的子目录。 这些名称是目标[!DNL Adobe Experience Manager] URL的编码版本。 例如，如果应用程序的目标为`localhost:4502`，则目录名称将为`localhost_4502`。

要清除缓存，请删除所需的Encoded [!DNL Adobe Experience Manager] Endpoint目录。 或者，如果删除首选项中指定的整个目录，则将清除应用程序已使用的所有实例的缓存。

清除[!DNL Adobe Experience Manager]桌面应用程序的缓存是一项初步的故障诊断任务，可以解决若干问题。 从应用程序首选项中清除缓存。 请参阅[设置首选项](install-upgrade.md#set-preferences)。 缓存文件夹的默认位置为：

## 看不到已放置的资产 {#placed-assets-missing}

如果看不到您或其他创意专业人士放置在支持文件（例如，INDD文件）中的资产，请检查以下内容：

* 与服务器的连接。 不稳定的网络连接可能会阻止资产下载。

* 文件大小。 下载和显示大型资产需要较长时间。

* 驱动器号一致性。 如果您或其他协作者在将[!DNL Experience Manager] DAM映射到其他驱动器盘符时放置了资产，则不会显示放置的资产。

* 权限. 要检查您是否有权获取已放置的资产，请联系[!DNL Experience Manager]管理员。

### 对桌面应用程序用户界面上文件所做的编辑不会立即反映在[!DNL Adobe Experience Manager]中 {#changes-on-da-not-visible-on-aem}

[!DNL Adobe Experience Manager] 桌面应用程序将由用户自行决定何时完成对文件的所有编辑。根据文件的大小和复杂性，将新版本的文件传输回[!DNL Adobe Experience Manager]需要大量时间。 应用程序的设计要求最大限度地减少文件来回传输的次数，而不是猜测文件编辑何时完成并自动上传。 建议用户通过选择上传文件更改来启动将文件传输回[!DNL Adobe Experience Manager]的过程。

### 在macOS上升级时的问题 {#issues-when-upgrading-on-macos}

在macOS上升级[!DNL Experience Manager]桌面应用程序时，有时可能会出现问题。 这是由于[!DNL Experience Manager]桌面应用程序的旧系统文件夹阻止正确加载新版本的[!DNL Experience Manager]桌面应用程序所致。 要解决此问题，可以手动删除以下文件夹和文件。

在执行以下步骤之前，将`Adobe Experience Manager Desktop`应用程序从“macOS应用程序”文件夹拖到垃圾桶。 然后，打开终端，执行以下命令，并在出现提示时提供您的密码。

```shell
sudo rm -rf ~/Library/Application\ Support/com.adobe.aem.desktop
sudo rm -rf ~/Library/Preferences/com.adobe.aem.desktop.plist
sudo rm -rf ~/Library/Logs/Adobe\ Experience\ Manager\ Desktop

sudo find /var/folders -type d -name "com.adobe.aem.desktop" | xargs rm -rf
sudo find /var/folders -type d -name "com.adobe.aem.desktop.finderintegration-plugin" | xargs rm -rf
```

## 无法上载文件 {#upload-fails}

如果您正在将桌面应用程序与[!DNL Experience Manager] 6.5.1或更高版本一起使用，请将S3或Azure连接器升级到版本1.10.4或更高版本。 它解决了与[OAK-8599](https://issues.apache.org/jira/browse/OAK-8599)相关的文件上传失败问题。 请参阅[安装说明](install-upgrade.md#install-v2)。

## [!DNL Experience Manager] 桌面应用程序连接问题 {#connection-issues}

如果您遇到一般连接问题，请通过以下方式获取有关[!DNL Experience Manager]桌面应用程序正在执行的操作的更多信息。

**检查请求日志**

[!DNL Experience Manager] 桌面应用程序将其发送的所有请求以及每个请求的响应代码记录在专用的日志文件中。

1. 在应用程序的日志目录中打开`request.log`以查看这些请求。

1. 日志中的每一行都表示请求或响应。 请求的URL后面将有一个`>`字符。 响应的字符后面将有`<`字符，后面跟有响应代码和请求的URL。 可以使用每行的GUID匹配请求和响应。

**检查应用程序的嵌入式浏览器加载的请求**

大多数应用程序请求都位于请求日志中。 但是，如果此处没有有用的信息，则查看应用程序嵌入式浏览器发送的请求将会非常有用。
有关如何查看这些请求的说明，请参阅[SAML部分](#da-connection-issue-with-saml-aem)。

### SAML登录身份验证无法正常工作 {#da-connection-issue-with-saml-aem}

[!DNL Experience Manager] 桌面应用程序可能无法连接到启用单点登录(SAML)的部 [!DNL Adobe Experience Manager] 署。该应用程序的设计尝试适应SSO连接和流程的变化和复杂性。 但是，设置可能需要进行其他故障诊断。

有时，SAML进程不会重定向回最初请求的路径，或者最终的重定向是到与[!DNL Adobe Experience Manager]桌面应用程序中配置的不同的主机。 要验证情况并非如此，请执行以下操作：

1. 打开Web浏览器。 访问`https://[aem_server]:[port]/content/dam.json` URL。

1. 登录到[!DNL Adobe Experience Manager]部署。

1. 登录完成后，在地址栏中查看浏览器的当前地址。 它应该与最初输入的URL完全匹配。

1. 另外，请验证`/content/dam.json`之前的所有内容是否与在[!DNL Adobe Experience Manager]桌面应用程序设置中配置的目标[!DNL Adobe Experience Manager]值匹配。

**根据上述步骤，登录SAML过程可以正确运行，但用户仍无法登录**

[!DNL Adobe Experience Manager]桌面应用程序中显示登录过程的窗口，只是显示目标[!DNL Adobe Experience Manager]实例的Web用户界面的Web浏览器：

* Mac版本使用[WebView](https://developer.apple.com/documentation/webkit/webview)。

* Windows版本使用基于Chromium的[CefSharp](https://cefsharp.github.io/)。

确保SAML进程支持这些浏览器。

要进行进一步的故障诊断，可以查看浏览器尝试加载的确切URL。 要查看此信息，请执行以下操作：

1. 按照在[调试模式](#enable-debug-mode)中启动应用程序的说明进行操作。

1. 重现登录尝试。

1. 导航到应用程序的[log目录](#check-log-files-v2)

1. 对于Windows:

   1. 打开“aemcompanionlog.txt”。

   1. 搜索以“登录浏览器地址已更改为”开头的消息。 这些条目还包含应用程序加载的URL。

   对于Mac:

   1. `com.adobe.aem.desktop-nnnnnnnn-nnnnnn.log`，其中n **** 将替换为最新文件名中的任何数字。

   1. 搜索以“已加载的帧”开头的消息。 这些条目还包含应用程序加载的URL。


查看正在加载的URL序列有助于在SAML的末尾进行故障诊断，以确定错误内容。

### SSL配置问题 {#ssl-config-v2}

[!DNL Experience Manager]桌面应用程序用于HTTP通信的库采用严格的SSL强制。 有时，使用浏览器连接可能会成功，但使用[!DNL Experience Manager]桌面应用程序时连接会失败。 要正确配置SSL，请在Apache中安装缺少的中间证书。 请参阅[如何在Apache](https://access.redhat.com/solutions/43575)中安装中间CA证书。

[!DNL Experience Manager]桌面应用程序用于HTTP通信的库利用严格的SSL强制执行。 因此，在某些情况下，通过浏览器成功的SSL连接在桌面应用程序[!DNL Adobe Experience Manager]中失败。 这是好事，因为它鼓励正确配置SSL并提高安全性，但当应用程序无法连接时可能会令人沮丧。

在这种情况下，建议使用工具分析服务器的SSL证书并识别问题，以便更正这些问题。 有一些网站会检查服务器的证书是否提供了其URL。

作为临时措施，可以在[!DNL Adobe Experience Manager]桌面应用程序中禁用严格的SSL强制。 这不是推荐的长期解决方案，因为它隐藏了未正确配置SSL的根本原因，从而降低了安全性。 要禁用严格强制执行，请执行以下操作：

1. 使用您选择的编辑器来编辑应用程序的JavaScript配置文件，该文件（默认情况下）位于以下位置（取决于操作系统）：

   在Mac:`/Applications/Adobe Experience Manager Desktop.app/Contents/Resources/javascript/lib-smb/config.json`

   在 Windows 中：`C:\Program Files (x86)\Adobe\Adobe Experience Manager Desktop\javascript\config.json`

1. 在文件中找到以下部分：

   ```shell
   ...
   "assetRepository": {
       "options": {
   ...
   ```

1. 通过添加`"strictSSL": false`修改部分，如下所示：

   ```shell
   ...
   "assetRepository": {
       "options": {
           "strictSSL": false,
   ...
   ```

1. 保存文件并重新启动[!DNL Adobe Experience Manager]桌面应用程序。

### 切换到其他服务器时出现登录问题 {#cannot-login-cookies-issue}

使用[!DNL Experience Manager]服务器后，当您尝试更改与其他服务器的连接时，可能会遇到登录问题。 这是由于旧Cookie干扰了新身份验证所致。 主菜单中的[!UICONTROL Clear Cookies]选项有帮助。 注销应用程序中的当前会话，然后选择[!UICONTROL Clear Cookies]，然后再继续连接。

![切换服务器时清除Cookie](assets/main_menu_logout_da2.png)

## 应用程序无响应 {#unresponsive}

应用程序很少会变得无响应、仅显示白屏，或在界面底部显示错误（界面上没有任何选项）。 按顺序尝试以下操作：

* 右键单击应用程序界面，然后单击&#x200B;**[!UICONTROL Refresh]**。
* 退出应用程序并再次将其打开。

在这两种方法中，应用程序都会在根DAM文件夹启动。

## 隐藏过期的资产 {#hide-expired-assets}

从[!DNL Experience Manager]用户界面中浏览资产时，不会显示已过期的资产。 要防止在从桌面应用程序和资产链接浏览资产时查看、搜索和获取过期的资产，管理员可以执行以下配置。 配置适用于所有用户，而不考虑管理员权限。

* [配置Experience Manager6.5以隐藏过期的资产](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.html#hide-expired-assets-via-acp-api)。
* [在Experience Manageras a Cloud Service中配置以隐藏已过期的资产](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/manage/manage-digital-assets.html#hide-expired-assets-via-acp-api)。

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

