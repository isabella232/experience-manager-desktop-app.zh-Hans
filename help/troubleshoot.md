---
title: 最佳作法和疑難排解 [!DNL Adobe Experience Manager] 案頭應用程式
description: 遵循最佳實務和疑難排解，以解決與安裝、升級、設定等相關的偶爾問題。
exl-id: f388e4ac-907d-4093-ba6f-86ecdafeb015
source-git-commit: 2c846fb9cd82691f6439e93429dffcca8127ba68
workflow-type: tm+mt
source-wordcount: '2260'
ht-degree: 0%

---

# 疑難排解 [!DNL Adobe Experience Manager] 案頭應用程式 {#troubleshoot-v2}

[!DNL Adobe Experience Manager] 案頭應用程式連線至 [!DNL Experience Manager] 部署的數位資產管理(DAM)存放庫。 應用程式會擷取您電腦上的存放庫資訊和搜尋結果、下載和上傳檔案及資料夾，並包含管理與Assets使用者介面衝突的功能。

請閱讀下文，針對應用程式進行疑難排解、瞭解最佳實務，並找出限制。

## 最佳實務 {#best-practices-to-prevent-troubles}

請遵循下列最佳實務，以避免一些常見問題和疑難排解。

* **瞭解案頭應用程式的運作方式**：在開始使用應用程式之前，請先花點時間瞭解應用程式的運作方式。 瞭解之間的連結 [!DNL Experience Manager] 網頁介面和案頭、存放庫對應、資產快取、本機儲存和背景上傳。 另請參閱 [運作方式](release-notes.md#how-app-works).

* **避免資料夾名稱中出現不支援的字元**：建立或上傳資料夾時，請勿使用空格和無效字元。 請參閱下列位置的字元清單： [在中建立資料夾 [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.html#creating-folders). 部分 [!DNL Experience Manager] 使用案例可能會受到資料夾名稱中不支援的字元影響。

* **避免衝突的最佳實務**：若要避免在共同作業多個資產時發生潛在衝突，請參閱 [避免編輯衝突](using.md#adv-workflow-collaborate-avoid-conflicts).

* **使用大型階層式資料夾的資料夾上傳**：請避免使用Assets網頁介面或其他方法，改用 [!DNL Experience Manager] 案頭應用程式來上傳大型資料夾。 應用程式會在背景使用記錄及監控功能上傳資產。 另請參閱 [大量上傳資產](using.md#bulk-upload-assets).

* **使用最新版本**：使用最新的應用程式版本，並在安裝新應用程式版本或升級至更新版本之前一律檢查相容性 [!DNL Experience Manager] 版本。 另請參閱 [發行說明](release-notes.md).

* **使用相同的磁碟機代號**：在組織內使用相同的磁碟機代號來對應至 [!DNL Experience Manager] DAM。 若要檢視其他使用者置入的資產，路徑必須相同。 使用相同的磁碟機代號可確保指向DAM資產的固定路徑。 即使不同的使用者使用不同的磁碟機代號，資產仍會放置且不會移除。

* **請留意網路**：網路效能對於 [!DNL Experience Manager] 案頭應用程式的效能。 如果您遇到檔案傳輸或大量作業回應速度變慢的問題，請關閉可能導致大量網路流量的功能或應用程式。

* **案頭應用程式不支援的使用案例**：請勿將應用程式用於資產移轉（需要規劃和其他工具）；適用於大量的DAM作業（例如移動大型資料夾、大型上傳、使用進階中繼資料搜尋尋找檔案）；以及作為同步使用者端(設計原則和使用模式有別於同步使用者端，例如Microsoft OneDrive或Adobe Creative Cloud案頭同步)。

* **逾時**：目前，案頭應用程式沒有可設定的逾時值，因此會中斷兩者之間的連線 [!DNL Experience Manager] 固定時間間隔後的伺服器和案頭應用程式。 上傳大型資產時，如果連線在一段時間後逾時，應用程式會增加上傳逾時，並重試上傳資產幾次。 沒有建議的方法可變更預設逾時設定。

## 如何疑難排解 {#troubleshooting-prep}

若要疑難排解案頭應用程式問題，請注意下列資訊。 此外，如果您選擇尋求支援，也能讓您更妥善地將問題傳達給Adobe客戶支援。

### 記錄檔的位置 {#check-log-files-v2}

[!DNL Experience Manager] 案頭應用程式會根據作業系統將其記錄檔儲存在下列位置：

在Windows上： `%LocalAppData%\Adobe\AssetsCompanion\Logs`

在Mac上： `~/Library/Logs/Adobe\ Experience\ Manager\ Desktop`

上傳許多資產時，如果部分檔案上傳失敗，請參閱 `backend.log` 識別失敗上傳的檔案。

>[!NOTE]
>
>處理Adobe客戶支援的支援要求或票證時，系統會要求您共用記錄檔，以協助客戶支援團隊瞭解問題。 封存整個 `Logs` 資料夾並與客戶支援聯絡人分享。

### 變更記錄檔中的詳細資訊層級 {#level-of-details-in-log}

若要變更記錄檔中的詳細資訊層級：

1. 確認應用程式未執行。

1. 在Windows系統上：

   1. 開啟命令視窗。

   1. Launch [!DNL Adobe Experience Manager] 案頭應用程式，執行命令：

   ```shell
   set AEM_DESKTOP_LOG_LEVEL=DEBUG&"C:\Program Files\Adobe\Adobe Experience Manager Desktop.exe
   ```

   在Mac系統上：

   1. 開啟終端機視窗。

   1. Launch [!DNL Adobe Experience Manager] 案頭應用程式，執行命令：

   ```shell
   AEM_DESKTOP_LOG_LEVEL=DEBUG open /Applications/Adobe\ Experience\ Manager\ Desktop.app
   ```

有效的記錄層級為DEBUG、INFO、WARN或ERROR。 記錄檔的詳細程度在DEBUG中是最高的，在ERROR中是最低的。

### 啟用偵錯模式 {#enable-debug-mode}

若要進行疑難排解，您可以啟用偵錯模式，並在記錄中取得更多資訊。

>[!NOTE]
>
>有效的記錄層級為DEBUG、INFO、WARN或ERROR。 記錄檔的詳細程度在DEBUG中是最高的，在ERROR中是最低的。

若要在Mac上以除錯模式使用應用程式：

1. 開啟終端機視窗或命令提示。

1. 啟動 [!DNL Experience Manager] 透過執行以下命令來操作案頭應用程式：

   `AEM_DESKTOP_LOG_LEVEL=DEBUG open /Applications/Adobe\ Experience\ Manager\ Desktop.app`。

若要在Windows上啟用偵錯模式：

1. 開啟命令視窗。

1. Launch [!DNL Experience Manager] 透過執行以下命令來操作案頭應用程式：

`AEM_DESKTOP_LOG_LEVEL=DEBUG&"C:\Program Files\Adobe\Adobe Experience Manager Desktop.exe`。

### 瞭解 [!DNL Adobe Experience Manager] 案頭應用程式版本 {#know-app-version-v2}

若要檢視版本編號，請執行下列動作：

1. 啟動應用程式。

1. 按一下右上角的省略符號，將滑鼠游標停留在 [!UICONTROL Help]，然後按一下 [!UICONTROL About].

   版本編號會列在此畫面上。

### 清除缓存 {#clear-cache-v2}

執行下列步驟：

1. 啟動應用程式並連線 [!DNL Experience Manager] 執行個體。

1. 按一下右上角的橢圓並選取「 」，開啟應用程式的偏好設定 [!UICONTROL Preferences].

1. 找到顯示 [!UICONTROL Current Cache Size]. 按一下此元素旁的垃圾桶圖示。

若要手動清除快取，請繼續下列步驟。

>[!CAUTION]
>
>這是潛在的破壞性作業。 如果有未上傳到的本機檔案變更 [!DNL Adobe Experience Manager]，則這些變更將會因繼續操作而遺失。

透過刪除應用程式的快取目錄（可在應用程式的偏好設定中找到）來清除快取。

1. 啟動應用程式。

1. 選取右上角的橢圓並選取「 」，開啟應用程式的偏好設定 [!UICONTROL Preferences].

1. 請注意 [!UICONTROL Cache Directory] 值。

   此目錄中有以編碼的子目錄 [!DNL Adobe Experience Manager] 端點。 名稱是目標的編碼版本 [!DNL Adobe Experience Manager] URL。 例如，如果應用程式正在鎖定目標 `localhost:4502` 則目錄名稱將為 `localhost_4502`.

若要清除快取，請刪除所需的編碼 [!DNL Adobe Experience Manager] 端點目錄。 或者，刪除偏好設定中指定的整個目錄將會清除應用程式已使用的所有例證的快取記憶體。

清除 [!DNL Adobe Experience Manager] 案頭應用程式的快取是初步的疑難排解工作，可解決數個問題。 從應用程式偏好設定中清除快取。 另請參閱 [設定偏好設定](install-upgrade.md#set-preferences). 快取資料夾的預設位置為：

## 看不到已放置的資產 {#placed-assets-missing}

如果您無法看到您或其他創意專業人士放置在支援檔案中的資產（例如INDD檔案），請檢查以下內容：

* 連線到伺服器。 不穩定的網路連線可能會延遲資產下載。

* 檔案大小。 大型資產的下載和顯示時間較長。

* 磁碟機代號一致性。 如果您或其他共同作業人員在對應資產時放置資產， [!DNL Experience Manager] DAM至不同的磁碟機代號，置入的資產不會顯示。

* 权限。若要檢查您是否擁有擷取所放置資產的許可權，請聯絡您的 [!DNL Experience Manager] 管理員。

### 對案頭應用程式使用者介面上的檔案所做的編輯不會反映在 [!DNL Adobe Experience Manager] 立即 {#changes-on-da-not-visible-on-aem}

[!DNL Adobe Experience Manager] 案頭應用程式可讓使用者決定檔案的所有編輯何時完成。 根據檔案的大小和複雜性，將檔案的新版本傳輸回需要花費大量時間 [!DNL Adobe Experience Manager]. 應用程式的設計要求將檔案來回傳輸的次數減到最少，而不是在檔案編輯完成並自動上傳時進行猜測。 建議使用者起始將檔案傳輸回 [!DNL Adobe Experience Manager] 選擇上傳檔案的變更。

### 在macOS上升級時的問題 {#issues-when-upgrading-on-macos}

升級時偶爾可能會發生問題 [!DNL Experience Manager] macOS上的案頭應用程式。 這是由於的舊版系統資料夾造成的 [!DNL Experience Manager] 案頭應用程式防止新版本的 [!DNL Experience Manager] 案頭應用程式以正確載入。 若要解決此問題，可以手動移除下列資料夾和檔案。

在執行下列步驟之前，拖曳 `Adobe Experience Manager Desktop` 應用程式從macOS Applications資料夾移至垃圾桶。 然後開啟「終端機」，執行以下命令，並在出現提示時提供您的密碼。

```shell
sudo rm -rf ~/Library/Application\ Support/com.adobe.aem.desktop
sudo rm -rf ~/Library/Preferences/com.adobe.aem.desktop.plist
sudo rm -rf ~/Library/Logs/Adobe\ Experience\ Manager\ Desktop

sudo find /var/folders -type d -name "com.adobe.aem.desktop" | xargs rm -rf
sudo find /var/folders -type d -name "com.adobe.aem.desktop.finderintegration-plugin" | xargs rm -rf
```

## 無法上傳檔案 {#upload-fails}

如果您使用案頭應用程式搭配 [!DNL Experience Manager] 6.5.1或更新版本，請將S3或Azure聯結器升級至1.10.4或更新版本。 它解決了與相關的檔案上傳失敗問題 [OAK-8599](https://issues.apache.org/jira/browse/OAK-8599). 另請參閱 [安裝指示](install-upgrade.md#install-v2).

## [!DNL Experience Manager] 案頭應用程式連線問題 {#connection-issues}

如果您遇到一般連線問題，以下提供一些取得更多資訊的方法 [!DNL Experience Manager] 案頭應用程式正在執行。

**檢查請求記錄**

[!DNL Experience Manager] 案頭應用程式會將它傳送的所有請求以及每個請求的回應代碼記錄在一個專用的記錄檔中。

1. 開啟 `request.log` 在應用程式的記錄檔目錄中檢視這些要求。

1. 記錄中的每一行代表請求或回應。 請求將具有 `>` 字元，後跟請求的URL。 回應將具有 `<` 字元，後面接著回應代碼和請求的URL。 可使用每一行的GUID來比對請求和回應。

**檢查應用程式內嵌瀏覽器載入的請求**

大部分應用程式的要求可在要求記錄中找到。 不過，如果沒有實用資訊，則檢視應用程式的內嵌瀏覽器所傳送的請求會很有用。
請參閱 [SAML區段](#da-connection-issue-with-saml-aem) 以取得如何檢視這些請求的指示。

### SAML登入驗證無法運作 {#da-connection-issue-with-saml-aem}

[!DNL Experience Manager] 案頭應用程式可能無法連線至已啟用SSO (SAML) [!DNL Adobe Experience Manager] 部署。 應用程式的設計嘗試適應SSO連線和程式的變異和複雜性。 不過，安裝程式可能需要額外的疑難排解。

有時SAML程式不會重新導向回最初請求的路徑，或最終重新導向到的主機與中設定的不同 [!DNL Adobe Experience Manager] 案頭應用程式。 若要確認情況並非如此：

1. 打开 Web 浏览器。存取 `https://[aem_server]:[port]/content/dam.json` URL。

1. 登入 [!DNL Adobe Experience Manager] 部署。

1. 登入完成後，請在位址列檢視瀏覽器目前的位址。 它應該與最初輸入的URL完全相符。

1. 同時確認之前的所有內容 `/content/dam.json` 符合目標 [!DNL Adobe Experience Manager] 值設定於 [!DNL Adobe Experience Manager] 案頭應用程式的設定。

**登入SAML程式按照上述步驟正確運作，但使用者仍然無法登入**

內的視窗 [!DNL Adobe Experience Manager] 顯示登入程式的案頭應用程式只是顯示目標的網頁瀏覽器 [!DNL Adobe Experience Manager] 執行個體的網頁使用者介面：

* Mac版本使用 [WebView](https://developer.apple.com/documentation/webkit/webview).

* Windows版本使用Chromium型 [CefSharp](https://cefsharp.github.io/).

請確定SAML程式支援這些瀏覽器。

若要進一步疑難排解，可以檢視瀏覽器嘗試載入的確切URL。 若要檢視此資訊，請執行下列動作：

1. 請依照中的指示啟動應用程式 [偵錯模式](#enable-debug-mode).

1. 重現登入嘗試。

1. 導覽至 [記錄檔目錄](#check-log-files-v2) 應用程式的

1. 對於Windows：

   1. 開啟「aemcompanionlog.txt」。

   1. 搜尋以「登入瀏覽器位址已變更為」開頭的訊息。 這些專案也包含應用程式載入的URL。

   若為Mac：

   1. `com.adobe.aem.desktop-nnnnnnnn-nnnnnn.log`，其中 **n** 會以最新檔案名稱中的數字取代。

   1. 搜尋以「載入的框架」開頭的訊息。 這些專案也包含應用程式載入的URL。


檢視正在載入的URL序列有助於在SAML端進行疑難排解，以判斷哪裡出了問題。

### SSL設定問題 {#ssl-config-v2}

具備下列條件的程式庫： [!DNL Experience Manager] 案頭應用程式用於HTTP通訊時，會使用嚴格的SSL強制執行。 有時，連線可能使用瀏覽器成功，但無法使用瀏覽器 [!DNL Experience Manager] 案頭應用程式。 若要正確設定SSL，請在Apache中安裝缺少的中間憑證。 另請參閱 [如何在Apache中安裝中間CA憑證](https://access.redhat.com/solutions/43575).

具備下列條件的程式庫： [!DNL Experience Manager] 案頭應用程式使用進行HTTP通訊時，會使用嚴格的SSL強制執行。 因此，在某些情況下，透過瀏覽器成功的SSL連線可能會失敗 [!DNL Adobe Experience Manager] 案頭應用程式。 這是好事，因為它鼓勵正確設定SSL並增加安全性，但當應用程式無法連線時可能會令人沮喪。

在此情況下，建議使用工具來分析伺服器的SSL憑證並識別問題，以便進行更正。 有些網站會在提供伺服器URL時檢查伺服器的憑證。

作為臨時措施，可以停用中嚴格的SSL強制執行 [!DNL Adobe Experience Manager] 案頭應用程式。 不建議使用此長期解決方案，因為它會隱藏錯誤設定SSL的根本原因，以降低安全性。 若要停用嚴格強制執行：

1. 使用您選擇的編輯器來編輯應用程式的JavaScript設定檔案，這些檔案可在（預設）下列位置找到（視作業系統而定）：

   在Mac上： `/Applications/Adobe Experience Manager Desktop.app/Contents/Resources/javascript/lib-smb/config.json`

   在Windows上： `C:\Program Files (x86)\Adobe\Adobe Experience Manager Desktop\javascript\config.json`

1. 在檔案中找出下列區段：

   ```shell
   ...
   "assetRepository": {
       "options": {
   ...
   ```

1. 透過新增來修改區段 `"strictSSL": false` 如下所示：

   ```shell
   ...
   "assetRepository": {
       "options": {
           "strictSSL": false,
   ...
   ```

1. 儲存檔案並重新啟動 [!DNL Adobe Experience Manager] 案頭應用程式。

### 切換至其他伺服器時出現登入問題 {#cannot-login-cookies-issue}

使用 [!DNL Experience Manager] 伺服器，當您嘗試變更其他伺服器的連線時，可能會遇到登入問題。 這是由於舊的Cookie干擾了新驗證。 主功能表中的選項 [!UICONTROL Clear Cookies] 有幫助。 登出應用程式中的目前工作階段並選取 [!UICONTROL Clear Cookies] 然後再繼續連線。

![切換伺服器時清除Cookie](assets/main_menu_logout_da2.png)

## 應用程式無回應 {#unresponsive}

極少數情況下，應用程式可能會變得無回應、只顯示白色熒幕，或在介面底部顯示錯誤（沒有任何介面選項）。 請依照順序嘗試下列操作：

* 在應用程式介面上按一下滑鼠右鍵，然後按一下 **[!UICONTROL Refresh]**.
* 請退出應用程式，然後重新開啟。

在這兩種方法中，應用程式都會從根DAM資料夾開始。

## 隱藏過期的資產 {#hide-expired-assets}

從內瀏覽資產時 [!DNL Experience Manager] 使用者介面中，不會顯示過期的資產。 若要防止在從案頭應用程式和Asset Link瀏覽資產時檢視、搜尋和擷取已到期資產，管理員可以執行下列設定。 此設定適用於所有使用者，無論管理員許可權為何。

* [Experience Manager6.5中隱藏過期資產的設定](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.html#hide-expired-assets-via-acp-api).
* [Experience Manageras a Cloud Service中用於隱藏過期資產的設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/manage/manage-digital-assets.html#hide-expired-assets-via-acp-api).

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
>* [避免編輯衝突](using.md#adv-workflow-collaborate-avoid-conflicts)

