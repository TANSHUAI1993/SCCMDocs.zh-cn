---
title: "使用 System Center Configuration Manager 部署 Windows to Go | Microsoft Docs"
description: "了解如何在 System Center Configuration Manager 中设置 Windows To Go 以创建从外部驱动器启动的 Windows To Go 工作区。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8eed50f5-80a4-422e-8aa6-a7ccb2171475
caps.latest.revision: "8"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: a8b1a42c43438553cfbb62328bed933378bb344c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="deploy-windows-to-go-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 部署 Windows to Go

*适用范围：System Center Configuration Manager (Current Branch)*

本主题提供用于在 System Center Configuration Manager 中设置 Windows To Go 的步骤。 Windows To Go 是 Windows 8 的企业功能，利用此功能，可以创建一个 Windows To Go 工作区，无论计算机上运行哪种操作系统，均可以在满足 Windows 7 或 Windows 8 认证要求的计算机上从 USB 连接的外部驱动器中启动该工作区。 Windows To Go 工作区可以使用企业对其台式机和便携计算机使用的相同映像，并且可以用相同的方式接受管理。  

 有关 Windows To Go 的详细信息，请参阅 [Windows To Go 功能概述](http://go.microsoft.com/fwlink/p/?LinkId=263433)。  

## <a name="provision-windows-to-go"></a>设置 Windows To Go  
 Windows To Go 是存储在通过 USB 连接的外部驱动器的操作系统上。 你可以设置 Windows To Go 驱动器，设置方法与设置其他操作系统部署的方法非常相似。 但是，因为 Windows To Go 旨在成为以用户为中心的高机动性解决方案，因此你必须采用略微不同的方法来设置这些驱动器。  

 在高级别，Windows To Go 是一个包含两个阶段的部署，它允许你配置 Windows To Go 设备以及为操作系统部署预留内容。 你能够以对用户影响最小的方式完成此操作，并且可以限制用户的计算机的停机时间。 在预留计算机之后，你必须完成设置过程以确保计算机可供用户使用。 设置过程类似于当前的操作系统部署过程。 下面列出了用于预留内容和设置 Windows To Go 的一般工作流：  

1.  [设置 Windows To Go 的先决条件](#BKMK_Prereqs)  

2.  [创建预留媒体](#BKMK_CreatePrestagedMedia)  

3.  [创建 Windows To Go Creator 包](#BKMK_CreatePackage)  

4.  [更新任务序列以对 Windows To Go 启用 BitLocker](#BKMK_UpdateTaskSequence)  

5.  [部署 Windows To Go Creator 包和任务序列](#BKMK_Deployments)  

6.  [用户运行 Windows To Go Creator](#BKMK_UserExperience)  

7.  [Configuration Manager 配置和暂存 Windows To Go 驱动器](#BKMK_ConfigureStageDrive)  

8.  [用户登录到 Windows 8](#BKMK_UserLogsIn)  

###  <a name="BKMK_Prereqs"></a> 设置 Windows To Go 的先决条件  
 在设置 Windows To Go 之前，你必须在 Configuration Manager 中完成以下操作：  

-   **将启动映像分发到分发点**  

     创建预留媒体之前，必须将启动映像分发到分发点。  

    > [!NOTE]  
    >  启动映像用于在 Configuration Manager 环境中的目标计算机上安装操作系统。 它们包含用于安装操作系统的 Windows PE 的某个版本，以及任何其他所需的设备驱动程序。 Configuration Manager 提供两个启动映像：一个用于支持 x86 平台，另一个用于支持 x64 平台。 你也可以创建自己的启动映像。 有关详细信息，请参阅[管理启动映像](../get-started/manage-boot-images.md)。  

-   **将 Windows 8 操作系统映像包分发到分发点**  

     创建预留媒体之前，必须将 Windows 8 操作系统映像包分发到分发点。  

    > [!NOTE]  
    >  操作系统映像是 .WIM 格式的文件，它们代表着经过压缩的集合，此集合包含在计算机上成功安装和配置操作系统所需的引用文件及文件夹。 有关详细信息，请参阅[管理操作系统映像](../get-started/manage-operating-system-images.md)。  

-   **创建用于部署 Windows 8 的任务序列**  

     你必须创建 Windows 8 部署的任务序列，创建预留媒体时将引用此任务序列。 有关详细信息，请参阅[管理任务序列以自动执行任务](manage-task-sequences-to-automate-tasks.md)。  

###  <a name="BKMK_CreatePrestagedMedia"></a> 创建预留媒体  
 预留媒体包含用于启动目标计算机的启动映像，以及应用到目标计算机的操作系统映像。 通过使用启动映像，可以启动用预留媒体设置的计算机。 然后，该计算机可以运行现有操作系统部署任务序列，以安装完整的操作系统部署。 此媒体不包含用于部署操作系统的任务序列。  

 你可以在预留阶段添加内容，如应用程序和设备驱动程序，以及操作系统映像包和启动映像。 这会减少部署操作系统所需的时间以及减少网络流量，因为内容已经在驱动器上。  

 使用以下过程来创建预留媒体。  

#### <a name="to-create-prestaged-media"></a>创建预留媒体  

1.  在 Configuration Manager 控制台中，单击“软件库” 。  

2.  在“软件库”工作区中，展开“操作系统”，然后单击“任务序列”。  

3.  在“主页”  选项卡上的“创建”  组中，单击“创建任务序列媒体”  以启动创建任务序列媒体向导。  

4.  在“选择媒体类型”  页上，指定以下信息，然后单击“下一步” 。  

    -   选择“预留媒体” 。  

    -   选择“允许无人参与的操作系统部署”  ，以在无用户干预的情况下启动到 Windows To Go 部署。  

        > [!IMPORTANT]  
        >  将此选项与 SMSTSPreferredAdvertID 自定义变量（在此过程中后面设置）一起使用时，不需要用户干预，计算机在检测到 Windows To Go 驱动器时将自动启动到 Windows To Go 部署。 如果针对密码保护配置了媒体，则仍会提示用户输入密码。 如果使用“允许无人参与的操作系统部署”  设置而不配置 SMSTSPreferredAdvertID 变量，则在部署任务序列时将出错。  

5.  在“媒体管理”  页上，指定以下信息，然后单击“下一步” 。  

    -   如果要允许管理点根据客户端在站点边界中的位置将媒体重定向到另一个管理点，请选择“动态媒体”  。  

    -   如果希望媒体仅与指定的管理点联系，请选择“基于站点的媒体”  。  

6.  在“媒体属性”   页上，指定以下信息，然后单击“下一步” 。  

    -   **创建者**：指定创建媒体的人员。  

    -   **版本**：指定媒体的版本号。  

    -   **注释**：指定媒体用途的唯一说明。  

    -   **媒体文件**：指定输出文件的名称和路径。 向导会将输出文件写入到此位置。 例如：**\\\servername\folder\outputfile.wim**  

7.  在“安全”  页上，指定以下信息，然后单击“下一步” 。  

    -   选择“启用未知计算机支持”，使媒体能够将操作系统部署到不是由 Configuration Manager 托管的计算机上。 Configuration Manager 数据库中没有这些计算机的记录。 未知计算机包括下列各项：  

        -   未安装 Configuration Manager 客户端的计算机  

        -   未导入到 Configuration Manager 中的计算机  

        -   未被 Configuration Manager 发现的计算机  

    -   选中“使用密码保护媒体”  ，并输入强密码来帮助防止未经授权访问媒体。 如果指定密码，则用户必须提供该密码才能使用预留媒体。  

        > [!IMPORTANT]  
        >  作为最佳安全方案，请始终分配密码来帮助保护预留媒体。  

        > [!NOTE]  
        >  如果用密码保护预留媒体，则会提示用户输入密码，即使使用“允许无人参与的操作系统部署”  设置配置了媒体也不例外。  

    -   对于 HTTP 通信，选择“创建自签名媒体证书” ，然后指定该证书的开始日期和到期日期。  

    -   对于 HTTPS 通信，选择“导入 PKI 证书” ，然后指定要导入的证书及其密码。  

         有关用于启动映像的此客户端证书的详细信息，请参阅 [PKI 证书要求](../../core/plan-design/network/pki-certificate-requirements.md)。  

    -   **用户设备相关性**：若要在 Configuration Manager 中支持以用户为中心的管理，请指定希望媒体如何将用户与目标计算机相关联。 有关操作系统部署如何支持用户设备相关性的详细信息，请参阅[如何将用户与目标计算机相关联](../get-started/associate-users-with-a-destination-computer.md)。  

        -   如果你希望媒体自动将用户与目标计算机关联，请指定“通过自动批准允许用户设备相关性”  。 此功能以部署操作系统的任务序列的操作为基础。 在此方案中，当任务序列将操作系统部署到目标计算机时，它会在指定的用户和目标计算机之间创建关系。  

        -   如果希望媒体获得批准后将用户与目标计算机关联，请指定“允许用户设备相关性挂起管理员批准”  。 此功能以部署操作系统的任务序列的作用域为基础。 在此方案中，任务序列在指定用户和目标计算机之间创建关系，但在部署操作系统之前等待管理用户的批准。  

        -   如果不希望媒体将用户与目标计算机关联，请指定“不允许用户设备相关性”  。 在此方案中，当任务序列部署操作系统时，它不会将用户与目标计算机关联。  

8.  在“任务序列”  页上，指定在上一部分中创建的 Windows 8 任务序列。  

9. 在“启动映像包”  页上，指定以下信息，然后单击“下一步” 。  

    > [!IMPORTANT]  
    >  分发的启动映像的体系结构必须适合于目标计算机的体系结构。 例如，x64 目标计算机可启动和运行 x86 或 x64 启动映像。 但是，x86 目标计算机只能启动和运行 x86 启动映像。 对于 EFI 模式下的 Windows 8 认证计算机，你必须使用 x64 启动映像。  

    -   **启动映像**：指定用于启动目标计算机的启动映像。  

    -   **分发点**：指定托管启动映像的分发点。 向导将从分发点中检索启动映像并将其写入媒体。  

        > [!NOTE]  
        >  管理用户必须对分发点上的启动映像内容具有“读取”  访问权限。 有关详细信息，请参阅[管理帐户以访问内容](../../core/plan-design/hierarchy/manage-accounts-to-access-content.md)。  

    -   如果在此向导的“媒体管理”  页上选择了“基于站点的媒体”  ，请在“管理点”  框中指定主站点中的管理点。  

    -   如果在向导的“媒体管理”  页上选择了“动态媒体”  ，请在“关联的管理点”  框中指定要使用的主站点管理点以及初始通信的优先级顺序。  

10. 在“映像”  页上，指定以下信息，然后单击“下一步” 。  

    -   **映像包**：指定包含 Windows 8 操作系统映像包的包。  

    -   **映像索引**：指定在包包含多个操作系统映像的情况下要部署的映像。  

    -   **分发点**：指定托管操作系统映像包的分发点。 向导将从分发点中检索操作系统映像并将其写入媒体。  

        > [!NOTE]  
        >  管理用户必须对分发点上的操作系统映像包内容具有“读取”  访问权限。 有关详细信息，请参阅[管理帐户以访问内容](../../core/plan-design/hierarchy/manage-accounts-to-access-content.md)。  

11. 在“选择应用程序”  页上，选择要包含在媒体文件中的应用程序内容，然后单击“下一步” 。  

12. 在“选择包”  页上，选择要包含在媒体文件中的其他包内容，然后单击“下一步” 。  

13. 在“选择驱动程序包”  页上，选择要包含在媒体文件中的驱动程序包内容，然后单击“下一步” 。  

14. 在“分发点”  页上，选择包含任务序列所需的内容的一个或多个分发点，然后单击“下一步” 。  

15. 在“自定义”  页上，指定以下信息，然后单击“下一步” 。  

    -   **变量**：指定任务序列用于部署操作系统的变量。 对于 Windows To Go，请使用 SMSTSPreferredAdvertID 变量通过以下格式自动选择 Windows To Go 部署：  

         SMSTSPreferredAdvertID = {*DeploymentID*}，其中 DeploymentID 是与将用于完成 Windows To Go 驱动器设置过程的任务序列关联的部署 ID。  

        > [!TIP]  
        >  将此变量与设置为以无人参与模式运行（在此过程中前面设置）的任务序列一起使用时，不需要用户干预，计算机在检测到 Windows To Go 驱动器时将自动启动到 Windows To Go 部署。 如果针对密码保护配置了媒体，则仍会提示用户输入密码。  

    -   **预先启动命令**：指定想要在运行任务序列之前运行的任何预启动命令。 预启动命令可能是可在运行任务序列以安装操作系统之前在 Windows PE 中与用户交互的脚本或可执行文件。 为 Windows To Go 部署配置以下各项：  

        -   **OSDBitLockerPIN**：适用于 Windows To Go 的 BitLocker 需要密码。 将“OSDBitLockerPIN”  变量设置为预启动命令的一部分，以为 Windows To Go 驱动器设置 BitLocker 密码。  

            > [!WARNING]  
            >  针对密码启用 BitLocker 后，每次计算机启动到 Windows To Go 驱动器时，用户必须输入密码。  

        -   **SMSTSUDAUsers**：指定目标计算机的主要用户。 使用此变量收集用户名，然后可以使用用户名关联用户和设备。 有关详细信息，请参阅[将用户与目标计算机相关联](../get-started/associate-users-with-a-destination-computer.md)。  

            > [!TIP]  
            >  要检索用户名，你可以在预启动命令中创建一个输入框，让用户输入其用户名，然后设置此变量和值。 例如，你可以将以下行添加到预启动命令脚本文件中：  
            >   
            >  `UserID = inputbox("Enter Username" ,"Enter your username:","",400,0)`  
            >   
            >  `env("SMSTSUDAUsers") = UserID`  

         有关如何创建要用作预启动命令的脚本文件的详细信息，请参阅[任务序列媒体的预启动命令](../understand/prestart-commands-for-task-sequence-media.md)。  

16. 完成向导。  

    > [!NOTE]  
    >  向导完成预留媒体文件可能需要很长一段时间。  

###  <a name="BKMK_CreatePackage"></a> 创建 Windows To Go Creator 包  
 在部署 Windows To Go 过程中，你必须创建包以部署预留媒体文件。 包必须包括配置 Windows To Go 驱动器并将预留媒体提取到驱动器的工具。 使用下面的过程可创建 Windows To Go Creator 包。  

#### <a name="to-create-the-windows-to-go-creator-package"></a>创建 Windows To Go Creator 包  

1.  在要承载 Windows To Go Creator 包文件的服务器上，创建包源文件的源文件夹。  

    > [!NOTE]  
    >  站点服务器的计算机帐户必须具有对源文件夹的“读取”  访问权限。  

2.  将在 [Create prestaged media](#BKMK_CreatePrestagedMedia) 部分中创建的预留媒体文件复制到包源文件夹。  

3.  将 Windows To Go Creator 工具 (WTGCreator.exe) 复制到包源文件夹中。 此 Creator 工具在任何主站点服务器上的以下位置中均可用：<ConfigMgrInstallationFolder>\OSD\Tools\WTG\Creator。  

4.  通过使用创建包和程序向导来创建包和程序。  

5.  在 Configuration Manager 控制台中，单击“软件库” 。  

6.  在“软件库”  工作区中，展开“应用程序管理” ，然后单击“包” 。  

7.  在“主页”  选项卡上的“创建”  组中，单击“创建包” 。  

8.  在“包”  页上，指定包的名称和描述。 例如，输入 **Windows To Go** 作为包的名称，并指定 **Package to configure a Windows To Go drive using System Center Configuration Manager** 为包的描述。  

9. 选择“此包包含源文件” ，指定在步骤 1 中创建的包源文件夹的路径，然后单击“下一步” 。  

10. 在“程序类型”  页上，选择“标准程序” ，然后单击“下一步” 。  

11. 在“标准程序”  页上，指定下列信息：  

    -   **名称**：指定程序的名称。 例如，键入 **Creator** 作为程序名。  

    -   “命令行”：键入 **WTGCreator.exe /wim:PrestageName.wim**，其中 PrestageName 是你创建并复制到 Windows To Go Creator 包的包源文件夹的预留文件的名称。  

         你可以根据需要添加下列选项：  

        -   **enableBootRedirect**：此命令行选项用于更改 Windows To Go 启动选项以允许启动重定向。 使用此选项时，计算机将从 USB 中启动，而不必在计算机固件中更改启动顺序或者在启动过程中让用户在启动选项列表中选择。 如果检测到 Windows To Go 驱动器，则计算机会启动到该驱动器。  

    -   **运行**：指定“常规”  以基于系统和程序默认值运行程序。  

    -   **程序可以运行**：指定程序是否只能在用户登录时运行。  

    -   **运行模式**：指定是将使用登录用户权限还是管理权限来运行程序。 运行 Windows To Go Creator 需要提升的权限。  

    -   选择“允许用户查看程序安装并与之交互” ，然后单击“下一步” 。  

12. 在“要求”页上，指定下列各项：  

    -   **平台要求**：选择相应的 Windows 8 平台以允许进行设置。  

    -   **估计磁盘空间**：指定 Windows To Go Creator 的包源文件夹的大小。  

    -   **最大允许运行时间(分钟)**：指定预计程序在客户端计算机上运行的最长时间。 默认情况下，此值设置为 120 分钟。  

        > [!IMPORTANT]  
        >  当你使用此程序运行的维护时段进行收集时，如果“最大允许运行时间”  大于计划的维护时段，就可能出现冲突。 如果最大运行时间设置为“未知” ，程序将在维护时段启动，会继续运行到维护时段结束后完成或失败。 如果你将最大运行时间设置为特定时段（没有设置为“未知”），此时段大于任何可用维护时段的长度，那么程序就不会运行。  

        > [!NOTE]  
        >  如果值设置为“未知”，则 Configuration Manager 会将最大允许运行时间设置为 12 小时（720 分钟）。  

        > [!NOTE]  
        >  如果超出最大运行时间（无论是由用户设置的值还是默认值），则在“标准程序”页上选中了“使用管理权限运行”而未选择“允许用户查看程序安装并与之交互”时，Configuration Manager 将停止该程序。  

     单击“下一步”  并完成向导。  

###  <a name="BKMK_UpdateTaskSequence"></a> 更新任务序列以对 Windows To Go 启用 BitLocker  
 Windows To Go 在外部可启动驱动器上启用 BitLocker 而不使用 TPM。 因此，必须使用单独的工具在 Windows To Go 驱动器上配置 BitLocker。 要启用 BitLocker，必须在“安装 Windows 和 ConfigMgr”  步骤之后向任务序列添加操作。  

> [!NOTE]  
>  适用于 Windows To Go 的 BitLocker 需要密码。 在 [Create prestaged media](#BKMK_CreatePrestagedMedia) 步骤中，你可以使用 OSDBitLockerPIN 变量将密码设置为预启动命令的一部分。  

 使用以下过程更新 Windows 8 任务序列以对 Windows To Go 启用 BitLocker。  

#### <a name="to-update-the-windows-8-task-sequence-to-enable-bitlocker"></a>更新 Windows 8 任务序列以启用 BitLocker  

1.  在 Configuration Manager 控制台中，单击“软件库” 。  

2.  在“软件库”  工作区中，展开“应用程序管理” ，然后单击“包” 。  

3.  在“主页”  选项卡上的“创建”  组中，单击“创建包” 。  

4.  在“包”  页上，指定包的名称和描述。 例如，键入 **BitLocker for Windows To Go** 作为包的名称，并指定 **Package to update BitLocker for Windows To Go** 为包的描述。  

5.  选择“此包包含源文件” ，指定适用于 Windows To Go 的 BitLocker 工具的位置，然后单击“下一步” 。 此 BitLocker 工具在任何 Configuration Manager 主站点服务器上的以下位置中均可用：<ConfigMgrInstallationFolder>\OSD\Tools\WTG\BitLocker\  

6.  在“程序类型”  页上，选择“不创建程序” 。  

7.  单击“下一步”  并完成向导。  

8.  在 Configuration Manager 控制台中，单击“软件库” 。  

9. 在“软件库”  工作区中，展开“操作系统” ，然后单击“任务序列” 。  

10. 选择在预留媒体中引用的 Windows 8 任务序列。  

11. 在“主页”  选项卡上的“任务序列”  组中，单击“编辑” 。  

12. 依次单击“安装 Windows 和 ConfigMgr”  步骤、“添加” 、“常规” 和“运行命令行” 。 “运行命令行”步骤将添加到“安装 Windows 和 ConfigMgr”步骤之后。  

13. 在“运行命令行”  步骤的“属性”  选项卡上，添加以下各项：  

    1.  **名称**：指定命令行的名称，例如 **Enable BitLocker for Windows To Go**。  

    2.  **命令行**：i386\osdbitlocker_wtg.exe /Enable /pwd:< None&#124;AD>  

         参数：  

        -   /pwd:<None&#124;AD> - 指定 BitLocker 密码恢复模式。 当你在命令行中使用 /Enable 参数时，需要此参数。  

             选择“AD”  以将 BitLocker 驱动器加密配置为将 BitLocker 保护的驱动器的恢复信息备份到 Active Directory 域服务 (AD DS)。 通过为 BitLocker 保护的驱动器备份恢复密码，管理用户可以在驱动器被锁定的情况下恢复驱动器。 这样可确保授权的用户始终可以访问属于企业的加密数据。 如果指定“无” ，则用户负责保留恢复密码或恢复密钥的副本。 如果用户丢失该信息，或者在离开组织之前忽略了解密驱动器，则管理用户无法轻松地访问驱动器。  

        -   /wait:<TRUE&#124;FALSE> - 指定任务序列在完成之前是否等待加密完成。  

    3.  选择“包” ，然后指定在此过程之初创建的包。  

    4.  在“选项”  选项卡上，添加以下条件：  

        -   条件 = 任务序列变量  

        -   变量 = _SMSTSWTG  

        -   条件 = 等于  

        -   值 = True  

    > [!NOTE]  
    >  “启用 BitLocker”  步骤可能在新命令行步骤之后，并且不用于为 Windows To Go 启用 BitLocker。 但是，你可以在任务序列中保留此步骤，以用于不使用 Windows To Go 驱动器的 Windows 8 部署。  

###  <a name="BKMK_Deployments"></a> 部署 Windows To Go Creator 包和任务序列  
 Windows To Go 是混合部署过程。 因此，你必须部署 Windows To Go Creator 包和 Windows 8 任务序列。 使用以下过程来完成部署过程。  

#### <a name="to-deploy-the-windows-to-go-creator-package"></a>部署 Windows To Go Creator 包  

1.  在 Configuration Manager 控制台中，单击“软件库” 。  

2.  在“软件库”  工作区中，展开“应用程序管理” ，然后单击“包” 。  

3.  选择在 [创建 Windows To Go Creator 包](#BKMK_CreatePackage) 步骤中创建的 Windows To Go 包。  

4.  在“主页”  选项卡上的“部署”  组中，单击“部署” 。  

5.  在“常规”  页上，指定下列设置：  

    1.  “软件”：验证是否已选中 Windows To Go 包。  

    2.  “集合”：单击“浏览”  以选择要将 Windows To Go 包部署到的集合。  

    3.  “使用与此集合关联的默认分发点组”：如果你想将包内容存储在集合默认分发点组中，请选择此选项。 如果未将所选集合与分发点组关联，则此选项将不可用。  

6.  在“内容”  页上，单击“添加”  ，然后选择要将与此包和程序关联的内容部署到的分发点或分发点组。  

7.  在“部署设置”  页上，为部署类型选择“可用”  ，然后单击“下一步” 。  

8.  在“计划” 上，配置将部署此包和程序或将其提供给客户端设备的时间。  

     视部署操作设置为“可用”  还是“必需” 而定，此页上的选项将有所不同。  

9. 在“计划” 上，配置以下设置，然后单击“下一步” 。  

    1.  **计划此部署将在何时变为可用**：指定包和程序在目标计算机上可以运行的日期和时间。 如果选中“UTC” ，则此设置可以确保包和程序按照目标计算机上的本地时间同时（而不是在不同时间）可用于多个目标计算机。  

    2.  **计划此部署将在何时过期**：指定包和程序在目标计算机上过期的日期和时间。 如果选中“UTC” ，则此设置确保任务序列按照目标计算机上的本地时间同时（而不是在不同时间）在多台目标计算机上过期。  

10. 在向导的“用户体验”  页上，指定下列信息：  

    -   “软件安装”：允许在任何已配置维护时段外安装软件。  

    -   “系统重新启动（如果要求完成安装）”：当软件安装需要时，允许在已配置的维护时段之外重新启动设备。  

    -   “嵌入式设备”：将包和程序部署到启用了写入筛选器的 Windows 嵌入式设备时，你可以指定将包和程序安装在临时覆盖区上并稍后提交更改，或者在安装截止时或在维护时段内提交更改。 如果在安装截止时或在维护时段内提交更改，则需要重新启动，而且更改将保留在设备上。  

11. 在“分发点”  页上，指定下列信息：  

    -   “部署选项”： 指定“从分发点下载内容并本地运行” 。  

    -   **允许客户端与同一子网上的其他客户端共享内容**：选择此选项，通过允许客户端从网络上已下载并缓存了内容的其他客户端下载内容来减轻网络上的负载。 此选项使用 Windows BranchCache 并且可以在运行 Windows Vista SP2 和更高版本的计算机上使用。  

    -   **所有客户端使用内容的回退源位置**：指定是否允许客户端在首选分发点上没有内容时回退并使用非首选分发点作为内容的源位置。  

12. 完成向导。  

#### <a name="to-deploy-the-windows-8-task-sequence"></a>部署 Windows 8 任务序列  

1.  在 Configuration Manager 控制台中，单击“软件库” 。  

2.  在“软件库”  工作区中，展开“操作系统” ，然后单击“任务序列” 。  

3.  选择在 [Prerequisites to provision Windows To Go](#BKMK_Prereqs) 步骤中创建的 Windows 8 任务序列。  

4.  在“主页”  选项卡上的“部署”  组中，单击“部署” 。  

5.  在“常规”  页上，指定下列设置：  

    1.  **任务序列**：验证是否选择了 Windows 8 任务序列。  

    2.  “集合”：单击“浏览”  ，以选择包含用户可能为其设置 Windows To Go 的所有设备的集合。  

        > [!IMPORTANT]  
        >  如果你在 [Create prestaged media](#BKMK_CreatePrestagedMedia) 部分中创建的预留媒体使用 SMSTSPreferredAdvertID 变量，则你可以将任务序列部署到“所有系统”  集合，并且可以在“内容”  页上指定“仅 Windows PE (隐藏)”  设置。 由于隐藏了任务序列，因此它将只对媒体可用。  

    3.  “使用与此集合关联的默认分发点组”：如果你想将包内容存储在集合默认分发点组中，请选择此选项。 如果未将所选集合与分发点组关联，则此选项将不可用。  

6.  在“部署设置”  页上，配置下列设置，然后单击“下一步” 。  

    -   **目的**：选择“可用” 。 将任务序列部署到用户时，用户将在应用程序目录中看到发布的任务序列，并可根据需要请求该任务序列。 如果将任务序列部署到设备，则用户将在软件中心看到该任务序列，并可根据需要安装它。  

    -   **可用于以下项目**：指定任务序列是否可用于 Configuration Manager 客户端、媒体或者 PXE。  

        > [!IMPORTANT]  
        >  将“仅媒体和 PXE (隐藏)”  设置用于自动化任务序列部署。 选择“允许无人参与的操作系统部署”  ，并将 SMSTSPreferredAdvertID 变量设置为预留媒体的一部分，以让计算机在检测到 Windows To Go 驱动器时在无用户干预的情况下自动启动到 Windows To Go 部署。 有关这些预留媒体设置的详细信息，请参阅 [Create prestaged media](#BKMK_CreatePrestagedMedia) 部分。  

7.  在“计划”  页上，配置下列设置，然后单击“下一步” 。  

    1.  **计划此部署将在何时变为可用**：指定任务序列在目标计算机上可以运行的日期和时间。 如果选中“UTC” ，则此设置确保任务序列按照目标计算机上的本地时间可以同时（而不是在不同时间）在多台目标计算机上可用。  

    2.  **计划此部署将在何时过期**：指定任务序列在目标计算机上过期的日期和时间。 如果选中“UTC” ，则此设置确保任务序列按照目标计算机上的本地时间同时（而不是在不同时间）在多台目标计算机上过期。  

8.  在“用户体验”  页上，指定下列信息：  

    -   **显示任务序列进度**：指定 Configuration Manager 客户端是否显示任务序列的进度。  

    -   **软件安装**：指定在计划的时间之后是否允许用户在已配置的维护时段之外安装软件。  

    -   “系统重新启动（如果要求完成安装）”：当软件安装需要时，允许在已配置的维护时段之外重新启动设备。  

    -   “嵌入式设备”：将包和程序部署到启用了写入筛选器的 Windows 嵌入式设备时，你可以指定将包和程序安装在临时覆盖区上并稍后提交更改，或者在安装截止时或在维护时段内提交更改。 如果在安装截止时或在维护时段内提交更改，则需要重新启动，而且更改将保留在设备上。  

    -   **基于 Internet 的客户端**：指定是否允许在基于 Internet 的客户端上运行任务序列。 此设置不支持安装诸如操作系统之类的软件的操作。 请将此选项仅用于在标准操作系统中执行操作的基于通用脚本的任务序列。  

9. 在“警报”页上，为此任务序列部署指定所需的警报设置，然后单击“下一步”。  

10. 在“分发点”  页上，指定以下信息，然后单击“下一步” 。  

    -   **部署选项**：选择“需要时通过运行任务序列本地下载内容” 。  

    -   **在没有本地分发点可用的情况下使用远程分发点**：指定客户端是否可以使用慢速和不可靠网络上的分发点来下载任务序列所需的内容。  

    -   **允许客户端使用内容源位置回退**：
        - 版本 1610 之前，可选中“允许内容源位置回退”复选框，以便在没有其他分发点可用时让这些边界组外部的客户端回退并使用分发点作为内容的源位置。
        - 从 1610 版起，用户不能再配置“允许内容源位置回退”。  取而代之的是，可配置边界组之间的关系，以确定客户端何时可以开始搜索有效内容源位置的其他边界组。 

11. 完成向导。  

###  <a name="BKMK_UserExperience"></a> 用户运行 Windows To Go Creator  
 在部署 Windows To Go 包和 Windows 8 任务序列之后，用户可以使用 Windows To Go Creator。 用户可以转到软件目录或软件中心（如果 Windows To Go Creator 已部署到设备），然后运行 Windows To Go Creator 程序。 在下载 Creator 包之后，任务栏上会显示一个闪烁的图标。 如果用户单击此图标，则会显示一个对话框，以便让用户选择要设置的 Windows To Go 驱动器（除非使用了 /drive 命令行选项）。 如果驱动器不符合对 Windows To Go 的要求，或者如果驱动器没有足够的可用磁盘空间来安装映像，则 Creator 程序会显示错误消息。 用户可以通过确认页来验证驱动器和将应用的映像。 在 Creator 配置内容并将其预留到 Windows To Go 驱动器时，它会显示进度对话框。 在预留完成后，Creator 会提示重新启动计算机以启动到 Windows To Go 驱动器。  

> [!NOTE]  
>  如果在 [Create a Windows To Go Creator package](#BKMK_CreatePackage) 部分中没有在 Creator 程序的命令行中启用启动重定向，则用户可能需要在每次系统重新启动时手动启动到 Windows To Go 驱动器。  

###  <a name="BKMK_ConfigureStageDrive"></a> Configuration Manager 配置和暂存 Windows To Go 驱动器  
 在计算机重启到 Windows To Go 驱动器之后，此驱动器将引导到 Windows PE，并连接到管理点以获得策略，以便完成操作系统部署。 Configuration Manager 配置和暂存驱动器。 在 Configuration Manager 暂存此驱动器之后，用户可以重新启动计算机，以完成设置过程（例如加入域或安装应用程序）。 此过程对于任何预留媒体都是相同的。  

###  <a name="BKMK_UserLogsIn"></a> 用户登录到 Windows 8  
 在 Configuration Manager 完成设置过程并且显示 Windows 8 锁屏之后，用户可以登录到操作系统。  
