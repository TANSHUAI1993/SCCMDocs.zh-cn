---
title: "用戶端部署最佳做法 | Microsoft Docs"
description: "取得在 System Center Configuration Manager 中進行用戶端部署的最佳做法。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a933d69c-5feb-4b2b-84e8-56b3b64d5947
caps.latest.revision: "11"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 979c21c436429cad03a61671b707a99817146d95
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="best-practices-for-client-deployment-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中進行用戶端部署的最佳做法

*適用於：System Center Configuration Manager (最新分支)*


## <a name="use-software-update-based-client-installation-for-active-directory-computers"></a>針對 Active Directory 電腦使用以軟體更新為基礎的用戶端安裝  
 此用戶端部署方法使用現有 Windows 技術，並與 Active Directory 基礎結構整合，其在 Configuration Manager 中需要最低的設定，且為設定防火牆的最簡單且最安全性的方式。 針對群組原則設定使用安全性群組和 WMI 篩選之外，您還擁有許多彈性可控制哪些電腦安裝 Configuration Manager 用戶端。  

 如需詳細資訊，請參閱 [如何使用以軟體更新為基礎的安裝來安裝 Configuration Manager 用戶端](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientSUP)。  

## <a name="extend-the-active-directory-schema-and-publish-the-site-so-that-you-can-run-ccmsetup-without-command-line-options"></a>延伸 Active Directory 架構並發佈站台，使您不用命令列選項就可執行 CCMSetup。  
 當您擴充 Configuration Manager 的 Active Directory 架構並將站台發佈至 Active Directory 網域服務時，許多用戶端安裝內容也會發佈至 Active Directory 網域服務。 如果電腦可以找到這些用戶端安裝內容，就可在 Configuration Manager 用戶端部署期間使用。 由於這是自動產生的資訊，因此可以排除手動輸入安裝內容所可能出現的人為錯誤風險。  

 如需詳細資訊，請參閱[關於 System Center Configuration Manager 中發佈至 Active Directory 網域服務的用戶端安裝內容](../../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md)。  

## <a name="use-a-phased-rollout-to-manage-cpu-usage"></a>使用分階段導入管理 CPU 使用量  
 您可以使用用戶端分階段導入，將站台伺服器上的 CPU 處理需求效果降到最低。 在工作時間以外部署用戶端可讓其他服務有較多的可用頻寬，且當電腦執行速度變慢或需要重新啟動時，使用者也不會受到干擾。  

## <a name="enable-automatic-upgrade-after-your-main-client-deployment-has-finished"></a>在完成主要用戶端部署之後啟用自動升級  
 當您想要針對一小部分可能因為離線而被主要用戶端安裝方法遺漏的用戶端電腦進行升級時，[自動用戶端升級](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md)就非常有用。 

> [!NOTE]  
>  Configuration Manager 的效能提升可讓您使用自動升級作為主要的用戶端升級方法。 不過，實際效能將視階層基礎結構而定，例如用戶端的數目。  


## <a name="use-smsmp-and-fsp-if-you-install-the-client-with-clientmsi-properties"></a>如果您使用 client.msi 內容安裝用戶端，請使用 SMSMP 和 FSP  
 SMSMP 內容會指定要與用戶端通訊的初始管理點，並移除 Active Directory 網域服務、DNS 和 WINS 等服務位置解決方案上的相依性。  

 使用 FSP 內容並安裝後援狀態點，使您可以監控用戶端安裝和指派，並識別任何的通訊問題。  

 如需這些選項的詳細資訊，請參閱[關於 System Center Configuration Manager 中的用戶端安裝內容](../../../../core/clients/deploy/about-client-installation-properties.md)。  

## <a name="install-client-language-packs-before-you-install-the-clients"></a>在安裝用戶端之前安裝用戶端語言套件  
我們建議您先安裝用戶端語言套件，然後再部署用戶端。 如果您在安裝用戶端之後才在站台上安裝[用戶端語言套件](../../../../core/servers/deploy/install/language-packs.md) (以便啟用其他語言)，則必須重新安裝用戶端才能讓其使用那些語言。 對行動裝置用戶端來說，您必須在抹除行動裝置後再次進行註冊。  

## <a name="prepare-required-pki-certificates-in-advance"></a>事先準備必要的 PKI 憑證  
 若要在網際網路、已註冊的行動裝置和 Mac 電腦上管理裝置，您的站台系統 (管理點和發佈點) 和用戶端裝置上都必須有 PKI 憑證。 在生產網路中，您可能需要變更管理核准才能使用新的憑證、重新啟動站台系統伺服器，或者使用者可能必須登出後再登入以取得新的群組成員資格。 此外，您可能必須提供足夠的時間來複寫安全性權限，並提供任何新的憑證範本。  

 如需必要 PKI 憑證的詳細資訊，請參閱 [System Center Configuration Manager 的 PKI 憑證需求](../../../../core/plan-design/network/pki-certificate-requirements.md)。  

## <a name="before-you-install-clients-configure-any-required-client-settings-and-maintenance-windows"></a>在安裝用戶端之前，設定任何必要的用戶端設定和維護期間  
 雖然您可以在安裝用戶端之前或之後[設定用戶端設定](../../../../core/clients/deploy/configure-client-settings.md)和維護時段，仍建議您在安裝用戶端之前完成必要的設定，以便您在安裝用戶端後立即使用這些設定。 

 針對伺服器和 Windows Embedded 裝置設定維護時段，以確保重要裝置的商務持續性。 維護時段可確保必要的軟體更新和反惡意程式碼軟體不會在工作時間內重新啟動電腦。  

> [!IMPORTANT]  
>  對於您打算要透過統一寫入篩選器 (UWF) 保護的 Windows 10 電腦，您必須先針對 UWF 設定裝置，才能安裝用戶端。 這可讓 Configuration Manager 安裝具有自訂認證提供者的用戶端，以鎖定低權限使用者，防止他們在維護模式期間登入裝置。  

## <a name="plan-your-user-enrollment-experience-for-mac-computers-and-mobile-devices"></a>規劃 Mac 電腦和行動裝置的使用者註冊體驗   
 如果使用者將使用 Configuration Manager 來註冊他們自己的 Mac 電腦和行動裝置，請規劃使用者體驗。 例如，您可以使用網頁來編寫安裝和註冊程序，讓使用者只需要輸入最少量的必要資訊，您也可以透過電子郵件傳送說明的連結。  

## <a name="use-file-based-write-filters-for-windows-embedded-devices"></a>針對 Windows Embedded 裝置使用以檔案為基礎的寫入篩選器 
 使用增強式寫入篩選器 (EWF) 的 Embedded 裝置可能會發生狀態訊息重新同步處理。 如果您只有少數的 Embedded 裝置會使用增強式寫入篩選器，您可能不會注意到此現象。 不過，如果您有許多 Embedded 裝置會重新同步處理其資訊 (例如傳送完整清查而非差異清查)，則會在站台伺服器上產生可觀的網路封包以及大量的 CPU 處理。  

 如果您可以選擇要啟用的寫入篩選器類型，請選擇檔案型寫入篩選器，並設定例外狀況以保存裝置重新啟動期間的用戶端狀態和清查資料，確保 Configuration Manager 用戶端上的網路和 CPU 效率。 如需寫入篩選器的詳細資訊，請參閱   [規劃將用戶端部署至 System Center Configuration Manager 中的Windows Embedded 裝置](../../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md)。  

 如需主要站台可支援之 Windows Embedded 用戶端數量上限的詳細資訊，請參閱[支援的用戶端與裝置作業系統](../../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)。  
