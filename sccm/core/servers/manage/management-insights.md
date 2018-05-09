---
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 控制台中可用的管理见解功能。
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a79f83be-884c-48e6-94d6-ed0a68c22e2f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9ded020bd654672bb6133c9aad15478c22498ab7
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="management-insights-in-system-center-configuration-manager"></a>System Center Configuration Manager 中的管理见解

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 中的管理见解提供有关环境当前状态的信息。 该信息基于对站点数据库中数据的分析。 见解有助于更好地了解环境，并根据见解执行操作。 此功能在 Configuration Manager 1802 版中发布。 <!--1353967-->

## <a name="review-management-insights-in-the-configuration-manager-console"></a>查看 Configuration Manager 控制台中的管理见解 
需要**站点读取**权限才能查看规则。

1. 请打开 Configuration Manager 控制台。 
2. 转到“管理”节点并单击“管理见解”。
3. 选择“所有见解”
4. 双击要查看的“管理见解组名称”。 或者，突出显示该见解，然后单击功能区中的“显示见解”。 
5. 可查看四个选项卡以及运行规则所需的先决条件。 
    - **所有规则**：提供所选管理见解组的完整规则列表。
    - **已完成**：列出无需执行任何操作的规则。 
    - **正在进行**：显示已完成部分（但非全部）先决条件的规则。
    - **需要执行操作**：列出需要执行操作的规则。 右键单击并选择“更多详细信息”可检索需要执行操作的特定项目。 
    - **先决条件**：如果某项规则需要完成一些项目后才能运行，则将在此处列出所需的项目。   
    
    **云服务组的所有规则和先决条件**![管理见解 - 云服务组的所有规则和先决条件](./media/Management-insights-all-cloud-rules.png)

## <a name="management-insights-reevaluation-and-logging"></a>管理见解重新评估和记录
管理见解规则每周重新评估一次适用性。 你可以按需重新评估某项规则，方法是右键单击该规则并选择“重新评估”。

**管理见解规则的日志文件**：SMS_DataEngine.log
## <a name="management-insights-groups-and-rules"></a>管理见解组和规则
规则分为不同的管理见解组。 当添加组和规则时，它们将被添加到以下列表中：

**应用程序**：对应用程序管理的见解。

- **没有部署的应用程序**：列出环境中没有活动部署的应用程序。 此规则有助于查找并删除未使用的应用程序，以简化显示在控制台中的应用程序列表。 

**云服务**：帮助你与多种云服务集成；实现设备的现代化管理。 
 - **评估共同管理准备情况**：帮助你了解启用共同管理所需执行的步骤。 此规则具有先决条件。 
 - **使设备加入混合 Azure Active Directory**：加入 Azure AD 的设备允许用户使用他们的域凭据登录，同时确保设备符合组织的安全性和符合性标准。 
 - **实现标识和访问基础结构的现代化**：使用集成式多重身份验证的 Azure AD 云服务可以保护本地和云端的敏感数据和应用程序。 
 - **将客户端升级到 Windows 10 1709 或更高版本**：Windows 10 1709 或更高版本对用户的计算体验进行了改进和现代化处理。 


**集合**：通过清理和重新配置集合来帮助简化管理的见解。
   - **空集合**：列出环境中没有成员的集合。 

**简化管理**：帮助简化日常环境管理的见解。 
   - **过时的客户端版本**：列出所有版本超过两年的客户端。 

**软件中心**：用于管理软件中心的见解。 
   - **将用户定向到软件中心而不是应用程序目录**：检查用户是否在过去 14 天内从应用程序目录安装或请求了应用程序。 应用程序目录的主要功能现在包含在软件中心内。 随着在 2018 年 6 月 1 日后发布首个更新，将不再支持应用程序目录网站
   - **使用新版软件中心**：不再支持以前的软件中心版本。 可通过启用客户端设置“计算机代理” >“使用新的软件中心”，将客户端设置为使用新的软件中心。

**Windows 10**：与 Windows 10 的部署和服务相关的见解。 当超过一半的客户端运行 Windows 7、Windows 8 或 Windows 8.1 时，可以使用 Windows 10 管理见解组。
   - **配置 Windows 遥测和商业 ID 键**：若要使用 Upgrade Readiness 中的数据，设备必须配置商业 ID 键并启用遥测。 Windows 10 设备必须设置为“增强型(有限)”或更高遥测级别。
   - **将 Configuration Manager 连接至 Upgrade Readiness**：在 Windows 7 不再受支持之前，利用 Upgrade Readiness 加快 Windows 10 部署。 “配置 Windows 遥测和商业 ID 键”是先决条件。

     **Windows 10 管理见解规则**
    ![管理见解 - 面向 Windows 10 的规则](./media/Windows-10-insights-group.png)
    