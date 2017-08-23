---
title: "選擇裝置管理解決方案 - Configuration Manager | Microsoft Docs"
description: "了解 System Center Configuration Manager 為管理電腦、伺服器和裝置所提供的解決方案。"
ms.custom: na
ms.date: 12/08/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 24633725-791a-4df7-8dce-2c24c1a19a03
caps.latest.revision: "14"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 9989ea1bf4cb74a6286ebae9de7614ed622de5b6
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="choose-a-device-management-solution-for-system-center-configuration-manager"></a>選擇 System Center Configuration Manager 的裝置管理解決方案

*適用於：System Center Configuration Manager (最新分支)*

System Center Configuration Manager (也稱為 ConfgMgr 或 SCCM) 提供不同的解決方案來管理電腦、伺服器和裝置。 您可以根據您需要管理的裝置平台以及您需要的管理功能，來選擇最適合的解決方案。  


##  <a name="overview-of-device-management-solutions"></a>裝置管理解決方案概觀  
 本文涵蓋四種裝置管理解決方案︰Configuration Manager 用戶端應用程式、內部部署 Configuration Manager 基礎結構、Microsoft Intune 以及 Exchange。 本文以兩份比較管理解決方案的表格作結，一份以[支援的行動裝置平台](#compare-device-management-solutions-based-on-supported-mobile-device-platforms)為基礎，另一份以[管理功能](#compare-mobile-device-management-solutions-based-on-management-functionality)為基礎。


###  <a name="manage-devices-with-the-configuration-manager-client"></a>使用 Configuration Manager 用戶端管理裝置  

這個選項 (需要在裝置上安裝 Configuration Manager 用戶端應用程式) 提供最多的功能來管理您環境中的電腦、伺服器和其他裝置。 如需詳細資訊，請參閱 [System Center Configuration Manager 中的用戶端安裝方法](/sccm/core/clients/deploy/plan/client-installation-methods)。  

###  <a name="manage-devices-with-on-premises-configuration-manager-infrastructure"></a>使用內部部署 Configuration Manager 基礎結構管理裝置  

這個選項使用部分裝置平台作業系統中內建的裝置管理功能。 雖然內部部署行動裝置管理不具有用戶端管理的完整功能，但使用內部部署 Configuration Manager 資源連接和管理裝置，能提供更輕的觸控方式來進行管理。 請注意，目前只有 Windows 10 電腦和 Windows 10 Mobile 裝置支援此選項。  

如需詳細資訊，請參閱[在 System Center Configuration Manager 中使用內部部署基礎結構管理行動裝置](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)。  

###  <a name="manage-devices-with-microsoft-intune-hybrid"></a>使用 Microsoft Intune (混合式) 管理裝置  

這個選項會使用 Microsoft Intune 來註冊及管理裝置，而不是使用 Configuration Manager 內部部署資源。 雖然是由 Intune 管理裝置，但是您會在 Configuration Manager 主控台中存取管理工作。 這個選項支援所有主要行動裝置作業系統 (包括 Windows 10 行動裝置版、Windows Phone、iOS、Mac OS X 和 Android)。 它也提供您組織中 Windows 8.1 和 Windows 10 電腦的管理。  

如需詳細資訊，請參閱[搭配 System Center Configuration Manager 和 Microsoft Intune 的混合式行動裝置管理 (MDM)](../../mdm/understand/hybrid-mobile-device-management.md)。  

###  <a name="manage-devices-with-microsoft-exchange"></a>使用 Microsoft Exchange 管理行動裝置  

此選項使用 Exchange Server 連接器將多部 Exchange 伺服器連接至 Configuration Manager。 如此可集中管理能夠連接到 Exchange ActiveSync 的裝置。 您可以從 Configuration Manager 主控台設定 Exchange 行動裝置管理功能，例如遠端裝置抹除，以及多部 Exchange Server 的設定控制。  

如需詳細資訊，請參閱[使用 System Center Configuration Manager 和 Exchange 管理行動裝置](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)。  

您可以單獨使用這些裝置管理解決方案或將它們搭配使用。 例如，您可以使用用戶端管理方式來管理您組織中的電腦和伺服器，也可以使用 Intune 來管理行動裝置。 透過這種方式來合併使用方式，您就可以從 Configuration Manager 主控台涵蓋所有的裝置管理需求。  

## <a name="compare-device-management-solutions-based-on-supported-mobile-device-platforms"></a>根據支援的行動裝置平台比較裝置管理解決方案  

|平台|使用 Configuration Manager 用戶端|Configuration Manager 與 Microsoft Intune (混合式)|內部部署行動裝置管理|使用 Exchange 的 Configuration Manager|  
|--------------|-------------------------------------------|-------------------------------------------------------------------|-------------------------------|-----------------------------------------|  
|Android||是||是|  
|iOS||是||是|  
|Mac OS X|是|||是|  
|UNIX/Linux|是|||是|  
|Windows 10|是|[是]|[是]|是|  
|Windows 10 Mobile||是|[是]|是|  
|Windows (舊版)|是|[是]||是|  
|Windows CE|是 (具有行動裝置舊版用戶端)|||是|  
|Windows Embedded|是||||  
|Windows Phone||是||是|  
|Windows Server|是|||是|  

 如需支援平台的完整清單，請參閱 [System Center Configuration Manager 用戶端和裝置支援的作業系統](configs\supported-operating-systems-for-clients-and-devices.md)。

##  <a name="bkmk_comp2"></a> 根據管理功能比較行動裝置管理解決方案  

|管理功能|使用 Configuration Manager 用戶端|Configuration Manager 與 Microsoft Intune (混合式)|內部部署行動裝置管理|使用 Exchange 的 Configuration Manager|  
|------------------------------|-------------------------------------------|-------------------------------------------------------------------|-------------------------------|-----------------------------------------|  
|行動裝置與 Configuration Manager 之間的公開金鑰基礎結構 (PKI) 安全性 (使用互相驗證和 SSL 加密資料傳輸)|是|[是]|是||  
|用戶端安裝|是||||  
|透過網際網路支援|是||||  
|探索|是|||是|  
|硬體清查|是|[是]|[是]|是|  
|軟體清查|是|||是|  
|設定|是|[是]|[是]|是|  
|軟體部署|是|[是]|是||  
|透過後援狀態點進行監視|是||||  
|管理點的連線|是||是||  
|發佈點的連線|是||是||  
|封鎖 Configuration Manager|是|[是]|是||  
|隔離和封鎖 Exchange Server (及 Configuration Manager)||||[是]|  
|遠端抹除| |是|[是]|是|  
