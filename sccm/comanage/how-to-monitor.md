---
title: 监视共同管理
titleSuffix: Configuration Manager
description: 使用共同管理仪表板查看有关共同管理的设备的信息。
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e83a7b0d-b381-4b4a-8eca-850385abbebb
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 35ae9ca2a4ec42dab6302f0473a10b4c57ae1741
ms.sourcegitcommit: 72faa1266b31849ce1a23d661a1620b01e94f517
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/26/2019
ms.locfileid: "68535003"
---
# <a name="how-to-monitor-co-management-in-configuration-manager"></a>如何监视 Configuration Manager 中的共同管理

适用范围：  System Center Configuration Manager (Current Branch)

启用共同管理后，请使用以下方法监视共同管理设备：

- [共同管理面板](#co-management-dashboard)  

- [部署策略](#deployment-policies)

- [WMI 设备数据](#wmi-device-data)

## <a name="co-management-dashboard"></a>共同管理仪表板

从版本 1802 开始，可查看含共同管理相关信息的仪表板。 此仪表板可帮助你查看环境中共同管理的计算机。 图形有助于标识可能需要注意的设备。<!--1356648-->

在 Configuration Manager 控制台中，转到“监视”工作区，然后选择“共同管理”节点   。

自版本 1810 开始，通过在共同管理仪表板中增加了更多详细信息，共同管理仪表板的功能得到了增强。 <!--1358980-->

![共同管理仪表板的屏幕截图](media/co-management-dashboard.png)

### <a name="co-managed-devices"></a>共同管理的设备

适用于 1802 和 1806 两个版本 

显示整个环境中共同管理的设备所占的百分比。

![共同管理的设备磁贴](media/co-management-dashboard/Percent-Co-managed-graph.PNG)

### <a name="client-os-distribution"></a>客户端 OS 分发

适用于所有版本  

按版本显示每个 OS 的客户端设备数量。 使用以下分组：  

- Windows 7 和 8.x
- Windows 10 1709 以下版本  
- Windows 10 1709 及更高版本  

    > [!Tip]  
    > Windows 10 1709 及更高版本是共同管理的先决条件。  

将鼠标悬停在图表的某个部分上方可显示该 OS 组中设备所占的百分比。

![客户端 OS 分发磁贴](media/co-management-dashboard/Co-management-OS-distribution-graph.PNG)

### <a name="co-management-status-donut"></a>共同管理状态（圆环图）

适用于 1802 和 1806 两个版本 

显示以下类别中设备成功或失败的细目：

- 成功，已联接混合 Azure AD
- 成功，已联接 Azure AD  
- 失败：自动注册失败  

将鼠标悬停在图表的某个部分上可显示该类别中设备所占的百分比。

![共同管理状态（圆环图）磁贴](media/co-management-dashboard/Co-management-status-graph.PNG)

选择图中某个部分可查看该类别的设备列表。

![注册失败设备列表](media/co-management-dashboard/Enrollment-Failure_Device-List.PNG)

### <a name="co-management-status-funnel"></a>共同管理状态（漏斗图）

适用于 1810 和更高版本 

漏斗图，显示注册过程中具有以下状态的设备的数量：
  
- 符合条件的设备
- 已计划  
- 已启动注册  
- 已注册  

![共同管理状态（漏斗图）磁贴](media/co-management-dashboard/1358980-status-funnel.png)

### <a name="co-management-enrollment-status"></a>共同管理注册状态

适用于 1810 和更高版本 

显示以下类别中设备状态的细目：

- 成功，已联接混合 Azure AD  
- 成功，已联接 Azure AD  
- 正在注册，已联接混合 Azure AD  
- 失败，已联接混合 Azure AD  
- 失败，已联接 Azure AD  
- 挂起用户登录  

    > [!Note]  
    > 从版本 1906 开始，若要减少处于挂起状态的设备数，新的共同管理设备现可根据其 Azure AD 设备令牌自动注册到 Microsoft Intune 服务  。 无需等待用户登录到设备，就能启动自动注册。 为支持此行为，设备需要运行 Windows 10 版本 1803 或更高版本。
    >
    > 如果设备令牌出现故障，它会使用用户令牌回退到上一行为。 在 ComanagementHandler.log 中查找以下条目  ：`Enrolling device with RegisterDeviceWithManagementUsingAADDeviceCredentials`

在该磁贴中选择一种状态，即可深入查看相关状态的设备列表。  

![共同管理注册状态磁贴](media/co-management-dashboard/1358980-enrollment-status.png)


### <a name="workload-transition"></a>工作负荷转换

适用于所有版本 

显示一个条形图，其中包含为可用工作负荷而转换为 Microsoft Intune 的设备数量。

工作负载列表因 Configuration Manager 的版本而异。 有关详细信息，请参阅[能够转换到 Intune 的工作负荷](/sccm/comanage/workloads)。

将鼠标悬停在图表某个部分上方可显示为该工作负荷转换的设备的数量。 

![工作负载转换条形图](media/co-management-dashboard/Workload-Transition.PNG)


### <a name="enrollment-errors"></a>注册错误

适用于 1810 和更高版本 

此表是设备的注册错误列表。 这些错误可能来自 Windows 中的 MDM 组件、核心 Windows 操作系统或 Configuration Manager 客户端。

有数百种可能的错误。 下表列出了最常见的错误。
<!-- SCCMDocs issue 1064, BUG 3158555 -->

| 错误 | 说明 |
|---------|---------|
| 2147549183 (0x8000FFFF) | 尚未在 Azure AD 上配置 MDM 注册，或者出现非预期的注册 URL。<br><br>[启用 Windows 10 自动注册](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment) |
| 2149056536 (0x80180018)<br>MENROLL_E_USERLICENSE | 用户许可证处于错误状态，阻止注册<br><br>[向用户分配许可证](https://docs.microsoft.com/intune/licenses-assign) |
| 2149056555 (0x8018002B)<br>MENROLL_E_MDM_NOT_CONFIGURED | 尝试自动注册到 Intune，但 Azure AD 配置未完全应用。 此问题应该是暂时性的，因为设备会在短时间后重试。 |
| 2149056554 (0x‭8018002A‬)<br>&nbsp; | 用户已取消操作<br><br>如果 MDM 注册需要多重身份验证，并且用户尚未使用受支持的第二因素登录，则 Windows 会向用户显示要注册的 toast 通知。 如果用户未响应 toast 通知，则会发生此错误。 此问题应该是暂时性的，因为 Configuration Manager 将重试并提示用户。 当用户登录 Windows 时应使用多重身份验证。 此外，指示用户预期会发生这一行为，如果出现提示，则采取措施。 | 
| 2149056533 (0x80180015)<br>MENROLL_E_NOTSUPPORTED | 通常不支持移动设备管理 | 
| 2149056514 (0x80180002)<br>MENROLL_E_DEVICE_AUTHENTICATION_ERROR | 服务器未能对用户进行身份验证<br><br> 用户没有 Azure AD 令牌。 确保用户可以对 Azure AD 进行身份验证。 |
| 2147942450 (0x‭80070032‬)<br>&nbsp; | 仅在 Windows RS3 及更高版本上支持 MDM 自动注册。<br><br>确保设备满足共同管理的[最低要求](/sccm/comanage/overview#windows-10)。 |
| 3400073293 | ADAL 用户领域帐户响应未知<br><br>检查 Azure AD 配置，并确保用户成功进行身份验证。 | 
| 3399548929 | 需要用户登录<br><br>此问题应该是暂时性的。 如果用户在注册任务发生之前快速注销，就会发生该问题。 | 
| 3400073236 | ADAL 安全令牌请求失败。<br><br>检查 Azure AD 配置，并确保用户成功进行身份验证。 |
| 2149122477 | 泛型 HTTP 问题 |
| 3400073247 | 仅在联合流中支持集成 ADAL 的 Windows 身份验证<br><br>[规划混合 Azure Active Directory 联接实现](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan) | 
| 3399942148 | 找不到服务器或代理。<br><br>如果客户端无法与云通信，此问题应该是暂时性的。 如果它仍然存在，请确保客户端与 Azure 具有一致的连接。 | 
| 2149056532 | 不支持特定平台或版本<br><br>确保设备满足共同管理的[最低要求](/sccm/comanage/overview#windows-10)。 |
| 2147943568 | 找不到元素<br><br>此问题应该是暂时性的。 如果问题持续出现，请与 Microsoft 支持部门联系。 |
| 2192179208 | 内存资源不足，无法处理此命令。<br><br>此问题应该是暂时性的，它应该会在客户端重试时自行解决。 |
| 3399614467 | 此断言的 ADAL 授权授予失败<br><br>检查 Azure AD 配置，并确保用户成功进行身份验证。 |
| 2149056517 | 管理服务器的一般故障，例如 DB 访问错误<br><br>此问题应该是暂时性的。 如果问题持续出现，请与 Microsoft 支持部门联系。 |
| 2149134055 | Winhttp 名称未解析<br><br>客户端无法解析服务的名称。 检查 DNS 配置。 | 
| 2149134050 | Internet 超时<br><br>如果客户端无法与云通信，此问题应该是暂时性的。 如果它仍然存在，请确保客户端与 Azure 具有一致的连接。 |

有关详细信息，请参阅 [MDM 注册错误值](https://docs.microsoft.com/windows/desktop/mdmreg/mdm-registration-constants)。

## <a name="deployment-policies"></a>部署策略

在“监视”工作区的“部署”节点中创建了两个策略   。 一个策略用于试点组，另一个策略用于生产。 这些策略仅报告其中 Configuration Manager 应用了此策略的设备数量。 这些策略不考虑 Intune 中注册了多少设备，这是设备可实现共同管理的前提。  

生产策略 (CoMgmtSettingsProd) 定目标到“所有系统”  集合。 它有检查 OS 类型和版本的适用性条件。 如果客户端是服务器 OS 或不是 Windows 10，那么策略就不适用，且不会执行任何操作。

## <a name="wmi-device-data"></a>WMI 设备数据

查询 SMS_Client_ComanagementState  WMI 类。 可以在 Configuration Manager 中创建自定义集合，帮助确定共同管理部署的状态。 有关创建自定义集合的详细信息，请参阅[如何创建集合](/sccm/core/clients/manage/collections/create-collections)。

下列字段在 WMI 类中可用：  

- **MachineId**：Configuration Manager 客户端的唯一设备 ID  

- **MDMEnrolled**：指定设备是否注册了 MDM  

- **机构**：设备注册的机构  

- **ComgmtPolicyPresent**：指定客户端上是否存在 Configuration Manager 共同管理策略。 如果“MDMEnrolled”值是“0”，则无论客户端是否存在共同管理策略，该设备都不会进行共同管理   。  

当“MDMEnrolled”和“ComgmtPolicyPresent”字段的值都为“1”时，设备才是被共同管理的    。  
