---
title: Technical Preview 1710 | Microsoft 文档
titleSuffix: Configuration Manager
description: 了解适用于 System Center Configuration Manager 的 Technical Preview 版本 1710 中的可用功能。
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: f4706a58-1f11-4eab-b1eb-3d1a0da02d0f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: e668baafac94dfc7da5008c37556c017c5e01c9d
ms.sourcegitcommit: 3936b869d226cea41fa0090e2cbc92bd530db03a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2019
ms.locfileid: "67286110"
---
# <a name="capabilities-in-technical-preview-1710-for-system-center-configuration-manager"></a>System Center Configuration Manager Technical Preview 1710 中的功能

适用范围：  System Center Configuration Manager（技术预览版）

本文介绍了 System Center Configuration Manager Technical Preview（版本 1710）中的可用功能。 你可以安装此版本，以更新 Technical Preview 站点的功能并向其添加新功能。 在安装此 Technical Preview 前，请查看 [System Center Configuration Manager 的 Technical Preview](../../core/get-started/technical-preview.md)，熟悉使用 Technical Preview 的常规要求和限制，如何在两版本之间进行更新，以及如何对 Technical Preview 中的有关功能提供反馈。     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**此 Technical Preview 中的已知问题：**
- **支持 Windows 10 版本 1709（也称为 Fall Creators Update）** 。  从此 Windows 版本开始，Windows Media 包括多个版本。 在配置用于使用操作系统升级包或操作系统映像的任务序列时，请务必选择[支持供 Configuration Manager 使用的版本](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client)。
- 如果站点服务器处于被动模式，则无法更新到新的预览版本  。 如果运行的是[主站点服务器处于被动模式](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability)的预览版本，则必须先卸载被动模式站点服务器，然后才能将预览站点成功更新到此新版本。 可以在站点完成更新后，重新安装被动模式站点服务器。

  若要卸载被动模式站点服务器，请执行以下操作：
  1. 在控制台中，依次转到“管理”   > “概述”   > “站点配置”   > “服务器和站点系统角色”  ，再选择被动模式站点服务器。
  2. 在“站点系统角色”  窗格中，右键单击“站点服务器”  角色，再选择“删除角色”  。
  3. 右键单击被动模式站点服务器，再选择“删除”  。
  4. 卸载站点服务器后，在处于主动模式的主站点服务器上重启服务 CONFIGURATION_MANAGER_UPDATE  。

**以下是此版本可以试用的新功能。**  

<!--  Section Template
##  FEATURE
### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improvements-for-deploying-powershell-scripts-from-configuration-manager"></a>针对从 Configuration Manager 部署 PowerShell 脚本的改进
在此版本中，现在部署的 PowerShell 脚本支持使用以下改进： 
- **安全作用域**。  脚本现在使用安全作用域来控制脚本创作和执行。 这是通过分配代表用户组的标记来完成的。 有关使用安全作用域的详细信息，请参阅[为 System Center Configuration Manager 配置基于角色的管理](../../core/servers/deploy/configure/configure-role-based-administration.md)。
- **实时监视**。 监视中的脚本运行状态和脚本运行的实时状态同步。
- **参数验证**。 脚本中的每一个参数都有一个“脚本参数属性”对话框，可以在此处添加该参数的验证信息  。 添加验证信息后，如果为参数输入了和验证不符的值，那么将收到错误消息。

PowerShell 脚本部署首次在 Technical Preview[ Tech Preview 1706](/sccm/core/get-started/capabilities-in-technical-preview-1706#create-and-run-powershell-scripts-from-the-configuration-manager-console) 中引入。 在 [Tech Preview 1707](/sccm/core/get-started/capabilities-in-technical-preview-1707#add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager) 和之后的 [Tech Preview 1708](/sccm/core/get-started/capabilities-in-technical-preview-1708#improvements-for-specifying-script-parameters-when-you-deploy-powershell-scripts-from-configuration-manager) 中提供了其他改进。


### <a name="try-it-out"></a>试试看！

若要尝试使用运行脚本功能，请参阅[创建并运行脚本](../../apps/deploy-use/create-deploy-scripts.md)。



## <a name="limit-windows-10-enhanced-telemetry-to-only-send-data-relevant-to-windows-analytics-device-health"></a>限制 Windows 10 增强遥测只发送与 Windows Analytics 设备运行状况相关的数据
<!-- 1356148 -->

在此版本中，现在可以将 Windows 10 遥测数据收集级别设置为“增强(受限)”  。 该设置使你能够在环境中获得对设备的可操作见解，而无需设备通过 Windows 10 版本 1709 或更高版本报告“增强”  遥测级别的所有数据。

“增强(受限)”遥测级别包括来自基本级别的指标，以及从与 Windows Analytics 相关的“增强”级别中收集的数据子集。  有关遥测级别的详细信息，请参阅[遥测级别](/windows/privacy/configure-windows-diagnostic-data-in-your-organization#use-group-policy-to-set-the-diagnostic-data-level)。

### <a name="try-it-out"></a>试试看！
若要在客户端上配置 Windows 10 遥测收集，请参阅[如何配置客户端设置](/sccm/core/clients/deploy/configure-client-settings)。 打开“云服务”  窗口，并将 Windows 10 遥测设置为“增强”  。


## <a name="software-center-no-longer-distorts-icons-larger-than-250x250"></a>软件中心不会再使大于 250 x 250 的图标失真  
<!-- 1356194 -->

在此版本中，软件中心不会再使大于 250 x 250 的图标失真。 软件中心曾使此类图标看起来很模糊。 现在图标的像素大小最大可设置为 512 x 512，并在显示时不会失真。

### <a name="try-it-out"></a>试试看！
在软件中心添加你的应用图标。 若要试用，请参阅[创建应用程序](/sccm/apps/deploy-use/create-applications)。


## <a name="check-compliance-from-software-center-for-co-managed-devices"></a>检查软件中心中共同托管的设备的符合性
<!-- 1356374 -->
在此版本中，用户可以使用软件中心来检查其共同托管的 Windows 10 设备的符合性，即使条件访问由 Intune 托管也同样适用。 有关详细信息，请参阅[适用于 Windows 10 设备的共同管理](./capabilities-in-technical-preview-1709.md#co-management-for-windows-10-devices)。


## <a name="support-for-exploit-guard"></a>对攻击防护的支持
此版本添加了对 Windows Defender 攻击防护的支持。 可以配置和部署策略，用于管理攻击防护的所有四个组件。 这些组件包括：
-   攻击面减少
-   受控文件夹访问权限
-   Exploit Protection
-   网络保护

从 Configuration Manager 控制台中可以获得攻击防护策略部署的符合性数据。

有关攻击防护和特定组件及规则的详细信息，请参阅 Windows 文档库中的 [Windows Defender 攻击防护](https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/windows-defender-exploit-guard)。

### <a name="prerequisites"></a>先决条件
托管的设备必须运行 Windows 10 1709 Fall Creators Update 或更高版本并满足以下要求，具体要取决于配置的组件和规则：

|攻击防护组件 |其他先决条件|
|------------------------|------------------------|
| 攻击面减少  | 设备必须启用 [Windows Defender AV 实时保护]( https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard)。  |
| 受控文件夹访问权限  | 设备必须启用 [Windows Defender AV 实时保护]( https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard)。   |
| Exploit Protection  | 无  |
| 网络保护  |  设备必须启用 [Windows Defender AV 实时保护]( https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard)。  |

### <a name="create-an-exploit-guard-policy----1355468---"></a>创建攻击防护策略  <!--1355468 -->
1. 在 Configuration Manager 控制台中，转到“资产和符合性”   > “Endpoint Protection”  ，然后单击“Windows Defender 攻击防护”  。
2. 在“主页”  选项卡上的“创建”  组中，单击“创建攻击策略”  。
3. 在“创建配置项目向导”  的“常规”  页面上，指定配置项目的名称和可选描述。
4. 接下来，选择你想要通过此策略管理的攻击防护组件。 然后，对于你选择的每个组件，可以配置更多详细信息。
   - **攻击面减少：** 配置想要阻止或审核的 Office 威胁、脚本威胁和电子邮件威胁。 此外，还可以从该规则中排除特定文件或文件夹。
   - **受控文件夹访问权限：** 配置阻止或审核，然后添加可绕过此策略的应用。  另外，还可以指定默认情况下未受保护的其他文件夹。
   - **Exploit Protection：** 指定一个 XML 文件，其中包含用于缓解对系统进程和应用攻击的设置。 可以在 Windows 10 设备上，从 Windows Defender 安全中心应用导出这些设置。
   - **网络保护：** 设置网络保护以阻止或审核对可疑域的访问。
5. 完成向导以创建策略，可稍后将该策略部署到设备。

### <a name="deploy-an-exploit-guard-policy"></a>部署攻击防护策略     
创建攻击防护策略后，使用“部署攻击防护策略”向导对其进行部署。 若要执行此操作，打开 Configuration Manager 控制台，进入“资产和符合性”   > “Endpoint Protection”  ，然后单击“部署攻击防护策略”  。

## <a name="limited-support-for-cng-certificates"></a>对 CNG 证书的有限支持
<!-- 1356191 -->
从此版本开始，现在可以使用[加密 API：下一代加密技术 (CNG)](https://msdn.microsoft.com/library/windows/desktop/bb204775.aspx) 证书模板用于以下方案：

- 客户端注册和与 HTTPS 管理点的通信。   
- 使用 HTTPS 分发点的软件分发和应用程序部署。   
- 操作系统部署。  
- 客户端消息 SDK（具有最新更新）和 ISV 代理。   
- 云管理网关配置。  

若要使用 CNG 证书，证书颁发机构 (CA) 需要为目标计算机提供 CNG 证书模板。  模板详细信息因场景而异；但是，还需要提供以下属性：

- “兼容性”  选项卡

    - “证书颁发机构”  必须是 Windows Server 2008 或更高版本。 （建议使用 Windows Server 2012）。

    - “证书接收者”  必须是 Windows Vista/Server 2008 或更高版本。 （建议使用 Windows 8/Windows Server 2012）。

- “加密”  选项卡

    - “提供程序类别”  必须是“密钥存储提供者”  。  （必需）

为获得最佳结果，我们建议从 Active Directory 信息中生成“使用者名称”。  使用“使用者名称格式”  的 DNS 名称，并在另一个使用者名称中包含 DNS 名称。  否则，必须在设备注册到证书配置文件时提供此信息。


## <a name="improved-descriptions-for-pending-computer-restarts-----1356283---"></a>对挂起的计算机重启的改进性说明   <!--1356283 -->
在 [technical preview 1708](/sccm/core/get-started/capabilities-in-technical-preview-1708#restart-computers-from-the-configuration-manager-console) 中，我们添加了功能来标识从 Configuration Manager 控制台中挂起重启的设备。

从此 Technical Preview 开始，控制台将显示附加详细信息，提供正在请求重新启动的进程或操作的相关信息。

## <a name="device-guard-policy-changes----1355092---"></a>设备防护策略更改 <!-- 1355092 -->
在 1710 Technical Preview 版本中，进行了与设备防护策略相关的三个更改，如下所示：

### <a name="device-guard-policies-renamed-to-windows-defender-application-control-policies"></a>设备防护策略被重命名为 Windows Defender 应用程序控制策略
设备防护策略已被重命名为 Windows Defender 应用程序控制策略。 因此，举例来说，“创建设备防护策略”向导  现命名为“创建 Windows Defender 应用程序控制策略”向导  。

### <a name="restart-is-not-required-to-apply-policies"></a>不需要重启来应用策略
从 Windows 版本 1709 Fall Creators Update 开始，使用新版本的 Windows 设备无需重启就能应用 Windows Defender 应用程序控制策略。

重启为默认设置。

#### <a name="try-it-out"></a>试试看！  

如果要关闭重启，请按照下列步骤：

1.  打开“创建 Windows Defender 应用程序控制策略”  向导。
2.  在“常规”  页上，清除复选框“强制重启设备，以便可为所有进程强制执行此策略”  。
3.  单击“下一步”  ，直至向导完成。

对于较旧版本的 Windows，仍强制执行自动重启。

### <a name="automatically-run-software-trusted-by-the-intelligent-security-graph"></a>自动运行受 Intelligent Security Graph 信任的软件

管理员现在可以选择允许锁定的设备运行信誉良好的受信任软件，这是由 Microsoft Intelligent Security Graph (ISG) 决定的。 ISG 包括 Windows Defender SmartScreen 和其他 Microsoft 服务。

设备必须运行 Windows Defender SmartScreen，以使软件受信任。

#### <a name="try-it-out"></a>试试看！  

若要使运行 Windows Defender SmartScreen 的设备运行受信任的软件，请按照下列步骤：

1.  打开“创建 Windows Defender 应用程序控制策略”  向导。
2.  在“包含”  页上，选中对应的框“授权受 Intelligent Security Graph 信任的软件”  。
3.  在“受信任的文件或文件夹”  框中，添加你想要信任的文件和文件夹。
4.  单击“下一步”  ，直至向导完成。

## <a name="configure-and-deploy-windows-defender-application-guard-policies----1351960---"></a>配置和部署 Windows Defender 应用程序防护策略 <!-- 1351960 -->

[Windows Defender 应用程序防护](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97)是一项新的 Windows 功能，通过在操作系统的其他部分无法访问的安全隔离容器中打开不受信任的网站来帮助保护用户安全。 在此 Technical Preview 版中，我们使用在配置后部署到集合的 Configuration Manager 符合性设置增加了对配置此功能的支持。 此功能将在 64 位版本的 Windows 10 创意者更新预览版 (codename:RS2) 中发布。 现在，若要测试此功能，必须使用此更新的预览版本。

### <a name="before-you-start"></a>开始之前
若要创建和部署 Windows Defender 应用程序防护策略，必须使用网络隔离策略配置要部署此策略的 Windows 10 设备。 有关详细信息，请参阅稍后引用的博客文章。 此功能仅适用于当前的 Windows 10 预览体验成员版本。 若要对其进行测试，客户端必须运行最新的 Windows 10 预览体验成员版本。

### <a name="try-it-out"></a>试试看！

若要了解有关 Windows Defender 应用程序防护的基础知识，请阅读[博客文章](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97)。

若要创建策略，并浏览可用设置，请执行以下操作：
1. 在“Configuration Manager”  控制台中，选择“资产和符合性”  。
2. 在“资产和符合性”  工作区中，选择“概述”   > “终结点保护”   > “Windows Defender 应用程序防护”  。
3. 在“主页”  选项卡的“创建”  组中，单击“创建 Windows Defender 应用程序防护策略”  。
4. 将此博客文章用作参考，可以浏览和配置可用的设置来试用此功能。
5. 在此版本中，已将新的“网络定义”页面添加到向导。 可在此指定公司标识并定义企业网络边界。

    > [!NOTE]
    > Windows 10 电脑仅在客户端上存储一个网络隔离列表。 在此版本中，可以创建两种网络隔离列表（一种从 Windows 信息保护创建，另一种从 Windows Defender 应用程序防护创建），并将其部署到客户端。 如果部署两个策略，两个网络隔离列表必须匹配。 如果部署的列表与同一个客户端不匹配，则部署失败。

    可在 [Windows 信息保护文档](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/create-wip-policy-using-sccm)中找到有关如何指定网络定义的详细信息。

6. 结束后，完成向导操作，并将策略部署到一个或多个 Windows 10 设备。

### <a name="further-reading"></a>延伸阅读

若要了解有关 Windows Defender 应用程序防护的详细信息，请参阅[这篇博客文章](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97)。 此外，若要详细了解 Windows Defender 应用程序防护独立模式，请参阅[这篇博客文章](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903)。

## <a name="next-steps"></a>后续步骤
有关安装和更新 Technical Preview 分支的信息，请参阅 [System Center Configuration Manager Technical Preview](/sccm/core/get-started/technical-preview)。    
