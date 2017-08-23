---
title: "使用軟體計量監視應用程式使用量 | Microsoft Docs"
description: 
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b1fdaee2-2816-4447-94cd-609f6948f215
caps.latest.revision: "8"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: eddf20bebd80028336503957dfc4c3d1dbbb23f2
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="software-metering-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的軟體計量

*適用於：System Center Configuration Manager (最新分支)*

這個主題包含使用 System Center Configuration Manager 軟體計量時您可能執行之所有作業的參考。

> [!IMPORTANT]
>  軟體計量用來監視檔案名稱結尾為 **.exe**的 Windows PC 桌面應用程式。 軟體計量不會監視最新 Windows 應用程式 (例如 Windows 8 所使用的最新 Windows 應用程式)。

##  <a name="prerequisites-for-software-metering"></a>軟體計量的必要條件
軟體計量沒有外部相依性，僅具有產品內的相依性。

|相依性|詳細資訊|
|----------------|----------------------|
|軟體計量的用戶端設定|若要使用軟體計量，用戶端設定 [在用戶端上啟用軟體計量]  必須啟用並部署至電腦。 您可以將軟體計量設定部署至階層中的所有電腦，也可以將自訂設定部署至電腦群組。 請參閱本主題中的**設定軟體計量**。|
|Reporting Services 點。|您必須先設定 Reporting Services 點，才能檢視軟體計量報告。 如需詳細資訊，請參閱 [Reporting in System Center Configuration Manager](../../core/servers/manage/reporting.md) (System Center Configuration Manager 中的報告)。|

##  <a name="configure-software-metering"></a>設定軟體計量
 這個程序設定軟體計量的預設用戶端設定，並套用至階層中的所有電腦。 如果您只想要將這些設定套用至部分電腦，請建立自訂裝置用戶端設定，並將它部署至包含您要使用軟體計量之電腦的集合。 如需如何建立自訂裝置設定的詳細資訊，請參閱[設定用戶端設定](../../core/clients/deploy/configure-client-settings.md)。

1.  在 Configuration Manager 主控台中，按一下 [管理] > [用戶端設定] > [預設用戶端設定]。

2.  在 [首頁]  索引標籤的 [內容]  群組中，按一下 [內容] 。

3.  在 [預設設定]  對話方塊中，按一下 [軟體計量] 。

4.  在 [裝置設定]  清單中，設定下列項目：

    -   **在用戶端上啟用軟體計量**：選取 [True]  啟用軟體計量。

    -   **排程資料收集**：設定從用戶端電腦收集軟體計量資料的頻率。 使用每 [7 天]  的預設值，或按一下 [排程]  指定自訂排程。

5.  按一下 [確定]  ，關閉 [預設設定]  對話方塊。

 用戶端電腦會在下一次下載用戶端原則時，使用這些設定進行設定。 若要起始單一用戶端的原則擷取，請參閱[管理用戶端](../../core/clients/manage/manage-clients.md)。

##  <a name="create-software-metering-rules"></a>建立軟體計量規則
 使用 [建立軟體計量規則精靈] 建立 Configuration Manager 站台的新軟體計量規則。

1.  在 Configuration Manager 主控台中，按一下 [資產與相容性] > 軟體計量。

3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立軟體計量規則] 。

4.  在 [建立軟體計量規則精靈] 的 [一般] 頁面中，指定下列資訊：

    -   **名稱** - 軟體計量規則的名稱。 這應該是唯一的描述性名稱。

        > [!NOTE]
        >  如果軟體計量規則中所包含的檔案名稱不同，則這些規則可以共用相同的名稱。

    -   **檔案名稱** - 您想要計量之程式檔的名稱。 您可以按一下 [瀏覽]  顯示 [開啟]  對話方塊，您可在其中選取要使用的程式檔。

        > [!NOTE]
        >  如果您在 [檔案名稱]  方塊中輸入可執行檔名稱，則不會執行檢查來判斷此檔案是否存在，或者是否包含必要的標頭資訊。 可能的話，請按一下 [瀏覽]  ，然後選取要計量的可執行檔。
        >
        >  檔案名稱中不允許使用萬用字元。
        >
        >  如果指定 [原始檔案名稱]  的值，則這個方塊是選擇性的。

    -   **原始檔案名稱** - 您想要計量之可執行檔的名稱。 這個名稱符合檔案標頭中的資訊，而非檔案名稱本身的資訊，讓它可以用於重新命名可執行檔但您想要透過原始名稱進行測量的情況。

        > [!NOTE]
        >  原始檔案名稱中不允許使用萬用字元。
        >
        >  如果指定 [檔案名稱]  的值，則這個方塊是選擇性的。

    -   **版本** - 您想要計量之可執行檔的版本。 您可以使用萬用字元 (*) 來表示任何字串，或使用萬用字元 (?) 來表示任何單一字元。 如果您想要測量可執行檔的所有版本，請使用預設值 (\*)。

    -   **語言** - 要計量之可執行檔的語言。 預設值是您正在使用之作業系統的目前地區設定。 如果您按一下 [瀏覽]  按鈕來選取要計量的可執行檔，則檔案標頭中有語言資訊時，會自動填入這個方塊。 若要計量檔案的所有語言版本，請選取下拉式清單中的 [任何]  。

    -   **描述** - 軟體計量規則的選擇性描述。

    -   **將此軟體計量規則套用到下列用戶端** - 選擇是要將軟體計量規則套用至階層中的所有用戶端，還是套用至指派給 [站台]  清單中所指定站台的用戶端。

5.  若要繼續，請按 [下一步] 。

6.  檢閱並確認設定，然後完成精靈來建立軟體計量規則。 新的軟體計量規則會顯示在 [資產與相容性]  工作區的 [軟體計量]  節點中。

##  <a name="configure-automatic-software-metering-rules"></a>設定自動軟體計量規則
 您可以在 Configuration Manager 中設定軟體計量，透過站台資料庫中所保留的最近使用情況清查資料自動產生停用的軟體計量規則。 您可以設定這個清查資料，只對所指定百分比的電腦使用的應用程式，建立計量規則。 您也可以指定站台上允許的自動產生軟體計量規則數上限。

> [!NOTE]
>  根據預設，會停用自動建立的軟體計量規則。 您必須先啟用這些規則，才能透過它們來開始收集使用量資料。

1.  在 Configuration Manager 主控台中，按一下 [資產與相容性] > [軟體計量]，然後在 [首頁] 索引標籤的 [設定] 群組中按一下 [軟體計量內容]。

3.  在 [軟體計量內容]  對話方塊中，設定下列項目：

    -   **資料保留期限 (天數)** - 指定軟體計量規則所產生之資料保留在站台資料庫中的時間量。 預設值是 **90** 天。

    -   啟用 [從最近使用情況清查資料自動建立停用的計量規則] 選項。

    -   **指定在自動建立軟體計量規則之前，階層中必須使用程式的電腦百分比** - 預設值是百分之 **10** 。

    -   **指定在停用自動建立規則之前，階層中必須超過的軟體計量規則數目** - 預設值是 **100** 個規則。

4.  按一下 [確定]  關閉 [軟體計量內容]  對話方塊。

##  <a name="manage-software-metering-rules"></a>管理軟體計量規則
 在 [資產與相容性]  工作區中，選取 [軟體計量] ，並選取要管理的軟體計量規則，然後選取管理工作。

 請參閱下表，了解選取管理工作前需要知道的資訊。

|管理工作|詳細資料|
|---------------------|-------------|
|**啟用**<br /><br /> **停用**|啟用或停用軟體計量規則。 根據用戶端設定之 [用戶端原則]  區段中的 [用戶端原則輪詢間隔] \(根據預設，每 60 分鐘)，將這個設定下載至用戶端電腦。<br /><br /> 請參閱[設定用戶端設定](../../core/clients/deploy/configure-client-settings.md)。|

##  <a name="monitor-software-metering"></a>監視軟體計量
 Configuration Manager 中的軟體計量包含數種內建報告，可讓您監視軟體計量作業的相關資訊。 這些報告的報告類別為 [軟體計量] 。

 如需如何在 Configuration Manager 設定報告的詳細資訊，請參閱 [System Center Configuration Manager 中的報告](../../core/servers/manage/reporting.md)。

 此外，您還可以根據軟體計量儲存在 Configuration Manager 資料庫中的資料來建立查詢和集合。

 如需 Configuration Manager 中集合的詳細資訊，請參閱[集合簡介](/sccm/core/clients/manage/collections/introduction-to-collections)。

 如需 Configuration Manager 中查詢的詳細資訊，請參閱[查詢簡介](/sccm/core/servers/manage/introduction-to-queries)。

##  <a name="security-and-privacy-for-software-metering"></a>軟體計量的安全性和隱私權

### <a name="security-issues-for-software-metering"></a>軟體計量的安全性問題
 攻擊者可以將無效的軟體計量資訊傳送給 Configuration Manager，這是管理點將接受的作業，即使停用軟體計量用戶端設定也是一樣。 這可能會導致複寫整個階層中的大量計量規則，造成網路和 Configuration Manager 站台伺服器的拒絕服務。

 因為攻擊者可能會建立無效的軟體計量資料，所以不會將軟體計量資訊視為已授權。

 軟體計量啟用預設為用戶端設定。

###  <a name="privacy-information-for-software-metering"></a>隱私權資訊的軟體計量
 軟體計量監視用戶端電腦上的應用程式的使用方式。 預設會啟用軟體計量。 您必須設定要計量的應用程式。 計量資訊會儲存在 Configuration Manager 資料庫中。 資訊會在傳送至管理點期間進行加密，但不會以加密格式儲存在 Configuration Manager 資料庫中。

 這項資訊會保留在資料庫中，直到由站台維護工作 [刪除過時軟體計量資料] \(每 5 天) 和 [刪除過時軟體計量摘要資料] \(每 270 天) 刪除為止。 您可以設定刪除間隔。 計量資訊不會傳送給 Microsoft。

 設定軟體計量之前，請考慮您的隱私權需求。

## <a name="example-scenario-for-using-software-metering"></a>使用軟體計量的示範案例
 在本節中，您將建立軟體計量規則範例，可協助您解決下列商務需求：

-   判斷在貴公司中有多少個特定應用程式的複本

-   探索應用程式任何未使用的複本

-   判斷哪些使用者定期使用特定的應用程式

 Woodgrove Bank 已部署 Microsoft Office 2010 為其標準辦公室產能套件。 不過，為了支援舊版應用程式，某些電腦必須繼續執行 Microsoft Office Word 2003。 如果舊版應用程式已不再使用，IT 部門想要移除這些 Word 2003 的複本，以減少支援和授權成本。 技術支援中心也想要識別哪些使用者使用舊版的應用程式。

 John 是 Woodgrove Bank IT 系統管理員，他使用 Configuration Manager 中的軟體計量來達成這些業務目標。 他會執行下列動作:

- John 檢查了軟體計量的必要條件，並確認已安裝 Reporting Services 點且可運作。
- John 設定了軟體計量的預設用戶端設定：<br>他啟用軟體計量，並使用每七天一次排程的預設資料集合。<br>他會設定軟體清查，來清查具有副檔名 .exe 的檔案，方法是設定軟體清查用戶端設定 [清查這些檔案類型] 。<br>他將新增新的軟體計量規則，名為 **woodgrove.exe**，來監視舊版應用程式。
- John 等候 7 天，之後用戶端電腦開始報告 **woodgrove.exe** 可執行檔使用量資料。
- John 使用 Configuration Manager 報告 [所有計量軟體程式的安裝基礎] 來查看哪些電腦已載入 **woodgrove.exe** 應用程式。
- 六個月後，John 執行報表 [已安裝計量程式，但在指定的日期後尚未執行此程式的電腦] ，其中指定軟體計量規則，以及在過去六個月之中的一個日期。 此報表會識別 120 部過去六個月內尚未執行該程式的電腦。
- John 會進一步檢查，確認識別的電腦上不需要一些舊版應用程式。 他接著會從這些電腦解除安裝舊版的應用程式和 Word 2003 的複本。<br>John 執行報表 [已經執行特定計量軟體程式的使用者]  ，以提供技術支援中心一份清單，列出繼續使用舊版應用程式的使用者。
- John 每週繼續檢查軟體計量報告，如有必要，也會採取修復動作。

 本課程中的動作，可藉由移除不再需要的應用程式而降低 IT 支援和授權成本。 此外，技術支援中心現在有要執行舊版應用程式的使用者清單。
