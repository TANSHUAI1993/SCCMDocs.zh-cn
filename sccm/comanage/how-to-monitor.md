---
title: 监视共同管理
titleSuffix: Configuration Manager
description: 使用共同管理仪表板查看有关共同管理的设备的信息。
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e83a7b0d-b381-4b4a-8eca-850385abbebb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7c731692bc2277cc5ce97e079387b392ca09ff3e
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754695"
---
# <a name="how-to-monitor-co-management-in-configuration-manager"></a>如何监视 Configuration Manager 中的共同管理

适用范围：System Center Configuration Manager (Current Branch)


启用共同管理后，请使用以下方法监视共同管理设备：

- [共同管理面板](#co-management-dashboard)  

- [部署策略](#deployment-policies)

- [WMI 设备数据](#wmi-device-data)



## <a name="co-management-dashboard"></a>共同管理仪表板

从版本 1802 开始，可查看含共同管理相关信息的仪表板。 此仪表板可帮助你查看环境中共同管理的计算机。 图表有助于标识可能需要注意的设备。<!--1356648-->

在 Configuration Manager 控制台中，转到“监视”工作区，然后选择“共同管理”节点。

自版本 1810 开始，通过在共同管理仪表板中增加了更多详细信息，共同管理仪表板的功能得到了增强。 <!--1358980-->

![共同管理仪表板的屏幕截图](media/co-management-dashboard.png)


### <a name="co-managed-devices"></a>共同管理的设备

适用于 1802 和 1806 两个版本

显示整个环境中共同管理的设备所占的百分比。

![共同托管的设备磁贴](media/co-management-dashboard/Percent-Co-managed-graph.PNG)


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

![共同管理状态 （圆环图） 磁贴](media/co-management-dashboard/Co-management-status-graph.PNG)

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

在该磁贴中选择一种状态，即可深入查看相关状态的设备列表。  

![共同管理注册状态磁贴](media/co-management-dashboard/1358980-enrollment-status.png)


### <a name="workload-transition"></a>工作负荷转换

适用于所有版本

显示一个条形图，其中包含为可用工作负荷而转换为 Microsoft Intune 的设备数量。 

工作负荷列表由 Configuration Manager 的版本而异。 有关详细信息，请参阅[能够转换到 Intune 的工作负荷](/sccm/comanage/workloads)。

将鼠标悬停在图表某个部分上方可显示为该工作负荷转换的设备的数量。 

![工作负荷转换条形图](media/co-management-dashboard/Workload-Transition.PNG)


### <a name="enrollment-errors"></a>注册错误

适用于 1810 和更高版本

此表是从设备注册错误的列表。 这些错误可能来自 Windows、 Windows 操作系统的核心或 Configuration Manager 客户端中的 MDM 组件。 

有数百个可能的错误。 下表列出了最常见的错误。
<!-- SCCMDocs issue 1064, BUG 3158555 -->

| 错误 | 描述 |
|---------|---------|
| 2147549183 (0x8000FFFF) | MDM 注册未配置尚未在 Azure AD，或 URL 不应的注册。<br><br>[启用 Windows 10 自动注册](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment) |
| 2149056536 (0x80180018)<br>MENROLL_E_USERLICENSE | 用户的许可证处于错误状态阻止注册<br><br>[向用户分配许可证](https://docs.microsoft.com/intune/licenses-assign) |
| 2149056555 (0x8018002B)<br>MENROLL_E_MDM_NOT_CONFIGURED | 当不是完全应用尝试自动注册到 Intune，但 Azure AD 配置。 此问题应该是暂时的作为在短时间后设备重试。 |
| 2149056554 (0x‭8018002A‬)<br>&nbsp; | 用户取消了操作<br><br>如果 MDM 注册要求多重身份验证，并且用户未登录的受支持的第二个因素，Windows 将为用户注册显示 toast 通知。 如果用户不会做出响应，向 toast 通知，出现此错误。 此问题应该是暂时的因为 Configuration Manager 将重试，并提示用户。 登录到 Windows 时，用户应使用多重身份验证。 此外指导他们需要此行为，如果系统提示，请采取措施。 | 
| 2149056533 (0x80180015)<br>MENROLL_E_NOTSUPPORTED | 通常不支持的移动设备管理 | 
| 2149056514 (0x80180002)<br>MENROLL_E_DEVICE_AUTHENTICATION_ERROR | 服务器无法对用户进行身份验证<br><br> 用户没有 Azure AD 令牌。 请确保用户能够进行 Azure AD 身份验证。 |
| 2147942450 (0x‭80070032‬)<br>&nbsp; | MDM 自动注册仅支持 Windows rs3 及更高版本。<br><br>请确保设备满足[最低要求](/sccm/comanage/overview#windows-10)进行共同管理。 |
| 3400073293 | ADAL 用户领域帐户响应未知<br><br>检查 Azure AD 配置，并确保用户已成功进行身份验证。 | 
| 3399548929 | 需要用户登录<br><br>此问题应该是暂时性的。 便会出现用户快速注销之前注册任务会发生。 | 
| 3400073236 | ADAL 安全令牌请求失败。<br><br>检查 Azure AD 配置，并确保用户已成功进行身份验证。 |
| 2149122477 | 泛型 HTTP 问题 |
| 3400073247 | ADAL 集成 Windows 身份验证仅支持在流中联合<br><br>[规划混合 Azure Active Directory 联接实现](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan) | 
| 3399942148 | 找不到服务器或代理。<br><br>当客户端不能与云通信时，应暂时的此问题。 如果仍存在，请确保客户端已一致连接到 Azure。 | 
| 2149056532 | 不支持特定平台或版本<br><br>请确保设备满足[最低要求](/sccm/comanage/overview#windows-10)进行共同管理。 |
| 2147943568 | 找不到元素<br><br>此问题应该是暂时性的。 如果仍存在，请联系 Microsoft 支持部门。 |
| 2192179208 | 没有足够的内存资源是可用于处理此命令。<br><br>此问题应该是暂时性的它应会自动解决时客户端将重试。 |
| 3399614467 | ADAL 授权授予对此断言失败<br><br>检查 Azure AD 配置，并确保用户已成功进行身份验证。 |
| 2149056517 | 从管理服务器，如数据库访问权限错误的一般失败<br><br>此问题应该是暂时性的。 如果仍存在，请联系 Microsoft 支持部门。 |
| 2149134055 | Winhttp 名称无法解析<br><br>客户端无法解析服务的名称。 检查 DNS 配置。 | 
| 2149134050 | internet 超时<br><br>当客户端不能与云通信时，应暂时的此问题。 如果仍存在，请确保客户端已一致连接到 Azure。 | 


有关详细信息，请参阅[MDM 注册错误值](https://docs.microsoft.com/windows/desktop/mdmreg/mdm-registration-constants)。



## <a name="deployment-policies"></a>部署策略

在“监视”工作区的“部署”节点中创建了两个策略。 一个策略用于试点组，另一个策略用于生产。 这些策略仅报告其中 Configuration Manager 应用了此策略的设备数量。 这些策略不考虑 Intune 中注册了多少设备，这是设备可实现共同管理的前提。  



## <a name="wmi-device-data"></a>WMI 设备数据

查询**SMS_Client_ComanagementState** WMI 类。 您可以创建自定义集合在配置管理器中，可帮助确定共同管理部署的状态。 有关创建自定义集合的详细信息，请参阅[如何创建集合](/sccm/core/clients/manage/collections/create-collections)。 

WMI 类中提供了以下字段：  

- **MachineId**：Configuration Manager 客户端的唯一设备 ID  

- **MDMEnrolled**：指定设备是否注册了 MDM  

- **机构**：设备注册为其颁发机构  

- **ComgmtPolicyPresent**：指定客户端上是否存在 Configuration Manager 共同管理策略。 如果“MDMEnrolled”值是“0”，则无论客户端是否存在共同管理策略，该设备都不会进行共同管理。  

当“MDMEnrolled”和“ComgmtPolicyPresent”字段的值都为“1”时，设备才是被共同管理的。  
