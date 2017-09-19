---
title: "如何管理 Windows Device Guard | Microsoft Docs"
description: "了解如何使用 System Center Configuration Manager 管理 Windows Device Guard。"
ms.custom: na
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.reviewer: dudeso
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5e5d854c-9cc1-4dd8-b33f-0fcac675b395
caps.latest.revision: "13"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 4555f7a9a6b5efd0fa01e9a101ea16bae7685117
ms.sourcegitcommit: b438515490e04fb09c82a8af642d38e9a0605178
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2017
---
# <a name="device-guard-management-with-configuration-manager"></a>使用 Configuration Manager 进行的 Device Guard 管理

*适用范围：System Center Configuration Manager (Current Branch)*

## <a name="introduction"></a>简介
Device Guard 是一组 Windows 10 功能，用于保护电脑免受恶意软件和其他不受信任的软件的侵害。 它通过确保只能运行已知的经过批准的代码来阻止恶意代码运行。

Device Guard 同时包含基于软件和基于硬件的安全功能。 可配置代码完整性是基于软件的安全层，它将强制执行允许在电脑上运行的软件的显式列表。 可配置代码完整性本身没有任何硬件或固件先决条件。 通过 Configuration Manager 部署的 Device Guard 策略在满足本主题列出的最低 Windows 版本和 SKU 要求的目标集合中的电脑上启用可配置代码完整性策略。 或者，可以选择通过合格硬件上的组策略对通过 Configuration Manager 部署的代码完整性策略启用基于虚拟机监控程序的保护。

若要详细了解 Device Guard，请阅读 [Device Guard 部署指南](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-deployment-guide)。

## <a name="using-device-guard-with-configuration-manager"></a>结合使用 Device Guard 和 Configuration Manager

可以使用 Configuration Manager 部署 Device Guard 策略，使你可以配置 Device Guard 在集合中的电脑上的运行模式。 

可以配置以下模式之一：

1.  **已启用强制** – 仅允许受信任的可执行文件运行。
2.  **仅审核** - 允许所有可执行文件运行，但是在本地客户端事件日志中记录运行的不受信任的可执行文件。

>[!TIP]
>在该 Configuration Manager 版本中，Device Guard 是预发行功能。 要启用该功能，请参阅 [System Center Configuration Manager 中的预发布功能](/sccm/core/servers/manage/pre-release-features)。

## <a name="what-can-run-when-you-deploy-a-device-guard-policy"></a>部署 Device Guard 策略后可以运行哪些功能？

通过 Windows Device Guard 可以严格控制可以在你所管理的电脑上运行的内容。 在高级安全部门的电脑中，禁止不需要的软件运行这一点至关重要，因此这一功能对于它们非常有用。

部署策略后，通常下列可执行文件可以运行：

- Windows 操作系统组件
- 硬件开发人员中心驱动程序（具有 Windows 硬件质量实验室签名）
- Windows 应用商店应用
- Configuration Manager 客户端 
- 处理 Device Guard 策略后通过电脑安装的 Configuration Manager 部署的所有软件。 
- 来自以下服务的 Windows 组件更新：
    - Windows 更新
    - Windows Update for Business
    - Windows Server 更新服务
    - 配置管理器

>[!IMPORTANT]
>这些项不包括通过 Internet 或第三方软件更新自动更新的未内置于 Windows 的所有软件，无论这些软件是通过前面所述任一更新机制还是通过 Internet 安装的都是如此。 仅通过 Configuration Manager 客户端部署的软件更改可以运行。

## <a name="before-you-start"></a>开始之前

配置或部署 Device Guard 策略前，请阅读下列信息：

- Device Guard 管理是 Configuration Manager 的预发行功能，可能会有所更改。
- 若要结合使用 Device Guard 和 Configuration Manager，你所管理的电脑必须运行 Windows 10 企业版 1703 或更高版本。
- 在客户端电脑上成功处理策略后，将 Configuration Manager 配置为此客户端上的托管安装程序，处理此策略后通过 SCCM 部署的软件将自动受到信任。 处理 Device Guard 策略前 Configuration Manager 安装的软件不会自动受到信任。
- 客户端电脑必须连接到其域控制器才能成功处理 Device Guard 策略。
- 部署期间可配置的 Device Guard 策略的默认符合性评估计划是每天一次。 如果在策略处理期间观测到问题，则将符合性评估计划配置为更短的时间可能会有所帮助，例如每小时一次。 此计划决定失败后客户端重新尝试处理 Device Guard 策略的频率。
- 无论选择的强制模式是什么，部署 Device Guard 策略后，客户端电脑都无法运行扩展名为 .hta 的 HTML 应用程序。

## <a name="how-to-create-a-device-guard-policy"></a>如何创建 Device Guard 策略
1.  在 Configuration Manager 控制台中，单击“资产和符合性” 。
2.  在“资产和符合性”工作区中，展开“Endpoint Protection”，然后单击“Device Guard 策略”。
3.  在“主页”选项卡上的“创建”组中，单击“创建 Device Guard 策略”。
4.  在“创建 Device Guard 策略向导”的“常规”页上，指定下列设置：
    - **名称** - 输入此 Device Guard 策略的唯一名称。 
    - **说明** - 可选择输入此策略的说明，帮助你在 Configuration Manager 控制台中识别它。
    - **强制模式** - 为客户端电脑上的 Device Guard 选择下列强制方法之一。
        - **已启用强制** – 仅允许受信任的可执行文件运行。
        - **仅审核** - 允许所有可执行文件运行，但是在本地客户端事件日志中记录运行的不受信任的可执行文件。
5.  如果想要选择性地添加对电脑上的特定文件或文件夹的信任，则在“创建 Device Guard 策略向导”的“包含项”选项卡中，单击“添加”。 
6.  在“添加受信任文件或文件夹”对话框中，指定有关你想要信任的文件或文件夹的信息。 你可以指定本地文件或文件夹路径，或者连接到你有权连接的远程设备，并指定文件或文件夹在该设备上的路径。
在 Device Guard 策略中添加对特定文件或文件夹的信任时，可以执行以下操作：
    - 解决托管安装程序行为的问题
    - 信任无法使用 Configuration Manager 部署的业务线应用
    - 信任包括在操作系统部署映像中的应用 
7.  单击“下一步”，然后完成向导。

>[!IMPORTANT]
>仅支持在运行 Configuration Manager 客户端版本 1706 或更高版本的客户端电脑上，添加受信任文件或文件夹。 如果 Device Guard 策略中有包含规则，并将此策略部署到运行旧版 Configuration Manager 客户端的客户端电脑，将无法应用此策略。 升级旧版客户端可以解决此问题。 不包括任何包含规则的策略仍可应用于旧版 Configuration Manager 客户端。

## <a name="how-to-deploy-a-device-guard-policy"></a>如何部署 Device Guard 策略
1.  在 Configuration Manager 控制台中，单击“资产和符合性” 。
2.  在“资产和符合性”工作区中，展开“Endpoint Protection”，然后单击“Device Guard 策略”。
3.  在策略列表中，选择要部署的策略，然后在“主页”选项卡上的“部署”组中单击“部署”。
4.  在“部署 Device Guard 策略”对话框中，选择要将此策略部署到的集合。 然后，配置客户端评估此策略的时间计划。 最后，选择客户端是否可以在任何已配置的维护时段之外评估此策略。
5.  完成后，单击“确定”以部署策略。 

在客户端电脑上处理策略后，根据“计算机重新启动”的“客户端设置”在该客户端上计划重启。
重启客户端电脑后，策略才会生效。

## <a name="how-to-monitor-a-device-guard-policy"></a>如何监控 Device Guard 策略

使用[监视符合性设置](/sccm/compliance/deploy-use/monitor-compliance-settings)主题中的信息来帮助你监视已部署的策略是否已正确应用于所有电脑。

若要监视 Device Guard 策略的处理过程，请使用客户端电脑上的下列日志文件：

**%WINDIR%\CCM\Logs\DeviceGuardHandler.log**

若要验证特定软件是否受到阻止或正在进行审核，请查看下列本地客户端事件日志：

1.  有关可执行文件的阻止和审核信息，请使用“应用程序和服务日志” > “Microsoft” > “Windows” > “代码完整性” > “运行”。
2.  有关 Windows Installer 和脚本文件的阻止和审核信息，请使用“应用程序和服务日志” > “Microsoft” > “Windows” > “AppLocker” > “MSI 和脚本”。

## <a name="security-and-privacy-information-for-device-guard"></a>Device Guard 的安全和隐私信息

- 在此预发行版本中，请勿在生产环境中使用强制模式“仅审核”来部署 Device Guard 策略。 此模式仅用于帮助你在测试实验室设置中测试该功能。
- 如果已使用“仅审核”或“已启用强制”模式向其部署策略的设备尚未重启来强制执行策略，则其易受到已安装的不受信任软件的攻击。
在这种情况下，即使设备重启或使用“已启用强制”模式收到策略，该软件也可以继续运行。
- 若要确保 Device Guard 策略有效，请在实验室环境中准备好设备。 然后，部署“已启用强制”策略，最后在向最终用户提供此设备前重启设备。
- 请勿使用“已启用强制”部署策略，然后再使用“仅审核”向同一设备部署策略。 此配置可能会允许不受信任的软件运行。
- 使用 Configuration Manager 在配备 Device Guard 策略的客户端电脑上启用可配置代码完整性时，该策略不会阻止具有本地管理员权限的用户绕过 Device Guard 策略或执行不受信任的软件。 
- 阻止具有本地管理员权限的用户禁用可配置代码完整性的唯一方法是部署已签名二进制策略。 此部署可以通过组策略完成，但是 Configuration Manager 中目前不支持此操作。
- 将 Configuration Manager 设置为客户端电脑上的托管安装程序使用 AppLocker 策略。 AppLocker 仅用于标识托管安装程序，整个强制过程通过可配置代码完整性进行。 




