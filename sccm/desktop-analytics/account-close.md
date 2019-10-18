---
title: 如何关闭你的帐户
titleSuffix: Configuration Manager
description: 如何从 Azure 帐户中删除桌面分析
ms.date: 10/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6e7d2850-b0af-497e-bbc1-bfc2a7420a7a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0a37062bc945a69bfb6679186954146a337f8aed
ms.sourcegitcommit: b64ed4a10a90b93a5bd5454b6efafda90ad45718
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72386778"
---
# <a name="how-to-close-your-account"></a>如何关闭你的帐户

如果你在环境中设置了 "桌面分析"，然后决定要删除它，请使用此过程来关闭你的帐户。

## <a name="prerequisites"></a>Prerequisites

只有**全局管理员**才能关闭或重新激活 Azure 门户中的帐户。

## <a name="process-to-offboard"></a>处理到下架

1. 以具有**全局管理员**角色的用户身份在 Microsoft 365 设备管理 "中打开[桌面分析门户](https://aka.ms/desktopanalytics)。

1. 在**全局设置**菜单中，选择 "**连接的服务**"。 在 "注册设备" 部分中，选择 "**下架**" 选项。

1. 如果你决定继续，你的帐户将会关闭。

> [!Important]
> 90天后，请继续阅读本文的剩余部分，如果不能重新激活。
>
> 如果你想要完全关闭你的帐户而不等待90天，请首先[重置](/sccm/desktop-analytics/account-reset)你的帐户。

## <a name="reactivate"></a>$

在接下来的90天，你的组织中访问桌面分析门户的任何管理员都将看到你选择下架的通知。

全局管理员可以在90天内重新激活帐户。 若要为你的组织还原桌面分析，请选择此选项以**返回**。

## <a name="delete-the-solution"></a>删除解决方案

> [!Warning]
> 90天后，请继续阅读本文的剩余部分，如果不能重新激活。 如果删除并断开这些其他组件的连接，请不要尝试重新激活。

1. 以具有**全局管理员**角色的用户身份登录到[Azure 门户](https://portal.azure.com)。

1. 在 "**所有资源**" 中搜索桌面分析工作区的名称。 此名称是在注册服务时创建的。

1. 删除类型**解决方案**的 `Microsoft365Analytics(YourWorkspaceName)`。

桌面分析数据基于工作区的数据保留策略过期。 你可以继续使用同一工作区中的任何其他解决方案。

> [!Important]  
> 如果将 Log Analytics 工作区与 Windows Analytics 等其他解决方案一起使用，请不要删除工作区。

## <a name="remove-user-and-app-access"></a>删除用户和应用访问权限

1. 以具有**全局管理员**角色的用户身份登录到[Azure 门户](https://portal.azure.com)。 请参阅**Azure Active Directory**。

1. 在 "**角色" 和 "管理员**" 中，搜索 "**桌面分析管理员**" 角色。 删除其成员。

1. 在 "**组**" 中，删除以下组的成员：

    - **M365 Analytics 客户端管理员（Log Analytics 所有者）**
    - **M365 Analytics 客户端管理员（Log Analytics 参与者）**

1. 在 "**企业应用程序**" 中，删除或撤消对以下应用的访问权限：

    - `MaLogAnalyticsReader`

    - ConfigMgr 应用。 若要查找此应用的名称，请前往 Configuration Manager 控制台。 在 "**管理**" 工作区中，展开 "**云服务**"，然后选择 " **Azure 服务**" 节点。 打开**桌面分析**服务的属性，并切换到 "**应用程序**" 选项卡。**Web 应用**是此 Azure 应用。

        > [!Important]  
        > 在 Azure AD 中对此应用进行更改之前，请确保不会将其与 Configuration Manager 中的其他服务一起使用。

## <a name="disconnect-configuration-manager"></a>断开连接 Configuration Manager

1. 以具有**完全权限管理员**角色的用户身份打开 Configuration Manager 控制台。

1. 中转到 "**管理**" 工作区，展开 "**云服务**"，然后选择 " **Azure 服务**" 节点。

1. 删除桌面分析服务。

### <a name="delete-collections-for-the-pilot-and-production-deployments"></a>删除试点和生产部署的集合

1. 在 Configuration Manager 控制台中，选择 "**资产和符合性**" 工作区中的 "**设备集合**"。

1. 删除不再使用的所有集合。 默认情况下，集合位于 "**部署计划**" 文件夹下。  

## <a name="reconfigure-clients"></a>重新配置客户端

### <a name="unenroll-devices"></a>取消注册设备

在已注册的设备上，从以下 Windows 注册表项中删除 CommercialID 值：

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

### <a name="windows-diagnostic-data-configuration"></a>Windows 诊断数据配置

如果你不希望设备继续发送诊断数据：

- Windows 10：将诊断数据级别设置为**安全性**
- Windows 7 SP1 或8.1：禁用**商业数据选择加入密钥**

使用以下方法之一设置这些值：

- "**计算机配置**" 中的组策略  > **管理模板** > **Windows 组件** > **数据收集和预览生成**
- 移动设备管理（MDM），如[Microsoft Intune](https://docs.microsoft.com/intune/device-restrictions-windows-10#reporting-and-telemetry)

有关详细信息，请参阅[配置组织中的 Windows 诊断数据](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)。

> [!NOTE]  
> 应用这些更改后，设备会立即停止发送诊断数据。 Microsoft 可能需要24-48 小时才能停止处理工作区的见解。 Microsoft 会在30天内或更短时间内从其云服务中删除此数据。
