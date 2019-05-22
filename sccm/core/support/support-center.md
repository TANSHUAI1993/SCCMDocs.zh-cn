---
title: 支持中心
titleSuffix: Configuration Manager
description: 使用支持中心对 Configuration Manager 客户端进行故障排除。
ms.date: 05/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c631197d-7daa-4faa-9e22-980cd6d604c2
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9246ea46787b1db466b8aca5d8a602617c80e26a
ms.sourcegitcommit: ab9f2a7fb7ea3a0c65808fce2975ab25a670281f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/14/2019
ms.locfileid: "65612525"
---
# <a name="support-center-for-configuration-manager"></a>Configuration Manager 的支持中心

适用范围：System Center Configuration Manager (Current Branch)

<!--1357489-->
自版本 1810 起，支持中心可用于排除客户端故障、查看实时日志，或捕获 Configuration Manager 客户端计算机状态以供日后分析。 支持中心是用于整合多个管理员故障排除工具的单一工具。 



## <a name="about"></a>关于 

支持中心旨在减少对 Configuration Manager 客户端计算机进行故障排除时的挑战和挫败感。 过去，使用支持来解决 Configuration Manager 客户端的问题时，需要手动收集日志文件和其他信息以帮助解决问题。 这样做容易不小心忽略至关重要的日志文件，给你和与你共事的支持人员带来更多麻烦。

使用支持中心可简化支持体验。 使用支持中心可以：

 - 创建包含 Configuration Manager 客户端日志文件的故障排除捆绑包（.zip 文件）。 然后，可以将单个文件发送给支持人员。  

 - 查看 Configuration Manager 客户端日志文件、证书、注册表设置、调试转储、客户端策略。  

 - 清单（替换 ContentSpy）、策略（替换 PolicySpy）和客户端缓存的实时诊断。  


### <a name="support-center-viewer"></a>支持中心查看器

支持中心包括支持中心查看器，支持人员可使用该工具打开使用支持中心创建的文件包。 支持中心的数据收集器从本地或远程 Configuration Manager 客户端收集和打包诊断日志。 要查看数据收集器捆绑包，请使用查看器应用程序。


### <a name="support-center-log-file-viewer"></a>支持中心日志文件查看器

支持中心包括最新日志查看器。 此工具取代了 CMTrace，提供可自定义的界面，并支持选项卡和可停靠窗口。 它具有快速表示层，可以在几秒钟内加载大型日志文件。


### <a name="powershell-cmdlets"></a>PowerShell cmdlet

支持中心还包括 [Windows PowerShell cmdlet](https://go.microsoft.com/fwlink/?linkid=397830)。 使用这些 cmdlet 可以创建与另一个 Configuration Manager 客户端的远程连接、配置数据收集选项以及启动数据收集。



## <a name="prerequisites"></a>先决条件

在安装支持中心的服务器或客户端计算机上安装以下组件：

- Configuration Manager 支持的操作系统版本。 有关详细信息，请参阅[支持的客户端操作系统版本](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices)。 支持中心不支持移动设备。  

- 运行支持中心及其组件的计算机需要 .NET Framework 4.5.2。  



## <a name="install"></a>安装

通过以下路径在站点服务器上找到支持中心安装程序：`cd.latest\SMSSETUP\Tools\SupportCenter\SupportCenterInstaller.msi`。

安装后，在 Microsoft System Center 组的“开始”菜单上找到以下项目：  
- 支持中心 (ConfigMgrSupportCenter.exe)  
- 支持中心日志文件查看器 (CMLogViewer.exe)  
- 支持中心查看器 (ConfigMgrSupportCenterViewer.exe)  



## <a name="known-issues"></a>已知问题 

#### <a name="you-cant-install-the-latest-version-if-an-older-version-is-already-installed"></a>如果已安装旧版本，则无法安装最新版本
<!--SCCMDocs-pr issue #3090-->
如果你已安装旧版支持中心，版本 1810 安装程序会失败。 文件在原始版本和最新版本之间进行版本控制，从而导致了此问题。 为解决此问题，请先卸载旧版支持中心。 然后从 Configuration Manager 1810 版安装最新版本。

#### <a name="remote-connections-must-include-computer-name-or-domain-as-part-of-the-user-name"></a>远程连接必须包括计算机名或域名作为用户名的一部分
如果从支持中心连接到远程客户端，在建立连接时，必须为用户帐户提供计算机名或域名。 如果使用缩写的计算机名或域名（例如 `.\administrator`），则连接会成功，但支持中心不会从客户端收集数据。 

要避免此问题，请使用以下用户名格式连接到远程客户端： 
- `ComputerName\UserName`  
- `DomainName\UserName`  

#### <a name="scripted-server-message-block-connections-to-remote-clients-might-require-removal"></a>可能需要删除与远程客户端的脚本化服务器消息块连接
使用 [New-CMMachineConnection](https://go.microsoft.com/fwlink/p/?linkid=390542) PowerShell cmdlet 连接到远程客户端时，支持中心会创建与每个远程客户端的服务器消息块 (SMB) 连接。 完成数据收集后，它会保留这些连接。 要避免超出 Windows 的最大远程连接数，请使用 `net use` 命令查看当前活动的远程连接集。 然后使用以下命令禁用所有不需要的连接：`net use <connection_name> /d` 
其中 `<connection_name>` 是远程连接的名称。

#### <a name="application-deployment-evaluation-cycle-request-isnt-sent-correctly-to-remote-machines"></a>向远程计算机发送的应用程序部署评估周期请求不正确
<!--2849356-->
在支持中心内，如果你在“内容”选项卡上的“调用触发器”操作中选择“应用程序部署评估”，此操作会启动任务来评估已部署的应用程序。 如果你已连接到本地客户端，则它会评估计算机和用户应用程序部署。 但是，如果你已连接到远程客户端，它将仅评估计算机应用程序部署。


## <a name="next-steps"></a>后续步骤

[支持中心快速入门](/sccm/core/support/support-center-quickstart)
