---
title: "確定裝置合規性 | Microsoft Docs"
description: "使用 System Center Configuration Manager 管理組織中的裝置設定和合規性。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7568c9aa-b99e-4466-bfc8-0301aa376930
caps.latest.revision: "8"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: f7ecfe550d2e28579ea873442b2a68dc1c7c5483
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="ensure-device-compliance-with-system-center-configuration-manager"></a>Ensure device compliance with System Center Configuration Manager (確定裝置與 System Center Configuration Manager 的相容性)

*適用於：System Center Configuration Manager (最新分支)*

System Center Configuration Manager 中的合規性設定可提供管理組織中裝置設定和合規性所需的工具和資源。 這可協助您支援下列商務需求：  

-   根據您建立或取自其他廠商的最佳做法組態，比較您所管理之 Windows 電腦、Mac 電腦、伺服器和行動裝置的組態  

-   識別未經授權的裝置組態  

-   報告與法規原則和內部安全性原則的相容性  

-   識別安全性弱點  

-   將透過識別不相容組態來偵測所報告事件和問題的可能原因資訊，提供給技術支援中心  

-   自動修復行動裝置上的部分不相容設定  

-   將應用程式、套件和程式或指令碼部署至會自動填入報告為不符合規範之裝置的集合，來補救不合規性  


## <a name="get-started"></a>開始使用  
 了解相容性設定的基本概念，以及使用這些設定所能完成的工作。  

 [開始使用合規性設定](../../compliance/get-started/get-started-with-compliance-settings.md)  

## <a name="plan-and-design"></a>規劃和設計  
 請先確定您已實作了本主題中的所需必要條件，再開始使用相容性設定。  

 [規劃和設定合規性設定](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)  

## <a name="common-tasks"></a>一般工作  
 在本節中，您會發現一些常見案例，可協助您了解如何使用 Configuration Manager 中的合規性設定。  

 [管理合規性的一般工作](../../compliance/plan-design/common-tasks-for-managing-compliance.md)  

## <a name="remote-connection-profiles"></a>遠端連線設定檔  
 當您的使用者未連線至網域，或者他們是透過網際網路連接其個人電腦時，此設定項目類型可讓您設定使用者的電腦，使其可從遠端連線至工作電腦。  

 [建立遠端連線設定檔](/sccm/compliance/deploy-use/create-remote-connection-profiles)  

## <a name="user-data-and-profiles"></a>使用者資料和設定檔  
 設定項目類型包含了某些設定，這些設定可為階層中的使用者管理執行 Windows 8 (含) 以後版本電腦上的資料夾重新導向、離線檔案和漫遊設定檔。  

 [建立使用者資料和設定檔設定項目](/sccm/compliance/deploy-use/create-user-data-and-profiles-configuration-items)  

## <a name="windows-edition-upgrade-policy"></a>Windows 版本升級原則  
 版本升級原則可讓您將 Windows 10 裝置自動升級至更新版本。 您可以指定產品金鑰來升級 Windows 10 桌上型電腦版本，或是為執行 Windows 10 行動裝置版和 Windows 10 全像攝影版的裝置指定可將其升級的授權檔案。  

 [使用版本升級原則升級 Windows 裝置](/sccm/compliance/deploy-use/upgrade-windows-version)  
