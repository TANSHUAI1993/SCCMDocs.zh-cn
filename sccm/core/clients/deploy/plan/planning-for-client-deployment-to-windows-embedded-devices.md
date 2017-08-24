---
title: "规划 Windows Embedded 设备的客户端部署 | Microsoft Docs"
description: "在 System Center Configuration Manager 中规划 Windows Embedded 设备的客户端部署。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 038e61f9-f49d-41d1-9a9f-87bec9e00d5d
caps.latest.revision: "7"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: f7ef476a2ebcf0161ebb70d8a3d95f77806aa05e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="planning-for-client-deployment-to-windows-embedded-devices-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中计划 Windows Embedded 设备的客户端部署

*适用范围：System Center Configuration Manager (Current Branch)*

<a name="BKMK_DeployClientEmbedded"></a>如果 Windows Embedded 设备不包括 System Center Configuration Manager 客户端，并且设备满足所需的依赖关系要求，则可以使用任何客户端安装方法。 如果嵌入式设备支持写入筛选器，则必须在安装客户端之前禁用这些筛选器，然后在安装客户端并将其分配给站点之后再次重新启用筛选器。  

 请注意，当禁用筛选器时，不应禁用筛选器驱动程序。 启动计算机时，这些驱动程序通常都将自动启动。 禁用驱动程序将阻止客户端的安装，或者将干扰写入筛选器业务流程，从而导致客户端操作失败。 以下是与必须保持运行状态的每个写入筛选器类型相关联的服务：  

|写入筛选器类型|驱动程序|类型|描述|  
|-----------------------|------------|----------|-----------------|  
|EWF|EWF|内核|在受保护的卷上实现扇区级别 I/O 重定向。|  
|FBWF|FBWF|文件系统|在受保护的卷上实现文件级别 I/O 重定向。|  
|UWF|uwfreg|内核|UWF 注册表重定向程序|  
|UWF|uwfs|文件系统|UWF 文件重定向程序|  
|UWF|uwfvol|内核|UWF 卷管理器|  

 写入筛选器控制在你进行更改时（如在安装软件时）如何更新嵌入式设备上的操作系统。 如果启用写入筛选器，则不会直接对操作系统进行更改，而是将这些更改重定向到临时覆盖区。 如果更改仅写入到覆盖区，则当嵌入式设备关闭时，更改将会丢失。 但是，如果临时禁用了写入筛选器，则可能会将更改设置为永久性更改，以便每次重启嵌入式设备时不必再进行更改（或重新安装软件）。 但是，临时禁用然后重新启用写入筛选器需要一次或多次重启，因此，你通常需要配置维护时段，使重启发生在工作时间之外，以控制其发生的时间。  

 你可以将选项配置为在部署软件（如应用程序、任务序列、软件更新和 Endpoint Protection 客户端）时先自动禁用然后再重新启用写入筛选器。 具有使用自动修正的配置项目的配置基线是个例外。 在此情况下，始终在覆盖区进行修正，以便仅在重启设备之前可以使用它。 在下一个评估周期会再次应用修正，但只对覆盖区应用，重启时会清除覆盖区。 要强制 Configuration Manager 提交修正更改，你可以部署配置基线，然后部署支持尽快提交更改的另一个软件部署。  

 如果禁用了写入筛选器，则可以使用软件中心在 Windows Embedded 设备上安装软件。 但是，如果启用了写入筛选器，则安装将失败，并且 Configuration Manager 会显示一条错误消息，表明你没有足够的权限安装应用程序。  

> [!WARNING]  
>  即使未选择 Configuration Manager 选项来提交更改，那么如果进行了提交更改的另一个软件安装或更改，则可能会提交更改。 在此情况下，将提交原始更改以及新更改。  

 当 Configuration Manager 禁用写入筛选器以使更改为永久更改时，只有具有本地管理权限的用户才能登录和使用嵌入式设备。 在此期间，低权限用户会被锁在外面并看到一条消息，告知他们计算机由于正在维护而不可用。 这有助于保护处于可以永久应用更改的状态的设备，此维护模式锁定行为是针对用户无法登录这些设备的时间配置维护时段的另一个原因。  

 Configuration Manager 支持管理下列类型的写入筛选器：  

-   基于文件的写入筛选器 (FBWF) – 有关详细信息，请参阅[基于文件的写入筛选器](http://go.microsoft.com/fwlink/?LinkID=204717)。  

-   增强型写入筛选器 (EWF) RAM – 有关详细信息，请参阅[增强型写入筛选器](http://go.microsoft.com/fwlink/?LinkId=204718)。  

-   统一写入筛选器 (UWF) – 有关详细信息，请参阅[统一写入筛选器](http://go.microsoft.com/fwlink/?LinkId=309236)。  

 当 Windows Embedded 设备处于 EWF RAM 注册模式时，Configuration Manager 不支持写入筛选器操作。  

> [!IMPORTANT]  
>  如果可以选择，请将基于文件的写入筛选器 (FBWF) 与 Configuration Manager 一起使用，以便提高效率和可伸缩性。
>
> **对于仅使用 FBWF 的设备：**配置以下例外以在设备重启之间保留客户端状态和清单数据：  
>   
>  -   CCMINSTALLDIR\\*.sdf  
> -   CCMINSTALLDIR\ServiceData  
> -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\StateSystem  
>   
>  运行 Windows Embedded 8.0 和更高版本的设备不支持包含通配符的排除项。 在这些设备上，必须分别配置以下排除项：  
>   
>  -   CCMINSTALLDIR 中的所有文件都具有 .sdf 扩展名，通常为：  
>   
>     -   UserAffinityStore.sdf  
>     -   InventoryStore.sdf  
>     -   CcmStore.sdf  
>     -   StateMessageStore.sdf  
>     -   CertEnrollmentStore.sdf  
> -   CCMINSTALLDIR\ServiceData  
> -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\StateSystem  
>   
> **对于仅使用 FBWF 和 UWF 的设备：**当工作组中的客户端使用证书向管理点进行身份验证时，还必须排除私钥以确保客户端继续与管理点通信。 在这些设备上配置以下例外：  
>   
>  -   c:\Windows\System32\Microsoft\Protect  
> -   c:\ProgramData\Microsoft\Crypto  
> -   HKEY_LOCAL_MACHINE\Software\Microsoft\SystemCertificates\SMS\Certificates  

 有关在 Configuration Manager 中部署和管理启用写入筛选器的 Windows Embedded 设备的示例场景，请参阅[在 Windows Embedded 设备上部署和管理 System Center Configuration Manager 客户端的示例场景](../../../../core/clients/deploy/example-scenario-for-deploying-and-managing-clients-on-windows-embedded-devices.md)。  

 有关如何生成 Windows Embedded 设备映像以及配置写入筛选器的详细信息，请参阅 Windows Embedded 文档或与你的 OEM 联系。  

> [!NOTE]  
>  为软件部署和配置项目选择合适的平台时，这些内容会显示 Windows Embedded 系列，而不是特定版本。 请使用以下列表将特定版本的 Windows Embedded 映射到列表框中的选项：  
>   
>  -   “基于 Windows XP (32 位)的嵌入式操作系统” 包括以下各项：  
>   
>      -   Windows XP Embedded  
>     -   Windows Embedded for Point of Service  
>     -   Windows Embedded Standard 2009  
>     -   Windows Embedded POSReady 2009  
> -   “基于 Windows 7 (32 位)的嵌入式操作系统” 包括以下各项：  
>   
>      -   Windows Embedded Standard 7（32 位）  
>     -   Windows Embedded POSReady 7（32 位）  
>     -   Windows ThinPC  
> -   “基于 Windows 7 (64 位) 的嵌入式操作系统” 包括以下各项：  
>   
>      -   Windows Embedded Standard 7（64 位）  
>     -   Windows Embedded POSReady 7（64 位）
