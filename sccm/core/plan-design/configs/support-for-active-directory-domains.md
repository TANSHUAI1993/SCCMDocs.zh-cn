---
title: "支援的 Active Directory 網域 | Microsoft Docs"
description: "取得 Active Directory 網域中的 System Center Configuration Manager 站台系統成員資格需求。"
ms.custom: na
ms.date: 3/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8c5a13f8-42d5-4898-b7b6-e594dae8b335
caps.latest.revision: "7"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 2654ab4eaaaf6a4bf3bd7dca9908e7033647dc2c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="supported-active-directory-domains-for-system-center-configuration-manager"></a>System Center Configuration Manager 支援的 Active Directory 網域

*適用於：System Center Configuration Manager (最新分支)*

所有 System Center Configuration Manager 站台系統皆必須是支援的 Windows Server Active Directory 網域成員。 Configuration Manager 用戶端電腦可以是網域成員或工作群組成員。  

 **需求和限制：**  

-   網域成員資格適用於支援周邊網路 (也稱為 DMZ、非軍事區域和遮蔽式子網路) 中，使用以網際網路為基礎之用戶端管理的站台系統。  

-   您無法為裝載站台系統角色的電腦變更下列項目：  

    -   網域成員資格  

    -   網域名稱  

    -   電腦名稱  

您必須先解除安裝站台系統角色 (若為站台伺服器，還包括站台)，才能執行這些變更。  

**支援具有下列網域功能等級的網域：**  
- Windows Server 2016

- Windows Server 2012 R2  

- Windows Server 2012

- Windows Server 2008 R2

- Windows Server 2008  







##  <a name="bkmk_Disjoint"></a> 脫離的命名空間  
Configuration Manager 可以在具有脫離之命名空間的網域中安裝站台系統和用戶端。  

脫離的命名空間是指電腦的主要網域名稱系統 (DNS) 尾碼不符合該電腦所在 Active Directory DNS 網域名稱的情況。 使用不相符的主要 DNS 尾碼的電腦即稱為脫離。 另一個脫離的命名空間案例則發生於網域控制站的 NetBIOS 網域名稱不符合 Active Directory DNS 網域名稱時。  

下表識別脫離的命名空間的支援案例。  

|案例|詳細資訊|  
|--------------|----------------------|  
|**案例 1：**<br /><br /> 網域控制站的主要 DNS 尾碼與 Active Directory DNS 網域名稱不同。 身為網域成員的電腦不一定會脫離。|在此案例中，網域控制站的主要 DNS 尾碼與 Active Directory DNS 網域名稱不同。 網域控制站在此案例中是脫離的。 身為網域成員的電腦，例如站台伺服器和電腦，主要 DNS 尾碼可以符合網域控制站主要 DNS 尾碼或符合 Active Directory DNS 網域名稱。|  
|**案例 2：**<br /><br /> Active Directory 網域成員電腦是脫離的，但網域控制站不脫離。|在此案例中，站台系統安裝所在的成員電腦的主要 DNS 尾碼不同於 Active Directory DNS 網域名稱，即使網域控制站的主要 DNS 尾碼與 Active Directory DNS 網域名稱相同。 在此案例中，您有未脫離的網域控制站，以及脫離的成員電腦。 執行 Configuration Manager 用戶端的成員電腦，主要 DNS 尾碼可以符合脫離的站台系統伺服器的主要 DNS 尾碼，或符合 Active Directory DNS 網域名稱。|  

 若要允許電腦存取脫離的網域控制站，您必須變更網域物件容器上的 **msDS-AllowedDNSSuffixes** Active Directory 屬性。 您必須將兩個 DNS 尾碼都新增給屬性。  

 此外，為了確定 DNS 尾碼搜尋清單包含組織內部署的所有 DNS 命名空間，您必須針對網域中脫離的每一部電腦設定搜尋清單。 請確定在命名空間清單中包含下列項目：網域控制站的主要 DNS 尾碼、DNS 網域名稱，以及 Configuration Manager 可能交互操作之其他伺服器的任何其他命名空間。 您可以使用群組原則管理主控台來設定 [網域名稱系統 (DNS) 尾碼搜尋]  清單。  

> [!IMPORTANT]  
>  當您在 Configuration Manager 中參考電腦時，請使用主要 DNS 尾碼來輸入電腦。 這個尾碼應該符合註冊為 Active Directory 網域中 **dnsHostName** 屬性的完整網域名稱，和與系統相關聯的服務主體名稱。  

##  <a name="bkmk_SLD"></a> 單一標籤網域  
 當符合下列準則時，Configuration Manager 支援單一標籤網域中的站台系統及用戶端：  

-   Active Directory 網域服務中的單一標籤網域，必須設定為具有有效的頂層網域的脫離 DNS 命名空間。  

     **例如：** Contoso 的單一標籤網域已設定為在 contoso.com 的 DNS 中具有脫離的命名空間。 因此，當您為 Contoso 網域中的電腦指定 Configuration Manager 中的 DNS 尾碼時，您會指定 "Contoso.com"，而不是 "Contoso"。  

-   系統內容中的站台伺服器之間的分散式元件物件模型 (DCOM) 連線必須成功使用 Kerberos 驗證。  
