---
title: "建立使用者資料和設定檔設定項目 | Microsoft Docs"
description: "在 System Center Configuration Manager 中使用資料和設定檔設定項目，管理資料夾重新導向、離線檔案和漫遊設定檔。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9fcbcc81-cd6f-496e-b075-ef1afa2b8ccc
caps.latest.revision: "6"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 85b984d739dc9f9d2046186b381eff54ba687c66
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="create-user-data-and-profiles-configuration-items-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中建立使用者資料和設定檔設定項目

*適用於︰System Center Configuration Manager (最新分支)*

System Center Configuration Manager 中的使用者資料和設定檔設定項目包含一些設定，這些設定可為階層中的使用者管理執行 Windows 8 (含) 以後版本電腦上的資料夾重新導向、離線檔案和漫遊設定檔。 例如，您可以：  

-   將使用者的 [文件] 資料夾重新導向到網路共用。  

-   請確定網路連線無法使用時，儲存在網路上的指定檔案在使用者電腦上可供使用。  

-   設定使用者登入和登出時，使用者漫遊設定檔中的哪些檔案要與網路共用同步處理。  

 與 Configuration Manager 中的其他設定項目不同，您不會將使用者資料和設定檔設定項目新增至您之後部署的設定基準。 相反地，您是直接使用 [部署使用者資料和設定檔組態項目]  對話方塊來部署組態項目。  

> [!IMPORTANT]  
>  您只能將使用者資料和設定檔組態項目部署至使用者集合。  

## <a name="enable-user-data-and-profiles-for-compliance-settings"></a>啟用相容性設定的使用者資料和設定檔  
 請使用下列程序，以設定使用者資料和設定檔相容性設定的預設用戶端設定，這些設定將套用至階層中的所有電腦。 如果您只想某些電腦套用這項設定，請建立自訂裝置用戶端設定，並將它指派給包含要使用使用者資料與設定檔相容性設定之電腦的集合。 如需如何建立自訂裝置設定的詳細資訊，請參閱[如何設定用戶端設定](../../core/clients/deploy/configure-client-settings.md)。  

1.  在 Configuration Manager 主控台中按一下 [管理] > [用戶端設定] > [預設設定]。  

4.  在 [首頁]  索引標籤的 [內容]  群組中，按一下 [內容] 。  

5.  在 [預設設定]  對話方塊中，按一下 [相容性設定] 。  

6.  從 [啟用使用者資料和設定檔]  下拉式清單中，選取 [是] 。  

7.  按一下 [確定]  ，關閉 [預設設定]  對話方塊。  

## <a name="create-a-user-data-and-profiles-configuration-item"></a>建立使用者資料和設定檔設定項目  

1.  在 Configuration Manager 主控台中，按一下 [資產與相容性] > [相容性設定] > [使用者資料和設定檔]。  

3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立使用者資料和設定檔設定項目] 。  

4.  在 [建立使用者資料和設定檔設定項目精靈]  的 [一般] 頁面上，指定下列資訊：  

    -   **名稱** ：輸入組態項目的唯一名稱。 您最多可以使用 256 個字元。  

    -   **描述:** 提供概略的組態項目和有助於識別 Configuration Manager 主控台中的其他相關資訊的描述。 您最多可以使用 256 個字元。  

    -   **資料夾重新導向** ：如果您想要設定這個組態項目進行資料夾重新導向的設定，請核取這個方塊。  

    -   **離線檔案** ：如果您想要設定這個組態項目之離線檔案的設定，請核取這個方塊。  

    -   **漫遊使用者設定檔** ：如果您想要設定這個組態項目之漫遊使用者設定檔的設定，請核取這個方塊。  

5.  在 [建立使用者資料和設定檔設定項目精靈]  的 [資料夾重新導向] 頁面中，指定您想要讓用戶端電腦的使用者接收這個設定項目來管理資料夾重新導向。 您可以設定使用者登入之任何裝置的設定，或僅使用者之主要裝置的設定。 如需資料夾重新導向的詳細資訊，請參閱 Windows Server 文件。  

    > [!NOTE]  
    >  只有在您核取精靈之 [一般] 頁面上的 [資料夾重新導向] 時，才會出現這個頁面。  

6.  在 [建立使用者資料和設定檔設定項目精靈]  的 [離線檔案] 頁面上，您可以啟用或停用下列使用者的離線檔案使用：接收這個設定項目以及設定離線檔案行為設定的使用者。 您也可以指定一律可在使用者登入之任何電腦上使用的離線檔案。 如需離線檔案的詳細資訊，請參閱 Windows Server 文件。  

    > [!NOTE]  
    >  只有在您核取精靈之 [一般] 頁面上的 [離線檔案] 方塊時，才會出現這個頁面。  

7.  在 [建立使用者資料和設定檔設定項目精靈]  的 [漫遊設定檔] 頁面上，您可以設定是否可在使用者登入之電腦上使用漫遊設定檔，也可以設定這些設定檔之行為方式的進一步資訊。 如需漫遊設定檔的詳細資訊，請參閱 Windows Server 文件。  

    > [!NOTE]  
    >  只有在您核取精靈之 [一般] 頁面上的 [漫遊使用者設定檔] 方塊時，才會出現這個頁面。  

8.  完成精靈。  

 新的使用者資料和設定檔組態項目會顯示在 [資產與相容性]  工作區的 [使用者資料和設定檔]  節點中。  

## <a name="deploy-a-user-data-and-profiles-configuration-item"></a>部署使用者資料和設定檔設定項目  

1.  在 Configuration Manager 主控台中，按一下 [資產與相容性] > [相容性設定] > [使用者資料和設定檔]。  

3.  選取您想要部署的使用者資料和設定檔組態項目，然後在 [首頁]  索引標籤的 [部署]  群組中按一下 [部署] 。  

4.  在 [部署使用者資料和設定檔設定項目]  對話方塊中，指定下列資訊。  

    -   **集合** - 按一下 [瀏覽]  選取您想要部署組態項目的使用者集合。  

        > [!IMPORTANT]  
        >  您只能將使用者資料和設定檔組態項目部署至使用者集合。  

    -   **支援時補救不相容的規則** - 啟用這個選項自動補救用戶端電腦上評估為不相容的任何規則。  

    -   **允許在維護期間以外補救** - 如果已針對您部署組態項目的集合設定維護期間，請啟用這個選項讓相容性設定補救維護期間以外的值。 如需維護期間的詳細資訊，請參閱[如何使用維護期間](../../core/clients/manage/collections/use-maintenance-windows.md)。  

    -   **產生警示** - 啟用這個選項進行設定，以在組態項目相容性低於指定日期和時間的指定百分比時產生警示。 您也可以指定是否要將警示傳送至 System Center Operations Manager。  

    -   **指定此組態項目的相容性評估排程** - 指定在用戶端電腦上評估已部署之組態項目的排程。 這可以是簡易或自訂排程。  

5.  按一下 [確定]  關閉 [部署使用者資料和設定檔設定項目]  對話方塊並建立部署。  

## <a name="monitor-a-user-data-and-profiles-configuration-item"></a>監視使用者資料和設定檔組態項目  
 監視這種類型之設定項目的方式，與監視其他相容性設定的方式相同。  

 如需詳細資訊，請參閱[如何監視相容性設定](../../compliance/deploy-use/monitor-compliance-settings.md)。  
