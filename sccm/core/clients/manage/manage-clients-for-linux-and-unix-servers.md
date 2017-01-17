---
title: "管理 Linux 和 UNIX 客户端 | Microsoft Docs"
description: "在 System Center Configuration Manager 中管理 Linux 和 UNIX 服务器上的客户端。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 948664f2-239d-47a8-92fc-f8efeebd5796
caps.latest.revision: 7
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 55c953f312a9fb31e7276dde2fdd59f8183b4e4d
ms.openlocfilehash: d3a44d516bb1e2766a7a10b62d52405eecef31fc


---
# <a name="how-to-manage-clients-for-linux-and-unix-servers-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中管理 Linux 和 UNIX 服务器客户端

*适用范围：System Center Configuration Manager (Current Branch)*

当使用 System Center Configuration Manager 管理 Linux 和 UNIX 服务器时，可以配置集合、维护时段和客户端设置，以帮助管理服务器。 此外，尽管适用于 Linux 和 UNIX 的 | System Center Configuration Manager 客户端没有用户界面，但可以强制客户端手动轮询客户端策略。

##  <a name="a-namebkmkcollectionsforlnua-collections-of-linux-and-unix-servers"></a><a name="BKMK_CollectionsforLnU"></a> Collections of Linux and UNIX servers  
 使用集合管理 Linux 和 UNIX 服务器组的方式与使用集合管理其他客户端类型的方式相同。 集合可以是直接成员身份集合，已可以是基于查询的集合（用于确定客户端操作系统、硬件配置或有关站点数据库中存储的客户端的其他详细信息）。 例如，你可以使用包括 Linux 和 UNIX 服务器的集合来管理下列各项：  

-   客户端设置  

-   软件部署  

-   强制维护时段  

 必须先成功地从客户端收集硬件清单，然后才可通过客户端的操作系统或分发来标识 Linux 或 UNIX 客户端。 关于收集硬件清单的信息，请参阅 [System Center Configuration Manager 中 Linux 和 UNIX 的硬件清单](../../../core/clients/manage/inventory/hardware-inventory-for-linux-and-unix.md)。  

 硬件清单的默认客户端设置包括有关客户端计算机的操作系统的信息。 你可以使用 **Operating System** 类的 **Caption** 属性来标识 Linux 或 UNIX 服务器的操作系统。  

 在 Configuration Manager 控制台的“资产和符合性”工作区中的“设备”节点下，可查看有关运行 Linux 和 UNIX 的 Configuration Manager 客户端的计算机的详细信息。 在 Configuration Manager 控制台的“资产和符合性”工作区中，可在“操作系统”列中查看每台计算机的操作系统名称。  

 默认情况下，Linux 和 UNIX 服务器属于 **所有系统** 集合的成员。 建议你生成仅包括 Linux 和 UNIX 服务器或其子集的自定义集合。 此集合可让你管理向适用计算机组部署软件或分配客户端设置等操作。 例如，如果你将 RHEL6 x64 计算机软件部署到包含 Windows 和 Linux 计算机的集合，则部署状态将显示为部分成功。 而在将软件部署到仅包含 RHEL6 x64 计算机的集合时，你可以使用状态消息和报表来准确地识别部署是否成功。  

 在为 Linux 和 UNIX 服务器生成自定义集合时，请包含成员身份规则查询，并在这些查询中包括操作系统特性的 Caption 特性。 有关创建集合的信息，请参阅[如何在 System Center Configuration Manager 中创建集合](../../../core/clients/manage/collections/create-collections.md)。  

##  <a name="a-namebkmkmaintenancewindowsforlnua-maintenance-windows-for-linux-and-unix-servers"></a><a name="BKMK_MaintenanceWindowsforLnU"></a> Maintenance windows for Linux and UNIX servers  
 Linux 和 UNIX 服务器的 Configuration Manager 客户端支持使用维护时段。 与对基于 Windows 的客户端的支持相比，此支持并无变化。  

 有关如何使用维护时段的详细信息，请参阅[如何在 System Center Configuration Manager 中使用维护时段](../../../core/clients/manage/collections/use-maintenance-windows.md)。  

##  <a name="a-namebkmkclientsettingsforlnua-client-settings-for-linux-and-unix-servers"></a><a name="BKMK_ClientSettingsforLnU"></a> Client settings for Linux and UNIX servers  
 你可以使用与配置其它客户端设置相同的方式配置适用于 Linux 和 UNIX 服务器的客户端设置。  

 默认情况下， **默认客户端代理设置** 适用于 Linux 和 UNIX 服务器。 也可以创建自定义客户端设置，并将它们部署到包含特定客户端操作系统或多种客户端操作系统的集合。  

 没有仅适用于 Linux 和 UNIX 客户端的其他客户端设置。 但是，有不适用于 Linux 和 UNIX 的客户端的默认客户端设置。 Linux 和 UNIX 客户端仅应用所支持功能的设置，并忽略不支持的功能的任何配置。  

 例如，你创建指定硬件清单计划的自定义客户端设备设置，然后将其分配给包括 Linux 计算机的集合。 结果是在 Linux 和 UNIX 服务器上强制执行硬件清单计划。 接下来，你创建启用并配置远程控制设置的自定义客户端设备设置，并将其分配给同一集合。 结果是 Linux 和 UNIX 服务器忽略远程控制设置。 这是因为在 Configuration Manager 中，Linux 和 UNIX 客户端不支持远程控制。  

 有关配置客户端设置的信息，请参阅[如何在 System Center Configuration Manager 中配置客户端设置](../../../core/clients/deploy/configure-client-settings.md)。  

##  <a name="a-namebkmkpolicyforlnua-computer-policy-for-linux-and-unix-servers"></a><a name="BKMK_PolicyforLnU"></a> Computer policy for Linux and UNIX servers  
 Linux 和 UNIX 服务器的 Configuration Manager 客户端定期轮询其站点中的计算机策略，以了解请求的配置，并检查部署。  

 也可以强制 Linux 或 UNIX 服务器的客户端立即轮询计算机策略。 若要立即轮询，请使用服务器上的 **根** 凭据运行以下命令： **/opt/microsoft/configmgr/bin/ccmexec -rs policy**  

 有关计算机策略轮询的详细信息包含在共享的客户端日志文件 **scxcm.log**中。  

> [!NOTE]  
>  Linux 和 UNIX 的 Configuration Manager 客户端从不请求或处理用户策略。  

##  <a name="a-namebkmkmanagelinuxcertsa-how-to-manage-certificates-on-the-client-for-linux-and-unix"></a><a name="BKMK_ManageLinuxCerts"></a> How to manage certificates on the client for Linux and UNIX  
 安装适用于 Linux 和 UNIX 的客户端后，你可以使用 **certutil** 工具来更新包含新 PKI 证书的客户端，并导入新的证书吊销列表 (CRL)。 安装适用于 Linux 和 UNIX 的客户端时，此工具放置在以下位置： **/opt/microsoft/configmgr/bin/certutil**  

 若要管理证书，请使用以下选项之一在每个客户端上运行 certutil：  

|选项|更多信息|  
|------------|----------------------|  
|importPFX|使用此选项可指定证书，以替换客户端当前使用的证书。<br /><br /> 使用 **-importPFX**时，还必须使用 **-password** 命令行参数来提供与 PKCS#12 文件关联的密码。<br /><br /> 使用 **-rootcerts** 可指定任何其他根证书要求。<br /><br /> 示例：**certutil -importPFX &lt;Path to the PKCS#12 certificate> -password &lt;Certificate password\> [-rootcerts &lt;comma-separated list of certificates>]**|  
|-importsitecert|使用此选项可更新管理服务器上的站点服务器签名证书。<br /><br /> 示例：**certutil -importsitecert &lt;Path to the DER certificate\>**|  
|-importcrl|使用此选项可通过一个或多个 CRL 文件路径更新客户端上的 CRL。<br /><br /> 示例：**certutil -importcrl &lt;comma separated CRL file paths\>**|  



<!--HONumber=Dec16_HO3-->


