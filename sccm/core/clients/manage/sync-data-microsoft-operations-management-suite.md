---
title: "同步数据 | Microsoft Docs | Microsoft Operations Management Suite "
description: "将数据从 System Center Configuration Manager 同步到 Microsoft Operations Management Suite。"
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 33bcf8b3-a6b6-4fc9-bb59-70a9621b2b0d
caps.latest.revision: "9"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: 608a9893011c6500d5d4cd2f756a124db66b1858
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
#  <a name="sync-data-from-configuration-manager-to-the-microsoft-operations-management-suite"></a>将数据从 Configuration Manager 同步到 Microsoft Operations Management Suite

*适用范围：System Center Configuration Manager (Current Branch)*

可以使用 Azure 服务向导配置从 Configuration Manager 到 Operations Management Suite (OMS) 云服务的连接。 从版本 1706 开始，向导将替换以前的工作流，以配置此连接。 对于较早的版本，请参阅[将数据从 Configuration Manager 同步到 Microsoft Operations Management Suite（1702 及更早版本）](#Sync-data-from-Configuration-Manager-to-the-Microsoft-Operations-Management-Suite-(1702-and-earlier))。

-   该向导用于配置适用于 Configuration Manager 的云服务，如 OMS、适用于企业的 Windows 应用商店 (WSfB) 和 Azure Active Directory (Azure AD)。  

-   Configuration Manager 连接到 OMS 以实现[日志分析](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite)或[升级就绪情况](/sccm/core/clients/manage/upgrade/upgrade-analytics)等功能。

## <a name="prerequisites-for-the-oms-connector"></a>OMS 连接器的先决条件
配置与 OMS 的连接的先决条件与 [Current Branch 版本 1702 中记录的](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite#prerequisites)先决条件并无任何区别。 此处重复了该信息：  

-   在 Configuration Manager 中安装 OMS 连接器之前，必须为 Configuration Manager 提供对 OMS 的访问权限。 具体而言，你必须授予*参与者*对 Azure *资源组*的访问权限，其中包含 OMS Log Analytics 工作区。 执行此操作的过程会被记录在 Log Analytics 内容中。 请参阅 OMS 文档中的[为 Configuration Manager 提供对 OMS 的访问权限](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms)。

-   必须在托管[联机模式](/sccm/core/servers/deploy/configure/about-the-service-connection-point#a-namebkmkmodesa-modes-of-operation)下的[服务连接点](/sccm/core/servers/deploy/configure/about-the-service-connection-point)的计算机上安装 OMS 连接器。

-   必须为在服务连接点上安装的 OMS 安装 Microsoft Monitoring Agent 以及 OMS 连接器。 必须将代理和 OMS 连接器配置为使用相同的 **OMS 工作区**。 若要安装代理，请参阅 OMS 文档中的[下载并安装代理](/azure/log-analytics/log-analytics-sccm#download-and-install-the-agent)。
-   安装连接器和代理后，必须配置 OMS 以使用 Configuration Manager 数据。 为此，请在 OMS 门户中[导入 Configuration Manager 集合](/azure/log-analytics/log-analytics-sccm#import-collections)。

## <a name="use-the-azure-services-wizard-to-configure-the-connection-to-oms"></a>使用 Azure 服务向导配置与 OMS 的连接

1.  在控制台中，转到“管理” > “概述” > “云服务” > “Azure 服务”，然后从功能区的“主页”选项卡上选择“配置 Azure 服务”，以启动“Azure 服务向导”。

2.  在“Azure 服务”页上，选择 Operation Management Suite 云服务。 提供“Azure 服务名称”的友好名称和可选说明，然后单击“下一步”。

3.  在“应用”页上，指定 Azure 环境（Technical Preview 仅支持公有云）。 然后，单击“浏览”以打开“服务器应用”窗口。

4.  选择 Web 应用：

    -   **导入**：若要使用 Azure 订阅中已存在的 Web 应用，请单击“导入”。 为应用和租户提供友好名称，然后为 Configuration Manager 要使用的 Azure Web 应用指定租户 ID、客户端 ID 和密钥。 “验证”信息后，单击“确定”以继续。   

    > [!NOTE]   
    > 在使用此预览配置 OMS 时，OMS 仅支持 Web 应用的导入功能。 不支持创建新的 Web 应用。 同样，无法为 OMS 重用现有的应用。

5.  如果已成功完成所有其他过程，则“OMS 连接配置”屏幕上的信息将自动显示在此页上。 应显示“Azure 订阅”、“Azure 资源组”和“Operations Management Suite 工作区”的连接设置的信息。

6.  向导使用输入的信息连接到 OMS 服务。 选择想要与 OMS 同步的设备集合，然后单击“添加”。

7.  在“摘要”屏幕上验证连接设置，然后选择“下一步”。 “进度”屏幕会显示连接状态，然后应显示“完成”。

8.  完成向导后，Configuration Manager 控制台会显示已将“Operation Management Suite”配置为“云服务类型”。

## <a name="sync-data-from-configuration-manager-to-the-microsoft-operations-management-suite-1702-and-earlier"></a>将数据从 Configuration Manager 同步到 Microsoft Operations Management Suite（1702 及更早版本）


适用于：System Center Configuration Manager（1702 及更早版本）

可以使用 Microsoft Operations Management Suite (OMS) 连接器将数据（如集合）从 System Center Configuration Manager 同步到 Microsoft Azure 中的 OMS Log Analytics。 这使得 Configuration Manager 部署中的数据在 OMS 中可见。
> [!TIP]
> OMS 连接器是一种预发行功能。 若要了解详细信息，请参阅[使用更新中的预发行功能](/sccm/core/servers/manage/pre-release-features)。

从版本 1702 开始，你可以使用 OMS 连接器连接到 Microsoft Azure Government 云上的一个 OMS 工作区。 这要求你先修改配置文件，然后才能安装 OMS 连接器。 请参阅本主题中的[将 OMS 连接器与 Azure Government 云结合使用](#fairfaxconfig)。

### <a name="prerequisites"></a>先决条件
- 在 Configuration Manager 中安装 OMS 连接器之前，必须为 Configuration Manager 提供对 OMS 的访问权限。 具体而言，你必须授予*参与者*对 Azure *资源组*的访问权限，其中包含 OMS Log Analytics 工作区。 执行此操作的过程会被记录在 Log Analytics 内容中。 请参阅 OMS 文档中的[为 Configuration Manager 提供对 OMS 的访问权限](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms)。

- 必须在托管[联机模式](/sccm/core/servers/deploy/configure/about-the-service-connection-point#a-namebkmkmodesa-modes-of-operation)下的[服务连接点](/sccm/core/servers/deploy/configure/about-the-service-connection-point)的计算机上安装 OMS 连接器。

  如果你已将 OMS 连接到独立主站点并打算将管理中心站点添加到你的环境，必须删除当前连接，然后在新的管理中心站点重新配置连接器。

- 必须为在服务连接点上安装的 OMS 安装 Microsoft Monitoring Agent 以及 OMS 连接器。  必须将代理和 OMS 连接器配置为使用相同的 **OMS 工作区**。 若要安装代理，请参阅 OMS 文档中的[下载并安装代理](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#download-and-install-the-agent)。

- 安装连接器和代理后，必须配置 OMS 以使用 Configuration Manager 数据。  为此，请在 OMS 门户中[导入 Configuration Manager 集合](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#import-collections)。



### <a name="install-the-oms-connector"></a>安装 OMS 连接器  
1. 在 Configuration Manager 控制台中，配置你的[层次结构以使用预发行功能](/sccm/core/servers/manage/pre-release-features)，然后启用 OMS 连接器。  

2. 接下来，转到“管理” > “云服务” > “OMS 连接器”。 在功能区中，单击“创建 Operations Management Suite 连接”。 这会打开“Operation Management Suite Wizard 连接向导”。 选择“下一步”。  


3.  在“常规”页上，确认你具有以下信息，然后选择“下一步”。  
  - 将 Configuration Manager 注册为“Web 应用程序和/或 Web API”管理工具，你会具有[来自此注册的客户端 ID](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)。  
  - 在 Azure Active Directory 中，为已注册的管理工具创建客户端密钥。  

  - 在 Azure 管理门户中，向已注册的 Web 应用提供访问 OMS 的权限，如[向 Configuration Manager 提供 OMS 权限](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms)中所述。  

4.  在“Azure Active Directory”页上，通过提供“租户”、“客户端 ID”和“客户端密钥”来配置 OMS 的连接设置，然后选择“下一步”。  

5.  在“OMS 连接配置”页上，通过填写“Azure 订阅”、“Azure 资源组”和“Operations Management Suite 工作区”，来提供连接设置。  工作区必须匹配为在服务连接点上安装的 Microsoft 管理代理配置的工作区。  

6.  在“摘要”页上验证连接设置，然后选择“下一步”。 “进度”页会显示连接状态，然后应单击“完成”。

将 Configuration Manager 链接到 OMS 之后，可以添加或删除集合，以及查看 OMS 连接的属性。

### <a name="verify-the-oms-connector-properties"></a>验证 OMS 连接器属性
1.  在 Configuration Manager 控制台中，依次转到“管理” > “云服务”，然后选择“OMS 连接器”，打开“OMS 连接”页。
2.  该页中有两个选项卡：
  - **Azure Active Directory：**   
    此选项卡显示“租户”、“客户端 ID”、“客户端机密密钥到期日期”，使你可以验证客户端密钥是否到期。

  - **OMS 连接属性：**  
    此选项卡显示“Azure 订阅”、“Azure 资源组”、“Operations Management Suite 工作区”和“Operations Management Suite 可以获取有关数据的设备集合”列表。 使用“添加”和“删除”按钮可修改允许使用的集合。

### <a name="fairfaxconfig"> </a>将 OMS 连接器与 Azure Government 云结合使用


1.  在任何安装了 Configuration Manager 控制台的计算机上，编辑以下配置文件，使其指向政府云：***&lt;CM 安装路径>\AdminConsole\bin\Microsoft.configurationManagmenet.exe.config***

  **编辑：**

    将设置名称 FairFaxArmResourceID 的值更改为等于“https://management.usgovcloudapi.net/”

   - **初始：**&lt;setting name="FairFaxArmResourceId" serializeAs="String">   
      &lt;value>&lt;/value>   
      &lt;/setting>

   - **编辑后：**     
      &lt;setting name="FairFaxArmResourceId" serializeAs="String"> &lt;value>https://management.usgovcloudapi.net/&lt;/value>  
      &lt;/setting>

  将设置名称 FairFaxAuthorityResource 的值更改为等于“https://login.microsoftonline.com/”

  - **原始：**&lt;setting name="FairFaxAuthorityResource" serializeAs="String">   
    &lt;value>&lt;/value>

    - **编辑后：**&lt;setting name="FairFaxAuthorityResource" serializeAs="String">   
    &lt;value>https://login.microsoftonline.com/&lt;/value>

2.  保存包含这两种更改的文件后，请在同一台计算机上重启 Configuration Manager 控制台，然后使用该控制台安装 OMS 连接器。 若要安装连接器，请使用[将数据从 Configuration Manager 同步到 Microsoft Operations Management Suite](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite) 中的信息，选择 Microsoft Azure 政府云上的 **Microsoft Operations Management Suite**。

3.  OMS 连接器安装后，使用任何连接到站点的控制台时，可使用与政府云的连接。
