---
title: "註冊裝置 | Microsoft Docs"
description: "了解在 System Center Configuration Manager 中註冊裝置以進行內部行動裝置管理的方法。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: b58472e3-31a5-4305-8eb6-2522befebe02
caps.latest.revision: "6"
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 4abaef35969ef1a5340ae8ca8aa5699cd3942642
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="enroll-devices-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中註冊裝置以進行內部行動裝置管理

*適用於：System Center Configuration Manager (最新分支)*

若要使用 System Center Configuration Manager 內部部署行動裝置管理來管理電腦和裝置，裝置需要註冊以便 Configuration Manager 能與裝置溝通管理工作。 Configuration Manager 提供兩種註冊裝置的方法：  

-   **使用者註冊** - 在此方法中，使用者在其裝置上起始註冊程序。 使用者註冊若要成功，裝置上必須安裝信任的根憑證，且必須佈建使用者，以便由 Configuration Manager 註冊。  若要註冊裝置，使用者只要提供工作認證，裝置便會註冊為受管理。  

     如需詳細資訊，請參閱[使用者如何在 System Center Configuration Manager 中使用內部部署行動裝置管理註冊裝置](../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md)  

-   **大量註冊** - 在此方法中，裝置的使用者不需要起始註冊。 而是會在 Configuration Manager 建立一個大量註冊套件，然後放在裝置上並開啟。 開啟時，套件會提供註冊裝置所需的資訊。  

     如需詳細資訊，請參閱[如何在 System Center Configuration Manager 中使用內部部署行動裝置管理大量註冊裝置](../../mdm/deploy-use/bulk-enroll-devices-on-premises-mdm.md)  

 > [!NOTE]  
>  Configuration Manager 的最新分支，支援執行下列作業系統的裝置在內部部署行動裝置管理中註冊︰  
>   
>  -   Windows 10 Enterprise  
> -   Windows 10 Pro  
> -   Windows 10 團隊版 
> -   Windows 10 Mobile  
> -   Windows 10 Mobile Enterprise   
