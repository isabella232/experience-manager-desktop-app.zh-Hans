---
title: 疑難排解案頭應用程式1.10版。
description: 疑難排解 [!DNL Adobe Experience Manager] 案頭應用程式1.10版，可解決安裝、升級和設定相關的偶然問題。
exl-id: 1e1409c2-bf5e-4e2d-a5aa-3dd74166862c
source-git-commit: 2ae49374b362921a5a82fc2e040064b4e573b8c1
workflow-type: tm+mt
source-wordcount: '3291'
ht-degree: 1%

---

# 疑難排解 [!DNL Adobe Experience Manager] 案頭應用程式v1.x {#troubleshoot-aem-desktop-app}

疑難排解AEM案頭應用程式，以解決與安裝、升級、設定等相關的偶爾問題。

[!DNL Adobe Experience Manager] 案頭應用程式包括協助您將此AEM Assets存放庫對應為案頭上的網路共用(Mac作業系統上的中小型企業共用)的公用程式。 網路共用是一種作業系統技術，可讓遠端來源被視為電腦本機檔案系統的一部分。 在案頭應用程式的情況下，遠端AEM例項的數位資產管理(DAM)存放庫結構會以遠端檔案來源為目標。 下圖說明案頭應用程式拓撲：

![案頭應用程式圖表](assets/aem-desktopapp-architecture.png)

透過此架構，案頭應用程式會攔截對掛載之網路共用的檔案系統呼叫（開啟、關閉、讀取、寫入等），並將這些呼叫轉譯成對AEM伺服器的原生AEM HTTP呼叫。 檔案會快取到本機。 如需詳細資訊，請參閱 [使用AEM案頭應用程式v1.x](use-app-v1.md).

## AEM案頭應用程式元件概觀 {#desktop-app-component-overview}

案頭應用程式包含下列元件：

* **案頭應用程式**：應用程式會將DAM掛載或解除安裝為遠端檔案系統，並在本機掛載的網路共用與其連線的遠端AEM執行個體之間轉譯檔案系統呼叫。
* **作業系統WebDAV/SMB使用者端**：處理Windows檔案總管/尋找器和案頭應用程式之間的通訊。 如果檔案被擷取、建立、修改、刪除、移動或複製，作業系統(OS) WebDAV/SMB使用者端會將此作業傳遞給案頭應用程式。 案頭應用程式在收到通訊後，會將其轉譯成原生AEM遠端API呼叫。 例如，如果使用者在掛載的目錄中建立檔案，則WebDAV/SMB使用者端會起始請求，而案頭應用程式會將其轉譯為HTTP請求，以便在DAM中建立檔案。 WebDAV/SMB使用者端是作業系統的內建元件。 它並未以任何方式與案頭應用程式、AEM或Adobe建立關聯。
* **Adobe Experience Manager執行個體**：提供對儲存在AEM Assets DAM存放庫中的資產的存取權。 此外，它代表與掛載網路共用互動的本機案頭應用程式，執行案頭應用程式要求的動作。 目標AEM執行個體應執行AEM 6.1版或更新版本。 執行舊版AEM的AEM執行個體可能需要安裝額外的功能套件和修補程式，才能完全正常運作。

## AEM案頭應用程式的預期使用案例 {#intended-use-cases-for-aem-desktop-app}

AEM案頭應用程式會使用網路共用技術，將遠端AEM存放庫對應至本機案頭。 不過，它並非要取代網路共用資產，因為使用者可以從本機案頭直接執行數位資產管理作業。 這些功能包括移動或複製多個檔案，或直接在Finder/Explorer中將大型資料夾結構拖曳至AEM Assets網路共用。

AEM案頭應用程式可讓您在AEM Assets觸控式UI和本機案頭之間存取（開啟）和編輯（儲存） DAM資產。 它會將AEM Assets伺服器中的資產與您的案頭工作流程連結在一起。

以下範例使用案例說明應如何使用AEM Desktop：

* 使用者登入AEM並使用Web UI來尋找資產。
* 使用AEM Web UI的案頭動作功能，使用者可視需要在案頭上開啟、顯示或編輯資產。
* AEM Desktop會在資產檔案型別的預設編輯器中開啟資產。
* 使用者對資產進行所需的變更。
* 修改檔案後，使用者可以使用AEM Desktop的背景同步狀態視窗來檢視檔案的同步狀態。
* 使用AEM Desktop的內容功能表，使用者可存回/取出資產，或返回DAM使用者介面。
* 完成檔案的變更後，使用者會返回AEM網頁UI

這不是唯一的使用案例。 不過，它說明了AEM Desktop如何成為本機存取/編輯資產的便利機制。 建議您儘可能使用DAM Web UI，因為它可提供更佳的體驗。 它為Adobe提供更大的彈性，以符合客戶需求。

## 限制 {#limitations}

WebDAV/SMB1網路共用提供在Explorer/Finder視窗中處理檔案的便利性。 不過，Explorer/Finder和AEM會透過具有特定限制的網路連線通訊。 例如，將1-GB檔案複製到掛載的WebDAV/SMB目錄所花費的時間，與使用網頁瀏覽器上傳1-GB檔案至網站所需的時間大致相同。 事實上，在前一種情況下，由於WebDAV/SMB通訊協定和OS的WebDAV/SMB使用者端(特別是Mac OS X)的效率低，因此持續的時間可能會更長。

從掛載的目錄可以執行的工作型別有限制。 一般而言，尤其是在不良/高延遲/低頻寬網路連線上處理大型檔案可能會很困難，尤其是在編輯大型檔案時。

Adobe建議您先執行一些使用案例測試，然後再將特定型別的檔案從掛載的目錄就地有效編輯提交給使用者端。

AEM Desktop不適合執行密集的檔案系統操作，包括但不限於：

* 移動或複製檔案和目錄
* 將許多資產新增至AEM
* 透過檔案系統搜尋及開啟檔案（瀏覽資料夾除外）
* 壓縮或解壓縮檔案封存檔

由於作業系統的限制，Windows的檔案大小限製為4,294,967,295位元組（約4.29 GB）。 這是因為登入設定定義了檔案在網路共用上的大小。 登入設定的值是DWORD，其大小上限等於參照的數字。

[!DNL Experience Manager] 案頭應用程式沒有可設定的逾時值，因此會中斷兩者之間的連線 [!DNL Experience Manager] 固定時間間隔後的伺服器和案頭應用程式。 上傳大型資產時，如果連線在一段時間後逾時，應用程式會增加上傳逾時，並重試上傳資產幾次。 沒有建議的方法可變更預設逾時設定。

## 快取和與AEM通訊 {#caching-and-communication-with-aem}

AEM案頭應用程式提供內部快取和背景上傳功能，以改善一般使用者體驗。 儲存大型檔案時，會先將檔案儲存在本機，讓您繼續工作。 過了一會兒（目前為30秒）後，檔案就會在背景傳送至AEM伺服器。

與Creative Cloud Desktop或其他檔案同步處理解決方案(例如Microsoft One Drive)不同，AEM案頭應用程式並非完整的Desktop Sync使用者端。 原因是因為它提供對整個AEM Assets存放庫的存取權，而完整同步可能會非常大（數百個GB或TB）。

快取可讓您將網路/儲存空間開銷限製為與使用者相關的資產子集。

>[!CAUTION]
>
>Adobe建議關閉縮圖產生功能，以加快瀏覽速度。 如果您啟用圖示預覽，應用程式會在您導覽至掛載的資料夾時快取數位資產。 此應用程式也會下載使用者可能不在乎的資產，這會增加伺服器的負載、消耗使用者的頻寬，以及使用更多使用者的磁碟空間。

以下是AEM案頭應用程式執行快取的方式：

* 當您在Finder中開啟資料夾並顯示檔案的縮圖/預覽時，或在應用程式中開啟檔案時，案頭應用程式會快取檔案二進位。
* 當您透過Finder或其他案頭應用程式儲存檔案時，檔案會先儲存在本機（快取），並通知作業系統。 然後，檔案會排入佇列，等待上傳至背景中的伺服器，並最終透過網路進行上傳。 發生網路錯誤時，案頭應用程式最多會重試上傳整個檔案三次。 如果重試三次後上傳失敗，檔案會標示為衝突檔案，且狀態會透過「背景上傳佇列狀態」視窗顯示。 案頭應用程式不再嘗試更新檔案。 使用者應更新檔案，並在連線恢復後重新上傳

不會在本機快取每個作業。 下列專案會立即傳輸至AEM伺服器，而不需要本機快取：

* 對資料夾執行的任何操作，例如建立、刪除等
* 1.4 版本中引入的“文件夹上传”功能可以上传本地文件夹层次结构，而不会在本地缓存文件

## 個別作業 {#individual-operations}

疑難排解個別使用者的次最佳化效能時，請先檢閱 [應用程式限制](#limitations). 後續章節包含改善個別使用者效能的建議。

## 頻寬建議 {#bandwidth-recommendations}

個別使用者可用的頻寬對WebDAV/SMB使用者端的效能至關重要。

Adobe建議個別使用者的上傳速度應接近10 Mbps。 對於無線連線，頻寬通常由多位使用者共用。 如果多個使用者同時執行消耗網路頻寬的工作，效能可能會進一步降低。 為避免此類問題，請使用有線連線。

<!-- AG, 8/18: The Windows KB article is removed by MS now. Giving 404. Also, Win 7 support is gone and the desktop app is also not supported on Win 7. Hiding this content for now.

## Windows-specific configurations {#windows-specific-configurations}

If you use Experience Manager on Windows, you can configure Windows to enhance the performance of the WebDAV client. For more information, go to [https://support.microsoft.com/en-us/kb/2445570](https://support.microsoft.com/en-us/kb/2445570).

On Windows 7, modifying IE settings can improve the performance of WebDAV. For details, see how to [fix slow WebDAV performance in Windows 7](https://oddballupdate.com/2009/12/fix-slow-webdav-performance-in-windows-7/).
-->

## 並行作業 {#concurrent-operations}

當您在本機與檔案互動時，AEM Desktop會檢查AEM中是否有較新版本的檔案可用。 如果有新版本可用，應用程式會將檔案的新復本下載到本機快取。 不過，如果本機快取檔案經過修改，AEM Desktop不會覆寫該檔案。 此功能可防止您的工作不慎被覆寫。

當本機和AEM中同時修改相同檔案時，本機修改的版本會覆寫AEM中的版本。 在這種情況下，資產的時間軸中會提供舊版。 您可以驗證兩個版本並解決任何衝突。

如果本機檔案與伺服器中的可用版本不一致，背景上傳狀態對話方塊會通知您有關衝突的情況。 若要解決此問題，請開啟衝突的檔案並儲存。 儲存檔案會強制AEM Desktop將您最新的本機變更同步到AEM。 您可以在時間軸中檢視資產的舊版本，並解決任何衝突。

當多個使用者嘗試在針對相同AEM執行個體的個別已掛載目錄中工作時，您應該考慮其他因素。 下列因素尤其重要：

* 使用者原始網路上的可用頻寬量
* 原始網路的網路設定，例如防火牆或代理
* 目標AEM執行個體網路中的可用頻寬量
* Dispatcher是否出現在目標AEM執行個體之前
* 目標AEM執行個體上的目前載入

## 其他AEM設定 {#additional-aem-configurations}

如果WebDAV/SMB效能在多位使用者同時工作時大幅降低，您可以在AEM中設定一些有助於改善效能的事項。

## 更新資產暫時性工作流程 {#update-asset-transient-workflows}

您可以為DAM更新資產工作流程啟用暫時性工作流程，以改善AEM端的效能。 啟用暫時性工作流程可減少在AEM中建立或修改資產時更新資產所需的處理能力。

1. 導覽至 `/miscadmin` 在Experience Manager執行個體中(`https://[aem_server]:[port]/miscadmin`)。
1. 在导航树中，展开&#x200B;**工具** > **工作流** > **模型** > **dam**。
1. 按兩下 **DAM更新資產**.
1. 從浮動工具面板，切換至 **頁面** 標籤，然後按一下 **頁面屬性**.
1. 選取 **暫時性工作流程** 核取方塊，然後按一下 **確定**.

### 调整 Granite Transient 工作流程队列 {#adjust-granite-transient-workflow-queue}

另一種改善AEM效能的方法是設定Granite暫時性工作流程佇列工作的最大並行工作值。 建議值大約是伺服器可用CPU數量的一半。 若要調整值，請執行下列步驟：

1. 導覽至 `/system/console/configMgr` 在要設定的AEM執行個體中(例如， `https://[aem_server]:[port]/system/console/configMgr`)。
1. 搜尋 `QueueConfiguration`，然後按一下以開啟每個工作，直到您找到 **Granite暫時性工作流程佇列** 工作，然後按一下 **編輯**.
1. 變更 `Maximum Parallel Jobs` 值，然後按一下 **儲存**.

## AWS設定 {#aws-configuration}

由於網路頻寬限制，當多個使用者同時工作時，WebDAV/SMB的效能可能會降低。 Adobe建議針對在AWS上執行的目標AEM例項，增加AWS例項的大小，以增強WebDAV/SMB的效能。

這項測量特別提高了伺服器可用的網路頻寬量。 以下是一些詳細資料：

* AWS執行個體專用的網路頻寬會隨著執行個體大小的增加而增加。 如需各執行個體大小可用的頻寬資訊，請參閱 [AWS檔案](https://aws.amazon.com/ec2/instance-types/).
* 針對大型使用者端進行疑難排解時，Adobe將其AEM執行個體的大小設定為c4.8xlarge，主要針對其提供的4000 Mbps專用頻寬。
* 如果AEM執行個體前面有Dispatcher，請確保其大小適當。 如果AEM執行個體提供4000 Mbps，但Dispatcher僅提供500 Mbps，則有效頻寬僅為500 Mbps。 這是因為Dispatcher會產生網路瓶頸。

## 已取出檔案限制 {#checked-out-file-limitations}

透過Explorer/Finder與已出庫檔案互動的方式有一些已知限制。 如果檔案已簽出，則除了已簽出該檔案的使用者之外，其他人都應該以唯讀方式存取該檔案。 在AEM中實作WebDAV/SMB1通訊協定會強制執行此規則。 不過，OS WebDAV/SMB使用者端通常無法與取出檔案正常互動。 下文將說明一些奇怪之處。

### 常规 {#general}

寫入出庫檔案時，只有在AEM WebDAV實作中才會強制執行鎖定。 因此，只有使用WebDAV的使用者端（例如案頭應用程式）才會強制執行鎖定。 鎖定不會透過AEM網頁介面強制執行。 AEM介面只會針對已出庫的資產，在卡片檢視中顯示鎖定圖示。 此圖示是裝飾性的，對AEM的行為沒有影響。

一般而言，WebDAV使用者端並不總是如預期般運作。 可能有其他問題。 不過，在AEM中重新整理或檢查資產是驗證資產是否未被修改的可靠方法。 這是典型的OS WebDAV使用者端行為，不受Adobe控制。

### Windows {#windows}

刪除檔案似乎成功，因為檔案會從Windows的檔案總管消失。 不過，重新整理目錄並簽入AEM資產會顯示檔案仍然存在。 此外，編輯檔案似乎已成功（不顯示警告對話方塊或錯誤訊息）。 不過，重新開啟檔案或入庫AEM資產會發現檔案未變更。

#### MAC OS X {#mac-os-x}

取代檔案不會顯示警告或錯誤，但檢查AEM中的資產會顯示它保持不變。 重新整理或檢查AEM中的資產，確認資產未被修改。

## 疑難排解案頭應用程式圖示問題(Mac OS X) {#troubleshooting-desktop-app-icon-issues-mac-os-x}

安裝案頭應用程式後，案頭應用程式功能表圖示會出現在功能表列中。 如果未出現圖示，請執行以下步驟以解決問題：

1. 開啟作業系統終端機視窗。
1. 在命令提示字元處鍵入以下命令，然後按Enter鍵：

   ```shell
    cd ../Library/Caches.
   ```

1. 輸入下列指令，然後按Enter鍵：

   ```shell
   rm -r com.adobe.aem.assetscompanion
   ```

1. 輸入下列指令，然後按Enter鍵：

   ```shell
   cd ~/Library/Preferences
   ```

1. 輸入下列指令，然後按Enter鍵：

   ```shell
   rm com.adobe.aem.assetscompanion.plist
   ```

1. 輸入下列指令，然後按Enter鍵：

   ```shell
   rm ~/Library/Group\ Containers/group.com.adobe.aem.desktop/*
   ```

1. 重新啟動系統。

AEM Desktop會嘗試同步任何指定檔案三次。 如果檔案在第三次嘗試後無法同步，AEM Desktop會將檔案視為衝突，並透過背景上傳狀態視窗通知您。 衝突狀態表示您在本機仍可使用您的最新變更，但是這些變更未同步回AEM。 AEM案頭應用程式不再嘗試同步。

解決此問題最簡單的方法是開啟衝突的檔案並再次儲存。 它會強制AEM Desktop嘗試另外三次同步處理。 如果檔案仍然無法同步，請參閱以下章節以取得更多說明。

## 正在清除AEM案頭快取 {#clearing-aem-desktop-cache}

清除AEM Desktop的快取是初步的疑難排解工作，可解決數個AEM Desktop問題。

您可以在下列位置刪除應用程式的快取目錄，以清除快取。
在Windows中， `%LocalAppData%\Adobe\AssetsCompanion\Cache\`

在Mac中， `~/Library/Group/Containers/group.com.adobe.aem.desktop/cache/`

不過，位置可能會根據AEM Desktop設定的AEM端點而變更。 值是目標URL的編碼版本。 例如，如果應用程式正在鎖定目標 `http://localhost:4502`，目錄名稱為 `http%3A%2F%2Flocalhost%3A4502%2F`.

若要清除快取，請刪除 &lt;encoded aem=&quot;&quot; endpoint=&quot;&quot;> 目錄。

>[!NOTE]
>
>如果您清除AEM案頭快取，未同步至AEM的本機檔案變更將會遺失。

>[!NOTE]
>
>從AEM案頭應用程式1.5版開始，案頭應用程式UI中有一個選項可清除快取。

## 尋找AEM案頭版本 {#finding-the-aem-desktop-version}

確定AEM Desktop版本的程式與Windows和Mac作業系統相同。

按一下AEM案頭圖示，然後選擇 **關於**. 版本編號會顯示在畫面上。

## 在macOS上升級AEM案頭應用程式 {#upgrading-aem-desktop-app-on-macos}

在macOS上升級AEM案頭應用程式時，偶爾可能會發生問題。 這是由於AEM案頭應用程式的舊版系統資料夾導致AEM案頭的新版本無法正確載入。 若要解決此問題，可以手動移除下列資料夾和檔案。

在執行下列步驟之前，請將「Adobe Experience Manager案頭」應用程式從「macOS應用程式」資料夾拖曳至垃圾桶。 然後開啟terminal，然後執行下列命令，在提示時提供您的密碼。

```shell
sudo rm -rf ~/Library/Application\ Support/com.adobe.aem.desktop
sudo rm -rf ~/Library/Preferences/com.adobe.aem.desktop.plist
sudo rm -rf ~/Library/Logs/Adobe\ Experience\ Manager\ Desktop

sudo find /var/folders -type d -name "com.adobe.aem.desktop" | xargs rm -rf
sudo find /var/folders -type d -name "com.adobe.aem.desktop.finderintegration-plugin" | xargs rm -rf
```

## 儲存由其他人簽出的檔案 {#saving-a-file-checked-out-by-others}

作業系統的技術限制，導致使用者在嘗試覆寫其他人簽出的檔案時，無法擁有一致的體驗。 體驗會因用來編輯出庫檔案的應用程式而異。 有時，應用程式會顯示錯誤訊息，指出磁碟寫入失敗，或顯示看似不相關或一般性的錯誤。 在其他情況下，不會顯示錯誤訊息，且操作似乎成功。

在這種情況下，關閉和重新開啟檔案可能會顯示內容未變更。 不過，有些應用程式可能會儲存檔案備份，以便套用您的變更。

無論行為為何，當您入庫檔案時，檔案都會保持不變。 即使顯示檔案的不同版本，變更也不會同步至AEM。

## 疑難排解移動檔案的相關問題 {#troubleshooting-problems-around-moving-files}

伺服器API需要傳遞其他標頭（X-Destination、X-Depth和X-Overwrite），才能讓移動和復製作業運作。 Dispatcher預設不會傳遞這些標頭，這會導致這些作業失敗。 如需詳細資訊，請參閱 [連線到Dispatcher後面的AEM](install-configure-app-v1.md#connect-to-an-aem-instance-behind-a-dispatcher).

## 疑難排解AEM案頭連線問題 {#troubleshooting-aem-desktop-connection-issues}

### SAML重新導向問題 {#saml-redirect-issue}

AEM Desktop連線至已啟用SSO (SAML) AEM執行個體時發生問題的最常見原因是SAML程式不會重新導向回最初請求的路徑。 或者，也可以將連線重新導向到未在AEM案頭中設定的主機。 執行以下步驟來驗證登入程式：

1. 打开 Web 浏览器。
1. 在位址列中，指定URL `/content/dam.json`.
1. 以目標AEM例項取代URL，例如 `https://localhost:4502/content/dam.json`.
1. 登入AEM。
1. 登入後，在位址列中檢查瀏覽器目前的位址。 它應該與您最初輸入的URL相符。
1. 確認之前的所有內容 `/content/dam.json` 符合AEM Desktop中設定的目標AEM值。

### SSL設定問題 {#ssl-configuration-issue}

AEM案頭應用程式用於HTTP通訊的程式庫會使用嚴格的SSL強制執行。 有時，連線可能會成功使用瀏覽器，但無法使用AEM案頭應用程式。 若要正確設定SSL，請在Apache中安裝缺少的中間憑證。 另請參閱 [如何在Apache中安裝中間CA憑證](https://access.redhat.com/solutions/43575).

## 搭配Dispatcher使用AEM Desktop {#using-aem-desktop-with-dispatcher}

AEM Desktop可與Dispatcher後面的AEM部署搭配使用，這是AEM伺服器的預設和建議設定。 AEM製作環境前的AEM Dispatcher通常會設定為略過快取DAM資產。 因此，Dispatcher不會從AEM Desktop的角度提供額外的快取。 確保已調整Dispatcher設定，以適用於AEM Desktop。 如需其他詳細資訊，請參閱 [連線到Dispatcher後面的AEM](install-configure-app-v1.md#connect-to-an-aem-instance-behind-a-dispatcher).

## 檢查記錄檔 {#checking-for-log-files}

根據您的作業系統，您可以在下列位置找到AEM Desktop的記錄檔：

* Windows: `%LocalAppData%\Adobe\AssetsCompanion\Logs`
* Mac： `~/Library/Logs/Adobe\ Experience\ Manager\ Desktop`
