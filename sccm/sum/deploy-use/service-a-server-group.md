---
title: "提供伺服器群組 | Microsoft Docs"
description: "System Center Configuration Manager 主控台提供警示與狀態，以監視更新及相容性。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 12/07/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: 304a83ea-0f72-437d-9688-2e6e0c7526dd
ms.openlocfilehash: ae09a02dd5d67113b9a7e2ce146c844efa4caf55
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
>[!IMPORTANT]
>這是在 Configuration Manager 版本 1606 和版本 1610 中提供的發行前版本功能。 發行前版本功能會包含在產品內，以便在生產環境中進行早期測試，但不應視為生產環境就緒。 您必須開啟這項功能才能使用。 如需詳細資訊，請參閱[使用發行前版本功能](https://docs.microsoft.com/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease)。


# <a name="service-a-server-group"></a>提供伺服器群組

*適用對象：System Center Configuration Manager (最新分支)*

從 System Center Configuration Manager 1606 版開始，您可以設定伺服器群組設定集合，定義集合內電腦安裝軟體更新的數量、百分比或順序。 您也可以設定預先部署和部署後的 PowerShell 指令碼來執行自訂動作。

當您將軟體更新部署到已設定伺服器群組設定的集合時，Configuration Manager 會判斷集合中有多少部電腦可在任何的指定時間內安裝軟體更新，並且提供相同的部署鎖定數目。 只有取得部署鎖定的電腦，才會啟動軟體更新安裝。 有部署鎖定可用時，電腦會取得部署鎖定、安裝軟體更新，然後在軟體更新安裝順利完成後釋出部署鎖定。 接著，部署鎖定就可以提供其他電腦使用。 如果電腦無法釋放部署鎖定，您可以手動釋放集合的所有伺服器群組部署鎖定。

>[!IMPORTANT]
>集合中的所有電腦都必須指派給相同的站台。

#### <a name="to-create-a-collection-for-a-server-group"></a>建立伺服器群組的集合  
伺服器群組設定是在裝置集合的內容中設定。 若要檢修伺服器群組，集合中的所有成員都必須指派給相同的站台。 使用下列步驟建立集合並設定伺服器群組設定︰
1.  [建立裝置集合](../../core/clients/manage/collections/create-collections.md)將伺服器群組的電腦包含在內。  

2.  在 [資產與相容性] 工作區中，按一下 [裝置集合]，再以滑鼠右鍵按一下包含伺服器群組電腦的集合，然後按一下 [內容]。  

3.  在 [一般] 索引標籤上，選取 [所有裝置都屬於相同的伺服器群組]，然後按一下 [設定]。  

4.  在 [伺服器群組設定] 頁面上，指定下列其中一項設定：  

    -   **允許同時更新一部分的電腦**︰指定任一時間只能更新某個百分比的用戶端。 例如，集合有 10 個用戶端，且設定在同一時間更新 30% 的用戶端，則在任何指定時間內，只有 3 個用戶端會安裝軟體更新。  

    -   **允許同時更新多部電腦**︰指定任一時間只能更新某個數量的用戶端。  

    -   **指定維護順序**︰指定集合中的用戶端要按照您設定的順序，一次更新一個。 用戶端只會在清單排位在它前面的用戶端完成軟體更新安裝之後，才安裝軟體更新。  

5.  指定是否要使用預先部署 (節點清空) 指令碼或部署後 (節點繼續) 指令碼。  

    > [!WARNING]
    > 自訂指令碼不是由 Microsoft 所簽署。 您必須負責維護這些指令碼的完整性。

    > [!TIP]  
    > 以下是可將目前時間寫入文字檔案之預先部署和部署後指令碼的測試範例：  
    >   
    >  **預先部署**  
    >   
    >  `#Start`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\start.txt`  
    >   
    >  **部署後**  
    >   
    >  `#End`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\end.txt`  

## <a name="deploy-software-updates-to-the-server-group-and-monitor-status"></a>將軟體更新部署至伺服器群組並監視狀態  
您使用一般的部署程序將軟體更新部署至伺服器群組集合。 部署軟體更新之後，您可以在 Configuration Manager 主控台中監視軟體更新部署。
1.  在伺服器群組集合中[部署軟體更新](manually-deploy-software-updates.md)。   

2.  [監視軟體更新部署](monitor-software-updates.md)。 除了標準的軟體更新部署監視檢視外，當用戶端等待安裝軟體更新時，也會顯示**等候鎖定**狀態。 如需詳細資訊，請檢閱 UpdatesDeployment.log 檔案。


## <a name="clear-the-deployment-locks-for-computers-in-a-server-group"></a>清除伺服器群組中的電腦部署鎖定  
當電腦無法釋放部署鎖定時，您可以手動釋放集合的所有伺服器群組部署鎖定。 只有當部署阻礙更新集合中的電腦，且仍有不相容的電腦時，才清除鎖定。  
1.  在 [資產與相容性] 工作區中，按一下 [裝置集合]，再按一下集合清除部署鎖定。  

2.  在 [常用] 索引標籤的 [部署] 群組中，按一下 [清除伺服器群組部署鎖定]。 當用戶端無法安裝軟體更新，並阻止其他用戶端安裝軟體更新時，您可以手動清除部署鎖定。  
