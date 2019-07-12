---
title: 如何管理 Windows Device Guard
titleSuffix: Configuration Manager
description: 了解如何使用 System Center Configuration Manager 管理 Windows Device Guard。
ms.date: 12/19/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 5e5d854c-9cc1-4dd8-b33f-0fcac675b395
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d7c6fcdf0113dd9fa83d2d303661ad5690362715
ms.sourcegitcommit: f9654cd1a3af6d67de52fedaccceb2e22dafc159
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/09/2019
ms.locfileid: "67678733"
---
# <a name="device-guard-management-with-configuration-manager"></a>使用 Configuration Manager 进行的 Device Guard 管理

*适用范围：System Center Configuration Manager (Current Branch)*

## <a name="introduction"></a>简介
Device Guard 是一组 Windows 10 功能，用于保护电脑免受恶意软件和其他不受信任的软件的侵害。 它通过确保只能运行已知的经过批准的代码来阻止恶意代码运行。

Device Guard 同时包含基于软件和基于硬件的安全功能。 Windows Defender 应用程序控制是基于软件的安全层，它将强制执行允许在电脑上运行的软件的显式列表。 应用程序控制本身没有任何硬件或固件先决条件。 通过 Configuration Manager 部署的 应用程序策略在满足本文列出的最低 Windows 版本和 SKU 要求的目标集合中的电脑上启用策略。 或者，可以选择通过合格硬件上的组策略对通过 Configuration Manager 部署的应用程序控制策略启用基于虚拟机监控程序的保护。

若要详细了解 Device Guard，请阅读 [Device Guard 部署指南](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-deployment-guide)。

   > [!NOTE]
   > 从 Windows 10（版本 1709）开始，可配置的代码完整性策略称为 Windows Defender 应用程序控制。

## <a name="using-device-guard-with-configuration-manager"></a>结合使用 Device Guard 和 Configuration Manager

可以使用 Configuration Manager 来部署 Windows Defender 应用程序控制策略。 使用此配置，可以在集合中配置在电脑上运行 Device Guard 所使用的模式。 

可以配置以下模式之一：

1. **已启用强制** – 仅允许受信任的可执行文件运行。
2. **仅审核** - 允许所有可执行文件运行，但是在本地客户端事件日志中记录运行的不受信任的可执行文件。

>[!TIP]
>在该 Configuration Manager 版本中，Device Guard 是预发行功能。 要启用该功能，请参阅 [System Center Configuration Manager 中的预发布功能](/sccm/core/servers/manage/pre-release-features)。

## <a name="what-can-run-when-you-deploy-a-windows-defender-application-control-policy"></a>部署 Windows Defender 应用程序控制策略时，可以运行哪些内容？

通过 Windows Device Guard 可以严格控制可以在你所管理的电脑上运行的内容。 在高级安全部门的电脑中，禁止不需要的软件运行这一点至关重要，因此这一功能对于它们非常有用。

部署策略后，通常下列可执行文件可以运行：

- Windows 操作系统组件
- 硬件开发人员中心驱动程序（具有 Windows 硬件质量实验室签名）
- Windows 应用商店应用
- Configuration Manager 客户端 
- 处理 Windows Defender 应用程序控制策略后通过电脑安装的 Configuration Manager 部署的所有软件。 
- 来自以下服务的 Windows 组件更新：
    - Windows 更新
    - Windows Update for Business
    - Windows Server 更新服务
    - 配置管理器
    - （可选）信誉良好的软件（由 Microsoft Intelligent Security Graph (ISG) 决定）。 ISG 包括 Windows Defender SmartScreen 和其他 Microsoft 服务。 设备必须运行 Windows Defender SmartScreen 和 Windows 10（版本 1709），以使此软件受信任。

>[!IMPORTANT]
>这些项不包括通过 Internet 或第三方软件更新自动更新的未  内置于 Windows 的所有软件，无论这些软件是通过前面所述任一更新机制还是通过 Internet 安装的都是如此。 仅通过 Configuration Manager 客户端部署的软件更改可以运行。

## <a name="before-you-start"></a>开始之前

配置或部署 Windows Defender 应用程序控制策略前，请阅读下列信息：

- Device Guard 管理是 Configuration Manager 的预发行功能，可能会有所更改。
- 若要结合使用 Device Guard 和 Configuration Manager，你所管理的电脑必须运行 Windows 10 企业版 1703 或更高版本。
- 在客户端电脑上成功处理策略后，Configuration Manager 在该客户端上即被配置为托管的安装程序。 策略处理完成后，通过它部署的软件将自动受信任。 处理 Windows Defender 应用程序控制策略前 Configuration Manager 安装的软件不会自动受到信任。
- 客户端电脑必须连接到其域控制器才能成功处理 Windows Defender 应用程序控制策略。
- 部署期间可配置的应用程序控制策略的默认符合性评估计划是每天一次。 如果在策略处理期间观测到问题，则将符合性评估计划配置为更短的时间可能会有所帮助，例如每小时一次。 此计划决定出现失败时客户端重新尝试处理 Windows Defender 应用程序控制策略的频率。
- 无论选择的强制模式是什么，部署 Windows Defender 应用程序控制策略后，客户端电脑都无法运行扩展名为 .hta 的 HTML 应用程序。

## <a name="how-to-create-a-windows-defender-application-control-policy"></a>如何创建 Windows Defender 应用程序控制策略
1. 在 Configuration Manager 控制台中，单击“资产和符合性”  。
2. 在“资产和符合性”  工作区中，展开“Endpoint Protection”  ，然后单击“ Windows Defender 应用程序控制”  。
3. 在“主页”  选项卡上的“创建”  组中，单击“创建应用程序控制策略”  。
4. 在“创建应用程序控制策略向导”  的“常规”  页上，指定下列设置：
    - **名称** - 输入此 Windows Defender 应用程序控制策略的唯一名称。 
    - **说明** - 可选择输入此策略的说明，帮助你在 Configuration Manager 控制台中识别它。
    - **强制执行设备的重启，以便向所有进程强制执行此策略** - 在客户端电脑上处理策略后，根据“计算机重启”  的“客户端设置”  在该客户端上计划重启。
        - 始终自动重启运行 Windows 10（版本 1703）或更早版本的设备。
        - 从 Windows 10（版本 1709）开始，在重新启动前，将不会对当前在设备上运行的应用程序应用新的应用程序控制策略。 但是，在策略应用后启动的应用程序将遵循新的应用程序控制策略。 
    - **强制模式** - 为客户端电脑上的 Device Guard 选择下列强制方法之一。
        - **已启用强制** – 仅允许受信任的可执行文件运行。
        - **仅审核** - 允许所有可执行文件运行，但是在本地客户端事件日志中记录运行的不受信任的可执行文件。
5. 在“创建应用程序控制策略向导”  的“包含”  选项卡上，选择是否要“授权受 Intelligent Security Graph 信任的软件”  。
6. 如果想要为电脑上的特定文件或文件夹添加信任，请单击“添加”  。 在“添加受信任的文件或文件夹”  对话框中，可以指定要信任的本地文件或文件夹路径。 此外，还可以指定有连接权限的远程设备上的文件或文件夹路径。 在 Windows Defender 应用程序控制策略中添加对特定文件或文件夹的信任时，可以执行以下操作：
    - 解决托管安装程序行为的问题
    - 信任无法使用 Configuration Manager 部署的业务线应用
    - 信任包括在操作系统部署映像中的应用 
8. 单击“下一步”  以完成向导。

>[!IMPORTANT]
>仅支持在运行 Configuration Manager 客户端版本 1706 或更高版本的客户端电脑上，添加受信任文件或文件夹。 如果 Windows Defender 应用程序控制策略中有包含规则，并将此策略部署到运行旧版 Configuration Manager 客户端的客户端电脑，此策略将无法应用。 升级旧版客户端可以解决此问题。 不包括任何包含规则的策略仍可应用于旧版 Configuration Manager 客户端。

## <a name="how-to-deploy-a-windows-defender-application-control-policy"></a>如何部署 Windows Defender 应用程序控制策略
1. 在 Configuration Manager 控制台中，单击“资产和符合性”  。
2. 在“资产和符合性”  工作区中，展开“Endpoint Protection”  ，然后单击“ Windows Defender 应用程序控制”  。
3. 在策略列表中，选择要部署的策略，然后在“主页”  选项卡上的“部署”  组中单击“部署应用程序控制策略”  。
4. 在“部署应用程序控制策略”  对话框中，选择要将此策略部署到的集合。 然后，配置客户端评估此策略的时间计划。 最后，选择客户端是否可以在任何已配置的维护时段之外评估此策略。
5. 完成后，单击“确定”  以部署策略。 

<!--Reworked article to put this inline while working on VSO 1355092
### Restarting the device after deploying the policy

After the policy is processed on a client PC, a restart is scheduled on that client according to the **Client Settings** for **Computer Restart**. A restart is not required to apply policies, but it is the default. If you want to turn off restarts, follow these steps:

1. Open the **Create Windows Defender Application Policy** wizard.
2. On the **General** page, clear the check box for **Enforce a restart of devices so that this policy can be enforced for all processes**.
3. Click **Next** until the wizard completes.-->


## <a name="how-to-monitor-a-windows-defender-application-control-policy"></a>如何监视 Windows Defender 应用程序控制策略

使用[监视符合性设置](/sccm/compliance/deploy-use/monitor-compliance-settings)一文中的信息来帮助你监视已部署的策略是否已正确应用于所有电脑。

若要监视 Windows Defender 应用程序控制策略的处理情况，请使用客户端电脑上的下列日志文件：

**%WINDIR%\CCM\Logs\DeviceGuardHandler.log**

若要验证特定软件是否受到阻止或正在进行审核，请查看下列本地客户端事件日志：

1. 有关可执行文件的阻止和审核信息，请使用“应用程序和服务日志”   > “Microsoft”   > “Windows”   > “代码完整性”   > “运行”  。
2. 有关 Windows Installer 和脚本文件的阻止和审核信息，请使用“应用程序和服务日志”   > “Microsoft”   > “Windows”   > “AppLocker”   > “MSI 和脚本”  。

<!--Reworked article to put this inline while working on VSO 1355092
## Automatically let software run if it is trusted by Intelligent Security Graph

You can let locked-down devices run software with a good reputation as determined by the Microsoft Intelligent Security Graph (ISG). The ISG includes [Windows Defender SmartScreen](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-smartscreen/windows-defender-smartscreen-overview) and other Microsoft services. The devices must be running Windows Defender SmartScreen for this software to be trusted.

1. Open the **Create Windows Defender Application Policy** wizard.
2. On the **Inclusions** page, check the box for **Authorize software that is trusted by the Intelligent Security Graph**.
3. Click **Next** until the wizard completes.
-->


## <a name="security-and-privacy-information-for-device-guard"></a>Device Guard 的安全和隐私信息

- 在此预发行版本中，请勿在生产环境中使用强制模式“仅审核”  来部署 Windows Defender 应用程序控制策略。 此模式仅用于帮助你在测试实验室设置中测试该功能。
- 如果已使用“仅审核”  或“已启用强制”  模式向其部署策略的设备尚未重启来强制执行策略，则其易受到已安装的不受信任软件的攻击。
在这种情况下，即使设备重启或使用“已启用强制”  模式收到策略，该软件也可以继续运行。
- 若要确保 Windows Defender 应用程序控制策略有效，请在实验室环境中准备设备。 然后，部署“已启用强制”  策略，最后在向最终用户提供此设备前重启设备。
- 请勿使用“已启用强制”  部署策略，然后再使用“仅审核”  向同一设备部署策略。 此配置可能会允许不受信任的软件运行。
- 使用 Configuration Manager 在客户端电脑上启用 Windows Defender 应用程序控制时，该策略不会阻止具有本地管理员权限的用户绕过应用程序控制策略或执行不受信任的软件。 
- 阻止具有本地管理员权限的用户禁用应用程序控制的唯一方法是部署已签名二进制策略。 此部署可以通过组策略完成，但是 Configuration Manager 中目前不支持此操作。
- 将 Configuration Manager 设置为客户端电脑上的托管安装程序使用 AppLocker 策略。 AppLocker 仅用于标识托管安装程序，所有的强制过程均通过 Windows Defender 应用程序控制进行。 




