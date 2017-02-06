---
title: "管理 Office 365 ProPlus 更新 | Microsoft Docs"
description: "Configuration Manager 将 Office 365 客户端更新从 WSUS 目录同步到站点服务器，使更新可部署到客户端。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 01/04/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: eac542eb-9aa1-4c63-b493-f80128e4e99b
translationtype: Human Translation
ms.sourcegitcommit: 46c8004afee4b18d5c7a2fcc5dac0f7d0d1f823c
ms.openlocfilehash: fb2fc409c2f734816e4f3bf93d61a748d957ebf0

---

# <a name="manage-office-365-proplus-updates-with-configuration-manager"></a>使用 Configuration Manager 管理 Office 365 ProPlus 更新

*适用范围：System Center Configuration Manager (Current Branch)*

从 Configuration Manager 版本 1602 开始，Configuration Manager 能够使用软件更新管理工作流管理 Office 365 客户端。 当 Microsoft 将新的 Office 365 客户端更新发布到 Office 内容交付网络 (CDN) 时，Microsoft 还会将更新包发布到 Windows Server 更新服务 (WSUS)。 将 Office 365 客户端更新从 WSUS 目录同步到站点服务器之后，更新可部署到客户端。

## <a name="office-365-client-management-dashboard"></a>Office 365 客户端管理仪表板  
自 Configuration Manager 1610 版起，可在 Configuration Manager 控制台中使用 Office 365 客户端管理仪表板。 若要查看该仪表板，请转到“软件库” > “概述” > “Office 365 客户端管理”。

<!--- >[!NOTE]
>In the **What's New** workspace in the Configuration Manager console, the new dashboard is incorrectly named **Office 365 Servicing dashboard**. --->

仪表板显示以下内容的图表：

- Office 365 客户端数
- Office 365 客户端版本
- Office 365 客户端语言
- Office 365 客户端通道     
有关详细信息，请参阅 [Office 365 专业增强版的更新频道概述](https://technet.microsoft.com/library/mt455210.aspx)。
<!--- - Automatic deployment rules with Office 365 apps (have Office 365 Client selected in the set of available products). --->

<!---You can take the following actions on the dashboard:
- --->

在仪表板顶部，使用“集合”下拉列表设置按特定集合的成员筛选仪表板数据。

<!---
 On the upper-right side of the dashboard, click **Office 365 Installer** to start the Office 365 Client Installation Wizard to deploy Office 365 apps to clients. For details, see [Deploy Office 365 apps to clients](#deploy-office-365-apps-to-clients).
- On the middle-right side of the dashboard, click **Create an ADR** to open the Automatic Deployment Rule Wizard to create a new automatic deployment rule (ADR). To create an ADR for Office 365 apps, select **Office 365 Client** when you choose the product. For more information, see [Automatically deploy software updates](/sccm/sum/deploy-use/automatically-deploy-software-updates).
- On the lower-right side of the dashboard, click **Create Client Agent Settings** to open Client Agent settings. For more information, see [About client settings](/sccm/core/clients/deploy/about-client-settings).
--->

## <a name="deploy-office-365-updates-with-configuration-manager"></a>使用 Configuration Manager 部署 Office 365 更新
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

<!--  ## Add other languages for Office 365 update downloads
Beginning in Configuration Manager version 1610, you can add support for Configuration Manager to download updates for any languages supported by Office 365 regardless of whether they are supported in Configuration Manager.

### To add support to download updates for additional languages
Use the following procedure on the central administration site, or stand-alone primary site, where the software update point site system role is installed.
1. From a command prompt, type *wbemtest* as an administrative user to open the Windows Management Instrumentation Tester.
2. Click **Connect**, and then type *root\sms\site_<siteCode>*.
3. Click **Query**, and then run the following query:
   *select &#42; from SMS_SCI_Component where componentname ="SMS_WSUS_CONFIGURATION_MANAGER"*
4. Double-click the object with the site code for the central administration site or stand-alone primary site.

5. Browse the properties for View Embedded.
3). Find the SMS_EmbeddedProperty instance with the PropertyName of "AdditionalUpdateLanguagesForO365"
4). Set Value2 to be additional languages, e.g.:  pt-pt,af-za,nn-no, and save
5). Right click to download an O365 update, choose languages from UI
6). Verify that the language packs got downloaded including the UI specified ones plus the SDK specified ones. Admin can check the content package share specified to verify this.
-->

<!-- ## Change the update channel after you enable Office 365 clients to receive updates from Configuration Manager
To change the update channel after you enable Office 365 clients to receive updates from Configuration Manager, you must distribute a registry key value change to Office 365 clients using group policy. Change the **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\ClickToRun\Configuration\CDNBaseUrl** registry key to use one of the following values:

- Current Channel:  
  **CDNBaseUrl** = http://officecdn.microsoft.com/pr/492350f6-3a01-4f97-b9c0-c7c6ddf67d60

- Deferred Channel:  
  **CDNBaseUrl** = http://officecdn.microsoft.com/pr/7ffbc6bf-bc32-4f92-8982-f9dd17fd3114

- First Release for Current Channel:  
  **CDNBaseUrl** = http://officecdn.microsoft.com/pr/64256afe-f5d9-4f86-8936-8840a6a4f5be

- First Release for Deferred Channel:  
  **CDNBaseUrl** = http://officecdn.microsoft.com/pr/b8f9b850-328d-4355-9145-c59439a0c4cf
-->

<!--- ## Next steps
Use the Office 365 Client Management dashboard in Configuration Manager to review Office 365 client information and deploy Office 365 apps. For details, see [Manage Office 365 apps](manage-office-365-apps.md). --->



<!--HONumber=Jan17_HO1-->


