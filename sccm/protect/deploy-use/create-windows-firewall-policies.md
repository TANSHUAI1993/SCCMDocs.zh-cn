---
title: "Endpoint Protection 的 Windows 防火牆原則 | Microsoft Docs"
description: "了解如何在 System Center 2012 Configuration Manager 中建立和部署 Endpoint Protection 的防火牆原則。"
ms.custom: na
ms.date: 03/07/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6ecdfad1-6305-45a8-ae75-3f33b967cb8f
caps.latest.revision: "5"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: acd75a8b22d050970b8c1176f725ddb4445633aa
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="create-and-deploy-windows-firewall-policies-for-endpoint-protection-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中建立和部署 Endpoint Protection 的 Windows 防火牆原則

*適用於：System Center Configuration Manager (最新分支)*

System Center 2012 Configuration Manager 中 Endpoint Protection 的防火牆原則可讓您在階層的用戶端電腦上執行基本 Windows 防火牆設定和維護工作。 您可以使用 Windows 防火牆原則來執行下列工作：  

-   控制開啟還是關閉 Windows 防火牆。  

-   控制用戶端電腦是否允許連入連線。  

-   控制當 Windows 防火牆阻擋新程式時是否通知使用者。  

1.  在 Configuration Manager 主控台中，按一下 [資產與相容性] 。  

2.  在 [資產與相容性] 工作區中，展開 [Endpoint Protection]，然後按一下 [Windows 防火牆原則]。  

3.  在 [首頁]  索引標籤的 [建立]  群組中，按一下 [建立 Windows 防火牆原則] 。  

4.  在 [建立 Windows 防火牆原則精靈]  的 [一般] 頁面上，指定這個防火牆原則的名稱和選擇性描述，然後按一下 [下一步] 。  

5.  在精靈的 [設定檔設定]  頁面上，設定每個網路設定檔的下列設定：  

    > [!IMPORTANT]  
    >  如果您想要將 Windows 防火牆原則部署到執行 Windows Server 2008 和 Windows Vista Service Pack 1 的電腦，則必須先在這些電腦上安裝 [Hotfix KB971800](http://go.microsoft.com/fwlink/p/?LinkId=231239) 。  

    > [!NOTE]  
    >  如需網路設定檔的詳細資訊，請參閱 Windows 文件。  

    -   **啟用 Windows 防火牆**  

        > [!NOTE]  
        >  如果未啟用 [啟用 Windows 防火牆]  ，則無法使用精靈的這個頁面上的其他設定。  

    -   **阻擋所有連入連線，包括允許之程式清單中的連線**  

    -   **當 Windows 防火牆阻擋新程式時通知使用者**  

6.  在精靈的 [摘要]  頁面上，檢閱要採取的動作，然後完成精靈。  

7.  確認新的 Windows 防火牆原則顯示在 [Windows 防火牆原則]  清單中。  

##  <a name="BKMK_Assign"></a> 部署 Windows 防火牆原則  

1.  在 Configuration Manager 主控台中，按一下 [資產與相容性] 。  

2.  在 [資產與相容性] 工作區中，展開 [Endpoint Protection]，然後按一下 [Windows 防火牆原則]。  

3.  在 [Windows 防火牆原則]  清單中，選取您想要部署的 Windows 防火牆原則。  

4.  在 [首頁]  索引標籤的 [部署]  群組中，按一下 [部署] 。  

5.  在 [部署 Windows 防火牆原則]  對話方塊中，指定您要將這個 Windows 防火牆原則指派到其中的集合，並指定指派排程。 Windows 防火牆原則評估相容性的方式，是在用戶端上使用這個排程和 Windows 防火牆設定來重新設定以符合 Windows 防火牆原則。  

6.  按一下 [確定]  關閉 [部署 Windows 防火牆原則]  對話方塊，並部署 Windows 防火牆原則。  

    > [!IMPORTANT]  
    >  將 Windows 防火牆原則部署至集合時，會在 2 小時期間內隨機將這個原則套用至電腦，避免網路流量過大。
