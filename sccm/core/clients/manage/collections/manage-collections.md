---
title: "管理集合 | Microsoft Docs"
description: "在 System Center Configuration Manager 中執行一般集合管理工作。"
ms.custom: na
ms.date: 4/25/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e102fd1a-76df-4d8e-b1b0-10ee18318f67
caps.latest.revision: "8"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 4d44f98eb0755619cdd2101203a13725186b835b
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-manage-collections-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中管理集合

適用於：System Center Configuration Manager (最新分支)

本主題中的概觀資訊可用來協助您執行 System Center Configuration Manager 中集合的管理工作。  

> [!NOTE]  
>  如需如何建立 Configuration Manager 集合的資訊，請參閱[如何在 System Center Configuration Manager 中建立集合](../../../../core/clients/manage/collections/create-collections.md)。  

## <a name="how-to-manage-device-collections"></a>如何管理裝置集合  
 在 [資產與相容性]  工作區中，選取 [裝置集合] ，並選取要管理的集合，然後選取管理工作。  

 請參閱下表，了解選取管理工作前需要知道的資訊。  

|管理工作|詳細資料|詳細資訊|  
|---------------------|-------------|----------------------|  
|**顯示成員**|在 [裝置]  節點下，顯示臨時節點中為所選取集合成員的所有資源。|沒有其他資訊。|  
|**新增選取的項目**|請提供下列選項來執行下列其中一個動作：<br /><br /> - <br />                    **將選取的項目新增至現有的裝置集合** - 開啟 [選取集合] 對話方塊，您可以在其中選取您要新增所選取集合成員的集合。 使用 [包含集合]  成員資格規則，將選取的集合包含在這個集合。<br /><br /> - **將選取的項目新增至新裝置集合** - 開啟 [建立裝置集合精靈]，您可以在其中建立新的集合。 使用 [包含集合]  成員資格規則，將選取的集合包含在這個集合。|[如何在 System Center Configuration Manager 中建立集合](../../../../core/clients/manage/collections/create-collections.md)|  
|**安裝用戶端**|開啟 [安裝用戶端精靈]，這個精靈使用用戶端推入安裝在所選取集合的所有電腦上安裝 Configuration Manager 用戶端。|[如何將用戶端部署至 Windows 電腦](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md)|  
|**管理親和性要求**|開啟 [管理使用者裝置親和性要求]  對話方塊，您可以在其中核准或拒絕擱置要求，以建立所選取集合中裝置的使用者裝置親和性。|[在 System Center Configuration Manager 中使用使用者裝置親和性連結使用者和裝置](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)|  
|**清除必要的 PXE 部署**|清除所選取集合之所有成員中的任何必要 PXE 開機部署。|[作業系統部署簡介](../../../../osd/understand/introduction-to-operating-system-deployment.md)|  
|**更新成員資格**|評估所選取集合的成員資格。 對於具有許多成員的集合，這個更新可能需要一些時間才能完成。 使用 [重新整理]  動作，會在更新完成之後，使用新的集合成員來更新顯示。|沒有其他資訊。|  
|**新增資源**|開啟 [將資源新增至集合]  對話方塊，您可以在其中搜尋要新增至所選取集合的新資源。<br /><br /> 所選取集合的圖示會顯示沙漏符號，同時進行更新。|沒有其他資訊。|  
|**用戶端通知**|指示所選取裝置集合中的所有用戶端下載電腦或使用者原則。|沒有其他資訊。|  
|**Endpoint Protection**|執行完整或快速反惡意程式碼掃描，或將最新的反惡意程式碼定義下載至所選取集合中的電腦。|[System Center Configuration Manager 中的 Endpoint Protection](../../../../protect/deploy-use/endpoint-protection.md)|  
|**匯出**|開啟 [匯出集合精靈]，以協助您將這個集合匯出至管理物件格式 (MOF) 檔案，之後再將這個檔案封存或用於另一個 Configuration Manager 站台。<br /><br /> 當您匯出集合時，不會匯出所選取集合利用 **Include** 或 **Exclude** 規則所參考的集合。|沒有其他資訊。|  
|**複製**|建立所選取集合的複本。 新的集合會使用選取的集合作為限制集合。|沒有其他資訊。|  
|**刪除**|刪除選取的集合。 您也可以從站台資料庫中刪除集合中的所有資源。<br /><br /> 您無法刪除 Configuration Manager 的內建集合。|如需內建集合的清單，請參閱 [System Center Configuration Manager 的集合簡介](../../../../core/clients/manage/collections/introduction-to-collections.md)。|  
|**模擬部署**|開啟 [模擬應用程式部署精靈]  ，可讓您不需要安裝或解除安裝應用程式，即可測試應用程式部署的結果。|[如何使用 System Center Configuration Manager 模擬應用程式部署](../../../../apps/deploy-use/simulate-application-deployments.md)|  
|**部署**|顯示下列選項：<br /><br /> - <br />                    **應用程式** - 開啟 [部署軟體精靈]，您可以在其中選取並設定所選取集合的應用程式部署。<br /><br /> - <br />                    **程式** – 開啟 [部署軟體精靈]  ，您可以在其中選取並設定所選取集合的封裝和程式部署。<br /><br /> - **設定基準** - 開啟 [部署設定基準] 對話方塊，您可以在其中設定將一個或多個設定基準部署至選取的集合。<br /><br /> - <br />                    **工作順序** – 開啟 [部署軟體精靈]  ，您可以在其中選取並設定所選取集合的工作順序部署。<br /><br /> - <br />                    **軟體更新** - 開啟 [部署軟體更新精靈]，您可以在其中設定將軟體更新部署至所選取集合中的資源。|[如何使用 System Center Configuration Manager 部署應用程式](../../../../apps/deploy-use/deploy-applications.md)<br /><br /> [System Center Configuration Manager 中的套件和程式](../../../../apps/deploy-use/packages-and-programs.md)<br /><br /> [如何在 System Center Configuration Manager 中部署設定基準](../../../../compliance/deploy-use/deploy-configuration-baselines.md)<br /><br /> [管理工作順序，將 System Center Configuration Manager 中的工作自動化](../../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md)<br /><br /> [在 System Center Configuration Manager 中管理軟體更新](/sccm/sum/understand/software-updates-introduction)|  

## <a name="how-to-manage-user-collections"></a>如何管理使用者集合  
 在 [資產與相容性]  工作區中，選取 [使用者集合] ，並選取要管理的集合，然後選取管理工作。  

 請參閱下表，了解選取管理工作前需要知道的資訊。  

|管理工作|詳細資料|詳細資訊|  
|---------------------|-------------|----------------------|  
|**顯示成員**|在 [使用者]  節點下，顯示臨時節點中為所選取集合成員的所有資源。|沒有其他資訊。|  
|**新增選取的項目**|這個選項可讓您執行下列其中一個動作：<br /><br /> - <br />                    **將選取的項目新增至現有的使用者集合** - 開啟 [選取集合] 對話方塊，您可以在其中選取您要新增所選取集合成員的集合。 使用 [包含集合]  成員資格規則，將選取的集合包含在這個集合。<br /><br /> - **將選取的項目新增至新使用者集合** - 開啟 [建立使用者集合精靈]，您可以在其中建立新的集合。 使用 [包含集合]  成員資格規則，將選取的集合包含在這個集合。|[如何在 System Center Configuration Manager 中建立集合](../../../../core/clients/manage/collections/create-collections.md)|  
|**管理親和性要求**|開啟 [管理使用者裝置親和性要求]  對話方塊，您可以在其中核准或拒絕擱置要求，以建立所選取集合中使用者的使用者裝置親和性。|[在 System Center Configuration Manager 中使用使用者裝置親和性連結使用者和裝置](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)|  
|**更新成員資格**|評估所選取集合的成員資格。 對於具有許多成員的集合，這個更新可能需要一些時間才能完成。 使用 [重新整理]  動作，會在更新完成之後，使用新的集合成員來更新顯示。<br /><br /> 所選取集合的圖示會顯示沙漏符號，同時進行更新。|沒有其他資訊。|  
|**新增資源**|開啟 [將資源新增至集合]  對話方塊，您可以在其中搜尋要新增至所選取集合的新資源。|沒有其他資訊。|  
|**匯出**|開啟 [匯出集合精靈]，以協助您將這個集合匯出至管理物件格式 (MOF) 檔案，之後再將這個檔案封存或用於另一個 Configuration Manager 站台。<br /><br /> 當您匯出集合時，不會匯出所選取集合利用 **Include** 或 **Exclude** 規則所參考的集合。|沒有其他資訊。|  
|**複製**|建立所選取集合的複本。 新的集合會使用選取的集合作為限制集合。|沒有其他資訊。|  
|**刪除**|刪除選取的集合。 您也可以從站台資料庫中刪除集合中的所有資源。<br /><br /> 您無法刪除 Configuration Manager 的內建集合。|如需內建集合的清單，請參閱 [System Center Configuration Manager 的集合簡介](../../../../core/clients/manage/collections/introduction-to-collections.md)。|  
|**模擬部署**|開啟 [模擬應用程式部署精靈]  ，可讓您不需要安裝或解除安裝應用程式，即可測試應用程式部署的結果。|[如何使用 System Center Configuration Manager 模擬應用程式部署](../../../../apps/deploy-use/simulate-application-deployments.md)|  
|**部署**|顯示下列選項：<br /><br /> - **應用程式** - 開啟 [部署軟體精靈]，您可以在其中選取並設定所選取集合的應用程式部署。<br /><br /> - <br />                    **程式** – 開啟 [部署軟體精靈]  ，您可以在其中選取並設定所選取集合的封裝和程式部署。<br /><br /> - **設定基準** - 開啟 [部署設定基準] 對話方塊，您可以在其中設定將一個或多個設定基準部署至選取的集合。|[如何使用 System Center Configuration Manager 部署應用程式](../../../../apps/deploy-use/deploy-applications.md)<br /><br /> [System Center Configuration Manager 中的套件和程式](../../../../apps/deploy-use/packages-and-programs.md)<br /><br /> [如何在 System Center Configuration Manager 中部署設定基準](../../../../compliance/deploy-use/deploy-configuration-baselines.md)|  

##  <a name="BKMK_CollProp"></a> 集合內容  
 當您開啟集合的 [內容]  對話方塊時，可以檢視並設定集合的下列內容。  

|索引標籤名稱|詳細資訊|  
|--------------|----------------------|  
|**一般**|可讓您檢視和設定所選取集合 (包含集合名稱和限制集合) 的一般資訊。|  
|**成員資格規則**|可讓您設定可定義這個集合成員資格的成員資格規則。 如需詳細資訊，請參閱[如何在 System Center Configuration Manager 中建立集合](../../../../core/clients/manage/collections/create-collections.md)。|  
|**電源管理**|可讓您設定指派給所選取集合中電腦的電源管理計畫。 如需詳細資訊，請參閱[電源管理簡介](../../../../core/clients/manage/power/introduction-to-power-management.md)。|  
|**部署**|顯示已部署至所選取集合成員的任何軟體。|  
|**維護期間**|可讓您檢視和設定套用至所選取集合成員的維護期間。 如需詳細資訊，請參閱[如何使用 System Center Configuration Manager 中的維護期間](../../../../core/clients/manage/collections/use-maintenance-windows.md)。|  
|**集合變數**|可讓您設定套用至這個集合並可供工作順序使用的變數。 如需詳細資訊，請參閱[工作順序內建變數](../../../../osd/understand/task-sequence-built-in-variables.md)。|  
|**發佈點群組**|可讓您將一個或多個發佈點群組與所選取集合成員產生關聯。 如需詳細資訊，請參閱[管理 System Center Configuration Manager 的內容與內容基礎結構](../../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)。|  
|**安全性**|顯示具有所選取集合與相關聯角色和安全性範圍權限的系統管理使用者。|  
|**監視**|可讓您設定何時產生用戶端狀態和 Endpoint Protection 的警示。 如需詳細資訊，請參閱[如何在 System Center Configuration Manager 中設定用戶端狀態](../../../../core/clients/deploy/configure-client-status.md)和[如何監視 System Center Configuration Manager 中的 Endpoint Protection](../../../../protect/deploy-use/monitor-endpoint-protection.md)。|  
