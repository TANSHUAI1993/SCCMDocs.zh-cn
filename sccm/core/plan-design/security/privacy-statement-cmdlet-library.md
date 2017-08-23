---
title: "System Center Configuration Manager 隱私權聲明 - Configuration Manager Cmdlet 程式庫 | Microsoft Docs"
description: "了解 Microsoft 如何收集和使用 System Center Configuration Manager Cmdlet 程式庫的相關資料。"
ms.custom: na
ms.date: 1/3/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bec00fb4-1ac0-4e49-b330-0871b3722459
caps.latest.revision: "5"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 3936075555cc0bb370ea6e42c7e720b864d565f7
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="system-center-configuration-manager-privacy-statement---configuration-manager-cmdlet-library"></a>System Center Configuration Manager 隱私權聲明 - Configuration Manager Cmdlet 程式庫

適用於：System Center Configuration Manager (最新分支)

本隱私權聲明涵蓋 System Center Configuration Manager Cmdlet 程式庫的功能。  

## <a name="usage-data"></a>使用方式資料  
 **此功能的作用：**   
您可利用 System Center Configuration Manager Cmdlet 程式庫，透過 Windows PowerShell Cmdlet 與指令碼，來管理 Configuration Manager 階層。 Cmdlet 程式庫會收集有關您如何使用程式庫中 Cmdlet 的資訊，以找出趨勢及使用習慣。 Cmdlet 程式庫也會收集您使用 Cmdlet 時所遇到的錯誤類型與數目。  

 **收集、處理或傳輸的資訊：**   
收集的使用方式資料包括啟動、停止及終止 Cmdlet、執行已取代的 Cmdlet，以及與 Cmdlet 相關之 Systems Management Server (SMS) 提供者作業的活動指標。 這項資訊不具個人識別性質。  收集的錯誤資訊包括 Cmdlet 所傳回的錯誤，以及例外狀況錯誤的錯誤詳細資料。 某些錯誤詳細資料報告可能會不小心包含個人識別資料，例如連接至您電腦的裝置序號。 Cmdlet 程式庫會篩選錯誤報告中的資訊，並以匿名方式處理資訊，以在將資訊傳輸給 Microsoft 之前移除個人識別資料。  

 **資訊的用途：**   
我們可使用這項資訊，改善所提供的產品與服務之品質、安全性與完整性。  

 **選擇/控制：**   
預設會啟用此使用方式資料功能。 System Center Configuration Manager Cmdlet 程式庫有兩個登錄機碼可控制這項功能。  

 若要完全退出，您需要設定這兩個登錄機碼值，每個 Windows 事件追蹤 (ETW) 提供者各一個登錄機碼值：  

-   HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Provider:CeipLevel=0 (且不使用磁碟機提供者的使用方式資料)  

-   HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Cmdlets:CeipLevel=0 (且不使用 Cmdlet 的使用方式資料)  

 使用方式資料設定的變更，只對進行變更的電腦有效。  

 如需如何設定使用方式資料 (集合) 的詳細資訊，請參閱 [System Center Configuration Manager Cmdlet Library documentation](https://technet.microsoft.com/en-us/library/dn958404.aspx) (System Center Configuration Manager Cmdlet 程式庫文件)。   
