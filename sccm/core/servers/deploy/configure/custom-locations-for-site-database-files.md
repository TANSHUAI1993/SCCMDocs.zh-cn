---
title: "自訂資料庫檔案位置 | Microsoft Docs"
description: "了解如何指定 SQL Server 資料庫檔案的自訂位置。"
ms.custom: na
ms.date: 10/06/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 500a9aa6-68aa-44eb-bf49-350c1314a697
caps.latest.revision: "3"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: cfac2c03c1b71b40c68d8acd5fbd96c5e98caaa9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="custom-locations-for-system-center-configuration-manager-site-database-files"></a>System Center Configuration Manager 站台資料庫檔案的自訂位置

*適用於：System Center Configuration Manager (最新分支)*

 System Center Configuration Manager 支援 SQL Server 資料庫檔案的自訂位置。  

> [!NOTE]  
>  當您使用 SQL Server 叢集時，無法使用指定非預設檔案位置的選項。  

 在新的主要站台或管理中心網站之**安裝期間**，您可以：  

-   **為站台資料庫指定非預設的檔案位置**：Configuration Manager 安裝程式之後會使用這些位置，建立站台資料庫。  

-   **指定採用使用自訂檔案位置之預先建立的 SQL Server 資料庫**：Configuration Manager 安裝程式之後會使用預先建立的資料庫及其預先設定的檔案位置。  

**安裝之後**，您可變更站台資料庫檔案的位置。 這必須停止站台及編輯 SQL Server 中的檔案位置：  

-   在 Configuration Manager 站台伺服器上，停止 **SMS_Executive** 服務。  

-   請使用您 SQL Server 版本的相關文件，指引您如何移動使用者資料庫。 例如，您若是使用 SQL Server 2014，請參閱 TechNet 上的 [移動使用者資料庫](https://technet.microsoft.com/library/ms345483\(v=sql.120\).aspx) 。  

-   移動好資料庫檔案之後，請重新啟動 Configuration Manager 站台伺服器上的 **SMS_Executive** 服務。  
