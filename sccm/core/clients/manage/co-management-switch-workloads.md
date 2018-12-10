---
title: 将 Configuration Manager 工作负荷切换到 Intune
titleSuffix: Configuration Manager
description: 了解如何将目前由 Configuration Manager 托管的工作负荷切换为由 Microsoft Intune 托管。
ms.prod: configuration-manager
ms.technology: configmgr-client
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.assetid: 60e2022f-a4f9-40dd-af01-9ecb37b43878
ms.openlocfilehash: 739773e83213033103b414cc9bb79f7abccb230c
ms.sourcegitcommit: 2cc635835709fb8d86cdb63ea34233b36c94d4d8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2018
ms.locfileid: "52258938"
---
# <a name="switch-configuration-manager-workloads-to-intune"></a>将 Configuration Manager 工作负荷切换到 Intune
在[准备 Windows 10 设备进行共同管理](co-management-prepare.md)中，你已准备好了 Windows 10 设备以便进行共同管理。 这些设备已加入 Azure AD（简称 AD），而且它们已在 Intune 中注册，具有 Configuration Manager 客户端。 你可能仍然具有已联接到 AD 且具有 Configuration Manager 客户端的 Windows 10 设备，但该设备未联接到 Azure AD 或在 Intune 中注册。 以下步骤介绍如何启用共同管理，准备其余的 Windows 10 设备（没有进行 Intune 注册的 Configuration Manager 客户端）进行共同管理，并允许开始将特定的 Configuration Manager 工作负荷切换到 Intune。


## <a name="switch-configuration-manager-workloads-to-intune"></a>将 Configuration Manager 工作负荷切换到 Intune

1. 在 Configuration Manager 控制台中，转到“管理” > “概述” > “云服务” > “共同管理”。    
2. 在“主页”选项卡的“管理”组中，选择“  **配置共同管理** ”以打开“共同管理配置”向导。    
3. 在“订阅”页中，单击“登录”并登录到 Intune 租户，然后单击“下一步”。   
4. 在“启用”页中，选择“试点”或“全部”，在 Intune 中启用自动注册，然后单击“下一步”。 如果选择“试点”，仅属于试点组成员的 Configuration Manager 客户端可在 Intune 中自动注册。 此选项允许对客户端子集启用共同管理，以初步测试共同管理，并使用分阶段的方式推出共同管理。 对于已在 Intune 中注册的设备，命令行可以用于将 Configuration Manager 客户端部署为 Intune 中的应用。 有关详细信息，请参阅[在 Intune 中注册的 Windows 10 设备](co-management-prepare.md#windows-10-devices-enrolled-in-intune)。
5. 在“工作负荷”页中选择是否将 Configuration Manager 工作负荷切换为由试点 Intune 或 Intune 托管，然后单击“下一步”。 “试点 Intune”设置只为试点组中的设备切换已关联工作负荷。 “Intune”设置则为所有共同管理的 Windows 10 设备切换已关联工作负荷。 
        
   > [!Important]    
   > 切换任何工作负荷之前，请确保已正确配置并部署 Intune 中的相应工作负荷。 这样做可确保工作负荷始终托管在设备的一个管理工具中。   
1. 在“暂存”页中，配置以下设置并单击“下一步”：
    - **试点**：试点组包含选定的一个或多个集合。 在分阶段推出共同管理过程中使用此组。 可从小型测试集合开始，然后随着向更多用户和设备推出共同管理，向试点组添加更多集合。 可随时在共同管理属性中更改试点组中的集合。
    - **生产**：使用一个或多个集合配置排除组。 将不对属于此组中任意集合的成员的设备使用共同管理。 
2. 要启用共同管理，请完成向导。  

<!--1357377-->自 Configuration Manager 版本 1806 起，在切换共同管理工作负荷时，共同托管的设备自动从 Microsoft Intune 同步 MDM 策略。 当从 Configuration Manager 控制台的客户端通知中启动“下载计算机策略”操作时也会进行此同步。 有关详细信息，请参阅[使用客户端通知启动客户端策略检索](/sccm/core/clients/manage/manage-clients#initiate-client-policy-retrieval-using-client-notification)。

## <a name="modify-your-co-management-settings"></a>修改你的共同管理设置
在使用向导启用共同管理后，便可修改共同管理属性中的设置。  
- 在 Configuration Manager 控制台中，转到“管理” > “概述” > “云服务” > “共同管理”。  
选择共同管理对象，然后在“主页”选项卡上单击“属性”。 

## <a name="workloads-able-to-be-transitioned-to-intune"></a>能够转换到 Intune 的工作负荷
某些工作负荷可以切换到 Intune。 当工作负荷可供转换时，系统将更新以下列表：
1. 设备合规性策略
2. 资源访问策略：资源访问策略在设备上配置 VPN、Wi-Fi、电子邮件以及证书设置。 有关详细信息，请参阅[部署资源访问配置文件](https://docs.microsoft.com/intune/device-profiles)。
      - 电子邮件配置文件
      - Wi-Fi 配置文件
      - VPN 配置文件
      - 证书配置文件
3. Windows 更新策略
4. Endpoint Protection（从 Configuration Manager 1802 版开始）
      - Windows Defender 应用程序防护
      - Windows Defender 防火墙
      - Windows Defender SmartScreen
      - Windows 加密
      - Windows Defender 攻击防护
      - Windows Defender 应用程序控制
      - Windows Defender 安全中心
      - Windows Defender 高级威胁防护
      - Windows 信息保护

5. 设备配置（自 Configuration Manager 版本 1806 起）<!--1357903-->
       - 自版本 1806 起，移动设备配置工作负荷时一并移动“资源访问”和“Endpoint Protection”工作负荷。
       - 自版本 1806 起，即使设备配置颁发机构是 Intune，你仍可将 Configuration Manager 中的设置部署到共同托管的设备。 此异常可用于配置组织所需但在 Intune 中尚不可用的设置。 在 [Configuration Manager 配置基线](/sccm/compliance/deploy-use/create-configuration-baselines.md)上指定此异常。 创建基线时，或在现有基线属性的“常规”选项卡上，启用选项“即使是共同托管客户端也要始终应用此基线”。
6. Office 365 即点即用应用（自 Configuration Manager 版本 1806 起）<!--1357841-->
       - 移动工作负荷后，设备上的“公司门户”中显示此应用。
       - Office 更新可能约在 24 小时后才在客户端上显示，除非重启设备。 
       - 存在一个新的全局条件，即“Office 365 应用程序是否在设备上由 Intune 进行托管”。 默认情况下将此条件作为一项要求添加到新的 Office 365 应用程序。 当转移此工作负荷时，共同托管客户端不满足应用程序的要求，因此不安装通过 Configuration Manager 部署的 Office 365。
7. 移动应用（自 Configuration Manager 版本 1806 起作为[预发布功能](/sccm/core/servers/manage/pre-release-features)引入）<!--1357892-->
      - 转移此工作负荷之后，任何从 Intune 部署的可用应用在公司门户中也变得可用。 
      -  从 Configuration Manager 部署的应用在软件中心可用。

## <a name="monitor-co-management"></a>监视共同管理
启用共同管理后，可以使用以下方法监视共同管理设备：

- [共同管理仪表板](/sccm/core/clients/manage/co-management-dashboard)
- **SQL 视图和 WMI 类**：可以在 Configuration Manager 站点数据库或 SMS&#95;Client&#95;ComanagementState WMI 类中查询 v&#95;ClientCoManagementState SQL 视图。 结合 WMI 类中的信息，可以在 Configuration Manager 中创建自定义集合，帮助判定共同管理部署的状态。 更多详细信息，请参阅[如何创建集合](/sccm/core/clients/manage/collections/create-collections)。 下列字段在 SQL 视图和 WMI 类中可用： 
    - **MachineId**：为 Configuration Manager 客户端指定唯一的设备 ID。
    - **MDMEnrolled**：指定设备是否注册了 MDM。 
    - **机构**：指定设备注册的机构。
    - **ComgmtPolicyPresent**：指定客户端上是否存在 Configuration Manager 共同管理策略。 如果 MDMEnrolled 值为 0，则设备未注册。 无论客户端是否存在共同管理策略，都进行共同管理。

   > [!Note]    
   > 当“MDMEnrolled”和“ComgmtPolicyPresent”字段的值都为“1”时，设备才是被共同管理的。

- **部署策略**：通过“监视” > “部署”创建两个策略，分别用于试点组和生产。 这些策略仅报告其中 Configuration Manager 应用了此策略的设备数量。 这些策略不考虑 Intune 中注册了多少设备，这是设备可实现共同管理的前提。  

## <a name="check-compliance-for-co-managed-devices"></a>检查共同管理的设备的符合性
无论条件访问是由 Intune 还是由 Configuration Manager 托管，用户都可在软件中心上检查其共同管理的 Windows 10 设备的符合性。 条件访问由 Intune 托管时，用户还可以使用公司门户应用检查符合性。

## <a name="next-steps"></a>后续步骤
以下资源可以帮助你管理切换至 Intune 的工作负荷：
- [设备合规性策略](https://docs.microsoft.com/intune/device-compliance-get-started)
- [资源访问策略](https://docs.microsoft.com/intune/device-profiles)
- [适用于企业的 Windows 更新策略](https://docs.microsoft.com/intune/windows-update-for-business-configure)
- [适用于 Microsoft Intune 的 Endpoint Protection](https://docs.microsoft.com/intune-classic/deploy-use/help-secure-windows-pcs-with-endpoint-protection-for-microsoft-intune)
