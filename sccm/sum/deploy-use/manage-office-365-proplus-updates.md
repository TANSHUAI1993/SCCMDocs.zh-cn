---

title: "管理 Office 365 ProPlus 更新 | Configuration Manager"
description: "Configuration Manager 将 Office 365 客户端更新从 WSUS 目录同步到站点服务器，使更新可部署到客户端。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: eac542eb-9aa1-4c63-b493-f80128e4e99b
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 58a551425591332264592713fa3cc4e04d9939aa


---

# <a name="manage-office-365-proplus-updates-with-configuration-manager"></a>使用 Configuration Manager 管理 Office 365 ProPlus 更新

*适用范围：System Center Configuration Manager (Current Branch)*

从 Configuration Manager 版本 1602 开始，Configuration Manager 能够使用软件更新管理工作流管理 Office 365 客户端。 当 Microsoft 将新的 Office 365 客户端更新发布到 Office 内容交付网络 (CDN) 时，Microsoft 还会将更新包发布到 Windows Server 更新服务 (WSUS)。 将 Office 365 客户端更新从 WSUS 目录同步到站点服务器之后，更新可部署到客户端。

#### <a name="to-deploy-office-365-updates-with-configuration-manager"></a>使用 Configuration Manager 部署 Office 365 更新
使用以下步骤通过 Configuration Manager 部署 Office 365 更新：

1.  在本主题的**使用 Configuration Manager 管理 Office 365 客户端更新的要求**部分，验证使用 Configuration Manager 管理 Office 365 客户端更新的[要求](https://technet.microsoft.com/library/mt628083.aspx)。  

2.  [配置软件更新点](../get-started/configure-classifications-and-products.md)来同步 Office 365 客户端更新。 针对分类设置**更新**，并为产品选择 **Office 365 客户端**。 可能需要至少先同步一次软件更新，才能选择 Office 365 客户端产品。 将软件更新点配置为使用**更新**分类后，必须同步软件更新。  

3.  使 Office 365 客户端可以从 Configuration Manager 接收更新。 可通过使用 Configuration Manager 客户端设置或使用组策略来完成此操作。 使用下列方法之一启用客户端：  
    - 方法 1：从 Configuration Manager 版本 1606 开始，可使用 Configuration Manager 客户端设置管理 Office 365 客户端代理。 配置此设置和部署 Office 365 更新后，Configuration Manager 客户端代理将与 Office 365 客户端代理通信，从分发点下载 Office 365 更新并进行安装。 Configuration Manager 盘点了 Office 365 ProPlus 客户端设置的步骤。
      1.  在 Configuration Manager 控制台中，单击“管理” > “概述” > “客户端设置”。  

      2.  打开相应的设备设置以启用客户端代理。 有关默认客户端设置和自定义客户端设置的详细信息，请参阅[如何在 System Center Configuration Manager 中配置客户端设置](../../core/clients/deploy/configure-client-settings.md)。  

      3.  单击“软件更新”，并针对“启用 Office 365 客户端代理的管理”设置选择“是”。  

    - 方法 2：使用 Office 部署工具或组策略从 Configuration Manager [启用 Office 365 客户端以接收更新](https://technet.microsoft.com/library/mt628083.aspx#BKMK_EnableClient)。  

4. [将 Office 365 更新部署](deploy-software-updates.md)到客户端。  



<!--HONumber=Nov16_HO1-->


