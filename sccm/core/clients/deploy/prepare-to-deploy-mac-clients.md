---
title: "準備將用戶端軟體部署到 Mac | Microsoft Docs"
description: "先完成設定工作，再將 Configuration Manager 用戶端部署至 Mac。"
ms.custom: na
ms.date: 05/04/2017
ms.prod: configuration-manager
ms.reviewer: aaroncz
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2285a953-6a86-4ed5-97dd-cd57b02bc1ee
caps.latest.revision: "12"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: b3bb72f81812705b4654e268025074402e89a7cb
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="prepare-to-deploy-client-software-to-macs"></a>準備將用戶端軟體部署到 Mac

*適用於：System Center Configuration Manager (最新分支)*

請遵循這些步驟以確保您準備好[將 Configuration Manager 用戶端部署至 Mac 電腦](/sccm/core/clients/deploy/deploy-clients-to-macs)。 

## <a name="mac-prerequisites"></a>Mac 必要條件

Configuration Manager 媒體不提供 Mac 用戶端安裝套件。 從 [Microsoft 下載中心](http://go.microsoft.com/fwlink/?LinkID=525184)下載**其他作業系統的用戶端**。  

**支援的版本：**  

-   **Mac OS X 10.6** (Snow Leopard) 

-   **Mac OS X 10.7** (Lion) 

-   **Mac OS X 10.8** (Mountain Lion)

-   **Mac OS X 10.9** (Mavericks)

-   **Mac OS X 10.9** (Mavericks)  

-   **Mac OS X 10.10** (Yosemite)  

-   **Mac OS X 10.11** (El Capitan)  

-   **Mac OS X 10.12** (macOS Sierra )  

## <a name="certificate-requirements"></a>憑證需求
Mac 電腦的用戶端安裝和管理需要公開金鑰基礎結構 (PKI) 憑證。 PKI 憑證會使用相互驗證及加密的資料傳送，對 Mac 電腦和 Configuration Manager 站台之間的通訊進行加密。 Configuration Manager 可以使用含有企業憑證授權單位 (CA) 的 Microsoft 憑證服務和 Configuration Manager 註冊點，以及註冊 Proxy 點站台系統角色來要求並安裝使用者用戶端憑證。 或者，如果憑證符合 Configuration Manager 的需求，您可以單獨從 Configuration Manager 要求及安裝電腦憑證。   
  
Configuration Manager Mac 用戶端一律執行憑證撤銷檢查。 您無法停用此功能。  
  
如果 Mac 用戶端因為找不到 CRL 而無法確認伺服器憑證的憑證撤銷狀態，它們將無法順利連線至 Configuration Manager 站台系統。 特別是在不同樹系中用於發行憑證授權單位的 Mac 用戶端，請檢查您的 CRL 設計以確定 Mac 用戶端可以找到並連線到 CRL 發佈點 (CDP) 以確保網站系統伺服器的連線。  

您必須先決定要如何安裝用戶端憑證，才能在 Mac 電腦上安裝 Configuration Manager 用戶端：  

-   利用 [CMEnroll 工具](/sccm/core/clients/deploy/deploy-clients-to-macs#install-the-client-and-then-enroll-the-client-certificate-on-the-mac)使用 Configuration Manager 註冊。 註冊程序不支援自動憑證更新，所以您必須在安裝的憑證到期前，先重新註冊 Mac 電腦。  

-   [使用與 Configuration Manager 無關的憑證要求和安裝方法](/sccm/core/clients/deploy/deploy-clients-to-macs#use-a-certificate-request-and-installation-method-that-is-independent-from-configuration-manager)。  

如需 Mac 用戶端憑證需求及其他支援 Mac 電腦所需 PKI 憑證的詳細資訊，請參閱 [System Center Configuration Manager 的 PKI 憑證需求](../../../core/plan-design/network/pki-certificate-requirements.md)。  

Mac 用戶端會自動指派給管理它們的 Configuration Manager 站台。 即使通訊受限於內部網路，Mac 用戶端還是會安裝為僅限網際網路的用戶端。 此用戶端設定表示當您將這些網站系統角色設定為允許來自網際網路的用戶端連線時，它們將會與其指派的網站內的網站系統角色 (管理點和發佈點) 通訊。 Mac 電腦不會與其指派的網站以外的網站系統角色通訊。  

> [!IMPORTANT]  
>  Configuration Manager Mac 用戶端無法用於連線到設定為使用[資料庫複本](../../../core/servers/deploy/configure/database-replicas-for-management-points.md)的管理點。  


## <a name="deploy-a-web-server-certificate-to-site-system-servers"></a>將 Web 伺服器憑證部署至站台系統伺服器  
如果這些站台系統沒有 Web 伺服器憑證，請將此種憑證部署至具有這些站台系統角色的電腦︰  

-   管理點  

-   發佈點  

-   註冊點  

-   註冊 Proxy 點  

Web 伺服器憑證必須包含網站系統內容中指定的網際網路 FQDN。 伺服器不必從網際網路存取也能支援 Mac 電腦。 如果您不需要以網際網路為基礎的用戶端管理，您可以將網際網路 FQDN 指定為內部網路 FQDN 值。  

請在管理點、發佈點和註冊 Proxy 點的 Web 伺服器憑證中，指定站台系統的網際網路 FQDN 值。 

如需建立及安裝此 Web 伺服器憑證的部署範例，請參閱[為執行 IIS 的站台系統部署 Web 伺服器憑證](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012)。  


## <a name="deploy-a-client-authentication-certificate-to-site-system-servers"></a>將用戶端驗證憑證部署至站台系統伺服器  
 如果這些站台系統沒有用戶端驗證憑證，請將此種憑證部署至裝載這些站台系統角色的電腦：  

-   管理點  

-   發佈點  

 如需建立及安裝管理點用戶端憑證的部署範例，請參閱[部署 Windows 電腦的用戶端憑證](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012)。  

 如需建立及安裝管理點用戶端憑證的部署範例，請參閱[部署發佈點的用戶端憑證](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012)。  

>[!IMPORTANT]
>  若要將用戶端部署到執行 macOS Sierra 的裝置上，必須正確設定管理點憑證的「主體名稱」，例如，使用管理點伺服器的 FQDN。

## <a name="prepare-the-client-certificate-template-for-macs"></a>準備 Mac 的用戶端憑證範本  

 憑證範本必須擁有將在 Mac 電腦上註冊憑證之使用者帳戶的 [讀取]  和 [註冊]  權限。  

 請參閱[部署 Mac 電腦的用戶端憑證](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_MacClient_SP1)。  

## <a name="configure-the-management-point-and-distribution-point"></a>設定管理點和發佈點  
 為管理點設定下列選項：  

-   HTTPS  

-   允許用戶端從網際網路連線。 此設定值是管理 Mac 電腦所必備。 然而，這並不代表網站系統伺服器必須能夠從網際網路存取。  

-   允許行動裝置和 Mac 電腦使用此管理點  

 雖然安裝用戶端不需要用到發佈點，但是如果要在安裝用戶端後將軟體部署到這些電腦，您必須設定發佈點，以允許用戶端從網際網路連線。  

 
### <a name="to-configure-management-points-and-distribution-points-to-support-macs"></a>設定管理點及發佈點以支援 Mac  

請確定已使用網際網路 FQDN 設定執行管理點和發佈點的網站系統伺服器，再開始執行此程序。 如果這些伺服器不支援以網際網路為基礎的用戶端管理，您可以將內部網路 FQDN 指定為網際網路 FQDN 值。 

這些站台系統角色必須位於主要站台中。  


1.  在 Configuration Manager 主控台中，選擇 [系統管理] > [站台設定] > [伺服器和站台系統角色]，然後選擇有正確站台系統角色的伺服器。  

3.  在詳細資料窗格中，以滑鼠右鍵按一下 [管理點]，選擇 [角色內容]，然後在 [管理點內容] 對話方塊中設定這些選項：  

    1.  選擇 [HTTPS]。  

    2.  選擇 [僅允許網際網路用戶端連線] 或 [允許內部網路和網際網路用戶端連線]。 這些選項需要網際網路或內部網路 FQDN。  

    3.  選擇 [允許行動裝置和 Mac 電腦使用此管理點]。  

4.  在詳細資料窗格中，以滑鼠右鍵按一下 [發佈點]，選擇 [角色內容]，然後在 [發佈點內容] 對話方塊中設定這些選項：  

    -   選擇 [HTTPS]。  

    -   選擇 [僅允許網際網路用戶端連線] 或 [允許內部網路和網際網路用戶端連線]。 這些選項需要網際網路或內部網路 FQDN。  

    -   選擇 [匯入憑證]，瀏覽至匯出的用戶端發佈點憑證檔案，然後指定密碼。  

5.  針對主要站台中您要搭配 Mac 使用的所有管理點和發佈點，重複步驟 2 到 4。  

## <a name="configure-the-enrollment-proxy-point-and-the-enrollment-point"></a>設定註冊 Proxy 點和註冊點  
 您必須在相同網站中安裝這兩種網站系統角色，但不需要在相同網站系統伺服器或相同 Active Directory 樹系中安裝它們。  

 如需站台系統角色放置和考量的詳細資訊，請參閱[為 System Center Configuration Manager 規劃站台系統伺服器和站台系統角色](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md)中的[站台系統角色](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md#bkmk_planroles)。  

 這些程序會設定網站系統角色以支援 Mac 電腦。   

-   [新的網站系統伺服器](#new-site-system-server)  

-   [現有的站台系統伺服器](#existing-site-system-server)  

###  <a name="new-site-system-server"></a>新增網站系統伺服器  

1.  在 Configuration Manager 主控台中，選擇 [系統管理] >  [站台設定] > [伺服器和站台系統角色]。  

3.  在 [首頁] 索引標籤的 [建立] 群組中，選擇 [建立站台系統伺服器]。  

4.  在 [一般] 頁面上，指定站台系統的一般設定。  請確定指定網際網路 FQDN 的值。 如果不會從網際網路存取伺服器，請使用內部網路 FQDN。  

5.  在 [系統角色選取] 頁面上，從可用角色的清單中選取 [註冊 Proxy 點] 和 [註冊點]。  

6.  在 [註冊 Proxy 點] 頁面上檢閱設定值，並進行必要的變更。  

7.  在 [指定註冊點設定] 頁面上檢閱設定值，並進行必要的變更。 然後完成精靈。  

### <a name="existing-site-system-server"></a>現有的網站系統伺服器  

1.  在 Configuration Manager 主控台中，選擇 [系統管理] >  [站台設定] > [伺服器和站台系統角色]，然後選擇您要用來支援 Mac 的伺服器。  

3.  在 [首頁] 索引標籤的 [建立] 群組中，選擇 [新增站台系統角色]。  

4.  在 [一般]  頁面上，指定網站系統的一般設定，然後按 [下一步] 。 請確定指定網際網路 FQDN 的值。 如果不會從網際網路存取伺服器，請使用內部網路 FQDN。   

5.  在 [系統角色選取] 頁面上，從可用角色的清單中選擇 [註冊 Proxy 點] 和 [註冊點]。  

6.  在 [註冊 Proxy 點] 頁面上檢閱設定值，並進行必要的變更。  

7.  在 [指定註冊點設定] 頁面上檢閱設定值，並進行必要的變更。 然後完成精靈。  

## <a name="install-the-reporting-services-point"></a>安裝 Reporting Services 點  
 若要執行 Mac 的報告，請[安裝 Reporting Services 點](../../../core/servers/manage/configuring-reporting.md)。  

### <a name="next-steps"></a>後續步驟

[將 Configuration Manager 用戶端部署至 Mac 電腦](/sccm/core/clients/deploy/deploy-clients-to-macs)。  