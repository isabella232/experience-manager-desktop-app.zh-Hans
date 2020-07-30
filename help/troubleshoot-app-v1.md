---
title: AEM桌面应用程序版本1.x疑难解答
description: 对AEM桌面应用程序版本1.x进行疑难解答，以解决与安装、升级、配置等相关的偶发问题。
uuid: ce98a3e7-5454-41be-aaaa-4252b3e0f8dd
contentOwner: AG
products: SG_EXPERIENCEMANAGER/6.3/ASSETS
discoiquuid: f5eb222a-6cdf-4ae3-9cf2-755c873f397c
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 3eb9ab89ff6338fb29cfad1a031944119908d0a2
workflow-type: tm+mt
source-wordcount: '3374'
ht-degree: 1%

---


# AEM桌面应用程序v1.x疑难解答 {#troubleshoot-aem-desktop-app}

对AEM桌面应用程序进行疑难解答，以解决与安装、升级、配置等相关的偶发问题。

Adobe Experience Manager(AEM)桌面应用程序包含实用程序，可帮助您将AEM Assets存储库映射为桌面上的网络共享（Mac OS上的SMB共享）。 网络共享是一种操作系统技术，它使远程源能够被视为计算机本地文件系统的一部分。 对于桌面应用程序，远程AEM实例的数字资产管理(DAM)存储库结构将作为远程文件源。 下图描述了桌面应用程序拓扑：

![桌面应用程序图](assets/aem-desktopapp-architecture.png)

使用此架构，桌面应用程序会截取装载的网络共享的文件系统调用（打开、关闭、读取、写入等），并将它们转换为到AEM服务器的本机AEM HTTP调用。 文件在本地缓存。 有关详细信息，请 [参阅使用AEM桌面应用程序v1.x](use-app-v1.md)。

## AEM desktop app component overview {#desktop-app-component-overview}

桌面应用程序包含以下组件：

* **桌面应用程序**: 应用程序将DAM装载或卸载为远程文件系统，并在本地安装的网络共享和它连接到的远程AEM实例之间转换文件系统调用。
* **操作系统WebDAV/SMB客户端**: 处理Windows Explorer/Finder和桌面应用程序之间的通信。 如果检索、创建、修改、删除、移动或复制文件，则操作系统(OS)WebDAV/SMB客户端会将此操作通知到桌面应用程序。 收到通信后，桌面应用程序将其转换为本机AEM远程API调用。 例如，如果用户在装入的目录中创建文件，WebDAV/SMB客户端将启动一个请求，桌面应用程序将其转换为在DAM中创建文件的HTTP请求。 WebDAV/SMB客户端是操作系统的内置组件。 它不以任何方式与桌面应用程序、AEM或Adobe相关。
* **Adobe Experience Manager实例**: 提供对存储在AEM AssetsDAM存储库中的资产的访问。 此外，它代表与已装载网络共享交互的本地桌面应用程序执行桌面应用程序请求的操作。 目标AEM实例应运行AEM版本6.1或更高版本。 运行早期AEM版本的AEM实例可能需要安装额外的功能包和热修复才能完全正常工作。

## AEM桌面应用程序的预期使用案例 {#intended-use-cases-for-aem-desktop-app}

AEM桌面应用程序使用网络共享技术将远程AEM存储库映射到本地桌面。 但是，它并不打算作为网络共享资产的替代，因为用户直接从其本地桌面执行数字资产管理操作。 这包括移动或复制多个文件，或将大型文件夹结构直接拖动到Finder/Explorer中的AEM Assets网络共享。

AEM桌面应用程序提供了一种在AEM Assets触屏UI和本地桌面之间访问（打开）和编辑（保存）DAM资源的便捷方式。 它将AEM Assets服务器中的资源与基于桌面的工作流链接。

以下示例用例说明了AEM Desktop的使用方式：

* 用户登录AEM并使用Web UI查找资产。
* 使用AEM web UI的桌面操作功能，用户根据需要在桌面上打开、显示或编辑资产。
* AEM Desktop在资产文件类型的默认编辑器中打开资产。
* 用户对资产进行所需的更改。
* 修改文件后，用户可以使用AEM桌面的后台同步状态窗口视图文件的同步状态。
* 使用AEM Desktop的上下文菜单，用户可签入／签出资产，或返回到DAM用户界面。
* 完成对文件的更改后，用户返回AEM Web UI

这不是唯一的用例。 但是，它说明了AEM Desktop是一种方便的本地访问／编辑资源的机制。 我们鼓励您尽可能使用DAM Web UI，因为它提供了更好的体验。 它为Adobe提供了更大的灵活性以满足客户需求。

## 限制 {#limitations}

WebDAV/SMB1网络共享为在Explorer/Finder窗口中处理文件提供了便利。 但是，Explorer/Finder和AEM通过具有某些限制的网络连接进行通信。 例如，将1-GB文件复制到已装载的WebDAV/SMB目录所消耗的时间与使用Web浏览器将1-GB文件上传到网站所需的时间大致相同。 事实上，在前一种情况下，持续时间可能会更长，原因是WebDAV/SMB协议和操作系统的WebDAV/SMB客户端（尤其是Mac OS X）效率低下。

可以从已装载的目录执行的任务类型存在限制。 通常，处理大文件（尤其是在低／高延迟／低带宽网络连接上）可能会很有挑战性，尤其是在编辑大文件时。

Adobe建议您先执行一些用例测试，然后再将某些类型的文件从安装的目录提交到客户端，以便有效地就地编辑。

AEM Desktop不适合执行密集的文件系统操作，包括但不限于：

* 移动或复制文件和目录
* 向AEM添加许多资源
* 通过文件系统搜索和打开文件（浏览文件夹除外）
* 压缩或解压缩文件档案

由于操作系统的限制，Windows的文件大小限制为4,294,967,295字节（约4.29 GB）。 这是由于注册表设置，它定义网络共享上的文件可以有多大。 注册表设置的值是一个DWORD，其最大大小等于引用的数。

Experience Manager桌面应用程序没有可配置的超时值，该值在固定时间间隔后会断开Experience Manager服务器与桌面应用程序之间的连接。 上传大型资产时，如果连接在一段时间后超时，应用程序会重试通过增加上传超时来上传资产几次。 不推荐更改默认超时设置。

## 缓存并与AEM通信 {#caching-and-communication-with-aem}

AEM桌面应用程序提供内部缓存和后台上传功能，可改善最终用户体验。 保存大文件时，它首先保存在本地以便继续工作。 在某个时候（当前为30秒）后，文件将在后台发送到AEM服务器。

与Creative Cloud桌面或其他文件同步解决方案（如Microsoft One Drive）不同，AEM桌面应用程序不是完全的桌面同步客户端。 其原因是它提供对整个AEM Assets库的访问，该存储库在完全同步时可能非常大（数百GB或TB）。

缓存功能可将网络/存储开销限制为仅与用户相关的资产子集。

>[!CAUTION]
>
>Adobe建议关闭缩览图生成，以加快浏览速度。 如果启用图标预览，则在您浏览已装载的文件夹时，应用程序会缓存数字资产。 该应用程序还下载用户可能不关心的资源，这会增加服务器负载、占用用户带宽并占用用户的更多磁盘空间。

以下是AEM桌面应用程序执行缓存的方式：

* 当您在Finder中打开文件夹并显示文件的缩略图/预览时，或者当您在应用程序中打开文件时，桌面应用程序会缓存文件二进制文件。
* 当您通过Finder或其他桌面应用程序存储文件时，首先在本地存储该文件（缓存），并通知操作系统。 然后，该文件将排队等候在后台上传到服务器，并最终通过网络上传。 如果出现网络错误，桌面应用程序重试上传整个文件最多三次。 如果在三次重试后无法上传，则文件会被标记为冲突文件，并且状态会通过“后台上传队列状态”窗口显示。 桌面应用程序不再尝试更新文件。 在连接恢复后，用户应更新文件并重新上传它

每个操作都不在本地缓存。 以下内容会立即发送到AEM服务器，而无需本地缓存：

* 对文件夹执行的任何操作，例如创建、删除等
* 1.4 版本中引入的“文件夹上传”功能可以上传本地文件夹层次结构，而不会在本地缓存文件

## 单个操作 {#individual-operations}

对个别用户的性能进行次优化故障诊断时，请首先查看 [限制](https://helpx.adobe.com/experience-manager/desktop-app/troubleshooting-desktop-app.html#limitations)。 后续部分包括改进单个用户性能的建议。

## 带宽建议 {#bandwidth-recommendations}

单个用户可用的带宽在WebDAV/SMB客户端的性能中起着关键作用。

Adobe建议单个用户的上传速度接近10 Mbps。 对于无线连接，带宽通常在多个用户之间共享。 如果多个用户同时执行消耗网络带宽的任务，性能可能进一步降低。 要避免此类问题，请使用有线连接。

## 特定于Windows的配置 {#windows-specific-configurations}

如果在Windows上运行AEM，则可以配置Windows以增强WebDAV客户端的性能。 有关详细信息，请访 [问https://support.microsoft.com/en-us/kb/2445570](https://support.microsoft.com/en-us/kb/2445570)。

在Windows 7中，修改IE设置可以提高WebDAV的性能。 有关详细信息，请 [访问](http://oddballupdate.com/2009/12/fix-slow-webdav-performance-in-windows-7/)http://oddballupdate.com/2009/12/fix-slow-webdav-performance-in-windows-7/。

## 并发操作 {#concurrent-operations}

当您与本地文件交互时，AEM Desktop将检查AEM中是否提供较新版本的文件。 如果有新版本可用，应用程序会将文件的新副本下载到本地缓存。 但是，如果修改了AEM Desktop，它不会覆盖本地缓存的文件。 此功能可防止您的作品被无意覆盖。

在本地和AEM中修改同一文件时，本地修改的版本将覆盖AEM中的版本。 在这种情况下，资产的时间轴中提供以前的版本。 您可以验证这两个版本并解决任何冲突。

如果本地文件与服务器中可用的版本不一致，则后台上传状态对话框会通知您有关该冲突的信息。 要解决此问题，请打开冲突文件并保存它。 保存文件会强制AEM Desktop将您最新的本地更改同步到AEM。 您可以视图时间轴中资产的先前版本并解决任何冲突。

当多个用户尝试在针对同一AEM实例的单独装载目录中工作时，您应考虑其他因素。 特别是，以下因素很重要：

* 用户原始网络上可用的带宽量
* 原始网络的网络配置，如防火墙或代理
* 目标AEM实例的网络中可用的带宽量
* 目标AEM实例之前是否存在调度程序
* 目标AEM实例的当前负载

## 其他AEM配置 {#additional-aem-configurations}

如果多个用户同时工作时WebDAV/SMB性能严重下降，您可以在AEM中配置一些内容，这有助于提高性能。

## 更新资产临时工作流 {#update-asset-transient-workflows}

您可以通过为DAM更新资产工作流启用临时工作流来提高AEM端的性能。 启用临时工作流会降低在AEM中创建或修改资产时更新资产所需的处理能力。

1. 导航到 `/miscadmin` 要配置的AEM实例中(例如 `http://[Server]:[Port]/miscadmin`)。
1. 在导航树中，展开&#x200B;**工具** > **工作流** > **模型** > **dam**。
1. 多次单击 **DAM更新资产**。
1. 从浮动工具面板切换到页面选 **项卡** ，然后单击 **页面属性**。
1. 选中“临 **时工作流** ”复选框，然后单击 **“确定”**。

### 调整 Granite Transient 工作流程队列 {#adjust-granite-transient-workflow-queue}

提高AEM性能的另一种方法是为Granite临时工作流队列作业配置最大并行作业的值。 建议的值大约是服务器可用CPU数的一半。 要调整值，请执行以下步骤：

1. 导航到 *要配置的AEM实例中的* /system/console/configMgr(例如 <http://&lt;Server&gt;:&lt;Port&gt;/system/console/configMgr>)。
1. 搜索 **QueueConfiguration**，然后单击以打开每个作业，直到找到Granite临时工 **作流队列作业** 。 单击其旁边的编辑。
1. 更改“ **Maximum Parallel Jobs** ”值，然后单击“ **Save**”。

## AWS配置 {#aws-configuration}

由于网络带宽限制，当多个用户同时工作时，WebDAV/SMB的性能可能会降低。 Adobe建议为在AWS上运行的目标AEM实例增加AWS实例的大小，以增强WebDAV/SMB的性能。

此衡量标准特别增加了服务器可用的网络带宽量。 以下是一些详细信息：

* AWS实例专用的网络带宽量随实例大小的增加而增加。 有关每个实例大小可用带宽的信息，请参阅 [AWS文档](https://aws.amazon.com/ec2/instance-types/)。
* 对大型客户端进行故障排除时，Adobe将其AEM实例的大小配置为c4.8xlarge，主要针对它提供的4000 Mbps专用带宽。
* 如果AEM实例前面有调度程序，请确保它的大小适当。 如果AEM实例提供4000 Mbps，但调度程序仅提供500 Mbps，则有效带宽仅为500 Mbps。 这是因为调度程序造成了网络瓶颈。

## 签出文件限制 {#checked-out-file-limitations}

在通过Explorer/Finder与签出文件交互的方式上存在一些已知限制。 如果文件已签出，则除已签出该文件的用户外，其应为只读文件。 在AEM中实施WebDAV/SMB1协议可强制执行此规则。 但是，操作系统WebDAV/SMB客户端通常不能与签出文件正常交互。 下面介绍了一些奇怪的情况。

### 常规 {#general}

写入签出文件时，仅在AEM WebDAV实现中强制执行锁定。 因此，仅使用WebDAV的客户端（如桌面应用程序）强制执行锁定。 锁不是通过AEM Web界面强制执行的。 AEM界面仅会在已签出的资产的卡视图中显示锁图标。 该图标为修饰，对AEM的行为没有影响。

通常，WebDAV客户端的行为并不总是如预期的那样。 可能还有其他问题。 但是，在AEM中刷新或检查资产是验证资产是否未被修改的一种有效方法。 此行为是OS WebDAV客户端的典型行为，该客户端不受Adobe控制。

### Windows {#windows}

删除文件似乎成功，因为该文件从Windows中的文件资源管理器中消失。 但是，刷新目录并检入AEM资源表明文件仍然存在。 此外，编辑文件似乎成功（不显示警告对话框或错误消息）。 但是，重新打开文件或签入AEM资产会显示文件未更改。

#### Mac OS X {#mac-os-x}

替换文件不会显示警告或错误，但检查AEM中的资产会显示它保持不变。 刷新或检查AEM中的资产，以验证资产是否未被修改。

## 桌面应用程序图标问题疑难解答(Mac OS X) {#troubleshooting-desktop-app-icon-issues-mac-os-x}

安装桌面应用程序后，菜单栏中将显示桌面应用程序菜单图标。 如果未显示该图标，请执行以下步骤以解决该问题：

1. 打开操作系统终端窗口。
1. 在命令提示符下键入以下命令，然后按Enter:

   ```shell
    cd ../Library/Caches.
   ```

1. 键入以下命令，然后按Enter:

   ```shell
   rm -r com.adobe.aem.assetscompanion
   ```

1. 键入以下命令，然后按Enter:

   ```shell
   cd ~/Library/Preferences
   ```

1. 键入以下命令，然后按Enter:

   ```shell
   rm com.adobe.aem.assetscompanion.plist
   ```

1. 键入以下命令，然后按Enter:

   ```shell
   rm ~/Library/Group\ Containers/group.com.adobe.aem.desktop/*
   ```

1. 重新启动系统。

AEM Desktop尝试同步任何给定文件三次。 如果第三次尝试后文件无法同步，AEM Desktop会认为文件冲突，并通过后台上传状态窗口通知您。 冲突状态表示您的最新更改仍在本地可用，但它们未同步回AEM。 AEM桌面应用程序不再尝试同步。

修复这种情况的最简单方法是打开冲突的文件并再次保存它。 它强制AEM Desktop再尝试三次同步。 如果文件仍无法同步，请参阅以下各节以获取更多帮助。

## 清除AEM桌面缓存 {#clearing-aem-desktop-cache}

清除AEM Desktop的缓存是一个初步的故障排除任务，可以解决几个AEM桌面问题。

您可以通过删除应用程序在以下位置的缓存目录来清除缓存。
在Windows中， `%LocalAppData%\Adobe\AssetsCompanion\Cache\`

在Mac中， `~/Library/Group/Containers/group.com.adobe.aem.desktop/cache/`

但是，位置可能会因AEM Desktop配置的AEM端点而异。 该值是目标URL的编码版本。 例如，如果应用程序正在定 `http://localhost:4502`位，则目录名称为 `http%3A%2F%2Flocalhost%3A4502%2F`。

要清除缓存，请删除&lt;已编码的AEM Endpoint>目录。

>[!NOTE]
>
>如果清除AEM桌面缓存，则未同步到AEM的本地文件更改将丢失。

>[!NOTE]
>
>从AEM桌面应用程序版本1.5开始，桌面应用程序UI中有一个选项可清除缓存。

## 查找AEM桌面版本 {#finding-the-aem-desktop-version}

确定AEM桌面版本的过程对于Windows和Mac OS都是相同的。

单击AEM桌面图标，然后选择“关 **于**”。 版本号显示在屏幕上。

## 在macOS上升级AEM桌面应用程序 {#upgrading-aem-desktop-app-on-macos}

在macOS上升级AEM桌面应用程序时，偶尔会发生问题。 这是由于AEM桌面应用程序的旧系统文件夹阻止新版本的AEM桌面正确加载导致的。 要解决此问题，可以手动删除以下文件夹和文件。

在执行以下步骤之前，将“Adobe Experience Manager桌面”应用程序从macOS Applications文件夹拖到垃圾桶。 然后打开终端，并执行以下命令，在出现提示时提供密码。

```shell
sudo rm -rf ~/Library/Application\ Support/com.adobe.aem.desktop
sudo rm -rf ~/Library/Preferences/com.adobe.aem.desktop.plist
sudo rm -rf ~/Library/Logs/Adobe\ Experience\ Manager\ Desktop

sudo find /var/folders -type d -name "com.adobe.aem.desktop" | xargs rm -rf
sudo find /var/folders -type d -name "com.adobe.aem.desktop.finderintegration-plugin" | xargs rm -rf
```

## 保存其他人签出的文件 {#saving-a-file-checked-out-by-others}

操作系统的技术限制使用户在尝试覆盖他人签出的文件时无法获得一致的体验。 体验因用于编辑签出文件的应用程序而异。 有时，应用程序会显示一条错误消息，指示磁盘写入失败，或显示一个看似不相关的或一般的错误。 在其他情况下，不显示任何错误消息，且操作似乎成功。

在这种情况下，关闭并重新打开文件可能会显示内容未更改。 但是，某些应用程序可能会存储文件的备份，以便应用您所做的更改。

无论何种行为，文件在签入时都保持不变。 即使显示文件的不同版本，更改也不会同步到AEM。

## 对移动文件相关问题进行疑难解答 {#troubleshooting-problems-around-moving-files}

服务器API需要额外的标头、X-Destination、X-Depth和X-Overwrite，以便移动和复制操作能够正常工作。 默认情况下，调度程序不传递这些标头，这会导致这些操作失败。 有关详细信息，请参 [阅在Dispatcher后连接到AEM](install-configure-app-v1.md#connect-to-an-aem-instance-behind-a-dispatcher)。

## AEM桌面连接问题疑难解答 {#troubleshooting-aem-desktop-connection-issues}

### SAML重定向问题 {#saml-redirect-issue}

AEM Desktop连接到启用SSO(SAML)AEM实例时出现问题的最常见原因是SAML进程没有重定向回最初请求的路径。 或者，可以将连接重定向到AEM桌面中未配置的主机。 执行以下步骤验证登录过程：

1. 打开Web浏览器。
1. 在地址栏中，指定URL `/content/dam.json`。
1. 例如，将URL替换为目标AEM实例 `http://localhost:4502/content/dam.json`。
1. 登录到AEM。
1. 登录后，在地址栏中检查浏览器的当前地址。 它应与最初输入的URL匹配。
1. 验证在AEM桌面中 `/content/dam.json` 配置的目标AEM值之前的所有内容。

### SSL配置问题 {#ssl-configuration-issue}

AEM桌面应用程序用于HTTP通信的库采用严格的SSL强制。 有时，连接可能使用浏览器成功，但使用AEM桌面应用程序失败。 要正确配置SSL，请在Apache中安装缺少的中间证书。 请参 [阅如何在Apache中安装Intermediate CA证书](https://access.redhat.com/solutions/43575)。

## 将AEM Desktop与调度程序结合使用 {#using-aem-desktop-with-dispatcher}

AEM Desktop可与AEM部署一起在调度程序后进行，这是AEM服务器的默认和推荐配置。 AEM创作环境前的AEM dispatcher通常配置为跳过缓存DAM资产。 因此，调度程序不从AEM Desktop的角度提供额外的缓存。 确保调度程序配置已调整为适用于AEM Desktop。 有关其他详细信息，请 [参阅连接到调度程序后的AEM](install-configure-app-v1.md#connect-to-an-aem-instance-behind-a-dispatcher)。

## 正在检查日志文件 {#checking-for-log-files}

根据您的操作系统，您可以在以下位置找到AEM Desktop的日志文件：

* Windows: `%LocalAppData%\Adobe\AssetsCompanion\Logs`
* Mac: `~/Library/Logs/Adobe\ Experience\ Manager\ Desktop`
