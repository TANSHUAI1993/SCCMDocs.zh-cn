---
title: "管理與 System Center Configuration Manager 相關聯的 Intune 訂用帳戶 | Microsoft Docs"
description: "管理與 System Center Configuration Manager 相關聯的 Intune 訂用帳戶。"
ms.custom: na
ms.date: 06/02/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9b494767-68c1-47b1-9a86-591bff0ad491
caps.latest.revision: "18"
caps.handback.revision: "0"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 2cb4d724c8b78657458a30c0bb020f67c6b62795
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="manage-an-intune-subscription-associated-with-system-center-configuration-manager"></a>管理與 System Center Configuration Manager 相關聯的 Intune 訂用帳戶

*適用於︰System Center Configuration Manager (最新分支)*

如果您將 Microsoft Intune (試用訂閱或付費訂閱) 新增至 Configuration Manager，但之後需要切換至不同的 Intune 訂閱，則必須先從 Configuration Manager 主控台刪除 **Microsoft Intune 訂閱**和**服務連接點**，才能新增訂閱。

> [!NOTE]
> 在混合式行動裝置管理中，您一次只能設定一個 Intune 訂用帳戶。

## <a name="how-to-delete-an-intune-subscription-from-configuration-manager"></a>如何從 Configuration Manager 刪除 Intune 訂閱

> [!IMPORTANT]
>  當您刪除 Intune 訂閱時，會移除包括針對訂閱所管理之裝置所設定的使用者註冊、原則和應用程式部署的所有內容。

1.  在 Configuration Manager 主控台中，移至 [系統管理] > [概觀] > [雲端服務] > [Microsoft Intune 訂閱]。

2.  以滑鼠右鍵按一下列出的 [Microsoft Intune 訂閱]，然後按一下 [刪除]。

3.   在精靈中，按一下 [Remove Microsoft Intune Subscription from Configuration Manager]\(從 Configuration Manager 移除 Microsoft Intune 訂閱)，並按一下 [下一步]，然後按一下 [下一步] 移除訂閱。


## <a name="how-to-remove-the-service-connection-point-role"></a>如何移除服務連接點角色

1.  移至 [系統管理] > [概觀] > [站台設定] > [伺服器和站台系統角色]。

2.  選取裝載 **服務連接點** 角色的伺服器。

3.  在 **[站台系統角色]** 清單中，選取 **[服務連接點]** ，然後按一下功能區中的 **[移除角色]** 。 確認您想要移除該角色。 隨即會刪除該服務連接點。

您現在可以建立新的服務連接點、將新的 Intune 訂閱加入至 Configuration Manager，然後將 Configuration Manager 設定為 MDM 授權單位。

## <a name="how-to-change-mdm-authority-to-intune"></a>如何將 MDM 授權單位變更為 Intune
自 Configuration Manager 1610 版和 Microsoft Intune 1705 版開始，不需要連絡 Microsoft 支援服務，也不需要將現有受管理裝置解除註冊並重新註冊，您便可以變更 MDM 授權單位。 如需詳細資訊，請參閱[變更您的 MDM 授權單位](/sccm/mdm/deploy-use/change-mdm-authority)。
