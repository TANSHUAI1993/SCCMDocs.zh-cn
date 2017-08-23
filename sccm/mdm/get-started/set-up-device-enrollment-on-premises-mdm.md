---
title: "設定裝置註冊 | Microsoft Docs"
description: "將在 System Center Configuration Manager 中註冊裝置以進行內部部署行動裝置管理的權限授與使用者。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9ffaea91-1379-4b86-9953-b25e152f56a9
caps.latest.revision: "10"
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 16d4106d486d821b7ce92a1de65ebb04469d18de
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="set-up-device-enrollment-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>設定 System Center Configuration Manager 中內部部署行動裝置管理的裝置註冊

*適用於：System Center Configuration Manager (最新分支)*

您必須授與使用者執行權限，使用者才可註冊裝置以進行 System Center Configuration Manager 內部部署行動裝置管理。 若要將裝置註冊權限授與使用者，請遵循下列工作進行。

-   [建立使用者能註冊新式裝置註冊設定檔](#bkmk_createProf)  

-   [針對已註冊裝置設定額外的用戶端設定](#bkmk_addClient)  

-   [讓使用者能收到新式裝置註冊設定檔](#bkmk_enableUsers)  

-   [將根憑證儲存在會註冊的裝置上](#bkmk_storeCert)  

##  <a name="bkmk_createProf"></a> 建立使用者能註冊新式裝置註冊設定檔  
 若要推送允許使用者註冊現代化行動裝置所需的設定，您可以將新的註冊設定檔新增至預設用戶端設定，以套用到 Configuration Manager 站台中所有探索到的使用者。  

1.  在 Configuration Manager 主控台中，按一下 [系統管理] > [概觀] > [用戶端設定]，並開啟 [預設用戶端設定]，然後選取 [註冊]。  

2.  在 [裝置設定] 下，指定輪詢新式裝置的間隔。  

3.  在 [使用者設定] 下，為 [允許使用者註冊新式裝置]  選取 [是] 。  

4.  在 [現代化裝置註冊設定檔] 旁邊按一下 [設定設定檔...]，然後按一下 [建立...]  

5.  在 [建立註冊設定檔] 中，輸入註冊設定檔的名稱，並選擇希望使用者註冊設定檔使用的管理站台碼。 按一下 [確定]  數次，結束 [預設值] 頁面。  

> [!NOTE]  
>  如果想要將註冊設定檔部署到探索到的一部分使用者，可以利用使用者集合，並建立自訂用戶端設定，部署至該集合。 如需建立自訂用戶端設定的詳細資訊，請參閱 [How to configure client settings in System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md)  

##  <a name="bkmk_addClient"></a> 針對已註冊裝置設定額外的用戶端設定  
 除了針對現代化裝置設定註冊設定檔之外，您還可以在裝置註冊後，設定額外的用戶端設定來設定裝置。  如需設定用戶端設定的資訊，請參閱[如何在 System Center Configuration Manager 中設定用戶端設定](../../core/clients/deploy/configure-client-settings.md)。  

 並非所有的用戶端設定都適用於進行內部部署行動裝置管理。 Configuration Manager 的最新分支支援進行內部部署行動裝置管理的下列用戶端設定：  

-   註冊 - 這些設定會指定受管理裝置的註冊設定檔。 如需如何設定註冊設定檔的詳細資訊，請參閱 [Create an enrollment profile that allows users to enroll modern devices](#bkmk_createProf)(建立使用者能註冊新式裝置的註冊設定檔)。  

-   用戶端原則 - 這些設定會指定下載用戶端原則到裝置的頻率。 您也可以啟用以原則輪詢將使用者設為目標的設定。 如需用戶端原則設定的詳細資訊，請參閱[關於 System Center Configuration Manager 中的用戶端設計](../../core/clients/deploy/about-client-settings.md)中的＜用戶端原則＞一節。  

-   軟體部署 - 這項設定會設定評估用戶端裝置以進行軟體部署的間隔。 如需軟體部署設定的詳細資訊，請參閱[關於 System Center Configuration Manager 中的用戶端設計](../../core/clients/deploy/about-client-settings.md)中的＜軟體部署＞一節。  

    > [!NOTE]  
    >  對於內部部署行動裝置管理，軟體部署設定僅能作為預設用戶端設定使用。 Configuration Manager 的最新分支中的自訂用戶端設定無法搭配軟體部署設定。  

##  <a name="bkmk_enableUsers"></a> 讓使用者能收到新式裝置註冊設定檔  
 若要讓使用者接收已修改的用戶端設定與進行內部部署行動裝置管理的註冊設定檔，必須先透過 Active Directory 探索方法探索到使用者。 為確保每個需要註冊設定檔的使用者皆可取得它，請執行 Active Directory 使用者探索。 如需如何探索使用者的指示，請參閱 [Run discovery for System Center Configuration Manager](../../core/servers/deploy/configure/run-discovery.md)。  

##  <a name="bkmk_storeCert"></a> 將根憑證儲存在會註冊的裝置上  
 其裝置已加入網域的使用者，應該已有必要的根憑證，可與裝載站台系統角色的伺服器進行受信任的通訊，因為利用 Active Directory 加入網域的過程中，會核發根。 未加入網域的電腦與行動裝置，需要在裝置上手動安裝根憑證，才可進行註冊。 這些裝置會自動具備必要的根憑證。  

 必須為裝置提供匯出的憑證檔案，進行手動安裝。 可利用電子郵件、OneDrive、SD 記憶卡、USB 磁碟，或任何適合您需求的方法，提供憑證檔案。  

 裝置上要使用的根憑證是在[將具有相同的根的憑證匯出為網頁伺服器憑證](../../mdm/get-started/set-up-certificates-on-premises-mdm.md#bkmk_exportCert)中匯出的憑證。  

1.  在要註冊的裝置上，找到根憑證檔案，然後按兩下該檔案。  

2.  在 [憑證] 視窗中，按一下 [安裝憑證...]  

3.  在 [憑證匯入精靈] 中，選取 [本機] ，然後按一下 [下一步] 。  

4.  在 [使用者帳戶控制] 視窗中，按一下 [是] 。  

5.  選取 [將所有憑證放入以下的存放區] ，然後按一下 [瀏覽] 。  

6.  依序按一下 [受信任的根憑證授權單位] 、[確定] 和 [下一步] 。  

7.  按一下 [完成] 。  
