---
title: "用戶端管理之裝置的一般相容性管理工作 - Configuration Manager | Microsoft Docs"
description: "透過處理一些常見的案例，了解 System Center Configuration Manager 相容性設定需要。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4e345791-74db-41ad-b472-024ce6521daf
caps.latest.revision: "8"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 2012ab5e55da8d707fd668e0163b42fe7d56c72f
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="common-tasks-for-managing-compliance-on-devices-with-the-system-center-configuration-manager-client"></a>使用 System Center Configuration Manager 用戶端管理裝置上相容性的一般工作

*適用對象：System Center Configuration Manager (最新分支)*

本主題中的案例透過您可能遇到的一些常見案例，為您簡介使用 System Center Configuration Manager 的相容性設定。  

 如已熟悉相容性設定，您可在 [Configuration items for devices managed with the System Center Configuration Manager client](../../compliance/deploy-use/configuration-items-for-devices-managed-with-the-client.md) (由 System Center Configuration Manager 用戶端管理的裝置設定項目) 一節中找到所用全部功能的詳細文件。  

 開始之前，請參閱[開始使用相容性設定](../../compliance/get-started/get-started-with-compliance-settings.md)，了解相容性設定的一些基本概念，另請參閱[規劃及設定相容性設定](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)，實作任何必要條件。  

## <a name="general-information-for-each-scenario"></a>每個案例的通用資訊  
 在每個案例中，您會建立執行特定工作的設定項目。 請使用下列步驟開啟 [建立設定項目精靈]：  

1.  在 Configuration Manager 主控台中，按一下 [資產與相容性] > [相容性設定] > [設定項目]。  

3.  在 [常用]  索引標籤上，按一下 [建立]  群組中的 [建立設定項目] 。  

4.  在 [建立設定項目精靈] 的 [一般]  索引標籤上 (如下所示)，指定設定項目的名稱和描述，然後為本主題的每個案例選擇適當的設定項目類型。  

     ![顯示 [建立設定項目精靈] 的 [一般] 頁面。](/sccm/compliance/plan-design/media/Compliance-Settings-Wizard---1.png)  

## <a name="scenarios-for-windows-10-devices-managed-with-the-configuration-manager-client"></a>使用 Configuration Manager 用戶端管理的 Windows 10 裝置案例  

### <a name="scenario-disable-the-use-of-bluetooth-on-windows-10-devices"></a>案例：停止在 Windows 10 裝置上使用藍牙  
 在此案例中，安全性部門發現裝置上的藍牙功能可作為用來在公司外部傳送公司機密資訊的方式。 您最近將所有電腦都升級為 Windows 10，並且決定停用這些裝置上的藍牙功能。  

1.  在 [建立設定項目精靈] 的 [一般]  頁面上，選取 [Windows 10]  設定項目類型，然後按一下 [下一步] 。  

2.  在精靈的 [支援的平台]  頁面上，選取所有 Windows 10 平台。  

3.  在 [裝置設定]  頁面上，選取 [裝置] ，然後按一下 [下一步] 。  

4.  在 [裝置]  頁面上，選取 [禁止]  作為 [藍牙] 的值。  

5.  選取 [補救不相容的設定]  確保變更套用至所有 Windows 10 裝置。  

6.  完成精靈以建立設定項目。  

 您現在可以使用 [Common tasks for creating and deploying configuration baselines with System Center Configuration Manager](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) (以 System Center Configuration Manager 建立及部署設定基準的一般工作) 主題中的資訊，協助您將已建立的設定部署至裝置。  

## <a name="scenarios-for-windows-desktop-and-server-computers-managed-with-the-configuration-manager-client"></a>使用 Configuration Manager 用戶端所管理之 Windows 桌上型電腦和伺服器電腦的案例  
 在執行 Configuration Manager 用戶端的 Mac 電腦上 ，有兩個評估相容性選項：  

-   評估 Mac OS X 喜好設定 (plist) 檔案。  

-   使用自訂指令碼，並評估指令碼所傳回的結果。  

 如需詳細資訊，請參閱[如何為 System Center Configuration Manager 用戶端所管理的 Mac OS X 裝置建立設定項目](../../compliance/deploy-use/create-configuration-items-for-mac-os-x-devices-managed-with-the-client.md)。  

### <a name="scenario-remediate-an-incorrect-registry-value-on-windows-desktop-computers"></a>案例：補救 Windows 桌上型電腦上的不正確登錄值  
 在此案例中，您發現您所管理且執行 Windows 8.1 的某些電腦上未正確地執行重要的企業營運應用程式。 調查之後，您會發現這是因為某些電腦上名為 **HKEY_LOCAL_MACHINE\SOFTWARE\Woodgrove\LOB App\Configuration\Configuration1** 的登錄機碼值設為 [0]  。 若要讓企業營運應用程式成功執行，此值必須設為 [1] 。  

 在此程序中，您將建立監視並自動補救所找到之任何不正確登錄機碼值的設定項目。  

1.  在 [建立設定項目精靈] 的 [一般]  頁面上，選取 [Windows 桌面或伺服器 (自訂)]  設定項目類型，然後按一下 [下一步] 。  

2.  在精靈的 **支援的平台** 頁面上，選取 **「Windows 8.1」** (確保設定項目僅套用至受影響的電腦)。  

3.  在 [設定]  頁面上，按一下 [新增]  建立新的設定。  

4.  在 [建立設定]  對話方塊的 [一般]  索引標籤上，設定下列項目：  

    -   **名稱** > **設定範例**  

    -   **設定類型** > **登錄值**  

    -   **資料類型** > **整數** (因為值只包含數字)  

    -   **Hive** > **HKEY_LOCAL_MACHINE**  

    -   **機碼** > **SOFTWARE\Woodgrove\LOB App\Configuration\Configuration1**  

    -   **值** > **1** (必要值)  

5.  在 [建立設定]  對話方塊的 [相容性規則]  索引標籤上，按一下 [新增] ，然後在 [建立規則]  對話方塊中設定下列項目：  

    -   **名稱** > **範例規則**  

    -   **選取的設定** – 確認選取的設定為 [範例設定] 。  

    -   **規則類型** > **值**  

    -   **設定必須符合下列規則** – 確認設定名稱正確，並將選項設定為指定設定值必須等於 **1**。  

    -   **支援時補救不相容的規則** – 檢查此方塊，以確保 Configuration Manager 在值不正確時會重設正確的登錄機碼值。  

6.  完成精靈以建立設定項目。  

 您現在可以使用[建立及部署設定基準的一般工作](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md)主題中的資訊，協助您將已建立的設定部署至裝置。  
