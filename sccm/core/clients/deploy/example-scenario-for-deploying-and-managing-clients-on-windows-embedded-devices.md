---
title: "示例方案 - 部署 Windows Embedded 客户端 | Microsoft Docs"
description: "请参阅在 Windows Embedded 设备上部署和管理 System Center Configuration Manager 客户端的示例方案。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 10049c89-b37c-472b-b317-ce4f56cd4be7
caps.latest.revision: "8"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: c535bc62497b5ff0b60ca266c28630d890af3604
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="example-scenario-for-deploying-and-managing-system-center-configuration-manager-clients-on-windows-embedded-devices"></a>在 Windows Embedded 设备上部署和管理 System Center Configuration Manager 客户端的示例场景

*适用范围：System Center Configuration Manager (Current Branch)*

此方案演示了如何使用 Configuration Manager 管理启用了写入筛选器的 Windows Embedded 设备。如果嵌入设备不支持写入筛选器，则这些设备将用作标准 Configuration Manager 客户端，这些过程将不适用。  

Coho Vineyard & Winery 正在开设一家访客中心，需要运行 Windows Embedded 的网亭来运行交互式演示文稿。 新访客中心的建筑距离 IT 部门不近，因此必须可远程管理网亭。 除了运行演示文稿的软件外，这些设备还必须运行最新的反恶意软件保护软件以符合公司安全策略。 网亭必须每周全天候运行，且在访客中心开放时没有停机时间。  

 Coho 已运行 Configuration Manager 来管理其网络上的设备。 Configuration Manager 配置为运行 Endpoint Protection 并安装软件更新和应用程序。 但是，由于 IT 团队以前未管理过 Windows Embedded 设备，因此 Configuration Manager 管理员 Jane 运行一个试点来管理接待大厅中的两个网亭。   

 为了管理这些启用了写入筛选器的 Windows Embedded 设备，Jane 执行以下步骤来安装 Configuration Manager 客户端，通过使用 Endpoint Protection 保护客户端，并安装交互式演示文稿软件。  

1.  为了保留软件安装，Jane 阅读了相关信息，了解了 Windows Embedded 设备如何使用写入筛选器，以及 Configuration Manager 如何通过自动禁用然后重新启用写入筛选器使写入筛选器的使用更加简单。  

     有关详细信息，请参阅[在 System Center Configuration Manager 中规划对 Windows Embedded 设备的客户端部署](../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md)。  

2.  在安装 Configuration Manager 客户端之前，Jane 为 Windows Embedded 设备创新建了一个基于查询的设备集合。 由于公司使用标准命名格式来标识其计算机，因此 Jane 可通过计算机名的前六个字母来唯一地标识 Windows Embedded 设备： **WEMDVC**。 她使用以下 WQL 查询来创建此集合： **select SMS_R_System.NetbiosName from SMS_R_System where SMS_R_System.NetbiosName like "WEMDVC%"**  

     此集合允许她使用与其他设备不同的配置选项来管理 Windows Embedded 设备。 她将使用此集合来控制重启、使用客户端设置部署 Endpoint Protection，以及部署交互式演示文稿应用程序。  

     请参阅[如何在 System Center Configuration Manager 中创建集合](../../../core/clients/manage/collections/create-collections.md)。  

3.  Jane 针对维护时段配置集合，以确保安装演示文稿应用程序和任何升级可能需要的重启不会在访客中心的开放时段进行。 开放时段将为星期一至星期日 09:00 至 18:00。 她将每天的维护时段配置为 18:30 至 06:00。  

4.  有关详细信息，请参阅[如何在 System Center Configuration Manager 中使用维护时段](../../../core/clients/manage/collections/use-maintenance-windows.md)。  

5.  然后，Jane 配置一个自定义设备客户端设置以通过为下列设置选择“是”  来安装 Endpoint Protection 客户端，然后将此自定义客户端设置部署到 Windows Embedded 设备集合：  

    -   **在客户端计算机上安装 Endpoint Protection 客户端**  

    -   **对于带有写入筛选器的 Windows Embedded 设备，提交 Endpoint Protection 客户端安装(需要重新启动)**  

    -   **允许安装 Endpoint Protection 客户端和在维护时段以外重启**  

     安装 Configuration Manager 客户端时，这些设置会安装 Endpoint Protection 客户端并确保其作为安装的一部分保留在操作系统中，而不仅仅只是写入覆盖区。 公司安全策略要求始终安装反恶意软件，并且 Jane 不希望面临网亭不受保护（即使在重启的情况下短时间不受保护）的风险。  

    > [!NOTE]  
    >  安装 Endpoint Protection 客户端所需进行的重启只会在访客中心运营之前设备的设置期间发生一次。 与定期部署应用程序或软件定义更新不同，下一次在同一设备上安装 Endpoint Protection 客户端将可能在公司升级到 Configuration Manager 的下一个版本时进行。  

     有关详细信息，请参阅[在 System Center Configuration Manager 中配置 Endpoint Protection](../../../protect/deploy-use/configure-endpoint-protection.md)。  

6.  在完成了客户端的配置设置后，Jane 准备安装 Configuration Manager 客户端。 她必须在 Windows Embedded 设备上手动禁用写入筛选器，然后才能安装客户端。 她阅读网亭附带的 OEM 文档，并按照其说明执行操作来禁用写入筛选器。  

     Jane 重命名设备，使其使用公司标准命名格式，然后在包含客户端源文件的映射驱动器中使用以下命令运行 CCMSetup 来手动安装客户端： **CCMSetup.exe /MP:mpserver.cohovineyardandwinery.com SMSSITECODE=CO1**  

     此命令安装客户端，将客户端分配给具有 Intranet FQDN **mpserver.cohovineyardandwinery.com**的管理点，并将客户端分配给名为 **CO1**的主站点。  

     Jane 知道，客户端安装并将其状态发送回站点始终会花很长时间。 因此，她等待一段时间，之后确认客户端已成功安装、分配到站点，并显示为她为 Windows Embedded 设备创建的集合中的客户端。  

     为了进一步确认，她在设备的“控制面板”中检查 Configuration Manager 的属性，并将其与站点管理的标准 Windows 计算机进行比较。 例如，在“组件”  选项卡上，“硬件清单代理”  显示“已启用” ，并且在“操作”  选项卡上有 11 项可用操作，其中包括“应用程序部署评估周期”  和“发现数据收集周期” 。  

     Jane 确信客户端已成功安装、分配并且正在从管理点接收客户端策略，然后按照 OEM 的说明手动启用写入筛选器。  

     有关详情，请参阅：  

    -   [如何在 System Center Configuration Manager 中将客户端部署到 Windows 计算机](../../../core/clients/deploy/deploy-clients-to-windows-computers.md)  

    -   [如何在 System Center Configuration Manager 中将客户端分配到一个站点](../../../core/clients/deploy/assign-clients-to-a-site.md)  

7.  在 Configuration Manager 客户端已安装在 Windows Embedded 设备上后，Jane 确认她可采用与管理标准 Windows 客户端相同的方式来管理它们。 例如，她可以从 Configuration Manager 控制台中使用远程控制进行远程管理、为它们启动客户端策略，以及查看客户端属性和硬件清单。  

     由于这些设备已加入了 Active Directory 域，因此她不必手动将它们批准为受信任的客户端，并从 Configuration Manager 控制台中确认它们已得到批准。  

     有关详细信息，请参阅 [How to manage clients in System Center Configuration Manager](../../../core/clients/manage/manage-clients.md)。  

8.  为了安装交互式演示文稿软件，Jane 运行“部署软件向导”  并配置所需的应用程序。 在向导的“用户体验”  页上的“Windows Embedded 设备的写入筛选器处理”  部分，她接受选择“在截止时间或在维护时段内提交更改(需要重启)” 的默认选项。  

     Jane 为写入筛选器保留此默认选项以确保应用程序在重启后保留，以使其始终可供使用网亭的访客使用。 在每天的维护时段中，可以安全地进行安装和任何更新的重启。  

     Jane 将应用程序部署到 Windows Embedded 设备集合。  

     有关详细信息，请参阅 [如何使用 System Center Configuration Manager 部署应用程序](../../../apps/deploy-use/deploy-applications.md)。  

9. 为了配置 Endpoint Protection 的定义更新，Jane 使用软件更新并运行创建自动部署规则向导。 她选择“定义更新”  模板以使用适合于 Endpoint Protection 的设置预先填充向导。  

     这些设置包括向导的“用户体验”  页上的下列设置：  

    -   **到期行为**：未选中“软件安装”  复选框。  

    -   **Windows Embedded 设备的写入筛选器处理**：未选中“在截止时间或在维护时段内提交更改 (需要重启)”  复选框。  

     Jane 保留这些默认设置。 这两个选项连同此配置一起，使得 Endpoint Protection 的任何软件更新可在白天安装到覆盖区，而不用等到维护时段安装和提交。 此配置与计算机运行反恶意软件保护的公司安全策略最为符合。  

    > [!NOTE]  
    >  与应用程序的软件安装不同，Endpoint Protection 的软件更新定义可能会非常频繁出现，甚至会一天出现多次。 它们通常是很小的文件。 对于这些类型的安全相关部署，始终安装到覆盖区（而不是等到维护时段再安装）通常可能很有利。 如果设备重启，Configuration Manager 客户端将快速重新安装软件定义更新，因为此操作将启动评估检查，而不会等到下一次计划的评估时进行。  

     Jane 为自动部署规则选择 Windows Embedded 设备集合。  

     有关详细信息，请参阅  
                  步骤 3：按[在 System Center Configuration Manager 中配置 Endpoint Protection](../../../protect/deploy-use/configure-endpoint-protection.md)中所述，配置 Configuration Manager 软件更新以将定义更新提供给客户端计算机  

10. Jane 决定配置一个定期在覆盖区上提交所有更改的维护任务。 此任务是为了支持软件更新定义部署，减少累积并必须在每次设备重启时再次安装的更新的数量。 在她的体验中，这可帮助反恶意软件程序更有效地运行。  

    > [!NOTE]  
    >  如果嵌入式设备曾经运行另一个支持提交更改的管理任务，这些软件更新定义将自动提交到映像。 例如，安装新版本的交互式演示文稿软件也会提交软件更新定义的更改。 或者，每个月安装将在维护时段中安装的标准软件更新也会提交软件更新定义的更改。 但是，在标准软件更新未运行并且交互式演示文稿软件不太可能非常频繁更新的此方案中，可能要几个月之后才会将软件定义更新自动提交到映像。  

     Jane 首先创建一个只有名称设置的自定义任务序列。 她运行创建任务序列向导：  

    1.  在“创建新的任务序列”  页上，她选择“创建新的自定义任务序列” ，然后单击“下一步” 。  

    2.  在“任务序列信息”  页面上，她输入 **Maintenance task to commit changes on embedded devices** 作为任务序列名称，然后单击“下一步” 。  

    3.  在“摘要”  页上，她选择“下一步” 并完成向导。  

     然后，Jane 将此自定义任务序列部署到 Windows Embedded 设备集合，并配置计划以每个月运行。 作为部署设置的一部分，她选中“在截止时间或在维护时段内提交更改(需要重启)”  复选框，以便在重启后保留更改。 为了配置此部署，她选择刚刚创建的自定义任务序列，然后在“主页”  选项卡上的“部署”  组中单击“部署”  以启动部署软件向导：  

    1.  在“常规”  页上，她选择 Windows Embedded 设备集合，然后单击“下一步” 。  

    2.  在“部署设置”  页上，她为“目的”  选择“必需” ，然后单击“下一步” 。  

    3.  在“计划”  页上，她单击“新建”  以指定维护时段内的一个每周计划，然后单击“下一步” 。  

    4.  她完成向导而未进行任何进一步的更改。  

     有关详细信息，请参阅  
                  [管理任务序列以在 System Center Configuration Manager 中自动执行任务](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md)。  

11. 为使网亭自动运行，Jane 编写了一个脚本，以按照下列设置来配置设备：  

    -   使用无密码的来宾帐户自动登录。  

    -   在启动时自动运行交互式演示文稿软件。  

     Jane 使用包和程序将此脚本部署到 Windows Embedded 设备集合。 在她运行“部署软件向导”时，她再次选中“在截止时间或在维护时段内提交更改(需要重启)”  复选框，以便在重新启动后保留更改。  

     有关详细信息，请参阅 [System Center Configuration Manager 中的包和程序](../../../apps/deploy-use/packages-and-programs.md)。  

12. 第二天早上，Jane 检查 Windows Embedded 设备。 她确认下列几点：  

    -   使用来宾帐户自动登录了网亭。  

    -   交互式演示文稿软件正在运行。  

    -   已安装 Endpoint Protection 客户端，而且它拥有最新的软件更新定义。  

    -   设备在维护时段内重新启动。  

     有关详情，请参阅：  

    -   [如何在 System Center Configuration Manager 中监视 Endpoint Protection](../../../protect/deploy-use/monitor-endpoint-protection.md)  

    -   [使用 System Center Configuration Manager 监视应用程序](/sccm/apps/deploy-use/monitor-applications-from-the-console)  

13. Jane 监视网亭，并向其经理报告成功管理网亭的情况。 最终，为访客中心订购了 20 个网亭。  

     为了避免手动安装 Configuration Manager 客户端（需要手动禁用写入筛选器，然后再启用它），Jane 确保订单中包含自定义映像，该映像已包含 Configuration Manager 客户端的安装和站点分配。 此外，还按照该公司的命名格式对设备进行命名。  

     这些网亭在距访客中心开张还有一周时运抵。 在这段时间内，这些网亭连接到网络，而且它们的所有设备管理工作都是自动进行的，无需本地管理员干预。 Jane 确认这些网亭按照要求工作：  

    -   网亭上的客户端完成站点分配，并通过 Active Directory 域服务下载受信任的根密钥。  

    -   网亭上的客户端自动添加到 Windows Embedded 设备集合中，并在维护时段内自动配置。  

    -   已安装 Endpoint Protection 客户端，而且它拥有用于反恶意软件防护的最新软件更新定义。  

    -   已安装并自动运行交互式演示文稿软件，可供访客使用。  

14. 在完成此初始设置之后，仅在访客中心关闭时，才会执行更新可能要求的重新启动操作。  
