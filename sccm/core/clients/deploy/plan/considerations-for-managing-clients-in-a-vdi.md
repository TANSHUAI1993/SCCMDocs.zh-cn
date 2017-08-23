---
title: "虛擬桌面基礎結構 (VDI) 用戶端管理 | Microsoft Docs "
description: "在虛擬桌面基礎結構 (VDI) 中管理 System Center Configuration Manager 用戶端。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: abd45393-d84e-4583-bc80-74bbb3709577
caps.latest.revision: "7"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: d73daf6427b8c58d21d579f3b41df513cc3e3b0b
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="considerations-for-managing-system-center-configuration-manager-clients--in-a-virtual-desktop-infrastructure-vdi"></a>在虛擬桌面基礎結構 (VDI) 中管理 System Center Configuration Manager 用戶端的考量

*適用對象：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 支援在下列虛擬桌面基礎結構 (VDI) 案例中安裝 Configuration Manager 用戶端︰  

-   **個人虛擬機器** - 個人虛擬機器通常會在您想要確定在各個工作階段間於虛擬機器上維護使用者資料及設定時使用。  

-   **遠端桌面服務工作階段** - 遠端桌面服務可讓伺服器同時裝載多個用戶端工作階段。 使用者可以連線至工作階段，然後在該伺服器上執行應用程式。  

-   **集區式虛擬機器** - 集區式虛擬機器不會保存在各個工作階段之間。 當工作階段關閉時，會放棄所有資料和設定。 當遠端桌面服務因所需的商務應用程式無法在裝載用戶端工作階段的 Windows Server 上執行而無法使用時，集區式虛擬機器便可派上用場。  

 下表列出在虛擬桌面基礎結構中管理 Configuration Manager 用戶端的考量。  

|虛擬機器類型|考量|  
|--------------------------|--------------------|  
|個人虛擬機器|Configuration Manager 會同等看待個人虛擬機器與實體電腦。 Configuration Manager 用戶端可以預先安裝在虛擬機器映像上，或可在佈建虛擬機器後再進行部署。|  
|遠端桌面服務|未針對個別遠端桌面工作階段安裝 Configuration Manager 用戶端。 反而只在遠端桌面服務伺服器上安裝一次用戶端。 所有 Configuration Manager 功能可以在遠端桌面服務伺服器上使用。|  
|集區式虛擬機器|當集區式虛擬機器解除委任時，使用 Configuration Manager 所做的所有變更都會遺失。<br /><br /> 從 Configuration Manager 功能傳回的資料 (例如硬體清查、軟體清查和軟體計量)，可能與您所需的資料無關，因為虛擬機器可能只會在短期間內運作。 請考慮從清查工作排除集區式虛擬機器。|  

 因為虛擬化支援在相同的實體電腦上執行多個 Configuration Manager 用戶端，所以許多用戶端操作皆會針對排程的動作內建隨機延遲時間，例如硬體和軟體清查、反惡意程式碼掃描、軟體安裝，以及軟體更新掃描。 此延遲有助於分散 CPU 處理，以及電腦的資料傳送，該電腦內含多部執行 Configuration Manager 用戶端的虛擬機器。  

> [!NOTE]  
>  Windows Embedded 用戶端的一項例外狀況是在維修模式下，未執行於虛擬化環境的 Configuration Manager 用戶端也會使用此隨機延遲。 當您有許多已部署的用戶端時，此行為可避免網路頻寬尖峰，以及降低 Configuration Manager 站台系統上的 CPU 處理需求，例如管理點和站台伺服器。 延遲間隔會依 Configuration Manager 功能而有所不同。  
>   
>  預設會針對必要的軟體更新和必要的應用程式部署來停用隨機延遲，但必須使用下列用戶端設定： **電腦代理程式**： **停用期限隨機設定**。
