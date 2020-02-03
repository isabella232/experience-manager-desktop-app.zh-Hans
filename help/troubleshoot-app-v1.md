---
title: AEM桌面应用程序版本1.x疑难解答
description: 对AEM桌面应用程序版本1.x进行疑难解答，以解决与安装、升级、配置等相关的临时问题。
uuid: ce98a3e7-5454-41be-aaaa-4252b3e0f8dd
contentOwner: AG
products: SG_EXPERIENCEMANAGER/6.3/ASSETS
discoiquuid: f5eb222a-6cdf-4ae3-9cf2-755c873f397c
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: ab63bfd7eea356be924e1ed62eef387796913e6c

---


# AEM桌面应用程序v1.x疑难解答 {#troubleshoot-aem-desktop-app}

对AEM桌面应用程序进行疑难解答，以解决与安装、升级、配置等相关的临时问题。

Adobe Experience Manager(AEM)桌面应用程序包含实用程序，可帮助您将AEM资产存储库映射为桌面上的网络共享（Mac OS上的SMB共享）。 网络共享是一种操作系统技术，它使远程源能够被视为计算机本地文件系统的一部分。 对于桌面应用程序，远程AEM实例的数字资产管理(DAM)存储库结构将作为远程文件源作为目标。 下图描述了桌面应用程序拓扑：

![桌面应用程序图](assets/aem-desktopapp-architecture.png)

使用此架构，桌面应用程序会截取对已装载网络共享的文件系统调用（打开、关闭、读取、写入等），并将它们转换为对AEM服务器的本机AEM HTTP调用。 文件在本地缓存。 有关详细信息，请 [参阅使用AEM桌面应用程序v1.x](use-app-v1.md)。

## AEM desktop app component overview {#desktop-app-component-overview}

桌面应用程序包括以下组件：

* **桌面应用程序**:应用程序将DAM作为远程文件系统进行安装或卸载，并在本地安装的网络共享与它连接到的远程AEM实例之间转换文件系统调用。
* **操作系统WebDAV/SMB客户端**:处理Windows资源管理器/Finder与桌面应用程序之间的通信。 如果检索、创建、修改、删除、移动或复制文件，则操作系统(OS)WebDAV/SMB客户端会将此操作通知到桌面应用程序。 在收到通信后，桌面应用程序会将其转换为本机AEM远程API调用。 例如，如果用户在安装的目录中创建文件，则WebDAV/SMB客户端会启动一个请求，桌面应用程序会将该请求转换为在DAM中创建文件的HTTP请求。 WebDAV/SMB客户端是操作系统的内置组件。 它不以任何方式与桌面应用程序、AEM或Adobe关联。
* **Adobe Experience manager实例**:提供对存储在AEM Assets DAM存储库中的资产的访问。 此外，它代表与安装的网络共享交互的本地桌面应用程序执行桌面应用程序请求的操作。 目标AEM实例应运行AEM版本6.1或更高版本。 运行先前AEM版本的AEM实例可能需要安装额外的功能包和修补程序才能使其完全正常工作。

## AEM桌面应用程序的预期用例 {#intended-use-cases-for-aem-desktop-app}

AEM桌面应用程序使用网络共享技术将远程AEM存储库映射到本地桌面。 但是，它并非作为网络共享资产的替代，因为用户直接从其本地桌面执行数字资产管理操作。 这包括移动或复制多个文件，或将大型文件夹结构直接拖动到Finder/资源管理器中的AEM资产网络共享。

AEM桌面应用程序为在AEM资产触屏UI和本地桌面之间访问（打开）和编辑（保存）DAM资产提供了一种便捷的方式。 它将AEM Assets服务器中的资产与基于桌面的工作流相关联。

以下示例用例说明了AEM Desktop的使用方式：

* 用户登录AEM并使用Web UI查找资产。
* 使用AEM Web UI的桌面操作功能，用户可以根据需要在桌面上打开、显示或编辑资产。
* AEM Desktop在资产文件类型的默认编辑器中打开资产。
* 用户对资产进行所需的更改。
* 修改文件后，用户可以使用AEM Desktop的后台同步状态窗口查看文件的同步状态。
* 使用AEM desktop的上下文菜单，用户可签入／签出资产，或返回DAM用户界面。
* 完成对文件的更改后，用户将返回AEM Web UI

这不是唯一的用例。 但是，它说明了AEM Desktop是一种方便的本地访问／编辑资产的机制。 我们鼓励您尽可能多地使用DAM Web UI，因为它提供了更好的体验。 它为Adobe提供了更大的灵活性以满足客户需求。

## 限制 {#limitations}

WebDAV/SMB1网络共享为在资源管理器/Finder窗口中处理文件提供了便利。 但是，Explorer/Finder和AEM通过具有某些限制的网络连接进行通信。 例如，将1-GB文件复制到已装载的WebDAV/SMB目录所耗时间与使用Web浏览器将1-GB文件上载到网站所需的时间大致相同。 事实上，在前一种情况下，持续时间可能会更长，因为WebDAV/SMB协议和操作系统的WebDAV/SMB客户端（尤其是Mac OS X）效率低下。

从已装载的目录可以执行的任务类型存在限制。 通常，在低／高延迟／低带宽网络连接上处理大文件可能具有挑战性，尤其是在编辑大文件时。

Adobe建议您在向客户端提交某些类型的文件可以从安装的目录中高效地就地编辑之前，先执行一些用例测试。

AEM Desktop不适合执行密集的文件系统操作，包括但不限于：

* 移动或复制文件和目录
* 向AEM添加许多资产
* 通过文件系统搜索和打开文件，浏览文件夹除外
* 压缩或解压缩文件存档

由于操作系统的限制，Windows的文件大小限制为4,294,967,295字节（约4.29 GB）。 这是由于注册表设置，它定义了网络共享上的文件可以有多大。 注册表设置的值是一个DWORD，其最大大小等于引用的数字。

Experience Manager桌面应用程序没有可配置的超时值，该值会在固定时间间隔后断开Experience manager服务器与桌面应用程序之间的连接。 上传大型资产时，如果连接在一段时间后超时，则应用程序会通过增加上传超时次数来重试上传资产。 不建议使用任何方法来更改默认超时设置。

## 缓存并与AEM通信 {#caching-and-communication-with-aem}

AEM桌面应用程序提供内部缓存和后台上传功能以改进最终用户体验。 保存大文件时，首先将其保存在本地，以便继续工作。 在某天（当前为30秒）之后，该文件随后将在后台发送到AEM服务器。

与Creative Cloud Desktop或其他文件同步解决方案（如Microsoft One Drive）不同，AEM桌面应用程序不是完全的Desktop sync客户端。 其原因是它提供了对整个AEM资产存储库的访问，该存储库可能非常大（数百GB或TB）以实现完全同步。

缓存功能可将网络／存储开销限制为仅与用户相关的资产子集。

以下是AEM桌面应用程序执行缓存的方式：

* 当您在Finder中打开文件夹并显示文件的缩览图／预览时，或者当您在应用程序中打开文件时，桌面应用程序会缓存文件二进制文件。
* 当您通过Finder或其他桌面应用程序存储文件时，文件首先在本地存储（缓存），并通知操作系统。 然后，该文件将排队等候在后台上传到服务器，并最终通过网络上传。 如果出现网络错误，桌面应用程序将重试上传整个文件，最多重试三次。 如果三次重试后无法上传，则文件会标记为有冲突的文件，并且状态会通过“后台上传队列状态”窗口显示。 桌面应用程序不再尝试更新文件。 用户应在恢复连接后更新文件并重新上传它

每个操作都不在本地缓存。 以下内容会立即发送到AEM服务器，而不会本地缓存：

* 对文件夹执行的任何操作，例如创建、删除等
* 1.4 版本中引入的“文件夹上传”功能可以上传本地文件夹层次结构，而不会在本地缓存文件

## 单个操作 {#individual-operations}

对个别用户未优化的性能进行故障诊断时，请首先查看限 [制](https://helpx.adobe.com/experience-manager/desktop-app/troubleshooting-desktop-app.html#limitations)。 后续部分包括改进单个用户性能的建议。

## 带宽建议 {#bandwidth-recommendations}

单个用户可用的带宽在WebDAV/SMB客户端的性能中起着关键作用。

Adobe建议单个用户的上传速度接近10 Mbps。 对于无线连接，带宽通常在多个用户之间共享。 如果多个用户同时执行消耗网络带宽的任务，性能可能进一步降低。 要避免此类问题，请使用有线连接。

## 特定于Windows的配置 {#windows-specific-configurations}

如果在Windows上运行AEM，则可以配置Windows以增强WebDAV客户端的性能。 有关详细信息，请访 [问https://support.microsoft.com/en-us/kb/2445570](https://support.microsoft.com/en-us/kb/2445570)。

在Windows 7中，修改IE设置可以提高WebDAV的性能。 有关详细信息，请访 [问http://oddballupdate.com/2009/12/fix-slow-webdav-performance-in-windows-7/](http://oddballupdate.com/2009/12/fix-slow-webdav-performance-in-windows-7/)。

## 并发操作 {#concurrent-operations}

当您与本地文件交互时，AEM Desktop会检查AEM中是否提供该文件的较新版本。 如果有新版本可用，则应用程序会将文件的新副本下载到本地缓存。 但是，如果已修改AEM Desktop文件，则它不会覆盖本地缓存的文件。 此功能可防止您的作品被无意中覆盖。

在本地和AEM中同时修改同一文件时，本地修改的版本将覆盖AEM中的版本。 在这种情况下，资产的时间轴中提供以前的版本。 您可以验证这两个版本并解决任何冲突。

如果本地文件与服务器中可用的版本不一致，则后台上传状态对话框会通知您有关冲突的信息。 要解决此问题，请打开冲突的文件并保存它。 保存文件会强制AEM Desktop将最新的本地更改同步到AEM。 您可以在时间轴中查看资产的先前版本并解决任何冲突。

当多个用户尝试在针对同一AEM实例的单独安装目录中工作时，应考虑其他因素。 特别是，以下因素很重要：

* 用户原始网络上可用的带宽量
* 原始网络的网络配置，如防火墙或代理
* 目标AEM实例的网络中可用的带宽量
* 目标AEM实例之前是否存在调度程序
* 目标AEM实例的当前加载

## 其他AEM配置 {#additional-aem-configurations}

如果多个用户同时工作时WebDAV/SMB性能严重下降，您可以在AEM中配置一些内容，这有助于提高性能。

## 更新资产临时工作流 {#update-asset-transient-workflows}

您可以通过为DAM更新资产工作流启用临时工作流来改进AEM端的性能。 启用临时工作流会降低在AEM中创建或修改资产时更新资产所需的处理能力。

1. 导航到 `/miscadmin` 要配置的AEM实例中(例如 `http://[Server]:[Port]/miscadmin`)。
1. 在导航树中，展开 **工具** >工 **作流** >模型 **>** dam ****。
1. 双击“ **DAM更新资产”**。
1. 从浮动工具面板中，切换到“页 **面** ”选项卡，然后单击“ **页面属性”**。
1. 选中“临 **时工作流** ”(Transient Workflow **)复选框，然后单击“**&#x200B;确定”(OK)。

### 调整 Granite Transient 工作流程队列 {#adjust-granite-transient-workflow-queue}

提高AEM性能的另一种方法是为Granite临时工作流队列作业配置最大并行作业的值。 建议的值大约是服务器可用CPU数的一半。 要调整值，请执行以下步骤：

1. 导航到 *要配置的AEM实例中的* /system/console/configMgr(例如， <http://&lt;Server&gt;:&lt;Port&gt;/system/console/configMgr>)。
1. 搜索 **QueueConfiguration**，然后单击以打开每个作业，直到找到 **Granite Transient Workflow Queue作业** 。 单击其旁边的编辑图标。
1. 更改“最 **大并行作业”值** ，然后单击“ **保存”**。

## AWS配置 {#aws-configuration}

由于网络带宽的限制，当多个用户同时工作时，WebDAV/SMB的性能可能会降低。 Adobe建议为在AWS上运行的目标AEM实例增加AWS实例的大小，以增强WebDAV/SMB的性能。

该衡量标准特别增加了服务器可用的网络带宽量。 以下是一些详细信息：

* AWS实例专用的网络带宽量随实例大小的增加而增加。 有关每个实例大小的可用带宽的信息，请参阅 [AWS文档](https://aws.amazon.com/ec2/instance-types/)。
* 在对大型客户端进行故障诊断时，Adobe将其AEM实例的大小配置为c4.8xlarge，主要用于它提供的4000 Mbps专用带宽。
* 如果AEM实例前面有调度程序，请确保它的大小合适。 如果AEM实例提供4000 Mbps，但调度程序仅提供500 Mbps，则有效带宽仅为500 Mbps。 这是因为调度程序造成了网络瓶颈。

## 已注销文件限制 {#checked-out-file-limitations}

通过Explorer/Finder与已注销文件交互的方式存在一些已知限制。 如果文件已签出，则除已签出该文件的用户之外，其他任何人都应为只读文件。 在AEM中实施WebDAV/SMB1协议将实施此规则。 但是，操作系统WebDAV/SMB客户端通常不能与签出文件正常交互。 下面介绍了一些奇怪之处。

### 常规 {#general}

写入签出文件时，仅在AEM webDAV实现中强制执行锁定。 因此，仅使用WebDAV的客户端（如桌面应用程序）强制执行锁定。 此锁不会通过AEM web界面实施。 AEM界面仅会在已签出的资产的卡片视图中显示锁定图标。 该图标为修饰图标，对AEM的行为没有影响。

通常，WebDAV客户端的行为并不总是如预期的那样。 可能还有其他问题。 但是，在AEM中刷新或检查资产是验证资产是否未被修改的一种有效方法。 这是操作系统WebDAV客户端的典型行为，Adobe不控制这些客户端。

### Windows {#windows}

删除文件似乎成功，因为该文件从Windows中的文件资源管理器中消失。 但是，刷新目录并签入AEM资产会显示文件仍然存在。 此外，编辑文件似乎成功（不显示警告对话框或错误消息）。 但是，重新打开文件或签入AEM资产会显示文件未更改。

#### Mac OS X {#mac-os-x}

替换文件不会显示警告或错误，但检查AEM中的资产会显示它保持不变。 在AEM中刷新或检查资产，以验证其是否未被修改。

## 桌面应用程序图标问题疑难解答(Mac OS X) {#troubleshooting-desktop-app-icon-issues-mac-os-x}

安装桌面应用程序后，菜单栏中会显示桌面应用程序菜单图标。 如果未显示该图标，请执行以下步骤以解决该问题：

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

AEM desktop尝试三次同步任何给定文件。 如果第三次尝试后文件无法同步，AEM Desktop会认为该文件有冲突，并通过后台上传状态窗口通知您。 冲突状态表示您的最新更改仍在本地可用，但不会同步回AEM。 AEM桌面应用程序不再尝试同步。

解决这种情况的最简单方法是打开冲突的文件并再次保存它。 它强制AEM Desktop再尝试三次同步。 如果文件仍无法同步，请参阅以下各节以获取更多帮助。

## 清除AEM Desktop缓存 {#clearing-aem-desktop-cache}

清除AEM Desktop缓存是一项初步的疑难解答任务，可解决多个AEM Desktop问题。

您可以通过删除位于以下位置的应用程序缓存目录来清除缓存：Windows:%LocalAppData%\Adobe\AssetsCompanion\Cache\

Mac:~/Library/Group/Containers/group.com.adobe.aem.desktop/cache/

但是，位置可能会因AEM Desktop配置的AEM端点而异。 该值是目标URL的编码版本。 例如，如果应用程序是定位的， `http://localhost:4502`则目录名称为 `http%3A%2F%2Flocalhost%3A4502%2F`。

要清除缓存，请删除&lt;已编码AEM端点>目录。

>[!NOTE]
>
>如果清除AEM Desktop缓存，则未同步到AEM的本地文件更改将丢失。

>[!NOTE]
>
>从AEM桌面应用程序版本1.5开始，桌面应用程序UI中有一个选项可清除缓存。

## 查找AEM Desktop版本 {#finding-the-aem-desktop-version}

在Windows和Mac OS中，确定AEM Desktop版本的过程相同。

单击AEM Desktop图标，然后选择“关 **于”**。 版本号显示在屏幕上。

## 在macOS上升级AEM桌面应用程序 {#upgrading-aem-desktop-app-on-macos}

在macOS上升级AEM桌面应用程序时，偶尔会出现问题。 这是由于AEM桌面应用程序的旧版系统文件夹阻止正确加载新版本的AEM Desktop所致。 要解决此问题，可以手动删除以下文件夹和文件。

在执行以下步骤之前，将“Adobe Experience Manager Desktop”应用程序从macOS Applications文件夹拖到垃圾桶。 然后打开终端，并执行以下命令，在出现提示时提供密码。

```shell
sudo rm -rf ~/Library/Application\ Support/com.adobe.aem.desktop
sudo rm -rf ~/Library/Preferences/com.adobe.aem.desktop.plist
sudo rm -rf ~/Library/Logs/Adobe\ Experience\ Manager\ Desktop

sudo find /var/folders -type d -name "com.adobe.aem.desktop" | xargs rm -rf
sudo find /var/folders -type d -name "com.adobe.aem.desktop.finderintegration-plugin" | xargs rm -rf
```

## 保存其他人签出的文件 {#saving-a-file-checked-out-by-others}

操作系统的技术限制使用户在尝试覆盖他人签出的文件时无法获得一致的体验。 体验因用于编辑签出文件的应用程序而异。 有时，应用程序会显示一条错误消息，指示磁盘写入失败，或显示一个看似不相关的或通用错误。 在其他情况下，不显示任何错误消息，且操作似乎成功。

在这种情况下，关闭并重新打开文件可能会显示内容未更改。 但是，某些应用程序可能会存储文件的备份，以便应用您所做的更改。

无论执行何种操作，在签入时，文件将保持不变。 即使显示了文件的其他版本，更改也不会同步到AEM。

## 对移动文件相关问题进行疑难解答 {#troubleshooting-problems-around-moving-files}

服务器API需要传递额外的标题、X-Destination、X-Depth和X-Overwrite，以便移动和复制操作能够正常工作。 默认情况下，调度程序不会传递这些标头，这会导致这些操作失败。 有关详细信息，请参 [阅连接到Dispatcher后面的AEM](install-configure-app-v1.md#connect-to-an-aem-instance-behind-a-dispatcher)。

## AEM Desktop连接问题疑难解答 {#troubleshooting-aem-desktop-connection-issues}

### SAML重定向问题 {#saml-redirect-issue}

AEM desktop连接到您的启用SSO(SAML)AEM实例时出现问题的最常见原因是SAML进程不会重定向回最初请求的路径。 或者，可以将连接重定向到未在AEM桌面中配置的主机。 执行以下步骤验证登录过程：

1. 打开Web浏览器。
1. 在地址栏中，指定URL `/content/dam.json`。
1. 例如，将URL替换为目标AEM实例 `http://localhost:4502/content/dam.json`。
1. 登录到AEM。
1. 登录后，在地址栏中检查浏览器的当前地址。 它应与您最初输入的URL匹配。
1. 验证之前的所 `/content/dam.json` 有内容是否与在AEM desktop中配置的目标AEM值匹配。

### SSL配置问题 {#ssl-configuration-issue}

AEM桌面应用程序用于HTTP通信的库采用严格的SSL强制。 有时，连接可能使用浏览器成功，但使用AEM桌面应用程序失败。 要正确配置SSL，请在Apache中安装缺少的中间证书。 请参 [阅如何在Apache中安装Intermediate CA证书](https://access.redhat.com/solutions/43575)。

## 将AEM Desktop与调度程序一起使用 {#using-aem-desktop-with-dispatcher}

AEM Desktop可与调度程序后面的AEM部署配合使用，这是AEM服务器的默认和建议的配置。 AEM创作环境前面的AEM调度程序通常配置为跳过缓存DAM资产。 因此，从AEM Desktop的角度，调度程序不提供其他缓存。 确保调度程序配置已调整为适用于AEM Desktop。 有关其他详细信息，请 [参阅连接到调度程序后面的AEM](install-configure-app-v1.md#connect-to-an-aem-instance-behind-a-dispatcher)。

## 检查日志文件 {#checking-for-log-files}

根据操作系统的不同，您可以在以下位置找到AEM Desktop的日志文件：

* Windows: `%LocalAppData%\Adobe\AssetsCompanion\Logs`
* Mac: `~/Library/Logs/Adobe\ Experience\ Manager\ Desktop`