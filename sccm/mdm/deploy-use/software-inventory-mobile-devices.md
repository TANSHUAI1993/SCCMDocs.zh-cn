---
title: "向 Microsoft Intune 註冊之行動裝置的軟體清查 | Microsoft Docs"
description: "向 Microsoft Intune 註冊之行動裝置的軟體清查。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a0eae17a-60a8-4132-91af-0b10ad338c92
caps.latest.revision: "18"
caps.handback.revision: "0"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 2ed79d02535768de136947e4a5b63ad186d9a3cd
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="software-inventory-for-mobile-devices-enrolled-with-microsoft-intune"></a>向 Microsoft Intune 註冊之行動裝置的軟體清查

*適用對象：System Center Configuration Manager (最新分支)*

 您可以收集行動裝置上所安裝之應用程式的清查。 清查的應用程式視裝置為公司所有或為個人所有而定。 若為個人裝置，將只會清查 Microsoft Intune 所管理的應用程式。  

> [!NOTE]  
>  行動裝置上所安裝之應用程式的清查會在[硬體清查](mobile-device-hardware-inventory-hybrid.md)過程中收集。  

 以下是針對個人擁有的裝置或公司擁有的裝置所清查的應用程式。  

|平台|屬個人擁有的裝置|屬公司擁有的裝置|  
|--------------|---------------------------------|--------------------------------|  
|Windows 10 (不含 Configuration Manager 用戶端)|僅限受管理的應用程式|僅限受管理的應用程式|
|Windows 8.1 (不含 Configuration Manager 用戶端)|僅限受管理的應用程式|僅限受管理的應用程式|  
|Windows Phone 8|僅限受管理的應用程式|僅限受管理的應用程式|  
|Windows RT|僅限受管理的應用程式|僅限受管理的應用程式|  
|iOS|僅限受管理的應用程式|安裝在裝置上的所有應用程式|  
|Android|僅限受管理的應用程式|安裝在裝置上的所有應用程式|  

如需使用軟體清查在用戶端裝置上收集檔案資訊的詳細資訊，請參閱[軟體清查簡介](../../core/clients/manage/inventory/introduction-to-software-inventory.md)和[如何設定軟體清查設定](../../core/clients/manage/inventory/configure-software-inventory.md)。
