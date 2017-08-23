---
title: "安裝混合式 MDM | Microsoft Docs"
description: "使用 Configuration Manager 和 Intune 設定混合式裝置註冊。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
caps.latest.revision: "34"
caps.handback.revision: "0"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: c494fcc38955571c06507278a1ae88e5777b5708
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="setup-hybrid-mobile-device-management-mdm-with-system-center-configuration-manager-and-microsoft-intune"></a>使用 System Center Configuration Manager 和 Microsoft Intune 設定混合式行動裝置管理 (MDM)

*適用於：System Center Configuration Manager (最新分支)*


必須先向 Intune 註冊 iOS、Windows 和 Android 裝置，才能使用 Configuration Manager 管理它們。 使用下列步驟，以搭配使用 Configuration Manager 與 Intune 來設定混合式裝置註冊。 完成下列步驟，即可啟用使用者的「自備裝置 (BYOD)」註冊。 這些步驟也是[註冊 BYOD 裝置](enroll-hybrid-ios-mac.md)及[註冊公司所擁有的裝置](enroll-company-owned-devices.md)的必要條件。

 |步驟|詳細資料|  
 |-----------|-------------|  
 |**步驟 1：**[建立 MDM 集合](create-mdm-collection.md)|建立可註冊其裝置之使用者的 Configuration Manager 使用者集合|  
 |**步驟 2：**[網域名稱需求](confirm-dns.md)|確認您組織的網域名稱服務 (DNS) 和 Active Directory 使用者管理符合 MDM 需求|
 |**步驟 3：**[設定 Intune 訂閱](configure-intune-subscription.md)|Intune 服務可讓您透過網際網路管理裝置。|  
 |**步驟 4：**[新增條款和條件](terms-and-conditions.md)| 建立使用者必須在使用公司入口網站應用程式之前接受的條款和條件|
 |**步驟 5：**[建立服務連接點](create-service-connection-point.md)|服務連接點會將設定和軟體部署資訊傳送至 Configuration Manager，並從行動裝置擷取狀態和清查訊息。 |  
 |**步驟 6：**[啟用平台註冊](enable-platform-enrollment.md)|適用於 iOS 和 Windows 裝置的 MDM 註冊需要額外的步驟，才能進行服務與裝置之間的通訊。 Android 不需要額外進行設定。|  
 |**步驟 7：**[設定額外的管理](set-up-additional-management.md)|(選擇性) 設定已註冊裝置的設定項目和條件式存取|
 |**步驟 8：**[確認 MDM 設定](verify-mdm-configuration.md)|檢視記錄檔，確認已成功建立服務連接點，而且使用者帳戶正在進行同步處理。|

在不使用 Configuration Manager 的情況下尋找 Intune？
> [!div class="button"]
[檢視 Intune 文件 >](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune)


## <a name="enroll-devices"></a>註冊裝置
完成混合式設定之後，有數種方式可以在 Configuration Manager 中註冊裝置︰
- **公司擁有的裝置 (COD)：**[註冊公司擁有的裝置](enroll-company-owned-devices.md)提供註冊公司所擁有裝置之不同平台特有方式的指引。
- **使用者擁有的 (BYOD) 裝置：**[註冊使用者擁有的 (BYOD) 裝置](enroll-hybrid-ios-mac.md)提供註冊使用者擁有之裝置的指引。
