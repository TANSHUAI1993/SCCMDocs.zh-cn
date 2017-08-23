---
title: "使用 System Center Configuration Manager 建立服務連接點 | Microsoft Docs"
description: "使用 System Center Configuration Manager 建立服務連接點。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 617abb22-d22f-41fb-a76b-1c4259e419d2
caps.latest.revision: "18"
caps.handback.revision: "0"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 9a21d02cb2a50162e5de50481f0f27f2dd7a616c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="create-a-service-connection-point-with-system-center-configuration-manager-and-microsoft-intune"></a>使用 System Center Configuration Manager 和 Microsoft Intune 建立服務連接點

*適用於：System Center Configuration Manager (最新分支)*

建立訂閱後，您就可以安裝服務連線點站台系統角色，該角色可讓您連線至 Intune 服務。 這個站台系統角色會將設定和應用程式推送到 Intune 服務。

 服務連接點會將設定和軟體部署資訊傳送至 Configuration Manager，並從行動裝置擷取狀態和清查訊息。 Configuration Manager 服務是與行動裝置進行通訊及儲存設定的閘道。

> [!NOTE]
>  服務連線點站台系統角色只能安裝在管理中心網站或獨立主要站台上。 服務連接點必須能夠存取網際網路。


## <a name="configure-the-service-connection-point-role"></a>設定服務連接點角色

1.  在 Configuration Manager 主控台中，按一下 [系統管理] 。

2.  在 [系統管理] 工作區中，展開 [站台]，然後按一下 [伺服器和站台系統角色]。

3.  使用關聯步驟，將 [服務連接點] 角色新增至新的或現有的站台系統伺服器：

    -   新增站台系統伺服器：在 [常用] 索引標籤的 [建立] 群組中，按一下 [建立站台系統伺服器] 以啟動 [建立站台系統伺服器精靈]。

    -   現有的站台系統伺服器：按一下您要安裝服務連接點角色的伺服器。 在 [常用] 索引標籤的 [伺服器] 群組中，按一下 [新增網站系統角色] 以啟動 [新增網站系統角色精靈]。

4.  在 [系統角色選取] 頁面上，選取 [服務連接點]，然後按一下 [下一步]。
![建立服務連接點](../media/mdm-service-connection-point.png)

* 完成精靈。

## <a name="how-does-the-service-connection-point-authenticate-with-the-microsoft-intune-service"></a>服務連接點如何向 Microsoft Intune 服務驗證？
 服務連接點會對透過網際網路管理行動裝置的雲端 Intune 服務建立連線，藉此擴充 Configuration Manager。 服務連接點使用 Intune 服務來驗證，如下所示：

1.  當您在 Configuration Manager 主控台建立 Intune 訂閱時，會連線到 Azure Active Directory 以驗證 Configuration Manager 系統管理員，其會重新導向至個別的 ADFS 伺服器，以提示輸入使用者名稱和密碼。 然後 Intune 會將憑證發行至租用戶。

2.  步驟 1 中的憑證安裝在服務接線點站台角色上，用來驗證和授權所有其他與 Microsoft Intune 服務的通訊。

> [!div class="button"]
[< 上一個步驟](terms-and-conditions.md)  [下一個步驟 >](enable-platform-enrollment.md)
