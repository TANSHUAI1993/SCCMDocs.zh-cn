---
title: "設定電源管理 | Microsoft Docs"
description: "設定 System Center Configuration Manager 的電源管理。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 435c923c-ea30-4dce-8afd-48962ed85502
caps.latest.revision: "5"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: e111ac2545dd9e0b96a50c10246bb75d286a737a
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="configuring-power-management-in-system-center-configuration-manager"></a>設定 System Center Configuration Manager 的電源管理

*適用對象：System Center Configuration Manager (最新分支)*

您必須先執行下列設定步驟，才能使用 System Center Configuration Manager 的電源管理。  

## <a name="enable-and-configure-power-management-client-settings"></a>啟用及設定電源管理用戶端設定  
 這項程序會設定電源管理的預設用戶端設定，並套用到階層中的所有電腦。 如果您只想某些電腦套用這些設定，請建立自訂裝置用戶端設定，並將它指派給包含要使用電源管理之電腦的集合。 如需如何建立自訂裝置設定的詳細資訊，請參閱 [How to configure client settings in System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md) (如何在 System Center Configuration Manager 中設定用戶端設定)。  

#### <a name="to-enable-power-management-and-configure-client-settings"></a>啟用電源管理及設定用戶端設定  

1.  在 Configuration Manager 主控台中，按一下 [系統管理] 。  

2.  在 [系統管理]  工作區中，按一下 [用戶端設定] 。  

3.  按一下 [預設用戶端設定] 。  

4.  在 [首頁]  索引標籤的 [內容]  群組中，按一下 [內容] 。  

5.  在 [預設用戶端設定]  對話方塊中按一下 [電源管理] 。  

6.  為電源管理用戶端設定設定下列值：  

    -   **允許管理裝置電源** – 從下拉式清單中選取 [True]  啟用電源管理。  

7.  設定您需要的用戶端設定。 如需您可設定的電源管理用戶端設定清單，請參閱[關於 Configuration Manager 中的用戶端設定](../../../../core/clients/deploy/about-client-settings.md#power-management)主題的[電源管理](../../../../core/clients/deploy/about-client-settings.md)一節。  

8.  按一下 [確定]  ，關閉 [預設用戶端設定]  對話方塊。  

 用戶端電腦將會在下一次下載用戶端原則時進行這些設定。 若要起始單一用戶端的原則擷取，請參閱 [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md)。  

## <a name="exclude-computers-from-power-management"></a>從電源管理中排除電腦  
 您可以阻止電腦集合接收電源管理設定。 如果電腦是被電源管理設定排除在外的任何集合的成員，該電腦不會套用電源管理設定，即使它也是套用了電源管理設定的另一個集合的成員。  

 您可能因為下列原因，想要將電腦排除在電源管理之外：  

-   因為業務需要，電腦必須隨時保持開啟狀態。  

-   您建立了電腦的控制項集合，不希望它套用電源管理設定。  

-   某些電腦無法套用電源管理設定。  

-   您想要電源管理排除執行 Windows Server 的電腦。  

> [!NOTE]  
>  如果用戶端設定中設定了 [允許使用者從電源管理排除其裝置]  選項，使用者就可以使用軟體中心從電源管理排除自己的電腦。  

 若要找出電源管理已排除的電腦，請執行 [排除的電腦] 報告。 如需這份報告的詳細資訊，請參閱 [How to monitor and plan for power management in System Center Configuration Manager](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md) (如何監視和規劃 System Center Configuration Manager 的電源管理) 主題中的 [Computers Excluded](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md#BKMK_Excluded) (排除的電腦)。  

> [!IMPORTANT]  
>  即使排除電腦不進行電源管理，執行 Windows XP 或 Windows Server 2003 的電腦所套用的電源設定還是不會還原為原始值。 在新版的 Windows 上，排除電腦不進行電源管理會將所有電源設定還原成其原始值。 您無法將個別的電源設定還原為其原始值。  

#### <a name="to-exclude-a-collection-of-computers-from-power-management"></a>從電源管理排除電腦集合  

1.  在 Configuration Manager 主控台中，按一下 [資產與相容性] 。  

2.  在 [資產與相容性]  工作區中，按一下 [裝置集合] 。  

3.  在 [裝置集合]  清單中，選取要從電源管理排除的集合，然後在 [首頁]  索引標籤的 [內容]  群組中按一下 [內容] 。  

4.  在 [<集合名稱\> 內容] 對話方塊的 [電源管理] 索引標籤中，選取 [絕不套用電源管理設定到此集合中的電腦]。  

5.  按一下 [確定] 關閉 [<集合名稱\> 內容] 對話方塊並儲存設定。  
