---
title: "發行和 Active Directory 結構描述 | Microsoft Docs"
description: "為 System Center Configuration Manager 延伸 Active Directory 架構，簡化部署及設定用戶端的程序。"
ms.custom: na
ms.date: 2/6/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: bc15ee7e-4d0a-4463-ae2c-f72d8d45d65d
caps.latest.revision: "17"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 58beef440db8e019a06ce7c4c8eaabc8e85ce954
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="prepare-active-directory-for-site-publishing"></a>準備 Active Directory 以發行站台

*適用對象：System Center Configuration Manager (最新分支)*

當您為 System Center Configuration Manager 延伸 Active Directory 架構時，會為 Active Directory 納入新的結構，而 Configuration Manager 站台會使用這些新結構在用戶端可輕鬆存取的安全位置，發佈重要資訊。  

管理內部部署用戶端時，最好是使用 Configuration Manager 與延伸的 Active Directory 架構。 延伸的架構可簡化部署以及設定用戶端的程序。 延伸的架構也可讓用戶端能有效地尋找資源，像是內容伺服器以及不同 Configuration Manager 站台系統角色所提供的其他服務。  

-   如果您不熟悉為 Configuration Manager 部署提供了哪些延伸架構，可以閱讀 [System Center Configuration Manager 的架構延伸](../../../core/plan-design/network/schema-extensions.md)以協助您進行決策。  

-   當您不使用延伸架構時，可設定其他方法 (像是 DNS 與 WINS) 以找出服務與站台系統伺服器。 服務位置的這些方法，需要額外的組態，而且不是最理想的用戶端服務位置方法。 若要深入了解，請閱讀[Understand how clients find site resources and services for System Center Configuration Manager](../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md) (了解用戶端如何找到 System Center Configuration Manager 的站台資源與服務)。  

-   如果 Active Directory 架構已為 Configuration Manager 2007 或 System Center 2012 Configuration Manager 延伸，您不需要執行其他動作。 延伸架構不會變更，且已準備就緒。  

對於任何樹系而言，擴充架構都是單次的動作。 若要延伸，然後使用延伸的 Active Directory 架構，請遵循下列步驟進行︰  

## <a name="step-1-extend-the-schema"></a>步驟 1： 擴充架構  
延伸 Configuration Manager 的架構：  

-   使用屬於 Schema Admins 安全性群組成員的帳戶。  

-   登入架構主機網域控制站。  

-   執行 **Extadsch.exe** 工具，或使用 LDIFDE 命令列公用程式並附 **ConfigMgr_ad_schema.ldf** 檔案。 工具與檔案都位於 Configuration Manager 安裝媒體的 **SMSSETUP\BIN\X64** 資料夾中。  

#### <a name="option-a-use-extadschexe"></a>選項 A：使用 Extadsch.exe  

1.  執行 **extadsch.exe** ，將新的類別與屬性加入 Active Directory 架構。  

    > [!TIP]  
    >  從命令列執行此工具，於執行期間檢視意見反應。  

2.  檢閱系統磁碟機根目錄中的 extadsch.log，確認已成功延伸架構。  

#### <a name="option-b-use-the-ldif-file"></a>選項 B：使用 LDIF 檔案  

1.  編輯 **ConfigMgr_ad_schema.ldf** 檔案，以定義您延伸的 Active Directory 根網域：  

    -   具備要延伸的網域全名之檔案內，中所有出現文字 **DC = x** 之處，都加以取代。  

    -   例如，若要擴充的網域全名為 widgets.microsoft.com，請將檔案中所有出現的 [DC=x]，都變更為 **DC=widgets, DC=microsoft, DC=com**。  

2.  使用 LDIFDE 命令列公用程式，將 **ConfigMgr_ad_schema.ldf** 檔案的內容匯入 Active Directory Domain Services：  

    -   例如，以下命令列會將延伸架構匯入 Active Directory Domain Services，並開啟詳細資訊記錄，然後於匯入期間建立記錄檔：**ldifde -i -f ConfigMgr_ad_schema.ldf -v -j &lt;位置，以儲存記錄檔\>**。  

3.  利用檢閱上一步驟中所用命令列所建立之記錄檔的方式，驗證延伸架構已成功。  

## <a name="step-2--create-the-system-management-container-and-grant-sites-permissions-to-the-container"></a>步驟 2：  建立「系統管理」容器，並為容器授與站台的權限  
 延伸架構之後，必須在 Active Directory Domain Services (AD DS) 中建立一個名為 **System Management** 的容器︰  

-   在具有會將資料發佈至 Active Directory 的主要或次要站台的每個網域中，都要建立一次此容器。  

-   您要為每個容器將權限授與每部主要和次要站台伺服器的電腦帳戶，這些伺服器會將資料發佈至該網域。 每個帳戶都需要有容器的**完全控制**權限，以及相當於 [此物件及所有子系物件] 之 [套用在] 的進階權限。  

#### <a name="to-add-the-container"></a>若要新增容器  

1.  所用帳戶應具有 Active Directory 網域服務之 **System** 容器的 **[建立所有子物件]** 權限。  

2.  執行 **ADSI 編輯器** (adsiedit.msc)，並連接至站台伺服器的網域。  

3.  建立容器：  

    -   依序展開 [網域]、[電腦完整網域名稱]&lt;\>、[辨別名稱]&lt;\>，在 [CN=System] 上按一下滑鼠右鍵，選擇 [新增]，然後選擇 [物件]。  

    -   在 [建立物件] 對話方塊中，選擇 [容器]，然後選擇 [下一步]。  

    -   在 [值] 方塊中輸入 **System Management**，然後選擇 [下一步]。  

4.  指派權限：  

    > [!NOTE]  
    >  您可視需要使用像是 Active Directory 使用者與電腦系統管理工具 (dsa.msc) 等其他工具，為容器加入權限。  

    -   在 [CN=System Management] 上按一下滑鼠右鍵，然後選擇 [內容]。  

    -   選取 [安全性] 索引標籤，選擇 [新增]，然後以**完全控制**權限新增站台伺服器電腦帳戶。  

    -   選擇 [進階]，並選取站台伺服器的電腦帳戶，然後選擇 [編輯]。  

    -   在 [套用到] 清單中，選取 [此物件及所有子系物件]。  

5.  按一下 [確定]，關閉對話方塊並儲存設定。  

## <a name="step-3-set-up-sites-to-publish-to-active-directory-domain-services"></a>步驟 3： 將站台設定為發佈至 Active Directory Domain Services  
 設定此容器並授與權限，且已安裝 Configuration Manager 主要站台之後，即可將該站台設定為將資料發佈至 Active Directory。  

 如需發佈的詳細資訊，請參閱[發佈 System Center Configuration Manager 的站台資料](../../../core/servers/deploy/configure/publish-site-data.md)。  
