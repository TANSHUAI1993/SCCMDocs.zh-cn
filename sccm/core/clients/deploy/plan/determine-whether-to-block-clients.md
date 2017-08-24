---
title: "阻止客户端 | Microsoft Docs"
description: "使用 System Center Configuration Manager 阻止客户端访问以实现系统安全性。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 54ef5fbb-521d-4ca5-a1c5-61e6f538d71e
caps.latest.revision: "8"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 3e323ab90ec4cc274581e19065fd7d81c0c11c35
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="determine-whether-to-block-clients-in-system-center-configuration-manager"></a>确定是否在 System Center Configuration Manager 中阻止客户端

*适用范围：System Center Configuration Manager (Current Branch)*

如果某个客户端计算机或客户端移动设备不再受信任，则可以在 System Center 2012 Configuration Manager 控制台中阻止该客户端。 Configuration Manager 基础结构会拒绝被阻止的客户端，使它们无法与站点系统通信，从而无法下载策略、上载清单数据或者发送状况或状态消息。  

 若要阻止和取消阻止客户端，必须通过为其分配的站点而不是通过辅助站点或管理中心站点来这样做。  

> [!IMPORTANT]  
>  虽然在 Configuration Manager 中进行阻止有助于保护 Configuration Manager 站点的安全，但如果你允许客户端使用 HTTP 与站点系统通信，则请勿依赖此功能来防止站点与不受信任的计算机或移动设备通信，因为被阻止的客户端可以使用新的自签名证书和硬件 ID 重新加入该站点。 应改为使用阻止功能来阻止丢失或泄漏你用于部署操作系统的启动媒体，当站点系统接受 HTTPS 客户端连接时也可以使用阻止功能。  

 如果客户端使用 ISV 代理证书来访问站点，则无法阻止这些客户端。 有关 ISV 代理证书的详细信息，请参阅 System Center Configuration Manager 软件开发工具包 (SDK)。  

 如果站点系统接受 HTTPS 客户端连接，而且公钥基础结构 (PKI) 支持证书吊销列表 (CRL)，则始终考虑将证书吊销作为预防证书泄漏的主要防线。 在 Configuration Manager 中阻止客户端为保护层次结构提供第二道防线。  

##  <a name="BKMK_Block_vs_CRL"></a> 阻止客户端的注意事项  

-   此选项可用于 HTTP 和 HTTPS 客户端连接，但其安全性在客户端使用 HTTP 连接到站点系统时会受到限制。  

-   Configuration Manager 管理用户具有阻止客户端的权限，该操作在 Configuration Manager 控制台中完成。  

-   只能从 Configuration Manager 层次结构中拒绝客户端通信。  

    > [!NOTE]  
    >  同一个客户端可以向不同的 Configuration Manager 层次结构注册。  

-   立即在 Configuration Manager 站点中阻止客户端。  

-   帮助防止可能有危害的计算机和移动设备侵害站点系统。  

## <a name="considerations-for-using-certificate-revocation"></a>使用证书吊销的注意事项  

-   如果公钥基础结构支持证书吊销列表 (CRL)，则此选项可用于 HTTPS Windows 客户端连接。  

     Mac 客户端始终会执行 CRL 检查，因此无法禁用此功能。  

     虽然移动设备客户端并不使用证书吊销列表来检查站点系统的证书，但 Configuration Manager 可以吊销和检查它们的证书。  

-   公钥基础结构管理员具有吊销证书的权限，该操作在 Configuration Manager 外完成。  

-   可以从需要此客户端证书的任何计算机或移动设备中拒绝客户端通信。  

-   在吊销证书和站点系统下载已修改的证书吊销列表 (CRL) 之间可能存在延迟。  

-   对许多 PKI 部署而言，此延迟可能达到一天或更长时间。 例如，在 Active Directory 证书服务中，默认的有效期对于完整 CRL 为一周，对于增量 CRL 为一天。  

-   帮助防止可能有危害的计算机和移动设备侵害站点系统及客户端。  

    > [!NOTE]  
    >  通过在 IIS 中配置证书信任列表 (CTL)，可以进一步防止未知的客户端对运行 IIS 的站点系统的损害。  
