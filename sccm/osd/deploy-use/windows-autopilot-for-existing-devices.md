---
title: 面向现有设备的 Windows Autopilot
titleSuffix: Configuration Manager
description: 使用 Configuration Manager 任务序列为 Windows Autopilot 用户驱动模式重置映像并预配 Windows 7 设备
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 2e96f847-5b5a-4da9-8e8f-6aa488838508
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4cc806009f9cb02e50a2b023722a2045d4bde655
ms.sourcegitcommit: b28a97e22a9a56c5ce3367c750ea2bb4d50449c3
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2019
ms.locfileid: "70243715"
---
# <a name="windows-autopilot-for-existing-devices"></a>面向现有设备的 Windows Autopilot
<!--3607717, fka 1358333-->

*适用范围：System Center Configuration Manager (Current Branch)*

[Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot) 为组织提供了一种方法，将全新未经使用的 Windows 10 设备直接交付给最终用户，并定义用户获得安全、高效的 Windows 10 设备需要完成的预配流程。 这类设备已注册 Windows Autopilot 服务，因此用户可以分配必要的 Windows Autopilot 配置文件。 此配置文件定义该设备的全新体验 (OOBE)。 

[面向现有设备的 Windows Autopilot](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) 可通过 Windows 10 版本 1809 或更高版本提供。 此功能可重置映像并使用单个本机 Configuration Manager 任务序列为 [Windows Autopilot 用户驱动模式](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven)预配 Windows 7 设备。 



## <a name="prerequisites"></a>先决条件

- 获取 Windows 10 版本 1809 或更高版本的安装介质。 然后创建 Configuration Manager OS 映像。 有关详细信息，请参阅[管理 OS 映像](/sccm/osd/get-started/manage-operating-system-images)。

- 在 Microsoft Intune 中，创建适用于 Windows Autopilot 的配置文件。 有关详细信息，请参阅[在 Intune 中使用 Windows AutoPilot 注册 Windows 设备](https://docs.microsoft.com/intune/enrollment-autopilot)。

- 设备尚未注册 Windows Autopilot 服务。 如果已注册设备，那么指定的配置文件优先级更高。 仅当联机配置文件超时时，Autopilot for 现有设备配置文件才适用。



## <a name="create-the-configuration-file"></a>创建配置文件

1. 在具有 Internet 连接的 Windows 设备上，打开管理 PowerShell 命令窗口，然后运行以下命令：  

    1. 安装所需的模块，并接受提示以继续  
        ``` PowerShell  
        Install-Module AzureAD
        Install-Module WindowsAutopilotIntune 
        Import-Module WindowsAutopilotIntune 
        ```

    2. 使用管理员凭据登录到 Intune  
        ``` PowerShell  
        Connect-AutopilotIntune 
        ```

    3. 检索与你的 Intune 租户相关联的所有 Windows Autopilot 配置文件  
        ``` PowerShell  
        $AutopilotProfile = Get-AutopilotProfile
        ```

    4. 为每个配置文件创建一个配置文件。 这些文件以配置文件的显示名称命名，保存在当前用户的桌面上。<!--PowerShell example courtesy of GitHub user treestryder from SCCMDocs issue #1196-->  
        ``` PowerShell  
        $AutopilotProfile | ForEach-Object { $_ | ConvertTo-AutoPilotConfigurationJSON | Set-Content -Encoding Ascii "~\Desktop\$($_.displayName).json" }
        ```  

        > [!Note]  
        > 配置文件只能包含一个配置文件。 每个配置文件都应位于大括号 `{}` 内。  

2. 将其中一个配置文件保存到一个名为“AutopilotConfigurationFile.json”  的 ANSI 编码文件。 将其保存到可作为 Configuration Manager 包源的适当位置。  

    > [!Tip]  
    > 如果使用 PowerShell cmdlet Out-File  将 JSON 输出重定向到文件，它将默认使用 Unicode 编码。 此 cmdlet 还可能会截断较长的行。 使用具有 `-Encoding ASCII` 参数的 Set-Content  cmdlet 设置正确的文本编码。   
    > 
    > 默认情况下，Windows 记事本使用 ANSI 编码。  

3. 创建包含该文件的 Configuration Manager 包。 它不需要程序。 有关详细信息，请参阅[创建包](/sccm/apps/deploy-use/packages-and-programs#create-a-package-and-program)。  

    > [!NOTE]  
    > Windows 需要将此文件命名为“AutopilotConfigurationFile.json”  。 若要使用多个 Autopilot 配置文件，请创建单独的 Configuration Manager 包。  



## <a name="create-the-task-sequence"></a>创建任务序列

1. 在 Configuration Manager 控制台中，转到“软件库”  工作区，展开“操作系统”  ，选择“任务序列”  节点。 选择功能区中的“创建任务序列”  。  

2. 在“创建新的任务序列”  页上，选择选项“为现有设备部署 Windows Autopilot”  。  

3. 在“任务序列信息”  页中指定名称，可以选择添加说明，并选择启动映像。 有关受支持的启动映像版本的详细信息，请参阅[支持 Windows 10](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk)。  

4. 在“安装 Windows”  页上，选择 Windows 10 映像包  。 然后配置下列设置：  

    - **映像索引**：根据组织要求，选择“Enterprise”、“Education”或“Professional”  

    - 启用该选项以“在安装操作系统之前对目标计算机进行分区和格式化”   

    - **配置用于 Bitlocker 的任务序列**：如果启用此选项，则任务序列包括启用 Bitlocker 所需的步骤  

    - **产品密钥**：如果需要指定用于激活 Windows 的产品密钥，请在此处输入  

    - 选择以下选项之一，在 Windows 10 中配置本地管理员帐户：  
        - **随机生成本地管理员密码并在所有支持的平台上禁用帐户(推荐)**
        - **启用帐户并指定本地管理员密码**

5. 在“配置网络”  页上，选择选项“加入工作组”  。 此任务序列使用 Windows 系统准备工具 (sysprep)。 如果设备已加入域，sysprep 将失败。  

6. 在“安装 Configuration Manager”  页上，为环境添加任何必要的安装属性。  

    > [!Tip]  
    > 只有在 sysprep 运行之前的任务序列期间需要 Configuration Manager 客户端组件时，任务序列才需要此信息。 例如，要安装软件更新或应用程序。 如果不执行这些操作，则不需要客户端。 它会在任务序列运行 sysprep 之前卸载。  

7. “包括更新”  页默认选择选项“不安装任何软件更新”  。  

    > [!Tip]  
    > 使用脱机映像服务，使映像与最新的 Windows 10 质量更新保持最新。 有关详细信息，请参阅[将软件更新应用于 OS 映像](/sccm/osd/get-started/manage-operating-system-images#BKMK_OSImagesApplyUpdates)。  

8. 在“安装应用程序”  页上，可以选择要在任务序列期间安装的应用程序。 但是，Microsoft 建议通过此方案来反映签名映像方法。 使用 Autopilot 预配设备后，从 Microsoft Intune 或 Configuration Manager 共同管理应用所有应用程序和配置。 此过程在接收新设备的用户与在现有设备中使用 Windows Autopilot 的用户之间提供一致体验。  

8. 在“系统准备”  页上，选择包含 Autopilot 配置文件的包。 默认情况下，任务序列在运行 Windows Sysprep 后重新启动计算机。 此外可以选择选项“在此任务序列完成后关闭计算机”  。 可通过此选项准备设备，然后将其交付给用户，以实现一致的 Autopilot 体验。  

9. 完成向导。  

如果编辑任务序列，它将类似于应用现有 OS 映像的默认任务序列。 此任务序列包括以下附加步骤：  

- **应用 Windows Autopilot 配置**：此步骤应用指定包中的 Autopilot 配置文件。 它不是一种新的步骤类型，而是用于复制文件的“运行命令行”  步骤。  

- **让 Windows 做好捕获准备**：此步骤运行 Windows Sysprep，并包括设置“在运行此操作后关闭计算机”  。 有关详细信息，请参阅[准备 Windows 以便捕获](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareWindowsforCapture)。  

面向现有设备的 Windows Autopilot 任务序列会使设备加入 Azure Active Directory (Azure AD)。 

请使用 OneDrive for Business [已知的文件夹移动](https://docs.microsoft.com/onedrive/redirect-known-folders)确保在 Windows 10 升级之前备份用户的数据。



## <a name="next-steps"></a>后续步骤

使用共同管理增强 Windows 10 设备的管理功能。 共同管理的第二个途径是使用 Windows Autopilot 进行新式预配。 有关详细信息，请参阅下列文章：

- [什么是共同管理？](/sccm/comanage/overview)
- [共同管理的途径](/sccm/comanage/quickstart-paths)
- [Windows Autopilot 与共同管理](/sccm/comanage/quickstart-autopilot)

## <a name="see-also"></a>另请参阅

- [使用 Windows Autopilot 在 Intune 中注册 Windows 设备](https://docs.microsoft.com/intune/enrollment-autopilot)
