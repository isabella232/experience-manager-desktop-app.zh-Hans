---
title: 桌面应用程序版本1.10疑难解答。
description: 疑难解答 [!DNL Adobe Experience Manager] 桌面应用程序版本1.10，用于解决与安装、升级和配置相关的偶然问题。
exl-id: 1e1409c2-bf5e-4e2d-a5aa-3dd74166862c
source-git-commit: 2ae49374b362921a5a82fc2e040064b4e573b8c1
workflow-type: tm+mt
source-wordcount: '3291'
ht-degree: 1%

---

# 疑难解答 [!DNL Adobe Experience Manager] 桌面应用程序v1.x {#troubleshoot-aem-desktop-app}

对AEM桌面应用程序进行故障排除，以解决与安装、升级、配置等相关的偶然问题。

[!DNL Adobe Experience Manager] 桌面应用程序包括可帮助您将AEM Assets存储库映射为桌面设备上的网络共享(Mac OS上的SMB共享)的实用程序。 网络共享是一种操作系统技术，它使远程源可以被视为计算机本地文件系统的一部分。 对于桌面应用程序，远程AEM实例的数字资产管理(DAM)存储库结构被定位为远程文件源。 下图描述了桌面应用程序拓扑：

![桌面应用程序图表](assets/aem-desktopapp-architecture.png)

利用此架构，桌面应用程序会截获对已挂载网络共享的文件系统调用（打开、关闭、读取、写入等），并将它们转换为对AEM服务器的本机AEM HTTP调用。 文件缓存在本地。 有关更多详细信息，请参阅 [使用AEM桌面应用程序v1.x](use-app-v1.md).

## AEM桌面应用程序组件概述 {#desktop-app-component-overview}

桌面应用程序包含以下组件：

* **桌面应用程序**：应用程序作为远程文件系统装载或卸载DAM，并在本地装载的网络共享与其连接的远程AEM实例之间转换文件系统调用。
* **操作系统WebDAV/SMB客户端**：处理Windows资源管理器/查找器和桌面应用程序之间的通信。 如果检索、创建、修改、删除、移动或复制了文件，操作系统(OS) WebDAV/SMB客户端会将此操作传递给桌面应用程序。 收到通信后，桌面应用程序会将其转换为本机AEM远程API调用。 例如，如果用户在已装载目录中创建文件，则WebDAV/SMB客户端会发起请求，桌面应用程序会将该请求转换为在DAM中创建文件的HTTP请求。 WebDAV/SMB客户端是操作系统的内置组件。 它未以任何方式与桌面应用程序、AEM或Adobe相关联。
* **Adobe Experience Manager实例**：提供对存储在AEM Assets DAM存储库中的资源的访问权限。 此外，它还代表与已装载的网络共享交互的本地桌面应用程序执行桌面应用程序请求的操作。 目标AEM实例应运行AEM版本6.1或更高版本。 运行早期AEM版本的AEM实例可能需要安装额外的功能包和热修复程序，才能完全正常工作。

## AEM桌面应用程序的预期用例 {#intended-use-cases-for-aem-desktop-app}

AEM桌面应用程序使用网络共享技术将远程AEM存储库映射到本地桌面。 但是，它并非旨在替代网络共享资产，即用户直接从本地桌面执行数字资产管理操作。 其中包括移动或复制多个文件，或者将大型文件夹结构直接拖到Finder/Explorer中的AEM Assets网络共享中。

AEM桌面应用程序提供了一种在AEM Assets触屏UI和本地桌面之间访问（打开）和编辑（保存） DAM资产的便捷方式。 它将AEM Assets服务器中的资产链接到基于桌面的工作流。

以下示例用例说明了应如何使用AEM Desktop：

* 用户登录到AEM并使用Web UI来查找资源。
* 使用AEM Web UI的桌面操作功能，用户可根据需要打开、显示或编辑桌面上的资产。
* AEM Desktop在资产文件类型的默认编辑器中打开资产。
* 用户对资源进行所需的更改。
* 修改文件后，用户可以使用AEM Desktop的后台同步状态窗口查看文件的同步状态。
* 使用AEM Desktop的上下文菜单，用户签入/签出资产，或返回到DAM用户界面。
* 完成对该文件的更改后，用户返回到AEM Web UI

这并非唯一的用例。 但是，它说明了AEM Desktop如何成为一种便于在本地访问/编辑资产的机制。 建议您尽可能多地使用DAM Web UI，因为它提供了更好的体验。 它为Adobe提供了更大的灵活性以满足客户需求。

## 限制 {#limitations}

WebDAV/SMB1网络共享提供了在Explorer/Finder窗口中处理文件的便利性。 但是，Explorer/Finder和AEM通过具有某些限制的网络连接进行通信。 例如，将1-GB文件复制到已装载的WebDAV/SMB目录所花费的时间与使用Web浏览器将1-GB文件上传到网站所需的时间大致相同。 事实上，在前一种情况下，由于WebDAV/SMB协议和操作系统的WebDAV/SMB客户端(特别是Mac OS X)效率低下，持续时间可能会更长。

可以从已装载目录执行的任务类型存在限制。 一般而言，处理大型文件，尤其是通过差/高延迟/低带宽网络连接处理大型文件可能具有挑战性，尤其是在编辑大型文件时。

Adobe建议在将特定类型的文件可以从已装载目录就地有效编辑的客户端提交到客户端之前执行一些用例测试。

AEM Desktop不适合执行密集的文件系统操作，包括但不限于：

* 移动或复制文件和目录
* 将许多资源添加到AEM
* 通过文件系统搜索和打开文件（浏览文件夹除外）
* 压缩或解压缩文件归档

由于操作系统的限制，Windows的文件大小限制为4,294,967,295字节（约4.29 GB）。 这是因为注册表设置定义了文件在网络共享上的大小。 注册表设置的值是DWORD，其最大大小等于引用的数字。

[!DNL Experience Manager] 桌面应用程序没有可配置的超时值，因此无法断开两者之间的连接 [!DNL Experience Manager] 固定时间间隔后的服务器和桌面应用程序。 上传大型资产时，如果连接在一段时间后超时，应用程序会通过增加上传超时来重试上传资产几次。 没有更改默认超时设置的推荐方法。

## 缓存和与AEM的通信 {#caching-and-communication-with-aem}

AEM桌面应用程序提供内部缓存和后台上传功能，以改善最终用户体验。 保存大文件时，首先会将文件保存在本地，以便您继续工作。 在某个时间（当前为30秒）后，该文件随后会被发送到后台的AEM服务器。

与Creative Cloud Desktop或其他文件同步解决方案(如Microsoft One Drive)不同，AEM桌面应用程序不是完整的Desktop Sync客户端。 原因在于，它提供了对整个AEM Assets存储库的访问，对于完全同步，存储库可能非常大（数百千兆字节或TB）。

缓存提供了将网络/存储开销限制为仅与用户相关的资源子集的能力。

>[!CAUTION]
>
>Adobe建议关闭缩略图生成以加快浏览速度。 如果启用图标预览，则当您浏览装入的文件夹时，应用程序将缓存数字资产。 该应用程序还会下载用户可能不在乎的资产，这会增加服务器的负载、占用用户的带宽，并占用更多用户的磁盘空间。

以下是AEM桌面应用程序执行缓存的方式：

* 当您在Finder中打开文件夹并显示文件的缩略图/预览时，或者在应用程序中打开文件时，桌面应用程序将缓存文件二进制文件。
* 当您通过Finder或其他桌面应用程序存储文件时，文件会先在本地存储（缓存），并通知操作系统。 然后，文件会排队等候在后台上传到服务器，并最终通过网络上传。 如果出现网络错误，桌面应用程序最多会重试上传整个文件三次。 如果在重试三次后无法上载，则该文件将被标记为冲突文件，并且状态会通过“后台上载队列状态”窗口显示。 桌面应用程序不再尝试更新文件。 用户应更新文件，并在连接恢复后重新上传

并非每个操作都缓存在本地。 以下内容将立即传输到AEM Server，而不进行本地缓存：

* 对文件夹的任何操作，例如创建、删除等
* 1.4 版本中引入的“文件夹上传”功能可以上传本地文件夹层次结构，而不会在本地缓存文件

## 单个操作 {#individual-operations}

在对单个用户的次优化性能进行故障诊断时，请先查阅 [应用程序限制](#limitations). 后续部分包含改进单个用户性能的建议。

## 带宽建议 {#bandwidth-recommendations}

单个用户可用的带宽对WebDAV/SMB客户端的性能起着至关重要的作用。

Adobe建议单个用户的上传速度应接近10 Mbps。 对于无线连接，带宽通常由多个用户共享。 如果多个用户同时执行占用网络带宽的任务，则性能可能会进一步降低。 要避免此类问题，请使用有线连接。

<!-- AG, 8/18: The Windows KB article is removed by MS now. Giving 404. Also, Win 7 support is gone and the desktop app is also not supported on Win 7. Hiding this content for now.

## Windows-specific configurations {#windows-specific-configurations}

If you use Experience Manager on Windows, you can configure Windows to enhance the performance of the WebDAV client. For more information, go to [https://support.microsoft.com/en-us/kb/2445570](https://support.microsoft.com/en-us/kb/2445570).

On Windows 7, modifying IE settings can improve the performance of WebDAV. For details, see how to [fix slow WebDAV performance in Windows 7](https://oddballupdate.com/2009/12/fix-slow-webdav-performance-in-windows-7/).
-->

## 并发操作 {#concurrent-operations}

当您在本地与文件交互时，AEM Desktop会检查文件的较新版本是否在AEM中可用。 如果有新版本可用，应用程序会将文件的新副本下载到本地缓存。 但是，如果本地缓存的文件已被修改，则AEM Desktop不会覆盖该文件。 此功能可防止意外覆盖您的工作。

在本地和AEM中修改同一文件时，本地修改的版本会覆盖AEM中的版本。 在这种情况下，资产时间轴中提供了先前版本。 您可以验证这两个版本并解决任何冲突。

如果本地文件与服务器中的可用版本不一致，则后台上传状态对话框将通知您存在冲突。 要解决此问题，请打开冲突文件并保存它。 保存文件会强制AEM Desktop将您的最新本地更改同步到AEM。 您可以在时间轴中查看资产的早期版本并解决任何冲突。

当多个用户尝试在针对同一AEM实例的单独已装载目录中工作时，您应该考虑其他因素。 特别是，以下因素很重要：

* 用户原始网络上的可用带宽量
* 原始网络的网络配置，如防火墙或代理
* 目标AEM实例网络中的可用带宽量
* Dispatcher是否在Target AEM实例之前存在
* 目标AEM实例上的当前加载

## 其他AEM配置 {#additional-aem-configurations}

如果WebDAV/SMB性能在多用户同时工作时急剧下降，您可以在AEM中配置一些内容，这有助于提高性能。

## 更新资产临时工作流 {#update-asset-transient-workflows}

您可以通过为DAM更新资产工作流启用临时工作流来提高AEM端的性能。 启用临时工作流会降低在AEM中创建或修改资产时更新资产所需的处理能力。

1. 导航到 `/miscadmin` 在Experience Manager实例中(`https://[aem_server]:[port]/miscadmin`)。
1. 在导航树中，展开&#x200B;**工具** > **工作流** > **模型** > **dam**。
1. 双击 **DAM更新资产**.
1. 从浮动工具面板切换到 **页面** 选项卡，然后单击 **页面属性**.
1. 选择 **瞬态工作流** 复选框，然后单击 **确定**.

### 调整 Granite Transient 工作流程队列 {#adjust-granite-transient-workflow-queue}

另一种提高AEM性能的方法是为Granite Transient Workflow Queue作业配置最大并行作业值。 建议值大约为服务器可用CPU数的一半。 要调整值，请执行以下步骤：

1. 导航到 `/system/console/configMgr` 在要配置的AEM实例中(例如， `https://[aem_server]:[port]/system/console/configMgr`)。
1. 搜索 `QueueConfiguration`，然后单击以打开每个作业，直到找到 **Granite Transient工作流队列** 作业，然后单击 **编辑**.
1. 更改 `Maximum Parallel Jobs` 值，然后单击 **保存**.

## AWS配置 {#aws-configuration}

由于网络带宽的限制，当多个用户同时工作时，WebDAV/SMB的性能可能会降低。 Adobe建议为在AWS上运行的目标AEM实例增加AWS实例的大小以增强WebDAV/SMB的性能。

这项措施特别提高了服务器可用的网络带宽量。 以下是一些详细信息：

* 专用于AWS实例的网络带宽量会随着实例大小的增加而增加。 有关每个实例大小有多少可用带宽的信息，请参见 [AWS文档](https://aws.amazon.com/ec2/instance-types/).
* 针对大型客户端进行故障排除时，Adobe将其AEM实例的大小配置为c4.8xlarge，主要针对其提供的4000 Mbps专用带宽。
* 如果AEM实例前面有一个Dispatcher，请确保其大小合适。 如果AEM实例提供4000 Mbps，而Dispatcher仅提供500 Mbps，则有效带宽仅为500 Mbps。 这是因为Dispatcher造成了网络瓶颈。

## 签出文件限制 {#checked-out-file-limitations}

通过Explorer/Finder与签出文件交互的方式存在一些已知限制。 如果文件已签出，则除已签出文件的用户外，任何人都应该以只读方式签出文件。 在AEM中实施WebDAV/SMB1协议会强制实施此规则。 但是，OS WebDAV/SMB客户端通常无法与签出文件正常交互。 下面介绍了一些奇怪的地方。

### 常规 {#general}

写入签出文件时，仅在AEM WebDAV实施中强制实施锁定。 因此，只有使用WebDAV的客户端（如桌面应用程序）才强制执行锁定。 不会通过AEM Web界面强制执行锁定。 AEM界面仅在卡片视图中为已签出的资产显示一个锁图标。 图标是修饰性的，对AEM的行为没有影响。

通常，WebDAV客户端并不总是按预期运行。 可能存在其他问题。 但是，在AEM中刷新或检查资源是验证资源是否未被修改的可靠方法。 这种行为是不受Adobe控制的OS WebDAV客户端的典型行为。

### Windows {#windows}

删除文件似乎成功，因为文件在Windows中从文件资源管理器中消失。 但是，刷新目录并签入AEM资产会显示文件仍然存在。 此外，编辑文件似乎成功（不显示警告对话框或错误消息）。 但是，重新打开文件或签入AEM资产会显示文件未更改。

#### MAC OS X {#mac-os-x}

替换文件不会显示警告或错误，但检查AEM中的资源会显示它保持不变。 在AEM中刷新或检查资源以验证它未被修改。

## 桌面应用程序图标问题疑难解答(Mac OS X) {#troubleshooting-desktop-app-icon-issues-mac-os-x}

安装桌面应用程序后，桌面应用程序菜单图标会显示在菜单栏中。 如果未显示该图标，请执行以下步骤来解决问题：

1. 打开操作系统终端窗口。
1. 在命令提示符下键入以下命令，然后按Enter键：

   ```shell
    cd ../Library/Caches.
   ```

1. 键入以下命令，然后按Enter键：

   ```shell
   rm -r com.adobe.aem.assetscompanion
   ```

1. 键入以下命令，然后按Enter键：

   ```shell
   cd ~/Library/Preferences
   ```

1. 键入以下命令，然后按Enter键：

   ```shell
   rm com.adobe.aem.assetscompanion.plist
   ```

1. 键入以下命令，然后按Enter键：

   ```shell
   rm ~/Library/Group\ Containers/group.com.adobe.aem.desktop/*
   ```

1. 重新启动系统。

AEM Desktop尝试同步任何给定文件三次。 如果在第三次尝试后文件无法同步，AEM Desktop会将该文件视为冲突，并通过后台上传状态窗口通知您。 冲突状态表示您最新的更改在本地仍然可用，但不会同步回AEM。 AEM桌面应用程序不再尝试同步。

解决此问题的最简单方法是打开冲突文件并再次保存。 它会强制AEM Desktop尝试另外三次同步。 如果文件仍无法同步，请参阅以下部分以获得更多帮助。

## 正在清除AEM桌面缓存 {#clearing-aem-desktop-cache}

清除AEM Desktop的缓存是一项初步的疑难解答任务，可解决多个AEM Desktop问题。

可以通过删除应用程序在下列位置的缓存目录来清除缓存。
在Windows中， `%LocalAppData%\Adobe\AssetsCompanion\Cache\`

在Mac中， `~/Library/Group/Containers/group.com.adobe.aem.desktop/cache/`

但是，该位置可能会根据AEM Desktop配置的AEM端点而更改。 值是目标URL的编码版本。 例如，如果应用程序正在定位 `http://localhost:4502`，目录名称为 `http%3A%2F%2Flocalhost%3A4502%2F`.

要清除缓存，请删除 &lt;encoded aem=&quot;&quot; endpoint=&quot;&quot;> 目录。

>[!NOTE]
>
>如果清除AEM Desktop缓存，则未同步到AEM的本地文件更改将丢失。

>[!NOTE]
>
>从AEM桌面应用程序版本1.5开始，桌面应用程序UI中有一个选项可用于清除缓存。

## 查找AEM桌面版 {#finding-the-aem-desktop-version}

确定AEM桌面版本的过程对于Windows和Mac操作系统都是相同的。

单击AEM Desktop图标，然后选择 **关于**. 版本号将显示在屏幕上。

## 在macOS上升级AEM桌面应用程序 {#upgrading-aem-desktop-app-on-macos}

在macOS上升级AEM桌面应用程序时，有时可能会出现问题。 这是由于AEM桌面应用程序的旧系统文件夹阻止正确加载新版本的AEM桌面所致。 要解决此问题，可以手动删除以下文件夹和文件。

在执行以下步骤之前，将“Adobe Experience Manager桌面”应用程序从macOS应用程序文件夹拖到垃圾桶中。 然后打开“终端”，执行以下命令，在出现提示时提供密码。

```shell
sudo rm -rf ~/Library/Application\ Support/com.adobe.aem.desktop
sudo rm -rf ~/Library/Preferences/com.adobe.aem.desktop.plist
sudo rm -rf ~/Library/Logs/Adobe\ Experience\ Manager\ Desktop

sudo find /var/folders -type d -name "com.adobe.aem.desktop" | xargs rm -rf
sudo find /var/folders -type d -name "com.adobe.aem.desktop.finderintegration-plugin" | xargs rm -rf
```

## 保存由其他人签出的文件 {#saving-a-file-checked-out-by-others}

由于操作系统的技术限制，用户在尝试覆盖其他人签出的文件时无法拥有一致的体验。 体验会因用于编辑检出文件的应用程序而异。 有时，应用程序会显示一条错误消息，指示磁盘写入失败，或显示一个看似不相关或一般性的错误。 在其他情况下，不会显示错误信息，并且操作似乎成功。

在这种情况下，关闭和重新打开文件可能会显示其内容未更改。 但是，某些应用程序可能会存储文件的备份，以便应用您的更改。

无论行为如何，将文件检入时，文件保持不变。 即使显示了该文件的其他版本，更改也不会同步到AEM。

## 解决与移动文件相关的问题 {#troubleshooting-problems-around-moving-files}

服务器API需要传递其他标头（X-Destination、X-Depth和X-Overwrite），以便移动和复制操作正常工作。 默认情况下，Dispatcher不传递这些标头，这会导致这些操作失败。 有关更多信息，请参阅 [连接到Dispatcher后的AEM](install-configure-app-v1.md#connect-to-an-aem-instance-behind-a-dispatcher).

## AEM桌面连接问题疑难解答 {#troubleshooting-aem-desktop-connection-issues}

### SAML重定向问题 {#saml-redirect-issue}

AEM Desktop连接到启用了SSO (SAML)的AEM实例时出现问题的最常见原因是SAML进程不会重定向回最初请求的路径。 或者，也可以将连接重定向到未在AEM Desktop中配置的主机。 执行以下步骤以验证登录过程：

1. 打开 Web 浏览器。
1. 在地址栏中，指定URL `/content/dam.json`.
1. 将URL替换为目标AEM实例，例如 `https://localhost:4502/content/dam.json`.
1. 登录到AEM。
1. 登录后，在地址栏中检查浏览器的当前地址。 它应该与您最初输入的URL匹配。
1. 验证之前的所有内容 `/content/dam.json` 与AEM Desktop中配置的目标AEM值匹配。

### SSL配置问题 {#ssl-configuration-issue}

AEM桌面应用程序用于HTTP通信的库利用严格的SSL强制实施。 有时，连接可能使用浏览器成功，但使用AEM桌面应用程序失败。 要正确配置SSL，请在Apache中安装缺少的中间证书。 参见 [如何在Apache中安装中间CA证书](https://access.redhat.com/solutions/43575).

## 将AEM Desktop与Dispatcher一起使用 {#using-aem-desktop-with-dispatcher}

AEM Desktop可与Dispatcher后面的AEM部署配合使用，这是AEM服务器的默认和推荐配置。 AEM创作环境前的AEM Dispatcher通常配置为跳过缓存DAM资源。 因此，调度程序不会从AEM Desktop角度提供其他缓存。 确保已调整Dispatcher配置以用于AEM Desktop。 有关其他详细信息，请参阅 [连接到Dispatcher后的AEM](install-configure-app-v1.md#connect-to-an-aem-instance-behind-a-dispatcher).

## 检查日志文件 {#checking-for-log-files}

根据您的操作系统，您可以在以下位置找到AEM Desktop的日志文件：

* Windows: `%LocalAppData%\Adobe\AssetsCompanion\Logs`
* Mac： `~/Library/Logs/Adobe\ Experience\ Manager\ Desktop`
