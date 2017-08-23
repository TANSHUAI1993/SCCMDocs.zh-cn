---
title: "註冊公司擁有的裝置 - Configuration Manager | Microsoft Docs"
description: "了解使用 Configuration Manager 註冊公司擁有的裝置以進行混合式部署的不同方法。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e2754ce6-1460-4ddd-9050-2cc87e7964f4
caps.latest.revision: "13"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: f0b503d8c9eba2dd1b6eb4c41ec40c001b727326
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="enroll-company-owned-devices-for-hybrid-deployments-with-configuration-manager"></a>使用 Configuration Manager 註冊公司擁有的裝置以進行混合式部署

*適用於：System Center Configuration Manager (最新分支)*

組織或公司擁有的裝置 (CYOD) 可以用各種不同的方式納入管理，視裝置與購買方式而定。  

## <a name="enroll-device-enrollment-program-ios-devices"></a>註冊裝置註冊方案 iOS 裝置  
 透過「雲端」將註冊設定檔部署至透過 Apple「裝置登記方案」購買的裝置。 當使用者在裝置上執行安裝程式小幫手時，便會在 Intune 中註冊該裝置。  透過 DEP 註冊的裝置不能由使用者取消註冊。 請參閱[使用 Configuration Manager 進行混合式部署的 iOS 裝置登記方案 (DEP) 註冊](../../mdm/deploy-use/ios-device-enrollment-program-for-hybrid.md)。  

## <a name="enroll-ios-devices-with-apple-configurator"></a>使用 Apple Configurator 註冊 iOS 裝置  
 此方法需要系統管理員以 USB 將 iOS 裝置連接到執行 Apple Configurator 的 Mac 電腦以預先設定註冊。 裝置接著會傳遞給執行「設定輔助程式」程序的使用者，以他們的工作或學校認證來設定裝置並完成註冊程序。 請參閱[使用 Apple Configurator 搭配 Configuration Manager 進行 iOS 混合式註冊](../../mdm/deploy-use/ios-hybrid-enrollment-using-apple-configurator.md)。  

## <a name="device-enrollment-manager"></a>裝置註冊管理員  
 組織可以搭配使用 Intune 與單一使用者帳戶 (稱為裝置註冊管理員帳戶) 來管理大量的行動裝置。 建立裝置註冊管理員帳戶後，管理員可以使用該帳戶註冊比一般使用者預設允許的標準五部裝置更多的裝置。 使用裝置註冊管理員註冊裝置，只適用於不是由特定使用者使用的裝置。 例如，這些裝置適合銷售點或公用程式應用程式，但不適合需要存取電子郵件或公司資源的使用者。 請參閱[使用裝置註冊管理員與 Configuration Manager 註冊](../../mdm/deploy-use/enroll-devices-with-device-enrollment-manager.md)。  

## <a name="user-affinity-for-managed-devices"></a>受管理裝置的使用者親和性  
 當設定屬公司擁有之裝置的設定檔時，系統管理員可以指定受管理的裝置是否支援「使用者親和性」，這會識別特定使用者與裝置。 已設定 [使用者親和性] 的裝置可以安裝並執行 [公司入口網站] 應用程式，以下載 App 及管理裝置。 請參閱 [Configuration Manager 中針對混合式受管理裝置的使用者親和性](../../mdm/deploy-use/user-affinity-for-hybrid-managed-devices.md)。  

## <a name="manage-devices-with-activation-lock"></a>使用啟用鎖定管理裝置  
 Microsoft Intune 可以協助您管理 iOS 啟用鎖定，這是 iOS 7.1 和更新版本裝置之「尋找我的 iPhone」應用程式中的一項功能。 當裝置上使用「尋找我的 iPhone」應用程式時，啟用鎖定會自動啟用。 請參閱[使用 System Center Configuration Manager 管理 iOS 啟用鎖定](../../mdm/deploy-use/manage-ios-activation-lock.md)。

 ## <a name="predeclare-devices-with-imei-or-ios-serial-numbers"></a>使用 IMEI 或 iOS 序號預先宣告裝置

您可以透過匯入國際站移動設備識別碼 (IMEI) 號碼或 iOS 序號，識別公司擁有的裝置。 您可以上傳一個包含裝置 IMEI 編號的逗號分隔值 (.csv) 檔案，也可以手動輸入裝置資訊。  請參閱[使用硬體識別碼與預先宣告裝置](../../mdm/deploy-use/predeclare-devices-with-hardware-id.md)。
