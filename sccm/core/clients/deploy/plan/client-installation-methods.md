---
title: "用戶端安裝方法 | Microsoft Docs"
description: "了解 System Center Configuration Manager 的用戶端安裝方法。"
ms.custom: na
ms.date: 04/25/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 51b5964b-374d-4abc-8619-414a9fffad2d
caps.latest.revision: "9"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: edca31249cc2bb3e0c67265962815c82e3f4711e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="client-installation-methods-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的用戶端安裝方法

*適用於：System Center Configuration Manager (最新分支)*

您可以使用不同的方法來安裝 Configuration Manager 用戶端軟體。 您可以使用其中一種方法或多種方法的組合。 在本主題中，您可以閱讀每種方法的相關資訊，以了解哪種方法最適合您的組織。  

## <a name="client-push-installation"></a>用戶端推入安裝  

 **支援的用戶端平台：** Windows  

 **優點**  

-   可將用戶端安裝在單一電腦或一組電腦上，或是安裝至查詢結果。  

-   可用於在所有探索的電腦上自動安裝用戶端。  

-   會自動使用在 [用戶端推入安裝內容]  對話方塊中，[用戶端]  索引標籤上定義的用戶端安裝內容。  

 **缺點**  

-   推入至大量集合時，可能會使網路流量增高。  

-   只能用於 Configuration Manager 已探索的電腦。  

-   不可用於將用戶端安裝於工作群組中。  

-   必須指定用戶端推入安裝帳戶，且此帳戶在目標用戶端電腦上必須具有系統管理權限。  

-   必須在用戶端電腦上設定 Windows 防火牆的例外狀況，才能完成用戶端推入安裝。  

-   您無法取消用戶端推入安裝。 在站台上使用此用戶端安裝方法時，Configuration Manager 會嘗試將用戶端安裝在所有探索的資源上，一旦失敗，會在 7 天內連續重試。  

 如需此安裝方法的詳細資訊，請參閱[如何在 System Center Configuration Manager 中將用戶端部署至 Windows 電腦](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md)。  

## <a name="software-update-point-based-installation"></a>以軟體更新點為基礎的安裝  
 **支援的用戶端平台：** Windows  

 **優點：**  

-   可以使用現有的軟體更新基礎結構管理用戶端軟體。  

-   如果 Active Directory 網域服務中的 Windows Server Update Services (WSUS) 和 [群組原則] 設定均正確無誤，則可在新電腦上自動安裝用戶端軟體。  

-   安裝用戶端前不需要先探索電腦。  

-   電腦可以讀取已發佈至 Active Directory 網域服務的用戶端安裝內容。  

-   如果之前已移除用戶端軟體，將會重新安裝。  

-   不需在目標用戶端電腦設定及維護安裝帳戶。  

 **缺點：**  

-   需要運作正常的軟體更新基礎結構作為必要條件。  

-   用戶端安裝和軟體更新必須使用同一個伺服器，且該伺服器必須位於主要站台中。  

-   若要安裝新的用戶端，必須在 Active Directory 網域服務中使用用戶端的主動式軟體更新點和連接埠來設定群組原則物件 (GPO)。  

-   如果未延伸 Configuration Manager 的 Active Directory 架構，您必須使用 [群組原則] 設定來佈建含用戶端安裝內容的電腦。  

 如需此安裝方法的詳細資訊，請參閱[如何在 System Center Configuration Manager 中將用戶端部署至 Windows 電腦](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md)。  

## <a name="group-policy-installation"></a>群組原則安裝  
 **支援的用戶端平台：** Windows  

 **優點：**  

-   安裝用戶端前不需要先探索電腦。  

-   可用於全新安裝或升級用戶端。  

-   電腦可以讀取已發佈至 Active Directory 網域服務的用戶端安裝內容。  

-   不需在目標用戶端電腦設定及維護安裝帳戶。  

 **缺點：**  

-   如果安裝大量用戶端，可能會使網路流量增高。  

-   如果未延伸 Configuration Manager 的 Active Directory 架構，您必須使用 [群組原則] 設定，將用戶端安裝內容新增至站台中的電腦。  

 如需此安裝方法的詳細資訊，請參閱[如何在 System Center Configuration Manager 中將用戶端部署至 Windows 電腦](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md)。  

## <a name="logon-script-installation"></a>登入指令碼安裝  
 **支援的用戶端平台：** Windows  

 **優點：**  

-   安裝用戶端前不需要先探索電腦。  

-   支援使用 CCMSetup 命令列屬性。  

 **缺點：**  

-   如果在短時間內安裝大量用戶端，可能會使網路流量增高。  

-   如果使用者不常登入網路，可能需花很長的時間才能安裝在所有用戶端電腦上。  

 如需此安裝方法的詳細資訊，請參閱[如何在 System Center Configuration Manager 中將用戶端部署至 Windows 電腦](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md)。  

## <a name="manual-installation"></a>手動安裝  
 **支援的用戶端平台：** Windows、UNIX/Linux、Mac OS X  

 **優點：**  

-   安裝用戶端前不需要先探索電腦。  

-   可供測試之用。  

-   支援使用 CCMSetup 命令列屬性。  

 **缺點：**  

-   不提供自動化功能，因此相當耗時。  

 如需有關如何在每個平台手動安裝用戶端的詳細資訊，請參閱下列主題：  

-   [如何在 System Center Configuration Manager 中將用戶端部署至 Windows 電腦](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md)  

-   [如何在 System Center Configuration Manager 中將用戶端部署至 UNIX 和 Linux 伺服器](../../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md)  

-   [How to deploy clients to Macs in System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-macs.md) (如何在 System Center Configuration Manager 中將用戶端部署至 Mac 電腦)  
