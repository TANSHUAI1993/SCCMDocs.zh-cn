---
title: 管理 Windows 10 传递更新
titleSuffix: Configuration Manager
description: Configuration Manager 支持 Windows 10 快速安装文件，所需下载文件更小，在客户端上安装速度更快。
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 06/15/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: b8d8af88-e8ac-4deb-921b-975e2d2afd80
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5a7bf171804922399f21551e9c8854883de9cf78
ms.sourcegitcommit: 9648ce8a8b5c82518e7c8b6a7668e0e9b076cae6
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 09/05/2019
ms.locfileid: "70379949"
---
# <a name="manage-express-installation-files-for-windows-10-updates"></a>管理 Windows 10 更新的快速安装文件

Configuration Manager 支持 Windows 10 更新的快速安装文件。 将客户端配置为仅下载当前月份的 Windows 10 累积质量更新与上个月更新之间的更改。 如果没有快速安装文件，Configuration Manager 客户端每个月都会下载完整的 Windows 10 累积更新，包括以前月份的所有更新。 使用快速安装文件，所需下载文件更小，在客户端上安装更快速。

要了解如何使用 Configuration Manager 管理更新内容以及时了解 Windows 10 动态，请参阅[优化 Windows 10 更新传递](/sccm/sum/deploy-use/optimize-windows-10-update-delivery)。  


> [!IMPORTANT]  
> Windows 10 版本 1607 中提供了 OS 客户端支持，其中包含 Windows 更新代理的更新。 2017 年 4 月 11 日发布的更新中包含此更新。 若要详细了解这些更新，请参阅[支持文章 4015217](https://support.microsoft.com/kb/4015217)。 未来的更新将利用此快速安装文件，以获得更小的下载文件。 之前版本的 Windows 10 和 Windows 10 版本 1607 不包含此更新，因此不支持快速安装文件。  


### <a name="enable-the-site-to-download-express-installation-files-for-windows-10-updates"></a>启用此站点以下载 Windows 10 更新的快速安装文件
若要开始同步 Windows 10 快速安装文件的元数据，请在软件更新点属性中将其启用。  

1. 在 Configuration Manager 控制台中，转到“管理”  工作区，展开“站点配置”  ，然后选择“站点”  节点。  

2. 选择管理中心站点或独立主站点。  

3. 在功能区中，单击“配置站点组件”   ，然后单击“软件更新点”。 转到“更新文件”选项卡，然后选择“下载所有 Windows 10 已审核更新和快速安装文件的完整文件”   。

> [!NOTE]    
> 无法将软件更新点组件配置为仅  下载快速更新。  除完整文件外，该站点还会下载快速安装文件。 这会增加内容库中存储的内容量，并分发和存储到分发点上。

> [!Tip]  
> 要确定文件在磁盘上实际使用的空间，请检查文件的  “占用空间”属性。 “占用空间”属性应远小于“大小”值。 有关详细信息，请参阅[有关优化 Windows 10 更新传递的常见问题解答](/sccm/sum/deploy-use/optimize-windows-10-update-delivery#bkmk_faq)。  


### <a name="enable-clients-to-download-and-install-express-installation-files"></a>启用客户端以下载并安装快速安装文件
若要在客户端上启用快速安装文件支持，请在客户端设置的软件更新组中启用快速安装文件。  此设置将创建新的 HTTP 侦听器，该侦听器会侦听在指定的端口下载快速安装文件的请求。

> [!NOTE]    
> 这是一个本地端口，客户端将用于侦听来自传递优化或后台智能传输服务 (BITS) 的请求，以从分发点下载快速内容。 无需在防火墙上打开此端口，因为所有流量都在本地计算机上。  

在客户端上部署客户端设置启用此功能后，会尝试下载当前月份的 Windows 10 累计更新和上一月份的更新之间的增量文件。 客户端必须运行支持快速安装文件的 Windows 10 版本。  

1. 在软件更新点组件属性中启用快速安装文件支持（上一过程）。  

2. 在 Configuration Manager 控制台中，转到“管理”工作区，并选择“客户端设置”   。  

3. 选择相应的客户端设置，然后在功能区  上单击“属性”。  

4. 选择“软件更新”  组。 配置为“是”  ，该设置将  “在客户端上启用快速更新安装”。 通过客户端上 HTTP 侦听器使用的端口配置用于下载快速更新  内容的端口。
