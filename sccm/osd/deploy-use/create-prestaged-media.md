---
title: "使用 System Center Configuration Manager 创建预留媒体 | Microsoft Docs"
description: "在 System Center Configuration Manager 中创建预留媒体来简化几个方案中的 Windows 部署。"
ms.custom: na
ms.date: 04/11/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ff6e7267-302a-4563-815e-cdc0d1a4b60f
caps.latest.revision: "12"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 33abf3853d912d423e427db4d35fb4a16167164e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="create-prestaged-media-with-system-center-configuration-manager"></a>使用 System Center Configuration Manager 创建预留媒体

*适用范围：System Center Configuration Manager (Current Branch)*

System Center Configuration Manager 中的预留媒体是 Windows 映像格式 (WIM) 文件，可以由制造商安装在裸机上，也可以安装在未连接到 Configuration Manager 环境的企业暂存中心。  
预留媒体包含用于启动目标计算机的启动映像，以及应用到目标计算机的操作系统映像。 你还可以指定要作为预留媒体的一部分包含的应用程序、包和驱动程序包。 此媒体不包含用于部署操作系统的任务序列。 在将新计算机发送给最终用户之前，预留媒体将应用到此计算机的硬盘驱动器。 为以下操作系统部署方案使用预留媒体：  

-   [为工厂中的 OEM 或本地 depot 创建映像](../../osd/deploy-use/create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

-   [在新计算机（裸机）上安装新版的 Windows](install-new-windows-version-new-computer-bare-metal.md)  

-   [部署 Windows To Go](deploy-windows-to-go.md)  

 在应用预留媒体后第一次启动计算机时，计算机会启动到 Windows PE 并连接到管理点，以查找将完成操作系统部署过程的任务序列。 你可以指定要作为预留媒体的一部分包含的应用程序、包和驱动程序包。 在部署使用预留媒体的任务序列时，向导会首先检查本地任务序列缓存以查找有效的内容，如果无法找到内容或内容已被修改，则向导会从分发点下载内容。  

##  <a name="BKMK_CreatePrestagedMedia"></a> 如何创建预留媒体  
 在使用“创建任务序列媒体向导”创建预留媒体之前，请确保满足以下所有条件：  

|任务|描述|  
|----------|-----------------|  
|启动映像|请考虑以下将用于在任务序列中部署操作系统的启动映像的相关事项：<br /><br /> -   启动映像的体系结构必须适合于目标计算机的体系结构。 例如，x64 目标计算机可启动和运行 x86 或 x64 启动映像。 但是，x86 目标计算机只能启动和运行 x86 启动映像。<br />-   确保启动映像包含预配目标计算机所需的网络和大容量存储驱动程序。|  
|创建用于部署操作系统的任务序列|作为预留媒体的一部分，必须指定用于部署操作系统的任务序列。<br /><br /> -   有关创建新任务序列的步骤，请参阅[创建用于安装操作系统的任务序列](../../osd/deploy-use/create-a-task-sequence-to-install-an-operating-system.md)。<br />-   有关任务序列的详细信息，请参阅[Manage task sequences to automate tasks](../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md)（管理任务序列以自动执行任务）。|  
|分发与任务序列关联的所有内容|必须将任务序列所需的所有内容至少分发到一个分发点。 这包括启动映像、操作系统映像和其他相关联的文件。 向导在创建独立媒体时从分发点中收集信息。 必须具有对该分发点上的内容库的 **读取** 访问权限。  有关详细信息，请参阅[关于内容库](../../core/plan-design/hierarchy/the-content-library.md)。|  
|目标计算机上的硬盘驱动器|在将预留媒体暂存到计算机的硬盘驱动器上之前，必须对目标计算机的硬盘驱动器进行格式化。 如果在应用媒体时硬盘驱动器未格式化，则部署操作系统的任务序列将在尝试启动目标计算机时失败。|  

> [!NOTE]  
>  “创建任务序列媒体向导”在媒体上设置以下任务序列变量条件：**_SMSTSMediaType = OEMMedia**。 你可以在任务序列中使用此条件。  

 使用以下过程来创建预留媒体。  

#### <a name="to-create-prestaged-media"></a>创建预留媒体  

1.  在 Configuration Manager 控制台中，单击“软件库” 。  

2.  在“软件库”工作区中，展开“操作系统”，然后单击“任务序列”。  

3.  在“主页”  选项卡上的“创建”  组中，单击“创建任务序列媒体”  以启动创建任务序列媒体向导。  

4.  在“选择媒体类型”  页上，指定以下信息，然后单击“下一步” 。  

    -   选择“预留媒体” 。  

    -   （可选）如果你希望允许在不需要用户输入的情况下部署操作系统，则选择“允许无人参与的操作系统部署” 。 如果选择此选项，则不会提示用户输入网络配置信息或指定可选的任务序列。 但是，如果针对密码保护配置了媒体，则仍会提示用户输入密码。  

5.  在“媒体管理”  页上，指定以下信息，然后单击“下一步” 。  

    -   如果要允许管理点根据客户端在站点边界中的位置将媒体重定向到另一个管理点，请选择“动态媒体”  。  

    -   如果希望媒体仅与指定的管理点联系，请选择“基于站点的媒体”  。  

6.  在“媒体属性”   页上，指定以下信息，然后单击“下一步” 。  

    -   **创建者**：指定创建媒体的人员。  

    -   **版本**：指定媒体的版本号。  

    -   **注释**：指定媒体用途的唯一说明。  

    -   **媒体文件**：指定输出文件的名称和路径。 向导会将输出文件写入到此位置。 例如：**\\\servername\folder\outputfile.wim**  

7.  在“安全”  页上，指定以下信息，然后单击“下一步” 。  

    -   选中“启用未知计算机支持”复选框，使媒体能够将操作系统部署到不是由 Configuration Manager 托管的计算机。 Configuration Manager 数据库中没有这些计算机的记录。  有关详细信息，请参阅[准备未知计算机部署](../get-started/prepare-for-unknown-computer-deployments.md)。  

    -   选中“使用密码保护媒体”  复选框，并输入强密码来帮助防止未经授权访问媒体。 如果指定密码，则用户必须提供该密码才能使用预留媒体。  

        > [!IMPORTANT]  
        >  作为最佳安全方案，请始终分配密码来帮助保护预留媒体。  

    -   对于 HTTP 通信，选择“创建自签名媒体证书” ，然后指定该证书的开始日期和到期日期。  

    -   对于 HTTPS 通信，选择“导入 PKI 证书” ，然后指定要导入的证书及其密码。  

         有关用于启动映像的此客户端证书的详细信息，请参阅 [PKI 证书要求](../../core/plan-design/network/pki-certificate-requirements.md)。  

    -   **用户设备相关性**：若要在 Configuration Manager 中支持以用户为中心的管理，请指定希望媒体如何将用户与目标计算机相关联。 有关操作系统部署如何支持用户设备相关性的详细信息，请参阅[如何将用户与目标计算机相关联](../get-started/associate-users-with-a-destination-computer.md)。  

        -   如果你希望媒体自动将用户与目标计算机关联，请指定“通过自动批准允许用户设备相关性”  。 此功能以部署操作系统的任务序列的操作为基础。 在此方案中，当任务序列将操作系统部署到目标计算机时，它会在指定的用户和目标计算机之间创建关系。  

        -   如果希望媒体获得批准后将用户与目标计算机关联，请指定“允许用户设备相关性挂起管理员批准”  。 此功能以部署操作系统的任务序列的作用域为基础。 在此方案中，任务序列在指定用户和目标计算机之间创建关系，但在部署操作系统之前等待管理用户的批准。  

        -   如果不希望媒体将用户与目标计算机关联，请指定“不允许用户设备相关性”  。 在此方案中，当任务序列部署操作系统时，它不会将用户与目标计算机关联。  

8.  在“任务序列”  页上，指定将在目标计算机上运行的任务序列。 任务序列引用的内容在“此任务序列引用了下列内容” 中显示。 验证内容，然后单击“下一步” 。  

9. 在“启动映像包”  页上，指定以下信息，然后单击“下一步” 。  

    > [!IMPORTANT]  
    >  分发的启动映像的体系结构必须适合于目标计算机的体系结构。 例如，x64 目标计算机可启动和运行 x86 或 x64 启动映像。 但是，x86 目标计算机只能启动和运行 x86 启动映像。  

    -   在“启动映像包”  框中，指定用于启动目标计算机的启动映像。 有关详细信息，请参阅[管理启动映像](../get-started/manage-boot-images.md)。  

    -   在“分发点”  框中，指定启动映像所在的分发点。 向导将从分发点中检索启动映像并将其写入媒体。  

        > [!NOTE]  
        >  你必须对分发点上的内容库具有 **读取** 访问权限。 有关详细信息，请参阅[关于内容库](../../core/plan-design/hierarchy/the-content-library.md)。  

    -   如果在此向导的“媒体管理”  页上选择了“基于站点的媒体”  ，请在“管理点”  框中指定主站点中的管理点。  

    -   如果在此向导的“媒体管理”  页上选择了“动态媒体”  ，请在“关联的管理点”  框中指定要使用的主站点管理点以及初始通信的优先级顺序。  

10. 在“映像”  页上，指定以下信息，然后单击“下一步” 。  

    -   在“映像包”  框中，指定操作系统映像。 有关详细信息，请参阅[管理操作系统映像](../get-started/manage-operating-system-images.md)。  

    -   如果该包中包含多个操作系统映像，请在“映像索引”  框中指定要部署的映像。  

    -   在“分发点”  框中，指定操作系统映像包所在的分发点。 向导将从分发点中检索操作系统映像并将其写入媒体。  

11. 在“自定义”  页上，指定以下信息，然后单击“下一步” 。  

    -   指定任务序列用于部署操作系统的变量。  

    -   指定想要在运行任务序列之前运行的任何预启动命令。 预启动命令是一个脚本或可执行文件，它可以在任务序列运行以安装操作系统之前在 Windows PE 中与用户交互。 有关用于媒体的预启动命令的详细信息，请参阅[任务序列媒体的预启动命令](../understand/prestart-commands-for-task-sequence-media.md)。  

        > [!TIP]  
        >  在任务序列媒体创建过程中，任务序列会将包 ID 和预启动命令行（包括任何任务序列变量的值）写入到运行 Configuration Manager 控制台的计算机上的 CreateTSMedia.log 日志文件。 你可以查看此日志文件以验证任务序列变量的值。  

12. 完成向导。  

## <a name="next-steps"></a>后续步骤
[部署企业版操作系统的方案](scenarios-to-deploy-enterprise-operating-systems.md)
