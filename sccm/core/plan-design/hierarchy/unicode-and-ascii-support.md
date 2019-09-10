---
title: Unicode 和 ASCII 支持
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 对象中对 Unicode 和 ASCII 字符的支持。
ms.date: 08/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 2bdec799-905f-48bc-aed5-2d92134739e8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0214abdf1dd7ce735542ebace443c8aed297b2c3
ms.sourcegitcommit: f679fc1e46c191a1780ae961d155c927fc353dce
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/30/2019
ms.locfileid: "70176722"
---
# <a name="unicode-and-ascii-support-in-configuration-manager"></a>Configuration Manager 中的 Unicode 和 ASCII 支持

适用范围：  System Center Configuration Manager (Current Branch)

Configuration Manager 使用 Unicode 字符来创建大部分对象。 但是，有几个对象仅支持 ASCII 字符，或者具有其他限制。  

## <a name="BKMK_ASCIIchar"></a>使用 ASCII 字符的对象

在创建下列对象时，Configuration Manager 仅支持 ASCII 字符集：  

- 站点代码  

- 所有站点系统服务器计算机的名称  

- 下列 Configuration Manager 帐户：  

    > [!NOTE]  
    > 在以俄语运行的站点上，这些帐户支持 ASCII 字符和 RUS 字符。  

    - 客户端请求安装帐户  

    - 管理点数据库连接帐户  

    - 网络访问帐户  

    - 包访问帐户  

    - 标准发件人帐户  

    - 站点系统安装帐户  

    - 软件更新点连接帐户  

    - 软件更新点代理服务器帐户  

    > [!NOTE]  
    > 你为基于角色的管理指定的帐户支持 Unicode。  
    >
    > Reporting Services 点帐户支持 Unicode（RUS 字符除外）。  

- 站点服务器和站点系统的完全限定的域名 (FQDN)  

- Configuration Manager 的安装路径  

- SQL Server 实例名称  

- 下列站点系统角色的路径：  

    - 注册点  

    - 注册代理点  

    - Reporting Services 点  

    - 状态迁移点  

- 下列文件夹的路径：  

    - 存储客户端状态迁移数据的文件夹  

    - 包含 Configuration Manager 报表的文件夹  

    - 存储 Configuration Manager 备份的文件夹  

    - 存储站点安装程序的安装源文件的文件夹  

    - 存储所下载的、供安装程序使用的必备组件的文件夹  

- 下列对象的路径：  

    - IIS 网站  

    - 虚拟应用程序安装路径  

    - 虚拟应用程序名称  

- 启动媒体 ISO 文件名  


## <a name="BKMK_OtherCharLimitations"></a>其他限制

下面是针对支持的字符集和语言版本的其他限制：  

- Configuration Manager 不支持更改站点服务器计算机的区域设置。  

- 企业证书颁发机构 (CA) 不支持使用双字节字符集 (DBCS) 的客户端计算机名称。 可以使用的客户端计算机名称受到 IA5 字符集的 PKI 限制的制约。 Configuration Manager 不支持使用 DBCS 的 CA 名称或使用者名称值。  


## <a name="BKMK_LangNonLocalize"></a> 未本地化的对象

Configuration Manager 数据库支持它存储的大多数对象使用 Unicode。 如果可能，它会以与计算机区域设置匹配的 OS 语言显示此信息。 若要使客户端界面或 Configuration Manager 控制台以计算机的 OS 语言显示信息，计算机的区域设置必须匹配在站点中安装的客户端或服务器语言。  

有几个 Configuration Manager 对象不支持 Unicode。 它们使用 ASCII 存储在数据库中，或者它们具有其他语言限制。 此信息始终使用 ASCII 字符集或者在创建对象时使用的语言来显示。  
