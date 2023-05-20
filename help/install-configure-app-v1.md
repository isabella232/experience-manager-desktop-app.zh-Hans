---
title: 安裝及設定案頭應用程式v1.10
description: 安裝及設定 [!DNL Experience Manager] 使用的案頭應用程式1.10版 [!DNL Assets] 將資產對應成磁碟機掛載到您的桌上型電腦上。
exl-id: 7f3bdfb1-d345-4e48-b020-6e06531f46f2
source-git-commit: 78f18e68178f711d925d7e308822c657087d009a
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 0%

---

# 安裝及設定 [!DNL Experience Manager] 案頭應用程式v1.10 {#install-and-configure-aem-desktop-app}

使用 [!DNL Experience Manager] 案頭應用程式，資產在 [!DNL Experience Manager] 可輕鬆在本機桌上型電腦上存取，並可用於任何桌上型電腦應用程式。 資產可在Mac Finder或Windows檔案總管中輕鬆顯示、在案頭應用程式中開啟，並在本機變更 — 變更會儲存回 [!DNL Experience Manager] 當您上傳並在存放庫中建立新版本時。

這種整合可讓組織中的各種角色集中管理Assets中的資產，並在Creative Cloud和其他應用程式中存取這些資產，同時讓您輕鬆遵守包括品牌在內的各種標準。

使用 [!DNL Experience Manager] 案頭應用程式，

* 確保您的 [!DNL Experience Manager] 伺服器版本受到支援 [!DNL Experience Manager] 案頭應用程式。 請參閱 [相容性矩陣](release-notes-of-v1.md#compatibilitymatrix).

* 下載並安裝應用程式。

* 使用幾個資產測試連線。 另請參閱 [存取和開啟您案頭上的資產](use-app-v1.md#openondesktop).

## 系統需求、必要條件和下載連結 {#system-requirements-prerequisites-and-download-links}

如需詳細資訊，請參閱 [[!DNL Experience Manager] 案頭應用程式發行說明](release-notes-of-v1.md).

## 安裝應用程式並將其連線至 [!DNL Experience Manager] 伺服器 {#install-and-connect-aem-desktop-app-to-aem-server}

如需詳細資訊，請參閱 [安裝並連線 [!DNL Experience Manager] 案頭應用程式至 [!DNL Experience Manager] 伺服器](use-app-v1.md#installandconnect).

>[!NOTE]
>
>只有一個例項 [!DNL Experience Manager] 案頭應用程式可以一次安裝並啟用。

## 檔案處理 {#file-handling}

從案頭應用程式掛載的網路共用位置變更檔案時，檔案會分兩個階段儲存至該位置。 在第一階段，檔案會儲存在本機。 使用者可以儲存檔案並繼續處理檔案，而無需等待傳輸完成。

在第二個階段，案頭應用程式會將更新的檔案上傳至 [!DNL Experience Manager] 在預先定義的延遲（例如30秒）之後傳送伺服器。 此作業會在背景中進行。 使用「檢視資產狀態」選項可檢視上傳作業的狀態。

1. 上傳資產至資產。

1. 按一下 [!DNL Experience Manager] 案頭應用程式圖示。

1. 從功能表中選取檢視資產狀態選項。

1. 在對話方塊中，檢閱上傳操作的狀態。

>[!NOTE]
>
>[!DNL Experience Manager] 案頭應用程式最多可處理40 GB大小的資產。

## 連線到 [!DNL Experience Manager] Dispatcher背後的執行個體 {#connect-to-an-aem-instance-behind-a-dispatcher}

Assets API中的複製和移動方法需要將以下附加標頭傳遞到 [!DNL Experience Manager]：

* X-Destination
* X深
* X覆寫

[!DNL Experience Manager] 案頭連線至 [!DNL Experience Manager] 使用包含預設連線埠的URL。 因此， `virtualhosts` dispatcher設定中的設定應包含預設連線埠號碼。 有關詳細資訊 `virtualhosts` 設定，請參閱 [識別虛擬主機](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#identifying-virtual-hosts-virtualhosts).

如需有關設定Dispatcher傳遞這些其他標頭的其他資訊，請參閱 [指定HTTP標題](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#specifying-the-http-headers-to-pass-through-clientheaders).

### Proxy支援 {#proxy-support}

[!DNL Experience Manager] 案頭應用程式會使用系統預先定義的Proxy，透過HTTPS連線至網際網路。 應用程式只能使用不需要額外驗證的網路Proxy連線。

如果您設定或修改Windows的Proxy伺服器設定（[網際網路選項] > [區域網路設定]），請重新啟動 [!DNL Experience Manager] 案頭應用程式讓變更生效。

>[!NOTE]
>
>Proxy設定只會在您啟動案頭應用程式時套用。 關閉並重新啟動應用程式，任何變更才會生效。

如果您的Proxy需要驗證，IT團隊可以允許Proxy伺服器設定中的Experience Manager Assets URL，讓應用程式流量通過。

## 自訂資產資訊對話方塊 {#customize-the-asset-info-dialog}

您可以覆蓋下列一個或兩個元件，以自訂「資產資訊」對話方塊：

* Granite使用者介面頁面位於 `/libs/dam/gui/content/assets/moreinfo`.

* HTL `/css/javascript` 元件於 `/libs/dam/gui/components/admin/moreinfo`.

覆蓋哪個元件，取決於自訂的性質。 若要變更哪些元件會顯示為「資產資訊」對話方塊的一部分，請覆蓋Granite使用者介面頁面。 若要變更對話方塊的HTML、CSS或JavaScript內容，請覆蓋HTL元件。

## 管理快取 {#manage-cache}

在Windows上，快取位於 `%LOCALAPPDATA%\Adobe\AssetsCompanion\Cache\`，其中是的編碼版本 [!DNL Experience Manager] 在案頭應用程式中設定的主機。 例如， `http://localhost:4502` 顯示為 `http%3A%2F%2Flocalhost%3A4502%2F`.

在Mac OS X上，類似的目錄位於 `~/Library/Group Containers/group.com.adobe.aem.desktop/cache`.

### 管理快取的應用程式內選項 {#in-app-option-to-manage-cache}

您可以控制可用於本機快取的磁碟空間量。 系統會在本機快取Assets伺服器的人工因素，以獲得更順暢的體驗。 您可以變更預設值以符合您的需求。 此外，您也可以清除快取，以重新擷取所有資產。 若要設定所需選項，請按一下應用程式的圖示，然後按一下 **[!UICONTROL Advanced]** > **[!UICONTROL Manage Cache]**.****

>[!NOTE]
>
>當您清除快取時，它會保留您未儲存的變更。 任何未簽入的資產 [!DNL Experience Manager] 伺服器會保留且不會刪除。

### 變更Windows上的快取位置 {#change-location-of-cache-on-windows}

的預設快取位置 [!DNL Experience Manager] 案頭應用程式如下：

* 在Windows中， `%LocalAppData%\Adobe\AssetsCompanion\Cache\EncodedAEMEndpoint`.

* 在Mac中， `~/Library/Group/Containers/group.com.adobe.aem.desktop/cache/EncodedAEMEndpoint`.

`EncodedAEMEndpoint` 應用程式是否已設定 [!DNL Experience Manager] 端點URL。 值是以下專案的目標URL的編碼版本： [!DNL Experience Manager] 伺服器。 例如，如果應用程式正在鎖定目標 `http://localhost:4502`，目錄名稱為 `http%3A%2F%2Flocalhost%3A4502`. 在此範例中，快取目錄的Windows路徑為 `%LocalAppData%\Adobe\AssetsCompanion\Cache\http%3A%2F%2Flocalhost%3A4502`.

若要將應用程式指向不同的資料夾或磁碟機，請編輯應用程式的組態檔。

1. 導覽至應用程式的安裝目錄。 Windows上的預設位置為 `C:\Program Files (x86)\Adobe\Adobe Experience Manager Desktop`.

1. 使用文字編輯器編輯Adobe Experience Manager Desktop.exe.config檔案。

   需要管理員許可權才能儲存對此檔案的變更。

1. 搜尋字串「ProxyCacheRoot」。 您會看到其值已設定為快取位置 `%LocalAppData%\Adobe\AssetsCompanion\Cache`. 只需將此值變更為任何有效路徑即可。

   >[!NOTE]
   >
   >應用程式會自動建立 *&lt;encoded aem=&quot;&quot; endpoint=&quot;&quot;>* 子目錄。 無法設定此行為。

>[!MORELIKETHIS]
* [簡介 [!DNL Experience Manager] 案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/creative-workflows/aem-desktop-app.html).
* [使用 [!DNL Experience Manager] 案頭應用程式](use-app-v1.md).
* [疑難排除 [!DNL Experience Manager] 案頭應用程式](troubleshoot-app-v1.md).

