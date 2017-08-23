---
title: "規劃將用戶端部署至 Windows Embedded 裝置 | Microsoft Docs"
description: "規劃在 System Center Configuration Manager 中將用戶端部署至 Windows Embedded 裝置。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 038e61f9-f49d-41d1-9a9f-87bec9e00d5d
caps.latest.revision: "7"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: f7ef476a2ebcf0161ebb70d8a3d95f77806aa05e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="planning-for-client-deployment-to-windows-embedded-devices-in-system-center-configuration-manager"></a>規劃將用戶端部署至 System Center Configuration Manager 中的Windows Embedded 裝置

適用於：System Center Configuration Manager (最新分支)

<a name="BKMK_DeployClientEmbedded"></a> 如果您的 Windows Embedded 裝置不包含 System Center Configuration Manager 用戶端，且該裝置符合必要的相依性，您可以使用任何一種用戶端安裝方法。 如內嵌裝置支援寫入篩選器，您必須先停用這些篩選器再安裝用戶端，等到用戶端安裝完畢並指派至網站後，再度重新啟用篩選器。  

 請注意當您停用篩選器時，您不應該停用此篩選器驅動程式。 通常這些驅動程式會在電腦啟動時自動啟動。 停用這些驅動程式將會阻礙用戶端安裝，或干擾寫入篩選器協調流程，這將會造成用戶端作業失敗。 這些是與每個必須持續執行之寫入篩選器類型相關聯的服務：  

|撰寫篩選器類型|驅動程式|類型|說明|  
|-----------------------|------------|----------|-----------------|  
|EWF|EWF|核心|會在受保護磁碟區上實作磁區層級 I/O 重新導向。|  
|FBWF|FBWF|檔案系統|會在受保護磁碟區上實作檔案層級 I/O 重新導向。|  
|UWF|uwfreg|核心|UWF 登錄重新導向器|  
|UWF|uwfs|檔案系統|UWF 檔案重新導向器|  
|UWF|uwfvol|核心|UWF 磁碟區管理員|  

 當您進行變更 (例如安裝軟體) 時，寫入篩選器會控制內嵌裝置更新作業系統的方式。 啟用寫入篩選器時，並不會直接對作業系統進行變更，而是將變更重新導向至暫時的重疊層。 如果只將變更寫入至重疊層中，當內嵌裝置關機時，就會失去變更。 不過，如果暫時停用寫入篩選器，就可以進行永久變更，您也不需要在每次內嵌裝置重新啟動後再次進行變更 (或重新安裝軟體)。 不過，暫時停用再重新啟用寫入篩選器後，必須重新啟動一次或一次以上，因此，通常可以透過設定維護期間的方式控制執行此作業的時間，以便在非工作時間重新啟動電腦。  

 您可以在部署如應用程式、工作順序、軟體更新，以及 Endpoint Protection 用戶端等軟體時設定選項，以自動停用再重新啟用寫入篩選器。 例外狀況是設定基準及使用自動補救的設定項目。 在此案例中，補救功能永遠會在重疊時發生，而且只能在裝置重新啟動時使用。 補救功能會在下一次評估週期再次套用，但只套用於在重新啟動時建立的重疊。 若要強制 Configuration Manager 認可補救變更，您可以先部署設定基準，再快速進行其他支援認可變更的軟體部署。  

 如果寫入篩選器已停用，您可以使用 [軟體中心] 在 Windows Embedded 裝置上安裝軟體。 不過，若已啟用寫入篩選器，則安裝會失敗，且 Configuration Manager 會顯示您的權限不足，無法安裝應用程式的錯誤訊息。  

> [!WARNING]  
>  即使您未選取 Configuration Manager 選項來認可變更，如果其他軟體安裝或變更已認可變更，則可能會認可這些變更。 在此案例中，除了新的變更之外，也會認可原始變更。  

 當 Configuration Manager 停用寫入篩選器以進行永久變更時，只有具有本機系統管理權限的使用者可以登入並使用內嵌裝置。 在此期間，權限低的使用者會被鎖定，並且會看到電腦因為維修中而無法使用的訊息。 這麼做可在裝置處於可能永久套用變更的狀態下時保護裝置，此服務模型鎖定行為是另一個設定維護期間的原因，使用者在這段期間內不會再登入這些裝置。  

 Configuration Manager 支援管理下列類型的寫入篩選器：  

-   檔案型寫入篩選器 (FBWF) - 如需詳細資訊，請參閱 [File-Based Write Filter](http://go.microsoft.com/fwlink/?LinkID=204717) (檔案型寫入篩選器)。  

-   增強式寫入篩選器 (EWF) RAM - 如需詳細資訊，請參閱 [Enhanced Write Filter](http://go.microsoft.com/fwlink/?LinkId=204718) (增強式寫入篩選器)。  

-   整合寫入篩選器 (UWF) - 如需詳細資訊，請參閱 [Unified Write Filter](http://go.microsoft.com/fwlink/?LinkId=309236) (整合寫入篩選器)。  

 當 Windows Embedded 裝置處於 EWF RAM Reg 模式時，Configuration Manager 不支援寫入篩選器。  

> [!IMPORTANT]  
>  如果您可以選擇，請搭配使用檔案型寫入篩選器 (FBWF) 與 Configuration Manager，以提升效率及增加延展性。
>
> **僅使用 FBWF 的裝置：**設定下列例外狀況，以便在裝置重新啟動期間保存用戶端狀態和清查資料：  
>   
>  -   CCMINSTALLDIR\\*.sdf  
> -   CCMINSTALLDIR\ServiceData  
> -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\StateSystem  
>   
>  執行 Windows Embedded 8.0 及更新版本的裝置，不支援包含萬用字元的排除項目。 在這些裝置上，您必須個別設定下列的排除項目：  
>   
>  -   所有在 CCMINSTALLDIR 中副檔名為 .sdf 的檔案，通常為：  
>   
>     -   UserAffinityStore.sdf  
>     -   InventoryStore.sdf  
>     -   CcmStore.sdf  
>     -   StateMessageStore.sdf  
>     -   CertEnrollmentStore.sdf  
> -   CCMINSTALLDIR\ServiceData  
> -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\StateSystem  
>   
> **僅使用 FBWF 和 UWF 的裝置：**當工作群組中的用戶端使用憑證來驗證管理點時，您還必須排除私密金鑰，以確保用戶端會繼續與管理點通訊。 在這些裝置上設定下列例外狀況：  
>   
>  -   c:\Windows\System32\Microsoft\Protect  
> -   c:\ProgramData\Microsoft\Crypto  
> -   HKEY_LOCAL_MACHINE\Software\Microsoft\SystemCertificates\SMS\Certificates  

 如需在 Configuration Manager 中部署和管理已啟用寫入篩選器之 Windows Embedded 裝置的範例案例，請參閱[在 Windows Embedded 裝置上部署及管理 System Center Configuration Manager 用戶端的範例案例](../../../../core/clients/deploy/example-scenario-for-deploying-and-managing-clients-on-windows-embedded-devices.md)。  

 如需如何為 Windows Embedded 裝置建立映像及設定寫入篩選器的詳細資訊，請參閱您的 Windows Embedded 文件，或洽詢您的 OEM。  

> [!NOTE]  
>  當您為軟體部署及設定項目選取適用的平台時，這些平台會顯示 Windows Embedded 系列，而不是顯示特定版本。 使用下列清單，對應 Windows Embedded 的特定版本與清單方塊中的選項：  
>   
>  -   [以 Windows XP 為基礎的內嵌作業系統 (32 位元)] 包括下列各項：  
>   
>      -   Windows XP Embedded  
>     -   Windows Embedded for Point of Service  
>     -   Windows Embedded Standard 2009  
>     -   Windows Embedded POSReady 2009  
> -   [以 Windows 7 為基礎的內嵌作業系統 (32 位元)] 包括下列各項：  
>   
>      -   Windows Embedded Standard 7 (32 位元)  
>     -   Windows Embedded POSReady 7 (32 位元)  
>     -   Windows ThinPC  
> -   [以 Windows 7 為基礎的內嵌作業系統 (64 位元)] 包括下列各項：  
>   
>      -   Windows Embedded Standard 7 (64 位元)  
>     -   Windows Embedded POSReady 7 (64 位元)
