---
title: "設定 Endpoint Protection 用戶端 | Microsoft Docs"
description: "了解如何設定可部署至階層中之電腦集合的 Endpoint Protection 自訂用戶端設定。"
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
caps.latest.revision: "21"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 1488aaa465fb9810bc1b641d41dad95189d37418
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="configure-custom-client-settings-for-endpoint-protection"></a>設定 Endpoint Protection 的自訂用戶端設定

*適用於：System Center Configuration Manager (最新分支)*

此程序會為 Endpoint Protection 設定自訂用戶端設定，這些設定可部署到階層中的電腦集合。

> [!IMPORTANT]
>  如果您確定要將設定套用到階層中的所有電腦，請僅設定預設的 Endpoint Protection 用戶端設定。

## <a name="to-enable-endpoint-protection-and-configure-custom-client-settings"></a>啟用 Endpoint Protection 及設定自訂用戶端設定

1.  在 Configuration Manager 主控台中，按一下 [系統管理] 。

2.  在 [系統管理]  工作區中，按一下 [用戶端設定] 。

3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立自訂用戶端裝置設定] 。

4.  在 [建立自訂用戶端裝置設定]  對話方塊中，提供設定群組的名稱和說明，然後選取 [Endpoint Protection] 。

5.  設定您需要的 Endpoint Protection 用戶端設定。 如需您可以設定的 Endpoint Protection 用戶端設定完整清單，請參閱[關於 System Center Configuration Manager 中的用戶端設定](../../core/clients/deploy/about-client-settings.md)中的＜Endpoint Protection＞一節。

   > [!IMPORTANT]
   >  您必須先安裝 Endpoint Protection 站台系統角色，才可以設定 Endpoint Protection 的用戶端設定。

6.  按一下 [確定]  關閉 [建立自訂用戶端裝置設定]  對話方塊。 新的用戶端設定會顯示在 [系統管理]  工作區的 [用戶端設定]  節點中。

7.  您必須先將自訂用戶端設定部署至集合，才可加以使用。 選取您想要部署的自訂用戶端設定，然後在 [首頁]  索引標籤的 [用戶端設定]  群組中，按一下 [部署] 。

8.  在 [選取集合]  對話方塊中，選取您想要在其中部署用戶端設定的集合，然後按一下 [確定] 。 新的部署會顯示在 [詳細資料] 窗格的 [部署]  索引標籤中。

用戶端電腦將會在下一次下載用戶端原則時進行這些設定。 若要起始單一用戶端的原則抓取，請參閱[如何在 System Center Configuration Manager 中管理用戶端](../../core/clients/manage/manage-clients.md)中的＜起始 Configuration Manager 用戶端的原則抓取＞一節。

## <a name="how-to-provision-the-endpoint-protection-client-in-a-disk-image-in-configuration-manager"></a>如何在 Configuration Manager 的磁碟映像檔中佈建 Endpoint Protection 用戶端。
您可以在將作為 Configuration Manager 作業系統部署磁碟映像來源的電腦上，安裝 Endpoint Protection 用戶端。 這個電腦通常稱為參照電腦。 在您建立作業系統的映像之後，就能使用 Configuration Manager 作業系統部署將可包含軟體套件 (包括 Endpoint Protection) 的映像部署至您的用戶端電腦。

使用本主題中的程序，可協助您在參照電腦上安裝並設定 Endpoint Protection 用戶端

### <a name="prerequisites-for-installing-the-endpoint-protection-client-on-the-reference-computer"></a>在參照電腦上安裝 Endpoint Protection 用戶端的必要條件
以下清單包含在參照電腦上安裝 Endpoint Protection 用戶端軟體所需的必要條件。

-   您必須能夠存取 Endpoint Protection 用戶端安裝套件 **scepinstall.exe**。 您可以在站台伺服器上 Microsoft System Center Configuration Manager 安裝資料夾的 [Client] 資料夾中找到這個套件。

-   為了確保 Endpoint Protection 用戶端與您組織所需的設定一起部署，請建立反惡意程式碼原則，然後將該原則匯出。 接著，您就可以指定要在手動安裝 Endpoint Protection 用戶端時使用的反惡意程式碼原則。 如需詳細資訊，請參閱[如何在 System Center Configuration Manager 中建立和部署 Endpoint Protection 的反惡意程式碼原則](endpoint-antimalware-policies.md)。

   > [!NOTE]
   >  [預設用戶端反惡意程式碼原則]  無法匯出。

-   如果您想要安裝具有最新定義的 Endpoint Protection 用戶端，您必須從 [Microsoft 惡意程式碼防護中心](http://go.microsoft.com/fwlink/?LinkID=200965)下載。

### <a name="how-to-install-the-endpoint-protection-client-software-on-the-reference-computer"></a>如何在參照電腦上安裝 Endpoint Protection 用戶端軟體
您可以從命令提示字元在參照電腦本機安裝 Endpoint Protection 用戶端。 若要執行這項操作，您必須先取得安裝檔案 **scepinstall.exe**。 您也可以使用預先設定的反惡意程式碼原則或先前匯出的反惡意程式碼原則安裝用戶端。

## <a name="to-install-the-endpoint-protection-client-from-a-command-prompt"></a>從命令提示字元安裝 Endpoint Protection 用戶端

1.  從 System Center Configuration Manager 安裝媒體上的 [Client] 資料夾，將 **scepinstall.exe** 複製到您要安裝 Endpoint Protection 用戶端軟體的電腦上。

2.  使用系統管理員權限開啟命令提示字元，瀏覽至 **scepinstall.exe** 所在的資料夾，然後執行以下命令，新增任何其他您需要的命令列內容：

   ```
   scepinstall.exe
   ```

    您可以指定下列其中一個命令列內容：

   |屬性|說明|
   |--------------|-----------------|
   |/s|指定要執行的無訊息安裝。|
   |/q|指定要執行的安裝檔案無訊息解壓縮。|
   |/i|指定要執行的一般安裝。|
   |/noreplace|指定在安裝期間不解除安裝的協力廠商反惡意程式碼軟體。|
   |/policy|指定在安裝期間用來設定用戶端的反惡意程式碼原則檔案。|
   |/sqmoptin|指定此用戶端軟體安裝加入 Microsoft 客戶經驗改進計畫。|

3.  遵循螢幕指示以完成用戶端安裝。

4.  如果您已下載最新的更新定義套件，請複製套件至用戶端電腦，然後按兩下定義套件予以安裝。

   > [!NOTE]
   >  在 Endpoint Protection 用戶端安裝完成之後，用戶端會自動執行定義更新檢查。 如果此更新檢查成功，您就不需要手動安裝最新的定義更新套件。

## <a name="to-install-the-client-software-with-an-antimalware-policy-from-the-command-prompt"></a>從命令提示字元使用反惡意程式碼原則安裝用戶端軟體

1.  將 **scepinstall.exe** 和匯出的或預先定義的反惡意程式碼原則，複製到您要安裝 Endpoint Protection 用戶端軟體的電腦上。

2.  使用系統管理員權限開啟命令提示字元，瀏覽至 **scepinstall.exe** 反惡意程式碼原則所在的資料夾，然後執行下列命令：

   ```
   scepinstall.exe /policy <full path>\<policy file>
   ```

3.  遵循螢幕指示以完成用戶端安裝。

4.  如果您已下載最新的定義套件，請複製套件至用戶端電腦，然後按兩下定義套件予以安裝。

   > [!NOTE]
   >  在 Endpoint Protection 用戶端安裝完成之後，用戶端會自動執行定義更新檢查。 如果此更新檢查成功，您就不需要手動安裝最新的定義更新套件。

## <a name="verify-that-the-endpoint-protection-client-is-installed-correctly"></a>確認 Endpoint Protection 用戶端是否正確安裝
在參照電腦上安裝 Endpoint Protection 用戶端之後，請確認用戶端是否正常運作。

### <a name="to-verify-that-the-endpoint-protection-client-is-installed-correctly"></a>確認 Endpoint Protection 用戶端是否正確安裝

1.  在參照電腦上，從 Windows 通知所在的位置開啟 **System Center Endpoint Protection**。

2.  在 [System Center Endpoint Protection] 對話方塊的 [首頁] 索引標籤上，確認 [即時保護] 已設為 [開啟]。

3.  確認 [病毒和間諜軟體定義]  顯示為 [最新] 。

4.  您可以在 [掃描選項] 下選取 [完整] ，然後按一下 [立即掃描] ，如此可協助您確認參照電腦是否就緒可以進行映像處理。

### <a name="how-to-prepare-the-endpoint-protection-client-for-imaging"></a>如何準備 Endpoint Protection 用戶端以進行映像處理
在您確認 Endpoint Protection 用戶端在參照電腦上正確安裝後，您就可以準備電腦以進行映像處理。 執行下列步驟以準備 Endpoint Protection 用戶端進行映像處理。


如需詳細資訊，請參閱[使用 System Center Configuration Manager 管理作業系統映像](/sccm/osd/get-started/manage-operating-system-images)。

### <a name="to-prepare-the-endpoint-protection-client-for-imaging"></a>準備 Endpoint Protection 用戶端以進行映像處理

1.  在參照電腦上，以具有系統管理員權限的使用者身分登入。

2.  從 TechNet 上的 **Windows SysInternals 網站** 下載並安裝 [PsTools](http://go.microsoft.com/fwlink/?LinkId=215263) 。

3.  開啟提升權限的命令提示字元，瀏覽至安裝 PsTools 的資料夾，然後輸入下列命令

   ```
   Psexec.exe -s -i regedit.exe
   ```

   > [!IMPORTANT]
   >  以此方式執行登錄編輯程式時請留意；PsExec.exe 中的 -s 選項會以 LocalSystem 權限執行登錄編輯程式。

4.  在 [登錄編輯程式] 中，瀏覽至下列各個登錄機碼，然後予以刪除。

   > [!IMPORTANT]
   >  刪除登錄機碼必須是在製作參照電腦映像之前的最後步驟。 登錄機碼會在 Endpoint Protection 用戶端啟動時重新建立。 如果您重新啟動參照電腦，就必須再次刪除登錄機碼。

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\InstallTime**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanRun**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanType**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastQuickScanID**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastFullScanID**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\RemovalTools\MRT\GUID**

在完成上述步驟後，您就可以準備參照電腦進行映像處理。 如需詳細資訊，請參閱[使用 System Center Configuration Manager 管理作業系統映像](/sccm/osd/get-started/manage-operating-system-images)。

部署含有 Endpoint Protection 用戶端軟體的映像時，Endpoint Protection 用戶端會自動將資訊報告給電腦被指派的 Configuration Manager 站台，並且會下載並套用適用於用戶端電腦的原則。
