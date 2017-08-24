---
title: "管理 Windows 10 更新的快速安装文件| Microsoft 文档"
description: "Configuration Manager 支持 Windows 10 快速安装文件，所需下载文件更小，在客户端上安装速度更快。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 03/24/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: b8d8af88-e8ac-4deb-921b-975e2d2afd80
ms.openlocfilehash: baffb5f026bd63c50f878214e71d2c9e9b8b51c2
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="manage-express-installation-files-for-windows-10-updates"></a>管理 Windows 10 更新的快速安装文件
从 Configuration Manager 版本 1702 起，Configuration Manager 支持 Windows 10 更新的快速安装文件。 如果使用支持版本的 Windows 10，可通过 Configuration Manager 设置只下载本月的 Windows 10 累积更新和上月更新之间的更改。 在没有快速安装文件的情况下，Configuration Manager 每个月都会下载完整的 Windows 10 累积更新（包括先前月份的所有更新）。 使用快速安装文件，所需下载文件更小，在客户端上安装更快速。

> [!IMPORTANT]
> 尽管 Configuration Manager 版本 1702 中支持快速安装文件的设置已可用，但此操作系统客户端支持仅在 Windows 10 版本 1607 中可用，并随附 Windows 更新代理更新。 2017 年 4 月 11 日（星期二的修补程序）发布的更新中包含此更新。 若要详细了解这些更新，请参阅[支持文章 4015217](http://support.microsoft.com/kb/4015217)。 未来的更新将利用此快速安装文件，以获得更小的下载文件。 不包含此更新的 Windows 10 版本 1607 和之前版本不支持快速安装文件。


### <a name="to-enable-the-download-of-express-installation-files-for-windows-10-updates"></a>启用 Windows 10 更新的快速安装文件下载
若要开始同步 Windows 10 快速安装文件的元数据，则必须在软件更新点属性中将其启用。
1.  在 Configuration Manager 控制台中，导航到“管理” > “站点配置” > “站点”。
2.  选择管理中心站点或独立主站点。
3.  在“主页”  选项卡上的“设置”  组中，单击“配置站点组件” ，再单击“软件更新点” 。 在“更新文件”选项卡上，选择“下载所有 Windows 10 已审核更新和快速安装文件的完整文件”。

### <a name="to-enable-support-for-clients-to-download-and-install-express-installation-files"></a>启用客户端对下载并安装快速安装文件的支持
若要在客户端上启用快速安装文件支持，则必须在客户端设置的软件更新分区中启用快速安装文件。 这将创建新的 HTTP 侦听器，该侦听器会侦听在指定的端口下载快速安装文件的请求。

> [!NOTE]    
> 这是一个本地端口，客户端将用于侦听来自传递优化 (DO) 或后台智能传输服务 (BITS) 的请求，以从分发点下载快速内容。 无需在防火墙上打开此端口，因为所有流量都在本地计算机上。

在客户端上部署客户端设置启用此功能后，会尝试下载当前月份的 Windows 10 累计更新和上一月份的更新之间的增量文件（客户端必须运行支持快速安装文件的 Windows 10 版本）。
1.  在“软件更新点组件”属性中启用快速安装文件支持（上一过程）。
2.  在 Configuration Manager 控制台中，导航到“管理” > “客户端设置”。
3.  选择相应的客户端设置，然后在“主页”选项卡上，单击“属性”。
4.  选择“软件更新”页，将“在客户端上启用快速更新安装”设置配置为“是”，并将“下载快速更新内容所用端口”设置配置为客户端上 HTTP 侦听器所使用的端口。
