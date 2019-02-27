---
title: 创建 Windows 应用程序
titleSuffix: Configuration Manager
description: 了解有关在 Configuration Manager 中创建和部署 Windows 应用程序的详细信息。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 9181c84e-d74f-44ea-9bb9-f7805eb465fc
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1fa26147539abc611b86791f6dd9a4be0bc89c59
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56156468"
---
# <a name="create-windows-applications-in-configuration-manager"></a>在 Configuration Manager 中创建 Windows 应用程序

适用范围：System Center Configuration Manager (Current Branch)

除了[创建应用程序](/sccm/apps/deploy-use/create-applications)的其他 Configuration Manager 要求和过程，在创建和部署适用于 Windows 设备的应用程序时还需考虑以下注意事项。  



## <a name="bkmk_general"></a> 一般注意事项  

Configuration Manager 支持为 Windows 8.1 和 Windows 10 设备部署 Windows 应用包 (.appx) 和应用程序包 (.appxbundle) 格式。

从版本 1806 开始，Configuration Manager 还支持新的 Windows 10 应用包 (.msix) 和应用程序包 (.msixbundle) 格式。 最新的 [Windows Insider Preview](https://insider.windows.com/) 内部版本当前支持这些格式。<!--1357427-->  

- 有关 MSIX 的概述，请参阅 [MSIX 详解](https://blogs.msdn.microsoft.com/sgern/2018/06/18/a-closer-look-at-msix/)。  

- 有关如何创建新的 MSIX 应用，请参阅 [Insider 内部版本 17682 中引入的 MSIX 支持](https://techcommunity.microsoft.com/t5/MSIX-Blog/MSIX-support-introduced-in-Insider-Build-17682/ba-p/202376)。  

在 Configuration Manager 控制台中创建应用程序时，请将应用程序安装文件“类型”选为“Windows 应用包”（\*.appx、\*.appxbundle、\*.msix、\*.msixbundle）。 有关详细信息，请参阅[创建应用程序](/sccm/apps/deploy-use/create-applications)。 

> [!Note]  
> 若要利用新的 Configuration Manager 功能，请先将客户端更新到最新版本。 即使在更新站点和控制台时 Configuration Manager 控制台中会显示新功能，但只有在客户端版本也是最新版本之后，完整方案才能正常运行。<!--SCCMDocs issue 646-->  



## <a name="bkmk_provision"></a> 为设备上的所有用户预配 Windows 应用包
<!--1358310--> 从版本 1806 开始，使用 Windows 应用包为设备上的所有用户预配应用程序。 此方案的一个常见示例是将来自适用于企业和适用于教育的 Microsoft Store 的应用（如 Minecraft: Education Edition）预配到学校学生使用的所有设备。 以前，Configuration Manager 仅支持按用户安装这些应用程序。 登录到新的设备后，学生不得不等会儿时间来访问应用。 现在，将应用预配到所有用户的设备时，他们的工作更快更高效。

> [!Important]  
> 在设备上安装、预配和更新相同 Windows 应用包的不同版本时要小心，否则可能会导致意外的结果。 使用 Configuration Manager 预配应用时就需要注意些，但随后用户可从 Microsoft Store 更新应用。 有关详细信息，请在[管理来自适用于企业的 Microsoft Store 的应用](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business#next-steps)时参阅下一步指南。  

当预配脱机许可应用时，Configuration Manager 不允许 Windows 从 Microsoft Store 自动更新它。  

Configuration Manager 支持在以下 Windows 版本上预配应用：<!--SCCMDocs-pr issue 2762-->
- 安装操作：Windows 10 1607 版及更高版本
- 卸载操作：Windows 10 1703 版及更高版本

若要配置此功能的 Windows 应用部署类型，请启用“为设备上的所有用户预配此应用程序”选项。 有关详细信息，请参阅[创建应用程序](/sccm/apps/deploy-use/create-applications)。


> [!Note]  
> 如果需要从用户已经登录的设备中卸载已预配的应用程序，则需要创建两个卸载部署。 将第一个卸载部署定位到包含设备的设备集合。 将第二个卸载部署定位到包含已登录到具有预配应用程序的设备的用户的用户集合。 当在设备上卸载预配的应用时，Windows 当前不会为用户卸载该应用。 



## <a name="bkmk_uwp"></a> 对通用 Windows 平台 (UWP) 应用的支持  

Windows 10 设备无需旁加载密钥即可安装业务线应用。 但是，若要在 Windows 上启用旁加载，注册表项 `HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\Appx\AllowAllTrustedApps` 的值必须为 1。  

如果未配置此注册表项，Configuration Manager 在第一次向设备部署应用时自动将此值设置为 1。 如果将此值设置为 0，则 Configuration Manager 无法自动更改此值，业务线应用部署失败。  

数字签名 UWP 业务线应用。 使用在部署应用的每台设备上受信任的代码签名证书。 使用组织 PKI 中的证书，或从 Windows 已信任其公共根证书的第三方提供程序购买证书。  

若要对移动应用包进行签名，请使用下表确定要使用的代码签名证书的类型：

| 包  | Symantec  | 非 Symantec  |
|---------|---------|---------|
| Windows 10 移动设备上的通用 .appx 包 | 是 | 是 |
| .xap 包 | 是 | 否 | 
| 为 Windows Phone 8.1 生成的 .appx 包，可在 Windows 10 移动设备上安装 | 是 | 否 | 



## <a name="bkmk_mdm-msi"></a> 将 Windows Installer 应用部署到已注册 MDM 的 Windows 10 设备  

**通过 MDM 的 Windows Installer (\*.msi)** 部署类型可用于创建基于 Windows Installer 的应用并将其部署到运行 Windows 10 且已注册 MDM 的设备上。  

使用此部署类型时，请考虑以下几点：    

-   仅上传具有 MSI 扩展的单个文件。  

-   Configuration Manager 使用文件的产品代码和产品版本进行应用检测。  

-   Windows 使用应用的默认重启行为。 Configuration Manager 不会控制应用重启行为。  

-   为单个用户安装每用户 MSI 包。  

-   为设备上的所有用户安装每计算机 MSI 包。  

-   Configuration Manager 支持应用更新。 每个版本的 MSI 产品代码必须相同。  
