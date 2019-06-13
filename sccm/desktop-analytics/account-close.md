---
title: 如何关闭你的帐户
titleSuffix: Configuration Manager
description: 如何从 Azure 帐户中删除桌面分析
ms.date: 06/11/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6e7d2850-b0af-497e-bbc1-bfc2a7420a7a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 499d24e20b8220e685cb7aed9adea3f21caa12ae
ms.sourcegitcommit: e3c1eb0b75d79c05a750d49354c851d15d5e26a3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/13/2019
ms.locfileid: "67039738"
---
# <a name="how-to-close-your-account"></a>如何关闭你的帐户

> [!Note]  
> 此信息与商业发布之前可能有大幅度修改的预览服务。 对于此处提供的信息，Microsoft 不提供任何明示或暗示的担保。  

如果在环境中，设置 Desktop 分析并确定还需要将其删除，使用此过程来关闭你的帐户。

## <a name="contact-support"></a>请联系支持人员

第一步是与 Microsoft 支持部门联系。 打开支持案例来关闭你的桌面 Analytics 帐户。 之前不要继续执行其他步骤收到确认 Microsoft 关闭你的帐户。

## <a name="delete-the-solution"></a>删除解决方案

1. 登录到[Azure 门户](https://portal.azure.com)具有的用户身份**公司管理员**角色。

1. 在中搜索**的所有资源**Desktop 分析工作区的名称。 此名称是注册该服务时创建的内容。

1. 删除`Microsoft365Analytics(YourWorkspaceName)`类型的**解决方案**。

Desktop 分析数据会过期，根据数据保留策略工作区。 您可以继续使用同一个工作区中的任何其他解决方案。

> [!Important]  
> 如果使用 Windows Analytics 等其他解决方案的 Log Analytics 工作区，不要删除工作区。

## <a name="remove-user-and-app-access"></a>删除用户和应用的访问权限

1. 登录到[Azure 门户](https://portal.azure.com)具有的用户身份**公司管理员**角色。 转到**Azure Active Directory**。

1. 在中**角色和管理员**，搜索**Desktop 分析管理员**角色。 删除其成员。

1. 在中**组**，删除以下组的成员：

    - **M365 分析客户端管理员 （日志分析所有者）**
    - **M365 分析客户端管理员 （Log Analytics 参与者）**

1. 在中**企业应用程序**、 删除或撤消针对以下应用的访问权限：

    - `MaLogAnalyticsReader`

    - ConfigMgr 应用程序。 若要查找此应用程序的名称，请转到 Configuration Manager 控制台。 在中**Administration**工作区中，展开**云服务**，然后选择**Azure 服务**节点。 打开的属性**Desktop 分析**服务，并切换到**应用程序**选项卡。**Web 应用**是此 Azure 应用程序。

        > [!Important]  
        > 在 Azure AD 中对此应用程序进行更改之前，请确保，您不能重复使用它与另一个服务配置管理器中。

## <a name="disconnect-configuration-manager"></a>断开连接配置管理器

1. 打开 Configuration Manager 控制台以用户身份**完全权限管理员**角色。

1. 转到**Administration**工作区中，展开**云服务**，然后选择**Azure 服务**节点。

1. 删除桌面分析服务。

## <a name="reconfigure-clients"></a>重新配置客户端

### <a name="unenroll-devices"></a>取消注册设备

在已注册的设备上从以下 Windows 注册表项中删除 CommercialID 值：

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

### <a name="windows-diagnostic-data-configuration"></a>Windows 诊断数据配置

如果不希望你继续发送诊断数据的设备：

- Windows 10： 将诊断数据级别设置为**安全**
- Windows 7 SP1 或 8.1： 禁用**商业数据选择的密钥**

设置这些值使用以下方法之一：

- 在组策略，**计算机配置** > **管理模板** > **Windows 组件** >  **数据收集和预览版本**
- 移动设备管理 (MDM)，如[Microsoft Intune](https://docs.microsoft.com/intune/device-restrictions-windows-10#reporting-and-telemetry)

有关详细信息，请参阅[配置组织中的 Windows 诊断数据](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)。

> [!NOTE]  
> 当应用这些更改时，设备将立即停止发送诊断数据。 可能需要 24-48 小时，microsoft 将停止处理你的工作区的见解。 在 30 天或更少 Microsoft 从其云服务中删除此数据。
