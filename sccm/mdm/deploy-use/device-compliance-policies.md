---
title: "裝置合規性政策 | Microsoft Docs"
description: "了解如何在 System Center Configuration Manager 中管理相容性原則，使裝置符合條件式存取原則。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ad8fa94d-45bb-4c94-8d86-31234c5cf21c
caps.latest.revision: "18"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: bcaa2a9b5474e06bf344dc4fd47dbb160ea36297
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="device-compliance-policies-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的裝置相容性原則

*適用於：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 中的**相容性原則**會定義裝置必須符合才能被條件式存取原則視為符合規範的規則與設定。 您也可以使用相容性原則，來監視和修復與條件式存取無關的裝置相容性問題。  


> [!IMPORTANT]  
>  本文說明 Microsoft Intune 所管理裝置的相容性原則。    如需 System Center Configuration Manager 所管理電腦的相容性原則，請參閱[管理 System Center Configuration Manager 所管理之電腦對 O365 服務的存取](../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md)。  

 這些規則包括需求，例如︰  

-   存取裝置用的 PIN 和密碼

-   裝置上儲存資料的加密

-   裝置為 jailbroken 或根目錄  

-   裝置上的電子郵件是否由 Intune 原則管理，或裝置是否被 Windows 裝置健康情況證明服務回報為狀況不良。
-   無法安裝在裝置上的應用程式。


 您可以將相容性原則部署到使用者集合。 將相容性原則部署到使用者時，即會檢查所有使用者裝置的相容性。  

 下表列出相容性原則支援的裝置類型，以及在將該原則與條件式存取原則搭配使用時如何管理不相容的設定。  

|規則|Windows 8.1 及更新版本|Windows Phone 8.1 和更新版本|iOS 6.0 和更新版本|Android 4.0 和更新版本、Samsung Knox Standard 4.0 和更新版本、Android for Work|  
|----------|---------------------------|---------------------------------|-----------------------|---------------------------|-----------------------------------------|  
|**PIN 碼或密碼設定**|已修復|已修復|已修復|已隔離|  
|**裝置加密**|N/A|已修復|已修復 (藉由設定 PIN 碼)|已隔離<br>(Android for Work 一律會加密)|  
|**已進行 JB 或 Root 破解的裝置**|N/A|N/A|隔離 (非設定)|隔離 (非設定)|  
|**電子郵件設定檔**|N/A|N/A|已隔離|N/A|  
|**最低 OS 版本**|已隔離|已隔離|已隔離|已隔離|  
|**最高 OS 版本**|已隔離|已隔離|已隔離|已隔離|  
|**裝置健康情況證明 (1602 更新)**|設定不適用於 Windows 8.1<br /><br /> 已隔離 Windows 10 和 Windows 10 行動裝置版。|N/A|N/A|N/A|  
|**無法安裝的應用程式**|N/A|N/A|已隔離|已隔離|

 **已修復** = 相容性由裝置作業系統執行 (例如強制使用者設定 PIN 碼)。  永遠不可能發生設定值不相容的情況。  

 **已隔離** = 裝置作業系統不會強制要求相容性 (例如，Android 裝置不會強制要求使用者加密裝置)。  在此情況下：  

-   如果使用者是條件式存取原則的目標，則將會封鎖該裝置。  

-   公司入口網站或 Web 入口網站將通知使用者任何相容性相關問題。  


### <a name="next-steps"></a>後續步驟  
[建立及部署裝置相容性原則](create-compliance-policy.md)
### <a name="see-also"></a>請參閱  
 [管理 System Center Configuration Manager 中的服務存取權](../../protect/deploy-use/manage-access-to-services.md)
