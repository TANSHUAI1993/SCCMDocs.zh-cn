---
title: Updates Publisher | Microsoft Docs
description: "使用 System Center Updates Publisher 以管理自訂更新"
ms.custom: na
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2200b02b-e76b-4aa7-a77a-6dc5e70f1333
caps.latest.revision: "1"
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: NOINDEX, NOFOLLOW
ms.openlocfilehash: f4951c204b32da58174b94a539b380c278fa9756
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="system-center-updates-publisher"></a>System Center 更新發行者

*適用於：System Center Updates Publisher*

System Center Updates Publisher (Updates Publisher) 是一個獨立的工具，可讓獨立軟體廠商或企業營運應用程式開發人員管理自訂更新。 這包含具有相依性的更新 (例如驅動程式和更新配套)。

Updates Publisher 可用於：

-   從外部目錄 (非 Microsoft 的更新目錄) 匯入更新。
-   修改更新定義，包括適用性及部署中繼資料。
-   將更新匯出至外部目錄。
-   將更新發行至更新伺服器。

將更新發行到更新伺服器之後，您便可以使用 System Center Configuration Manager 來偵測那些更新，並將它們部署至受管理的裝置。

> [!TIP]  
> 目前仍持續支援舊版的 [System Center Updates Publisher 2011 (英文)](http://go.microsoft.com/fwlink/?LinkId=848111)。 此更新版本保留相同的功能，但能支援額外的作業系統、提供可簡化某些作業的新功能，並有更新的使用者介面。

## <a name="workspaces"></a>工作區
當您開啟 Updates Publisher 時，預設會顯示 [更新工作區] 的 [概觀] 節點。

![Updates Publisher 主控台](media/console1.png)   


Updates Publisher 具有四個工作區來協助整理其功能。


**更新工作區：**使用此工作區來[建立](/sccm/sum/tools/create-updates-with-updates-publisher)及[管理](/sccm/sum/tools/manage-updates-with-updates-publisher)軟體更新和更新配套。 這包含將更新和配套指派至發行集，以及發行和匯出至另一個 Updates Publisher 存放庫。

**發行集工作區：**這是您[管理發行集](/sccm/sum/tools/updates-publisher-publications)的位置。 發行集是您所建立之更新的群組，以簡化更新的匯出及發行。

管理發行集包括將更新發行到伺服器，來讓用戶端可以尋找並安裝更新、匯出更新和配套以供另一個 Updates Publisher 安裝使用，或是修改發行集的內容或詳細資料。



**規則工作區：**您可以在此[管理適用性規則](/sccm/sum/tools/updates-publisher-applicability-rules)並儲存它們，然後搭配您部署的更新使用。 規則有兩種：

-   可安裝的規則 - 這些規則可協助判斷用戶端是否應安裝更新。
-   已安裝的規則 - 這些規則會驗證更新是否已安裝。

**目錄工作區：**使用此工作區來新增及[管理軟體更新目錄](/sccm/sum/tools/updates-publisher-catalogs)。 這包含將軟體更新從那些目錄匯入到 Updates Publisher 存放庫。
## <a name="first-steps"></a>第一步
若要開始使用，請先[安裝](/sccm/sum/tools/install-updates-publisher) Updates Publisher，然後[設定 Updates Publisher 的選項](/sccm/sum/tools/updates-publisher-options)。
