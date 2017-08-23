---
title: "軟體更新的安全性和隱私權 | Microsoft Docs"
description: "遵循軟體更新安全性的這些最佳作法，並深入了解 Configuration Manager 如何處理隱私權資訊。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: 41d6d5d8-ba84-4efb-b105-4d1eed239824
ms.openlocfilehash: 4b4f045138abc14b6e93b3b990c5f3a8b4f2f952
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="security-and-privacy-for-software-updates-in-system-center-configuration-manager"></a>System Center Configuration Manager 中軟體更新的安全性和隱私權

*適用對象：System Center Configuration Manager (最新分支)*

本主題包含 System Center Configuration Manager 的軟體更新安全性和隱私權資訊。  

##  <a name="BKMK_Security_HardwareInventory"></a> 軟體更新的安全性最佳做法  
 為用戶端部署軟體更新時，請參閱下列安全性最佳作法：  

-   請勿變更軟體更新套件的預設權限。  

     軟體更新套件預設為允許系統管理員進行 [完全控制]  ，使用者則擁有 [讀取]  權限。 如果變更這些權限，攻擊者就有可能趁機新增、移除或刪除軟體更新。  

-   控制軟體更新下載位置的存取權限。  

     SMS 提供者、站台伺服器及實際將軟體更新下載至下載位置的系統管理使用者必須具備下載位置的 [寫入]  存取權限。 限制下載位置存取權限可以降低攻擊者在下載位置竄改軟體更新來源檔案的風險。  

     此外，如果以 UNC 共用區作為下載位置，請使用 IPsec 或 SMB 簽署功能保護網路通道，防止攻擊者趁機在透過網路傳送軟體更新來源檔案時進行竄改。  

-   使用 UTC 評估部署時間。  

     如果您使用本機時間而非 UTC，使用者只要變更電腦的時區即可延後安裝軟體更新。  

-   請在 WSUS 啟用 SSL 並依照最佳作法進行，以保障 Windows Server Update Services (WSUS) 的安全性。  

     識別並依照與 Configuration Manager 一起使用之 WSUS 版本的最佳安全性作法。  

    > [!IMPORTANT]  
    >  如果設定軟體更新點以在 WSUS 伺服器上啟用 SSL 通訊，您必須在 WSUS 伺服器上設定 SSL 的虛擬根。  

-   啟用 CRL 檢查。  

     根據預設，在部署至電腦上之前，Configuration Manager 不會透過檢查憑證撤銷清單 (CRL) 的方式驗證軟體更新的簽章。 每次使用憑證時皆檢查，提供比使用已撤銷憑證更多的安全性，但同時也會造成連線延遲，以及對執行 CRL 檢查的電腦產生額外的處理需求。  

     如需有關啟用軟體更新 CRL 檢查方式的詳細資訊，請參閱[如何啟用軟體更新的 CRL 檢查](../get-started/manage-settings-for-software-updates.md#crl-checking-for-software-updates)。  

-   設定 WSUS 使用自訂網站。  

     在軟體更新點上安裝 WSUS 時，您可以選擇使用現有的 IIS 預設網站或建立自訂的 WSUS 網站。 為 WSUS 建立自訂網站可讓 IIS 在專用的虛擬網站上裝載 WSUS 服務，而不是共用與其他 Configuration Manager 站台系統或其他應用程式使用的相同網站。  

     如需詳細資訊，請參閱[將 WSUS 設定為使用自訂網站](plan-for-software-updates.md#BKMK_CustomWebSite)。  

##  <a name="BKMK_Privacy_HardwareInventory"></a> 軟體更新的隱私權資訊  
 軟體更新會掃描用戶端電腦以判定所需的軟體更新，再將資訊傳回站台資料庫。 軟體更新期間，Configuration Manager 可能會在用戶端和伺服器之間傳送可識別電腦與登入帳戶的資訊。  

 Configuration Manager 會保存軟體部署程序的相關資訊。 傳送或儲存時均不會加密狀態資訊。 狀態資訊儲存在 Configuration Manager 資料庫中，由資料庫維護工作進行刪除。 所有狀態資訊皆不會傳送給 Microsoft。  

 使用 Configuration Manager 軟體更新在用戶端電腦上安裝軟體更新時，必須遵守這些更新的軟體授權條款，這些條款不同於 System Center Configuration Manager 的軟體授權條款。 請務必先詳閱並同意軟體授權條款，再使用 Configuration Manager 安裝軟體更新。  

 Configuration Manager 預設不會實作軟體更新，而且在收集資訊之前必須執行數個設定步驟。  

 設定軟體更新之前，請考慮您的隱私權需求。  
