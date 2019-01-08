---
title: 将 Configuration Manager 工作负荷切换到 Intune
titleSuffix: Configuration Manager
description: 了解如何将目前由 Configuration Manager 托管的工作负荷切换为由 Microsoft Intune 托管。
ms.prod: configuration-manager
ms.technology: configmgr-client
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 12/10/2018
ms.topic: conceptual
ms.assetid: 60e2022f-a4f9-40dd-af01-9ecb37b43878
ms.openlocfilehash: e3bd3bfda92fb877bac3ca68dbecf8b4a4078d4d
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2018
ms.locfileid: "53416939"
---
# <a name="switch-configuration-manager-workloads-to-intune"></a>将 Configuration Manager 工作负荷切换到 Intune

在[准备 Windows 10 设备进行共同管理](/sccm/core/clients/manage/co-management-prepare)之后，下一步是启用自动客户端注册到 Intune。 准备好之后，开始将特定的 Configuration Manager 工作负荷切换到 Intune。 


## <a name="setup-co-management"></a>安装共同管理

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“云服务”，然后选择“共同管理”节点。  

2. 在功能区的“主页”选项卡上，在“管理”组中，选择“配置共同管理” ****。 此操作将打开共同管理配置向导。  

3. 在“订阅”页上，选择“登录”。 登录到你的 Intune 租户，然后选择“下一步”。  

4. 在“启用”页面上，选择“试点”或“全部”。  

    此操作可在 Intune 中启用自动客户端注册。 如果选择“试点”，仅属于试点集合成员的 Configuration Manager 客户端才会自动注册到 Intune。 此选项允许对客户端子集启用共同管理，以初步测试共同管理，并使用分阶段的方式推出共同管理。  

    对于已在 Intune 中注册的设备，使用显示的命令行将 Configuration Manager 客户端部署为 Intune 中的应用。 有关详细信息，请参阅[在 Intune 中注册的 Windows 10 设备](/sccm/core/clients/manage/co-management-prepare#windows-10-devices-enrolled-in-intune)。  

5. 在“工作负荷”页面中，选择是否将 Configuration Manager 工作负荷切换为由 Intune 托管。 你可以在上一页面上启用注册，而无需在此时切换任何工作负荷。 

    “试点 Intune”设置只为试点集合中的设备切换已关联工作负荷。 “Intune”设置则为所有共同管理的 Windows 10 设备切换已关联工作负荷。  

    > [!Important] 
    > 切换任何工作负荷之前，请确保在 Intune 中正确配置并部署相应的工作负荷。 请确保工作负荷始终由设备的某个管理工具进行托管。  

6. 在“暂存”页上，请配置下列设置：  

    - **试点**：试点组包含选定的一个或多个集合。 在分阶段推出共同管理过程中使用此组。 从小型测试集合开始，然后随着向更多用户和设备推出共同管理，向试点组添加更多集合。 可随时更改试点组中的集合。  

    - **生产**：使用一个或多个集合配置排除组。 将不对属于此组中任意集合的成员的设备使用共同管理。  

7. 要启用共同管理，请完成向导。  

<!--1357377-->自 Configuration Manager 版本 1806 起，在切换共同管理工作负荷时，共同托管的设备自动从 Microsoft Intune 同步 MDM 策略。 当从 Configuration Manager 控制台的客户端通知中启动“下载计算机策略”操作时也会进行此同步。 有关详细信息，请参阅[使用客户端通知启动客户端策略检索](/sccm/core/clients/manage/manage-clients#initiate-client-policy-retrieval-using-client-notification)。



## <a name="modify-your-co-management-settings"></a>修改你的共同管理设置

在使用向导启用共同管理后，请修改共同管理属性中的设置。 在 Configuration Manager 控制台中，转到“管理”工作区，展开“云服务”，然后选择“共同管理”节点。 选择共同管理对象，然后选择功能区中的“属性”。 



## <a name="supported-workloads"></a>支持的工作负荷

当前可以将以下工作负荷从 Configuration Manager 切换到 Intune：

- **设备合规性策略**  

- **资源访问策略**：有关这些 Intune 策略的详细信息，请参阅[部署资源访问配置文件](https://docs.microsoft.com/intune/device-profiles)。
    - 电子邮件配置文件  
    - Wi-Fi 配置文件  
    - VPN 配置文件  
    - 证书配置文件  

- **Windows 更新策略**  

- **Endpoint Protection**：从 Configuration Manager 版本 1802 开始，此工作负荷包含以下功能：  
    - Windows Defender 应用程序防护  
    - Windows Defender 防火墙  
    - Windows Defender SmartScreen  
    - Windows 加密  
    - Windows Defender 攻击防护  
    - Windows Defender 应用程序控制  
    - Windows Defender 安全中心  
    - Windows Defender 高级威胁防护  
    - Windows 信息保护  

- **设备配置**：从 Configuration Manager 版本 1806 开始<!--1357903-->：  

    - 移动设备配置工作负荷时一并移动“资源访问”和“Endpoint Protection”工作负荷  

    - 即使设备配置颁发机构是 Intune，你仍可将 Configuration Manager 中的设置部署到共同托管的设备。 此异常可用于配置组织所需但在 Intune 中尚不可用的设置。 在 [Configuration Manager 配置基线](/sccm/compliance/deploy-use/create-configuration-baselines)上指定此异常。 创建基线时，或在现有基线属性的“常规”选项卡上，启用选项“即使是共同托管客户端也要始终应用此基线”。  

- **Office 365 即点即用应用**：从 Configuration Manager 版本 1806 开始<!--1357841-->：  

    - 移动工作负荷后，此应用将显示在设备上的“公司门户”中  

    - 除非重启设备，否则 Office 更新可能约在 24 小时后才能显示在客户端上  

    - 存在一个新的全局条件，即“Office 365 应用程序是否在设备上由 Intune 进行托管”。 默认情况下将此条件作为一项要求添加到新的 Office 365 应用程序。 如果在转换此工作负荷时，共同托管客户端不满足应用程序的要求。 则不会安装通过 Configuration Manager 部署的 Office 365。  

- **客户端应用**：从 Configuration Manager 版本 1806 开始，作为[预发布功能](/sccm/core/servers/manage/pre-release-features)）<!--1357892-->：  

    - 转换此工作负荷之后，在公司门户中也可使用任何从 Intune 部署的可用应用  

    - 可在软件中心使用从 Configuration Manager 部署的应用  



## <a name="monitor-co-management"></a>监视共同管理

启用共同管理后，请使用以下方法监视共同管理设备：

- [共同管理仪表板](/sccm/core/clients/manage/co-management-dashboard)  

- **SQL 视图和 WMI 类**：查询 Configuration Manager 站点数据库中的“v_ClientCoManagementState”SQL 视图或“SMS_Client_ComanagementState”WMI 类。 结合 WMI 类中的信息，可以在 Configuration Manager 中创建自定义集合，帮助判定共同管理部署的状态。 更多详细信息，请参阅[如何创建集合](/sccm/core/clients/manage/collections/create-collections)。 下列字段在 SQL 视图和 WMI 类中可用：  
  - **MachineId**：为 Configuration Manager 客户端指定唯一的设备 ID  
  - **MDMEnrolled**：指定设备是否注册了 MDM  
  - **机构**：指定设备注册的机构  
  - **ComgmtPolicyPresent**：指定客户端上是否存在 Configuration Manager 共同管理策略。 如果“MDMEnrolled”值是“0”，则无论客户端是否存在共同管理策略，该设备都不会进行共同管理。  

    > [!Note]  
    > 当“MDMEnrolled”和“ComgmtPolicyPresent”字段的值都为“1”时，设备才是被共同管理的。  

- **部署策略**：在“监视”工作区的“部署”节点中创建了两个策略。 一个策略用于试点组，另一个策略用于生产。 这些策略仅报告其中 Configuration Manager 应用了此策略的设备数量。 这些策略不考虑 Intune 中注册了多少设备，这是设备可实现共同管理的前提。  



## <a name="check-compliance-for-co-managed-devices"></a>检查共同管理的设备的符合性

无论条件访问是由 Intune 还是由 Configuration Manager 托管，用户都可在软件中心上检查其共同管理的 Windows 10 设备的符合性。 条件访问由 Intune 托管时，用户还可以使用公司门户应用检查符合性。



## <a name="next-steps"></a>后续步骤

以下资源可以帮助你管理切换至 Intune 的工作负荷：
- [设备合规性策略](https://docs.microsoft.com/intune/device-compliance-get-started)
- [资源访问策略](https://docs.microsoft.com/intune/device-profiles)
- [适用于企业的 Windows 更新策略](https://docs.microsoft.com/intune/windows-update-for-business-configure)
- [适用于 Microsoft Intune 的 Endpoint Protection](https://docs.microsoft.com/intune-classic/deploy-use/help-secure-windows-pcs-with-endpoint-protection-for-microsoft-intune)
