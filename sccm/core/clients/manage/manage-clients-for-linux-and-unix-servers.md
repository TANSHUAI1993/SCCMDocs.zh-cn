---
title: "管理 Linux 和 UNIX 用戶端 | Microsoft Docs"
description: "在 System Center Configuration Manager 中管理 Linux 和 UNIX 伺服器上的用戶端。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 948664f2-239d-47a8-92fc-f8efeebd5796
caps.latest.revision: "7"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 506df4f7c7baa5f0586a1ddf0cb02b3de9f4d076
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-manage-clients-for-linux-and-unix-servers-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中管理 Linux 和 UNIX 伺服器的用戶端

適用於：System Center Configuration Manager (最新分支)

當您使用 System Center Configuration Manager 管理 Linux 和 UNIX 伺服器時，可以設定集合、維護期間和用戶端設定來協助管理伺服器。 此外，雖然 Linux 和 UNIX 的 Configuration Manager 用戶端沒有使用者介面，但是您可以強制用戶端手動輪詢用戶端原則。

##  <a name="BKMK_CollectionsforLnU"></a> Collections of Linux and UNIX servers  
 使用集合來管理 Linux 和 UNIX 伺服器群組的方式，與使用集合來管理其他用戶端類型的方式相同。 集合可以是直接成員資格集合，或是查詢式集合。 查詢式集合會識別用戶端作業系統、硬體設定，或其他關於存放在站台資料庫中的用戶端詳細資料。 例如，您可以使用包含 Linux 和 UNIX 伺服器的集合來管理下列設定：  

-   用戶端設計  

-   軟體部署  

-   強制維護期間  

 您必須先收集來自用戶端的[硬體清查](../../../core/clients/manage/inventory/hardware-inventory-for-linux-and-unix.md)，才能透過作業系統或發佈來識別 Linux 或 UNIX 用戶端。  

 硬體清查的預設用戶端設定包含用戶端電腦之作業系統的相關資訊。 您可以使用 **Operating System** 類別的 **Caption** 屬性來識別 Linux 或 UNIX 伺服器的作業系統。  

 在 Configuration Manager 主控台 [資產與相容性] 工作區的 [裝置] 節點中，可以針對執行 Linux 和 UNIX 版本 Configuration Manager 用戶端的電腦，檢視有關電腦的詳細資料。 在 Configuration Manager 主控台的 [資產與相容性] 工作區中，[作業系統] 欄中會顯示每部電腦的作業系統名稱。  

 根據預設，Linux 和 UNIX 伺服器是 **All Systems** 集合的成員。 建議您建立僅包含 Linux 和 UNIX 伺服器或其子集的自訂集合。 自訂集合可讓您管理作業 (例如，部署軟體，或將用戶端設定指派給同類電腦的群組)，以便能正確地評估部署是否成功。   

 當您建立 Linux 和 UNIX 伺服器的自訂集合時，請包含內含 Operating System 屬性之 Caption 屬性中的成員資格規則查詢。 如需建立集合的資訊，請參閱[如何在 System Center Configuration Manager 中建立集合](../../../core/clients/manage/collections/create-collections.md)。  

##  <a name="BKMK_MaintenanceWindowsforLnU"></a> Maintenance windows for Linux and UNIX servers  
 Linux 和 UNIX 伺服器的 Configuration Manager 用戶端支援使用[維護期間](../../../core/clients/manage/collections/use-maintenance-windows.md)。 對於 Windows 用戶端，此支援維持不變。  

##  <a name="BKMK_ClientSettingsforLnU"></a> Client settings for Linux and UNIX servers  
 [設定用戶端設定](../../../core/clients/deploy/configure-client-settings.md) (適用於 Linux 和 UNIX 伺服器) 的方式，與設定其他用戶端設定的方式相同。  

 根據預設， **Default Client Agent Settings** 適用於 Linux 和 UNIX 伺服器。 您也可以建立自訂用戶端設定，然後將它們部署至特定用戶端集合。  

 沒有僅套用至 Linux 和 UNIX 用戶端的額外用戶端設定。 不過，具有未套用至 Linux 和 UNIX 用戶端的預設用戶端設定。 Linux 和 UNIX 的用戶端僅會套用所支援功能的設定。  

 例如，因為 Linux 和 UNIX 的用戶端不支援遠端控制，所以Linux 和 UNIX 伺服器將會忽略啟用和進行遠端控制設定的自訂用戶端裝置設定。  

##  <a name="BKMK_PolicyforLnU"></a> Computer policy for Linux and UNIX servers  
 Linux 和 UNIX 伺服器的用戶端會定期輪詢其站台中的電腦原則，以深入了解要求的設定，以及檢查部署。  

 您也可以在 Linux 或 UNIX 伺服器上強制用戶端立即輪詢電腦原則。 若要這麼做，請在伺服器上使用 **root** 認證來執行下列命令：**/opt/microsoft/configmgr/bin/ccmexec -rs policy**。  

 電腦原則輪詢的詳細資料會輸入至共用用戶端記錄檔 ( **scxcm.log**)。  

> [!NOTE]  
>  Linux 和 UNIX 的 Configuration Manager 用戶端永遠不會要求，也不會處理使用者原則。  

##  <a name="BKMK_ManageLinuxCerts"></a> How to manage certificates on the client for Linux and UNIX  
 在您安裝 Linux 和 UNIX 的用戶端之後，即可使用 **certutil** 工具，以使用新的 PKI 憑證來更新用戶端，以及匯入新的憑證撤銷清單 (CRL)。 當您安裝 Linux 和 UNIX 的用戶端時，這個工具位於 **/opt/microsoft/configmgr/bin/certutil**。 

 若要管理憑證，請在每個用戶端上執行具有下列其中一個選項的 certutil：  

|選項|詳細資訊|  
|------------|----------------------|  
|importPFX|使用這個選項指定憑證，以取代用戶端目前所使用的憑證。<br /><br /> 當您使用 **-importPFX** 時，也必須使用 **-password** 命令列參數來提供與 PKCS#12 檔案相關聯的密碼。<br /><br /> 使用 **-rootcerts** 指定任何其他根憑證需求。<br /><br /> 範例︰**certutil -importPFX &lt;PKCS#12 憑證的路徑> -password &lt;憑證密碼\> [-rootcerts &lt;以逗號分隔的憑證清單>]**|  
|-importsitecert|使用這個選項更新管理伺服器上的站台伺服器簽署憑證。<br /><br /> 範例：**certutil -importsitecert &lt;DER 憑證的路徑\>**|  
|-importcrl|使用這個選項，利用一個或多個 CRL 檔案路徑來更新用戶端上的 CRL。<br /><br /> 範例︰**certutil importcrl &lt;以逗號分隔的 CRL 檔案路徑\>**|  
