---
title: "軟體更新的最佳做法 | Microsoft Docs"
description: "使用 System Center Configuration Manager 軟體更新的這些最佳做法。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: 6d20389a-9de2-4a64-bced-9fc4fa519174
ms.openlocfilehash: 5df20f3703442de1be6220ca2770e182e330c036
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="best-practices-for-software-updates-in-system-center-configuration-manager"></a>System Center Configuration Manager 軟體更新的最佳作法

*適用於：System Center Configuration Manager (最新分支)*

本主題包括 System Center Configuration Manager 軟體更新的最佳做法。 該資訊會根據針對進行中操作的初始安裝和最佳作法進行排序。  

## <a name="installation-best-practices"></a>安裝最佳作法  
 當您在 Configuration Manager 中安裝軟體更新時，請使用下列最佳做法。  

### <a name="use-a-shared-wsus-database-for-software-update-points"></a>針對軟體更新點使用共用的 WSUS 資料庫  
 當您在主要站台安裝一個以上的軟體更新點時，請在相同的 Active Directory 樹系中針對各軟體更新點使用相同的 WSUS 資料庫。 藉由共用相同的資料庫，您可以在用戶端切換至新軟體更新點時大幅降低對用戶端和網路效能所造成的影響。 當用戶端切換到與舊軟體更新點共用資料庫的新軟體更新點時，仍會進行差異掃描，但此掃描遠低於 WSUS 伺服器本身擁有資料庫的情況。  

> [!IMPORTANT]  
>  當您針對軟體更新點使用共用的 WSUS 資料庫時，您也必須共用本機 WSUS 內容資料夾。  

 如需軟體更新點切換的詳細資訊，請參閱[在 Configuration Manager 中規劃軟體更新](../../sum/plan-design/plan-for-software-updates.md)主題中的[軟體更新點切換](../../sum/plan-design/plan-for-software-updates.md#BKMK_SUPSwitching)一節。  

### <a name="when-configuration-manager-and-wsus-use-the-same-sql-server-configure-one-of-these-to-use-a-named-instance-and-the-other-to-use-the-default-instance-of-sql-server"></a>當 Configuration Manager 和 WSUS 使用相同的 SQL Server 時，請將其中一項設定為使用具名執行個體，並將其他應用程式設定為使用預設的 SQL Server 執行個體  
 如果 Configuration Manager 和 WSUS 資料庫使用相同的 SQL Server，並且共用相同的 SQL Server 執行個體，您會很難在兩個應用程式間判斷資源使用情況。 當您的 Configuration Manager 和 WSUS 使用不同的 SQL Server 執行個體時，就可以很容易地疑難排解和診斷各個應用程式間可能發生的資源使用問題。  

### <a name="specify-the-store-updates-locally-setting-for-the-wsus-installation"></a>針對 WSUS 安裝指定 [在本機存放更新] 設定  
 當您安裝 WSUS 時，請選取 [在本機存放更新] 設定。 當選取此設定時，會在同步處理進行期間下載與軟體更新相關聯的授權條款，並將其儲存在 WSUS 伺服器的本機硬碟。 如果未選取此設定，用戶端電腦可能會無法針對具有授權條款的軟體更新，掃描其軟體更新相容性。 當您安裝軟體更新點時，WSUS 同步處理管理員預設每隔 60 分鐘就會確認一次此設定。  

## <a name="operational-best-practices"></a>操作的最佳作法  
 當您使用軟體更新時，請使用下列最佳作法：  

### <a name="limit-software-updates-to-1000-in-a-single-software-update-deployment"></a>在單一軟體更新部署時，將軟體更新數目限制為 1000  
 您必須將各軟體更新部署的軟體更新數目限制為 1000。 當您建立自動部署規則時，請確認您指定的準則不會導致多於 1000 個軟體更新。 當您手動部署軟體更新時，請勿選取部署多於 1000 個軟體更新。  

### <a name="create-a-new-software-update-group-each-time-an-automatic-deployment-rule-runs-for-patch-tuesday-and-for-general-deployment"></a>每一次針對「週二修補程式日」和一般部署執行自動部署規則，以建立新的軟體更新群組。  
 軟體更新部署的限制為 1000 個軟體更新。 當您建立自動部署規則時，可以指定每一次執行規則時皆使用現有的更新群組，或建立新更新群組。 當您指定的準則適用於會產生多個軟體更新的自動部署規則，以及週期性排程執行規則時，請指定每次執行規則時建立新的軟體更新群組。 如此可防止每次部署超過 1000 次軟體更新的每一部署限制。  

### <a name="use-an-existing-software-update-group-for-automatic-deployment-rules-for-endpoint-protection-definition-updates"></a>使用自動部署規則的現有軟體更新群組進行 Endpoint Protection 定義更新  
 當您經常使用自動部署規則部署 Endpoint Protection 定義更新時，請務必使用現有的軟體更新群組。 否則，在一段時間後可能會建立數百個軟體更新群組。 通常，定義更新發行者會將定義更新設定為在該更新由四個較新的更新所取代時到期。 因此，自動部署規則所建立的軟體更新群組，絕不會包含四個以上發行者的定義更新：一個使用中，三個已取代。  

## <a name="see-also"></a>另請參閱  
 [在 System Center Configuration Manager 中規劃軟體更新](../../sum/plan-design/plan-for-software-updates.md)
