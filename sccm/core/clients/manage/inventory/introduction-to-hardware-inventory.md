---
title: "硬體清查 - Configuration Manager | Microsoft Docs"
description: "了解 System Center Configuration Manager 中的硬體清查簡介。"
ms.custom: na
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 3969952e-9d05-49c9-82a2-e7e90ccef511
caps.latest.revision: "6"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: c64f0b42bff25e8e91cf9101d6fbb538634eab15
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="introduction-to-hardware-inventory-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的硬體清查簡介

適用於：System Center Configuration Manager (最新分支)

您可使用 System Center Configuration Manager 的硬體清查功能，收集組織用戶端裝置的硬體設定相關資訊。 若要收集硬體清查，必須啟用用戶端設定中的 [在用戶端上啟用硬體清查]  設定。  

 在啟用硬體清查且用戶端執行硬體清查週期之後，用戶端會將資訊傳送至用戶端站台中的某個管理點。 管理點接著會將清查資訊轉送至 Configuration Manager 站台伺服器，再由該伺服器將清查資訊儲存到站台資料庫。 硬體清查會根據您在用戶端設定中指定的排程在用戶端上執行。  

 您有多種方法可以檢視 Configuration Manager 收集的硬體清查資料。 包含以下各項：  

-   [建立傳回裝置的查詢，這些裝置是以特定的硬體組態為基礎](../../../../core/servers/manage/queries-technical-reference.md)。  

-   [建立以特定硬體組態為基礎的查詢式集合](../../../../core/clients/manage/collections/introduction-to-collections.md)。 查詢式集合成員資格會依照排程自動更新。 您可以使用包括軟體部署在內的數個工作集合。 。  

-   [執行報告，顯示貴組織硬體組態的特定詳細資料](../../../../core/servers/manage/reporting.md)。   

-   [使用資源總管](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md)，檢視從用戶端裝置收集之硬體清查的詳細資訊。   

 在用戶端裝置上執行硬體清查時，用戶端傳回的第一筆清查資料一律是完整清查。 後續的清查報告只包含 Delta 清查資訊。 站台伺服器會依差異清查資訊收到的順序來進行處理。 如果遺漏某個用戶端的差異資訊，站台伺服器會拒絕其他的差異資訊，並指示該用戶端執行完整清查週期。  

 Configuration Manager 提供雙重開機電腦的有限支援。 Configuration Manager 可以探索雙重開機電腦，但只會傳回清查週期執行時仍作用中的作業系統清查資訊。  

> [!NOTE]  
>  如需如何搭配執行 Linux 和 UNIX 用戶端使用硬體清查資訊，請參閱 [System Center Configuration Manager 中的 Linux 及 UNIX 的硬體清查](../../../../core/clients/manage/inventory/hardware-inventory-for-linux-and-unix.md)。  

## <a name="extending-configuration-manager-hardware-inventory"></a>擴充 Configuration Manager 硬體清查  
 除了 Configuration Manager 的內建硬體清查，您也可以使用下列方法之一來擴充硬體清查，收集其他資訊：  

- 您可以從 Configuration Manager 主控台啟用、停用、新增和移除硬體清查的清查類別。|  
- 使用 NOIDMIF 檔案收集 Configuration Manager 無法清查的用戶端裝置相關資訊。 例如，您可能要收集裝置的資產數字資訊存在於只要在裝置上的標籤。 NOIDMIF 清查會自動關聯於它所收集從用戶端裝置。  
- 使用 IDMIF 檔案來收集尚未與 Configuration Manager 用戶端建立關聯之資產的資訊，例如投影機、影印機及網路印表機。  

 如需如何使用這些方法來擴充 Configuration Manager 硬體清查的詳細資訊，請參閱 [How to configure hardware inventory in System Center Configuration Manager](../../../../core/clients/manage/inventory/configure-hardware-inventory.md) (如何在 System Center Configuration Manager 中設定硬體清查)。  
