---
title: "Configuration Manager Technical Preview 1704 中的功能"
description: "了解 System Center Configuration Manager Technical Preview 1704 版中可用的功能。"
ms.custom: na
ms.date: 4/21/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e318e705-20f2-417d-8cde-7dfe661b2fa7
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: d7caee47ca74064630e09c1bdb94187af256d4b4
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="capabilities-in-technical-preview-1704-for-system-center-configuration-manager"></a>System Center Configuration Manager Technical Preview 1704 中的功能

*適用於︰System Center Configuration Manager (Technical Preview)*

本文介紹 System Center Configuration Manager Technical Preview 1704 版中可用的功能。 您可以安裝此版本，以更新並新增功能至 Configuration Manager Technical Preview 站台。 安裝此版本的 Technical Preview 之前，請檢閱 [System Center Configuration Manager 的 Technical Preview](../../core/get-started/technical-preview.md) 簡介主題，以熟悉使用 Technical Preview 的一般需求和限制、如何在版本之間進行更新，以及如何針對 Technical Preview 中的功能提供意見反應。    


**以下是您可以使用此版本試用的新功能。**  

## <a name="configure-android-apps-with-app-configuration-policies"></a>使用應用程式組態原則設定 Android 應用程式
您可以在 System Center Configuration Manager (Configuration Manager) 中使用應用程式設定原則，發佈使用者在 Android for Work 裝置上執行應用程式時可能需要的設定。 Android 應用程式設定原則僅可於執行 Android for Work 的裝置上使用，並適用於來自 Play for Work 商店的已核准應用程式。

### <a name="try-it-out"></a>試試看                 

在 Configuration Manager 主控台中，選擇 [軟體程式庫] > [應用程式管理] > [應用程式設定原則]，並選擇 [建立應用程式設定原則]。 在精靈的 [一般] 頁面上，您現在可以 [選取設定原則類型]。 指定應用程式設定原則的目標平台：[適用於 Android for Work 應用程式的設定原則]。 您接著可以 [指定名稱或值組]，或 [瀏覽至屬性清單 JSON 檔案]。 新的應用程式設定原則會顯示在 [軟體程式庫] 工作區的 [應用程式設定原則] 節點中。 若要建立應用程式設定原則與 Android for Work 應用程式部署的關聯，請使用[部署應用程式](/sccm/apps/deploy-use/deploy-applications)主題中的程序像平常那樣部署應用程式。

## <a name="hardware-inventory-collects-secure-boot-information"></a>硬體清查會收集安全開機資訊
硬體清查現在會收集安全開機是否在用戶端上啟用的相關資訊。 此資訊預設會儲存在 **SMS_Firmware** 類別 (於 1702 版中推出) 中，並於硬體清查中啟用。 如需硬體清查的詳細資訊，請參閱[如何設定硬體清查](/sccm/core/clients/manage/inventory/configure-hardware-inventory)。

## <a name="add-child-task-sequences-to-a-task-sequence"></a>將子工作順序新增至工作順序
在此版本中，您可以新增會執行另一個工作順序的新工作順序步驟，這會在工作順序之間建立父子式關係。 這可讓您建立更多可以重複使用的模組化工作順序。  

當您將子工作順序新增至工作順序時，請考慮下列項目：

- 父工作順序和子工作順序會有效地結合成用戶端執行的單一原則。
- 不支援將另一個工作順序的父工作順序新增為子工作順序。
- 環境是全域的。 例如，如果有某個變數是由父工作順序所設定，並由子工作順序做出變更，該變數將會繼續保持變更。 類似地，如果子工作順序建立一個新變數，該變數將可在父工作順序的剩餘步驟中提供使用。
- 針對單一工作順序作業，將會按一般的方式傳送狀態訊息。
- 工作順序會將項目寫入 smsts.log 檔案，其中有會清楚交代子工作順序何時開始的新記錄項目。
- 在 Configuration Manager Technical Preview 1704 版中，如果子工作順序參考任何套件，且您從軟體中心執行父工作順序，用戶端將無法在執行子工作順序時找到該套件。 在此案例中，您必須從媒體 (開機媒體、PXE 等) 執行工作順序。  

    如果子工作順序使用如「執行命令列」(不含任何套件參考)、「格式化」、「BitLocker」等步驟，則工作順序將會成功自軟體中心執行。

### <a name="to-add-a-child-task-sequence-to-a-task-sequence"></a>將子工作順序新增至工作順序
1. 在工作順序編輯器中，按一下 [新增]，選取 [一般]，然後按一下 [執行工作順序]。
2. 按一下 [瀏覽] 以選取子工作順序。  

## <a name="reload-boot-images-with-current-windows-pe-version"></a>以目前的 Windows PE 版本重新載入開機映像
當您在選取的開機映像上執行 [更新發佈點] 時，您現在可以選擇在開機映像中重新載入 (來自 Windows ADK 安裝目錄的) 最新版本的 Windows PE。 精靈的 [一般] 頁面會提供站台伺服器上所安裝的 Windows ADK 版本、開機映像中使用 Windows PE 的 Windows ADK 版本，以及 Configuration Manager 用戶端的版本。 您可以使用此資訊來協助決定是否要重新載入開機映像。 此外，當您在 [開機映像] 節點中檢視開機映像時，您也可以利用新的 [用戶端版本] 欄位來了解每個開機映像所使用的 Configuration Manager 用戶端版本為何。

### <a name="to-reload-a-boot-image-with-the-current-windows-pe-version"></a>以目前的 Windows PE 版本重新載入開機映像

1. 在 Configuration Manager 主控台中，移至 [軟體程式庫] > [作業系統] > [開機映像]。
2. 選取開機映像，並按一下 [更新發佈點]。
3. 在精靈的 [一般] 頁面上，選取 [使用來自已安裝 Windows ADK 的 Windows PE 目前版本重新載入開機映像]。

## <a name="improvements-to-operating-system-deployment"></a>作業系統部署增強功能
我們已對作業系統部署進行下列改善，它們都是使用者意見反應的結果。

- [針對作業系統映像的新 [OS 版本] 欄位 (英文)](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17558407-add-a-column-to-the-operating-system-images-node-f)：我們已新增名為 [OS 版本] 的新欄位，以在您檢視 [作業系統映像] 和 [作業系統升級套件] 節點中的資訊時，顯示映像的作業系統版本。 僅會顯示 .WIM 中第一個索引的版本。 請移至 [詳細資料] 索引標籤以取得映像以檢閱其他索引的作業系統版本。

- [Smsts.log 中更有效率的記錄 (英文)](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/16791919-stop-filling-smsts-log-with-useless)：從此版本開始，我們將不再針對 CCM_CIVersionInfo.PolicyID 資訊將項目寫入 smsts.log 檔案中。 在此版本之前，可能會有很多具有此資訊的項目，這使得在記錄檔中尋找更相關的資訊變得較為困難。
