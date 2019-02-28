---
title: 发行说明
titleSuffix: Configuration Manager
description: 了解有关产品中尚未解决或 Microsoft 支持知识库文章中未涵盖的紧急问题。
ms.date: 02/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: bc19092f1272611ea3e05d708bf89bda1a4ba3b9
ms.sourcegitcommit: 0a23cde6112cbb5987f433bffcf6f223b994ba72
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/22/2019
ms.locfileid: "56667454"
---
# <a name="release-notes-for-configuration-manager"></a>Configuration Manager 发行说明

适用范围：System Center Configuration Manager (Current Branch)

在 Configuration Manager 中，产品发布说明仅限于紧急问题。 产品中尚未解决这些紧急问题，Microsoft 支持知识库文章中也未对此进行详细介绍。  

特定于功能的文档包含有关影响核心方案的已知问题的信息。  

> [!TIP]  
>  本主题包含 Configuration Manager 当前分支的发行说明。 有关技术预览分支的信息，请参阅[技术预览](/sccm/core/get-started/technical-preview)  

有关不同版本引入的新功能的信息，请参阅以下文章：
- [1810 版中的新增功能](/sccm/core/plan-design/changes/whats-new-in-version-1810)
- [1806 版中的新增功能](/sccm/core/plan-design/changes/whats-new-in-version-1806)  
- [1802 版中的新增功能](/sccm/core/plan-design/changes/whats-new-in-version-1802)



## <a name="set-up-and-upgrade"></a>设置和升级  


### <a name="when-using-redistributable-files-from-the-cdlatest-folder-setup-fails-with-a-manifest-verification-error"></a>在使用 CD.Latest 文件夹中的可再发行文件时安装失败，并出现清单验证错误
<!-- 510080, 490569  -->

从为版本 1606 创建的 CD.Latest 文件夹运行安装程序并使用该 CD.Latest 文件夹中包含的可再发行文件时，将导致安装失败，Configuration Manager 安装日志中显示以下错误：

  `ERROR: File hash check failed for defaultcategories.dll`  
  `ERROR: Manifest verification failed. Wrong version of manifest?`

#### <a name="workaround"></a>解决方法
使用以下选项之一：
 - 在安装过程中，选择从 Microsoft 下载最新可再发行文件。 使用最新可再发行文件而不是 CD.Latest 文件夹中包含的文件。
 - 手动删除 *cd.latest\redist\languagepack\zhh* 文件夹，然后再次运行安装程序。


### <a name="setup-command-line-option-joinceip-must-be-specified"></a>必须指定安装程序命令行选项 JoinCEIP
<!--510806-->
适用范围：Configuration Manager 版本 1802

从 Configuration Manager 版本 1802 开始，从产品中删除了客户体验改善计划 (CEIP) 功能。 从命令行或无人参与的脚本中[自动安装](/sccm/core/servers/deploy/install/command-line-options-for-setup)新站点时，安装程序返回指示缺失所需参数的错误。 

#### <a name="workaround"></a>解决方法
虽然它对安装进程的结果没有影响，但请在安装程序命令行中包含 JoinCEIP 参数。

 > [!Note]  
 > [控制台安装程序](/sccm/core/servers/deploy/install/install-consoles)的 EnableSQM 参数不是必需的。


### <a name="cloud-service-manager-component-stopped-on-site-server-in-passive-mode"></a>在被动模式下，站点服务器上的云服务管理器组件停止
<!--VSO 2858826, SCCMDocs issue 772-->
适用范围：Configuration Manager 版本 1806

如果[服务连接点](/sccm/core/servers/deploy/configure/about-the-service-connection-point)与[被动模式下的站点服务器](/sccm/core/servers/deploy/configure/site-server-high-availability)共存，则无法启动[云管理网关](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)的部署和监视。 云服务管理器组件 (MS_CLOUD_SERVICES_MANAGER) 处于停止状态。

#### <a name="workaround"></a>解决方法
将服务连接点角色移至另一台服务器。



<!-- ## Backup and recovery  -->


<!--## Client deployment and upgrade-->



## <a name="os-deployment"></a>OS 部署

### <a name="after-passive-site-server-is-promoted-the-default-boot-image-packages-still-have-package-source-on-the-previous-active-server"></a>提升被动站点服务器之后，默认启动映像包在上一个活动服务器上仍有包源
<!--3453224, SCCMDocs-pr issue 3097-->
适用范围：Configuration Manager 版本 1810

如果站点服务器处于被动模式（服务器 B），在将其提升为活动模式时，默认启动映像的内容位置将继续引用先前活动的服务器（服务器 A）。 如果服务器 A 出现硬件故障，则无法更新或更改默认启动映像。

#### <a name="workaround"></a>解决方法
无



## <a name="software-updates"></a>软件更新

### <a name="security-roles-are-missing-for-phased-deployments"></a>分阶段部署缺少安全角色
<!--3479337, SCCMDocs-pr issue 3095-->
适用范围：Configuration Manager 版本 1810

OS Deployment Manager 内置安全角色具有[分阶段部署](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence)的权限。 以下角色缺少这些权限：  

- **应用程序管理员**  
- **应用程序部署管理员**  
- **软件更新管理员**  

“应用创建者”角色可能看起来对分阶段部署具有某些权限，但无法创建部署。 

具有这些角色的用户可以启动“创建分阶段部署”向导，并可以查看应用程序或软件更新的分阶段部署。 他们无法完成向导，也无法对现有部署进行任何更改。

#### <a name="workaround"></a>解决方法
创建自定义安全角色。 复制现有安全角色，并在“分阶段部署”对象类上添加以下权限：
- 创建  
- 删除  
- 修改  
- 读取  

有关详细信息，请参阅[创建自定义安全角色](/sccm/core/servers/deploy/configure/configure-role-based-administration#BKMK_CreateSecRole)。


### <a name="changing-office-365-client-setting-doesnt-apply"></a>更改 Office 365 客户端设置不适用 
<!--511551-->
适用范围：Configuration Manager 版本 1802  

部署[客户端设置](/sccm/core/clients/deploy/about-client-settings#enable-management-of-the-office-365-client-agent)，其中将“启用 Office 365 客户端代理的管理”配置为 `Yes`。 然后，将该设置更改为 `No` 或 `Not Configured`。 更新目标客户端上的策略后，Office 365 更新仍由 Configuration Manager 管理。 

#### <a name="workaround"></a>解决方法
将以下注册表值更改为 `0` 并重启 **Microsoft Office 即点即用服务** (ClickToRunSvc)：

```
[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\office\16.0\Common\officeupdate]
"OfficeMgmtCOM"=dword:00000000
```



## <a name="mobile-device-management"></a>移动设备管理  

### <a name="you-can-no-longer-deploy-windows-phone-81-vpn-profiles-to-windows-10"></a>无法再将 Windows Phone 8.1 VPN 配置文件部署到 Windows 10
<!-- 503274  -->
适用范围：Configuration Manager 版本 1710

无法使用 Windows Phone 8.1 工作流创建 VPN 配置文件，Windows 10 设备同样如此。 对于这些配置文件，创建向导不再显示“支持的平台”页。 后端上自动选择 Windows Phone 8.1。 可从配置文件属性中获取“支持的平台”页，但它不会显示 Windows 10 选项。

#### <a name="workaround"></a>解决方法
 对 Windows 10 设备使用 Windows 10 VPN 配置文件工作流。 如果此选项不适用于你的环境，请联系支持部门。 支持部门可帮助添加 Windows 10 目标。



<!-- ## Reports and monitoring    -->
<!-- ## Conditional access   -->
<!-- ## Endpoint Protection -->
