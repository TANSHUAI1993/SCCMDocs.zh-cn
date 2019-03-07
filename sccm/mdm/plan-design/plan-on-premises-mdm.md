---
title: 规划本地 MDM
titleSuffix: Configuration Manager
description: 规划本地移动设备管理来管理移动设备在 Configuration Manager
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 02979fb8-ea7e-4ec6-b7e0-ecbfda73e52d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: bb9349a8c3f107f2da139148e4476537fe6aa7ed
ms.sourcegitcommit: f3dd8405018fe1043434386be15c16752c1a4a3c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/07/2019
ms.locfileid: "57558076"
---
# <a name="plan-for-on-premises-mdm-in-configuration-manager"></a>规划本地 MDM 配置管理器中

适用范围：System Center Configuration Manager (Current Branch)

在本地移动设备管理 (MDM)，可使用内置于设备操作系统的管理功能管理移动设备。 该管理功能基于开放移动联盟 (OMA) 设备管理 (DM) 标准，许多设备平台都使用此标准来允许对设备进行管理。 这些设备称为*新式设备*的文档和 Configuration Manager 控制台中。 此术语将它们与其他需要 Configuration Manager 客户端管理这些设备区分开来。  

准备 Configuration Manager 基础结构来处理本地 MDM 之前，请考虑以下要求



## <a name="bkmk_devices"></a>支持的设备  

Configuration Manager 的 Current Branch 支持针对运行以下操作系统的设备的本地移动设备管理中的注册：  
  
- Windows 10 企业版  
- Windows 10 专业版  
- Windows 10 协同版   
- Windows 10 移动版  
- Windows 10 移动企业版
- Windows 10 IoT 企业版   



##  <a name="bkmk_intune"></a> Microsoft Intune 订阅  

若要开始使用本地 MDM，需要 Microsoft Intune 订阅。 订阅仅用于跟踪设备授权并不用于管理或存储管理的设备的信息。 所有管理数据都存储在你的组织使用本地 Configuration Manager 基础结构。  

> [!Note]  
> 从版本 1810年，Intune 连接不再新的本地 MDM 部署所必需的。<!--3607730, fka 1359124--> 组织仍需要 Intune 许可证才能使用此功能。 当前不能从现有的本地 MDM 部署中删除 Intune 连接。 有关详细信息，请参阅 [Intune 支持博客文章](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150)。  

如果你的站点拥有通过 internet 连接的设备，可以使用 Intune 服务通知设备检查设备管理点有策略更新。 此行为使用 Intune 严格意义的面向 internet 的设备的通知。 设备而不能由 Intune 联系的 internet 连接与，不依赖于已配置的轮询间隔来签入站点系统角色的管理功能。  

> [!TIP]  
> 设置所需的站点系统角色之前，请设置 Intune 订阅。 此操作最小化角色开始正常运行所需的时间。  

有关如何设置 Intune 订阅的信息，请参阅[设置为在本地 MDM 的 Microsoft Intune 订阅](/sccm/mdm/get-started/set-up-intune-subscription-on-premises-mdm)。  



##  <a name="bkmk_roles"></a> Site system roles  

在本地 MDM 需要至少一个以下站点系统角色的每个：  

- **注册代理点** ，用于支持注册请求。  

- **注册点** ，用于支持设备注册。  

- **设备管理点** ，用于策略传递。 此站点系统角色是管理点角色的变体，后者已配置为允许移动设备管理。  

- **分发点** ，用于内容传递。  

- **服务连接点**，用于连接到 Intune 以通知位于防火墙外的设备。  

这些站点系统角色可以安装在单个站点系统服务器上，或者可以根据你的组织的需求的不同服务器上单独运行。 使用本地 MDM 的每个站点系统服务器必须配置为 HTTPS 终结点用于与受信任的设备进行通信。 有关详细信息，请参阅 [所需受信任的通信](#bkmk_trustedComs)。  

有关规划站点系统角色的详细信息，请参阅[为 Configuration Manager 规划站点系统服务器和角色](/sccm/core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles)。  

有关如何添加所需的站点系统角色的详细信息，请参阅[为本地 MDM 安装站点系统角色](/sccm/mdm/get-started/install-site-system-roles-for-on-premises-mdm)。  



##  <a name="bkmk_trustedComs"></a> 受信任的通信  

在本地 MDM 要求站点系统角色以启用 HTTPS 通信。 具体取决于您的需要，可以使用您的企业证书颁发机构 (CA) 来建立受信任的服务器和设备之间的连接。 您还可以使用公开发布的 CA 是受信任的颁发机构。 无论哪种方式，您需要在 IIS 中承载所需的站点系统角色的站点系统服务器上配置的 web 服务器证书。 您还需要在需要连接到这些服务器的设备上安装该 CA 的根证书。  

如果使用企业的 CA 建立受信任的通信，请执行以下任务：  

- 在 CA 上创建和颁发 Web 服务器证书模板。  

- 为托管所需站点系统角色的每个站点系统服务器请求一个 Web 服务器证书。  

- 在站点系统服务器上配置 IIS 以使用所需的 Web 服务器证书。  

对于已加入企业 Active Directory 域的设备，企业 CA 的根证书在受信任连接的设备上已经可用。 此行为意味着，已加入域的设备与站点系统服务器的 HTTPS 连接会自动受到信任。 但是，非加入域的设备不会自动获得安装所需的根证书。 为了与支持的本地 MDM 的站点系统服务器成功通信，如移动设备未加入域的设备要求你在其上手动安装根证书。  

导出供各设备使用的颁发 ca 的根证书。 若要获取根证书文件，可以将其使用 CA 导出。 另一种方法是使用由 CA 颁发的 web 服务器证书提取根目录，并创建根证书文件。 然后必须将根证书传递到设备。 传递方法示例包括：

- 文件系统  

- 电子邮件附件  

- 内存卡  

- 受限设备  

- 云存储（例如 OneDrive）  

- 近场通信 (NFC) 连接  

- 条形码扫描程序  

- 现成体验 (OOBE) 预配包  

有关详细信息，请参阅[设置中的本地 MDM 的受信任通信的证书](/sccm/mdm/get-started/set-up-certificates-on-premises-mdm)  



##  <a name="bkmk_enrollment"></a> 设备注册

若要启用的本地 MDM 的设备注册
- 必须为用户授予注册权限 
- 设备必须使用托管所需的角色的站点系统服务器配置为受信任的通信  

向用户授予权限来设置 Configuration Manager 客户端设置中的注册配置文件注册设备。 默认客户端设置可用于将注册配置文件推送到发现的所有用户。 此外可以设置自定义客户端设置中的注册配置文件，并将设置传递到一个或多个用户集合。  

一旦用户被授予权限，他们可以注册他们自己的设备。 要进行注册，用户的设备必须具有颁发托管所需的角色的站点系统服务器上使用的 web 服务器证书的证书颁发机构 (CA) 的根证书。  

为用户启动注册的替代方法，您可以设置批量注册程序包。 此包可让设备注册无需用户干预。 它可以传递到设备，才能使用或在设备处于完成其 OOBE 流程之后对其进行设置。  

有关如何设置和注册设备的详细信息，请参阅以下文章： 

- [设置本地 MDM 的设备注册](/sccm/mdm/get-started/set-up-device-enrollment-on-premises-mdm)  

- [注册设备以实现本地 MDM](/sccm/mdm/deploy-use/enroll-devices-on-premises-mdm)  

