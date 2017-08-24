---
title: "Azure 服务向导 | Microsoft Docs"
description: "关于 System Center Configuration Manager 的 Azure 服务向导。"
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a26a653e-17aa-43eb-ab36-0e36c7d29f49
caps.latest.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 22203b358830903cf2e531c0532ae3111b8265fc
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="configure-azure-services-for-use-with-configuration-manager"></a>配置用于 Configuration Manager 的 Azure 服务

*适用范围：System Center Configuration Manager (Current Branch)*

从 Current Branch 版本 1706 开始，“Azure 服务向导”可简化用于 Configuration Manager 的 Azure 服务的配置过程。

此向导使用 Azure Web 应用提供订阅和配置详细信息，从而提供通用配置体验。 每次设置新 Configuration Manager 组件或 Azure 服务时，Web 应用都会输入此相同的信息。

使用“配置 Azure 服务”向导配置以下 Azure 服务：
-   **云管理**   
    [使用 Azure Active Directory (Azure AD) 支持客户端进行身份验证]()。 还可以[配置 Azure AD 用户发现](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc)。
-   **OMS 连接器**
    [连接到 Operations Manager Suite](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite) (OMS)，并将集合等数据同步到 OMS Log Analytics。
-   **升级就绪情况**
    [连接到升级就绪情况](/sccm/core/clients/manage/upgrade/upgrade-analytics)并查看客户端升级兼容性数据。
-   **适用于企业的 Windows 应用商店**连接到[适用于企业的 Windows 应用商店](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)的在线商店，并为你的组织获取应用以通过 Configuration Manager 进行部署。

使用向导配置服务时，可以使用几个常见的操作。
其中包括:
-   配置 Azure 环境：在向导的“应用”页中，选择所用的“Azure 环境”。 请参阅每个服务的内容，了解它是否仅支持 Azure 公有云或是否可以支持私有云。
-   创建或导入服务器应用：在向导的“应用”页上，可以“创建”和“导入”Azure Web 应用。 可用选项取决于你配置的服务。  此外，某些服务可能需要更多的应用。 例如，服务可能还需要“本机客户端应用”。


有关 Azure Web 应用的信息，请参阅 [Azure 应用服务中的身份验证和授权](/azure/app-service/app-service-authentication-overview)和 [Web 应用概述](/azure/app-service-web/app-service-web-overview)


## <a name="webapp"></a> 创建 Azure Web 应用以用于 Configuration Manager

Azure 服务 Web 应用将 Configuration Manager 站点连接到 Azure AD，这也是将 Azure 服务与基础结构结合使用的先决条件。 要执行此操作：

1.  在 Configuration Manager 控制台的“管理”工作区中，展开“云服务”，然后单击“Azure 服务”。
2.  在“主页”选项卡上的“Azure 服务”组中，单击“配置 Azure 服务”。
3.  在 Azure 服务向导的“Azure 服务”页上，选择“云管理”以允许客户端使用 Azure AD 对层次结构进行身份验证。
4.  在向导的“常规”页上，指定一个名称和 Azure 服务的说明。
5.  在向导的“应用”页上，从列表中选择 Azure 环境，然后单击“浏览”以选择要用于配置 Azure 服务的“Web 应用”和“本机客户端应用”。     
    **Web 应用：**浏览并打开“服务器应用”窗口。    
      在“服务器应用”窗口中，选择要使用的服务器应用，然后单击“确定”。 服务器应用是包含 Azure 帐户配置的 Azure Web 应用，包括客户端的租户 ID、客户端 ID 和密钥。
    如果没有可用的应用，请使用以下操作之一：
        - **创建**：若要创建新的服务器应用，请单击“创建”。 接下来提供应用的友好名称、主页 URL、应用 ID URI 和密钥有效期。 默认情况下，密钥有效期为一年。

         若要继续，现在必须登录到 Azure 以在 Azure 中完成 Web 应用的创建。 用于登录 Azure 的帐户不必与运行 Azure 服务向导的帐户相同。 登录 Azure 后，Configuration Manager 在 Azure 中为用户创建 Web 应用，包括用于 Web 应用的客户端 ID 和密钥。 之后，可在 Azure 门户中查看这些内容。

         使用“创建”配置 Web 应用时，Configuration Manager 可以在 Azure AD 中为你创建 Web 应用。
        - **导入**：若要使用 Azure 订阅中已存在的 Web 应用，请单击“导入”。 为应用和租户提供友好名称，然后为 Configuration Manager 要使用的 Azure Web 应用指定租户 ID、客户端 ID 和密钥。 验证此信息后，单击“确定”以继续。

          此选项并非适用于你可能配置的所有服务。

   **本机客户端应用：**浏览并打开“客户端应用”窗口。  
     在“客户端应用”窗口中，选择要使用的客户端应用，然后单击“确定”。

     如果没有可用的客户端应用，请使用以下操作之一：
     - **创建**：若要创建新的客户端应用，请单击“创建”。 接下来，提供应用的友好名称和回复 URL。

          若要继续，现在必须登录到 Azure 以在 Azure 中完成客户端应用的创建。 用于登录 Azure 的帐户不必与运行 Azure 服务向导的帐户相同。 登录 Azure 后，Configuration Manager 在 Azure 中为用户创建本机客户端应用，包括用于 Web 应用的客户端 ID。 之后，可在 Azure 门户中查看这些内容。
          使用“创建”配置应用时，Configuration Manager 可以在 Azure AD 中为你创建本机客户端应用。
     - **导入**：若要使用 Azure 订阅中已存在的客户端应用，请单击“导入”。 为应用和客户端 ID 提供友好名称。 然后，单击“确定”继续。
           此选项并非适用于你可能配置的所有服务。

  <!--  MOVE THIS AND STEP 6 TO configure Azure AD User Discover  content
       [!TIP]  
     When you use Import, the account you use to run the wizard must have the *Read directory data* application permission in the Azure portal. This is required to set the correct permissions for the App. When you use Create, Configuration Manager creates the app with the correct permissions. However, you still must give consent to the application in the Azure portal.   -->


6.  在向导的“发现”页上，单击“启用 Azure Active Directory 用户发现”，然后单击“设置”。
在“Azure AD 用户发现设置”对话框中，配置出现发现的时间计划。 此外，还可以启用增量发现，用于仅查看 Azure AD 中新增或更改的帐户。 详细了解 [Azure AD 用户发现](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc)。
 
 7. 完成向导。

此时，已将 Configuration Manager 站点连接到 Azure AD。

## <a name="view-the-configuration-of-an-azure-service"></a>查看 Azure 服务的配置
可以查看已配置进行使用的 Azure 服务的属性。

在控制台中，转到“管理” > “概述” > “云服务” > “Azure 服务”。 接下来，选择你想要查看或编辑的服务，然后单击“属性”。
