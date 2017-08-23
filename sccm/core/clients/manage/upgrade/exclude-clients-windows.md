---
title: "排除用戶端升級 | Windows | System Center Configuration Manager"
description: "了解如何在 System Center Configuration Manager 中排除 Windows 用戶端升級。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4cd6031f-8844-4d0b-8166-b24d6528a94e
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: de5602179f3ac55b51133b8280a0143f1b0ff30e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-exclude-upgrading-clients-for-windows-computers-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中排除升級的 Windows 電腦用戶端

*適用於：System Center Configuration Manager (最新分支)*

從 1610 版開始，您可以排除用戶端集合自動安裝更新的用戶端版本。 這適用於自動升級及其他方法，例如以軟體更新為基礎的升級、登入指令碼和群組原則。 這可以在升級用戶端時，用於需要更小心對待的電腦集合。 排除集合中的用戶端會略過安裝更新版用戶端軟體的要求。

## <a name="configure-exclusion-for-automatic-upgrades"></a>設定排除自動升級

1. 在 Configuration Manager 主控台中，移至 [系統管理] > [站台設定] > [站台]，然後按一下 [階層設定]。

2. 按一下 [用戶端升級] 索引標籤。

3. 按一下 「Exclude specified clients from upgrade」 (排除升級指定的用戶端) 核取方塊，然後針對 「Exclusion collection」 (排除集合) 選取您要排除的集合。 您只能選取單一集合進行排除。

4.  按一下 [確定] 以關閉並儲存設定。 然後，在用戶端更新原則之後，排除集合中的用戶端就不會再自動安裝用戶端軟體的更新。 如需詳細資訊，請參閱[如何升級 Windows 電腦的用戶端](upgrade-clients-for-windows-computers.md)。

![自動升級的排除範圍設定](media/automatic_upgrade_exclusion.png)



>[!NOTE]
>雖然使用者介面指出用戶端不會透過任何方法升級，但您可以使用兩種方法來覆寫這些設定。 用戶端推入安裝和手動用戶端安裝可用來覆寫此設定。 如需詳細資訊，請參閱下一節。

## <a name="how-to-upgrade-a-client-that-is-in-an-excluded-collection"></a>如何升級排除集合中的用戶端

只要集合設定為要排除，該集合的成員只能透過兩種方法之一覆寫此排除範圍，以升級其用戶端軟體：
 - **用戶端推入安裝** - 您可以使用用戶端推入安裝來升級排除集合中的用戶端。 因為這視為系統管理員的意圖，所以允許這樣做。此方法可讓您升級用戶端，而不需要從排除範圍中移除整個集合。       

 - **手動用戶端安裝** - 您可以使用下列命令列參數搭配 ccmsetup，手動升級排除集合中的用戶端：***/ignoreskipupgrade***

  如果您嘗試手動升級屬於排除集合成員的用戶端，但未使用此參數，則用戶端不會安裝新的用戶端軟體。 如需詳細資訊，請參閱[如何手動安裝 Configuration Manager 用戶端](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Manual)。

如需用戶端安裝方法的詳細資訊，請參閱[如何在 System Center Configuration Manager 中將用戶端部署至 Windows 電腦](/sccm/core/clients/deploy/deploy-clients-to-windows-computers)。
