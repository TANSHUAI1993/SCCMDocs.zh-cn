---
title: "用戶端管理基本概念 | Microsoft Docs"
description: "深入了解您執行以管理 System Center Configuration Manager 用戶端的工作。"
ms.custom: na
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8d4e5641-354e-4439-8b4f-620a760e233d
caps.latest.revision: "4"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 0fee4f4ba462e59859ac93c4218b67cb26bdd6f6
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="fundamentals-of-client-management-tasks-for-system-center-configuration-manager"></a>System Center Configuration Manager 的用戶端管理基本概念

適用於：System Center Configuration Manager (最新分支)

安裝 System Center Configuration Manager 用戶端之後，您可以執行數項工作來管理用戶端。  有些工作是從 Configuration Manager 主控台執行。 其他工作則是從 Configuration Manager 用戶端應用程式執行。 Configuration Manager 用戶端應用程式是與 Configuration Manager 用戶端軟體一起安裝。

## <a name="configuration-manager-console-tasks"></a>Configuration Manager 主控台工作
 在 Configuration Manager 主控台中，您可以執行各種用戶端管理工作︰  

-   部署應用程式、軟體更新、維護指令碼及作業系統。 設定特定日期和時間的安裝、將軟體設為使用者要求時即可安裝，或設定解除安裝應用程式。  

-   協助保護您的電腦不受惡意程式碼侵襲及其他安全性威脅，並在偵測到問題時通知您。  

-   定義要監視的用戶端組態設定，並針對不符合規範的設定加以補救。  

-   收集硬體和軟體清查資訊，其中包括在 Microsoft 監視及協調授權資訊。  

-   使用遠端控制對電腦進行疑難排解。  

-   執行電源管理設定來管理與監視電腦的電源消耗。  

Configuration Manager 主控台會以幾近即時的方式監視先前的工作。 Configuration Manager 主控台中提供每個工作的通知和狀態資訊。 若要擷取資料和歷史趨勢，請使用 SQL Server Reporting Services 的整合式報告功能。 用戶端會將詳細資料以用戶端狀態的形式提交給站台。  用戶端狀態資訊提供有關用戶端健全狀況和用戶端活動的資料，在主控台中或透過使用 Configuration Manager 的內建報表均可檢視這項資訊。 此資料可協助識別沒有回應的電腦，在某些情況下還會自動補救問題。  

 如需用戶端管理工作的詳細資訊，請參閱[如何管理 System Center Configuration Manager 中的用戶端](../../core/clients/manage/manage-clients.md)和[如何在 System Center Configuration Manager 中管理 Linux 和 UNIX 伺服器的用戶端](../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md)。 若要了解如何使用報表，請參閱   
            [System Center Configuration Manager 的報告簡介](../../core/servers/manage/introduction-to-reporting.md)。  

## <a name="configuration-manager-client-application"></a>Configuration Manager 用戶端應用程式  
 當您安裝 Configuration Manager 用戶端軟體時，也會安裝 Configuration Manager 用戶端應用程式。 與軟體中心不同，Configuration Manager 用戶端應用程式的設計對象是技術服務人員，而非使用者。 部分設定選項需要有本機系統管理權限，且大部分選項都需要具備 Configuration Manager 用戶端應用程式運作方式的技術知識。 您可以使用此應用程式在用戶端上執行下列工作︰  

-   檢視用戶端內容，例如組建編號、其指派的站台、與其通訊的管理點，以及用戶端使用的是公開金鑰基礎結構 (PKI) 憑證還是自我簽署憑證。  

-   確認在第一次安裝用戶端之後是否已成功下載用戶端原則。 也確認是否根據 Configuration Manager 主控台中所設定的用戶端設定，如預期地啟用或停用用戶端設定。  

-   啟動用戶端動作。 例如，如果最近已變更 Configuration Manager 主控台設定，而您不想等到下次排程時間，即可下載用戶端原則。  

-   將用戶端手動指派至 Configuration Manager 站台，或嘗試找到站台。 然後針對發佈至網域名稱系統 (DNS) 的管理點指定 DNS 尾碼。  

-   設定可暫時儲存檔案的用戶端快取。 然後，在需要更多磁碟空間來安裝軟體時，刪除快取中的檔案。  

-   針對以網際網路為基礎的用戶端管理進行設定。  

-   檢視部署至用戶端的設定基準、起始相容性評估及檢視相容性報告。  
