---
title: "Asset Intelligence 必要條件 | Microsoft Docs"
description: "取得 System Center Configuration Manager 中的 Asset Intelligence 必要條件。"
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 23ab4f94-7bfe-436e-8a6a-029409a2730c
caps.latest.revision: "10"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 2bcc6dd84b236187ea9cbfa0b85c25e7ec25719c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="prerequisites-for-asset-intelligence-in-system-center-configuration-manager"></a>System Center Configuration Manager 中之 Asset Intelligence 的先決條件

*適用於：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 中的 Asset Intelligence 具有外部相依性和產品內的相依性。  

## <a name="dependencies-external-to-configuration-manager"></a>Configuration Manager 外部的相依性  
 下表提供 Configuration Manager 外部的 Asset Intelligence 相依性。  

|相依性|更多資訊|  
|----------------|----------------------|  
|成功登入事件稽核的先決條件|系統提供四種 Asset Intelligence 報告，以顯示在用戶端電腦上收集到的 Windows 安全性事件記錄檔資訊。 如果未將安全性事件記錄檔設定為記錄所有成功登入事件，這些報告就不會包含任何資料，即使已啟用適當的硬體清查報告類別亦同。<br /><br /> 下列 Asset Intelligence 報告需要所收集的 Windows 安全性事件記錄檔資訊：<br /><br /> -   硬體 03A - 主要電腦使用者<br />-   硬體 03B - 特定主要主控台使用者的電腦<br />-   硬體 04A - 共用 (多使用者) 電腦<br />-   硬體 05A - 特定電腦上的主控台使用者<br /><br /> 若要啟用硬體清查用戶端代理程式以清查支援這些報告所需的資訊，您必須先修改用戶端上的 Windows 安全性事件記錄檔設定，以記錄所有成功的登入事件，並啟用 **SMS_SystemConsoleUser** 硬體清查報告類別。 如需修改安全性事件記錄檔設定以記錄所有成功登入事件的詳細資訊，請參閱[啟用成功登入事件的稽核](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md#BKMK_EnableSuccessLogonEvents)。|  

> [!NOTE]  
>  **SMS_SystemConsoleUser** 硬體清查報告類別只會保留最近 90 天安全性事件記錄檔的成功登入事件資料，而不論記錄檔的長度為何。 如果安全性事件記錄檔所包含的資料少於 90 天，則會讀取整個記錄檔。  

## <a name="dependencies-internal-to-configuration-manager"></a>Configuration Manager 內部的相依性  
 下表提供 Configuration Manager 內部的 Asset Intelligence 相依性。  

|相依性|更多資訊|  
|----------------|----------------------|  
|用戶端代理程式先決條件|Asset Intelligence 報告需要透過用戶端硬體和軟體清查報告所取得的用戶端資訊。 若要取得所有 Asset Intelligence 報告的必要資訊，您必須啟用下列用戶端代理程式：<br /><br /> -   硬體清查用戶端代理程式<br />-   軟體計量用戶端代理程式|  
|硬體清查用戶端代理程式相依性|若要收集某些 Asset Intelligence 報告所需的清查資料，您必須啟用硬體清查用戶端代理程式。 此外，您還必須在主要站台伺服器電腦上，啟用 Asset Intelligence 報告所需的一些硬體清查報告類別。<br /><br /> 如需啟用硬體清查用戶端代理程式的相關資訊，請參閱[如何在 System Center Configuration Manager 中擴充硬體清查](../../../../core/clients/manage/inventory/extend-hardware-inventory.md)。|  
|軟體計量用戶端代理程式相依性|有些 Asset Intelligence 軟體報告需要軟體計量用戶端代理程式來提供資料。 如需啟用軟體計量用戶端代理程式的相關資訊，請參閱[在 System Center Configuration Manager 中使用軟體計量監視應用程式使用量](../../../../apps/deploy-use/monitor-app-usage-with-software-metering.md)。<br /><br /> 下列 Asset Intelligence 報告需要軟體計量用戶端代理程式來提供資料：<br /><br /> -   軟體 07A - 依電腦數目列出最近使用過的可執行檔<br />-   軟體 07B - 最近使用過指定可執行檔的電腦<br />-   軟體 07C - 特定電腦上最近使用過的可執行檔<br />-   軟體 08A - 依使用者數目列出最近使用過的可執行檔<br />-   軟體 08B - 最近使用過指定可執行檔的使用者<br />-   軟體 08C - 依指定使用者列出最近使用過的可執行檔|  
|Asset Intelligence 硬體清查報告類別先決條件|Configuration Manager 中的 Asset Intelligence 報告需要特定硬體清查報告類別。 在啟用硬體清查報告類別，且用戶端已根據這些類別回報硬體清查之前，相關聯的 Asset Intelligence 報告不會包含任何資料。 您可以啟用下列硬體清查報告類別，來支援 Asset Intelligence 報告需求：<br /><br /> -   SMS_SystemConsoleUsage<sup>1</sup><br />-   SMS_SystemConsoleUser<sup>1</sup><br />-   SMS_InstalledSoftware<br />-   SMS_AutoStartSoftware<br />-   SMS_BrowserHelperObject<br />-   Win32_USBDevice<br />-   SMS_InstalledExecutable<br />-   SMS_SoftwareShortcut<br />-   SoftwareLicensingService<br />-   SoftwareLicensingProduct<br />-   SMS_SoftwareTag<br /><br /> <sup>1</sup> 預設已啟用 **SMS_SystemConsoleUsage** 和 **SMS_SystemConsoleUser** Asset Intelligence 硬體清查報告類別。<br /><br /> 當您按一下 [Asset Intelligence] 節點時，您可以在 Configuration Manager 主控台的 [資產與相容性] 工作區中，編輯 Asset Intelligence 硬體清查報告類別。 如需詳細資訊，請參閱[設定 System Center Configuration Manager 中的 Asset Intelligence](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md) 主題中的[啟用 Asset Intelligence 硬體清查報告類別](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md#BKMK_EnableAssetIntelligence)一節。|  
|Reporting Services 點|您必須先安裝 Reporting Services 點站台系統角色，才會顯示軟體更新報告。 如需建立 Reporting Services 點的詳細資訊，請參閱 [在 Configuration Manager 中設定報告](http://go.microsoft.com/fwlink/p/?LinkId=232661)。|  
