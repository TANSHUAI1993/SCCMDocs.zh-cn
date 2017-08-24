---
title: "部署 Wi-Fi、VPN、电子邮件和证书配置文件 | Microsoft Docs"
description: "了解如何在 System Center Configuration Manager 中部署 Wi-Fi、VPN、电子邮件和证书配置文件。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3753608d-b539-44dc-8e3f-b631319e7687
caps.latest.revision: "5"
author: Nbigman
ms.author: nbigman
manager: angrobe
ms.openlocfilehash: 70372d5df13034b48f3e43b766776442f1be5823
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="deploy-profiles-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中部署配置文件

*适用范围：System Center Configuration Manager (Current Branch)*

必须将配置文件部署到一个或多个集合，然后才能使用这些配置文件。  

 使用“部署 Wi-fi 配置文件”、“部署 VPN 配置文件”、“部署 Exchange ActiveSync 配置文件”或“部署证书配置文件”对话框可配置这些配置文件的部署。 在配置过程中，你可以定义将向其中部署配置文件的集合，以及指定对配置文件的符合性进行评估的频率。  

> [!NOTE]  
>  如果部署多个公司资源访问配置文件到同一个用户时，会出现下列行为：  
>   
>  -   如果冲突的设置中包含一个可选值，则它将不会发送到设备。  
> -   如果冲突设置包含必需的值，则默认值将发送到设备。 如果没有默认值，则整个公司资源访问配置文件将失败。 例如，如果你将两个电子邮件配置文件部署到同一用户并且为“Exchange ActiveSync 主机”  或“电子邮件地址”  指定的值不同，则这两个电子邮件配置文件将失败，因为它们是强制设置。  

> -   你必须首先配置基础结构并创建证书配置文件，然后才能部署证书配置文件。 有关详细信息，请参阅下列主题：  
>   
>  -   [在 System Center Configuration Manager 中配置证书基础结构](certificate-infrastructure.md)  
> -   [如何在 System Center Configuration Manager 中创建证书配置文件](create-certificate-profiles.md)    

> [!IMPORTANT]  
>  删除 VPN 配置文件部署时，不会从客户端设备中将其删除。 如果要从设备中删除配置文件，你必须将其手动删除。
>   

## <a name="deploying--profiles"></a>部署配置文件  


1.  在 System Center Configuration Manager 控制台中，选择“资产和符合性”。  

2.  在“资产和符合性” 工作区中，展开“符合性设置”，展开“公司资源访问”，然后选择合适的配置文件类型，如“Wi-Fi 配置文件”。  

3.  在配置文件列表中，选择要部署的配置文件，然后在“主页”选项卡上的“部署”组中单击“部署”。  

4.  在部署配置文件对话框中，指定下列信息：  

    -   **集合** - 单击“浏览”以选择要在其中部署配置文件的集合。  

    -   **生成警报** - 启用此选项以配置一个警报，如果在指定日期和时间之前配置文件符合性小于指定百分比，则生成该警报。 你也可以指定是否希望将警报发送到 System Center Operations Manager。  

    -   -   **随机延迟(小时)**：（仅适用于包含简单证书注册协议设置的证书配置文件）指定一个延迟时段以避免对网络设备注册服务进行过度处理。 默认值为 **64** 小时。  

    -   **指定此 <type> 配置文件的符合性评估计划** - 指定在客户端计算机上对部署的配置文件进行评估所依据的计划。 该计划可以是简单计划或自定义计划。  

        > [!NOTE]  
        >  当用户登录时，客户端计算机将评估配置文件。  

5.  单击“确定”关闭对话框并创建部署。

### <a name="see-also"></a>另请参阅  

[如何在 System Center Configuration Manager 中监视 Wi-Fi、VPN 和电子邮件配置文件](monitor-wifi-email-vpn-profiles.md)

[如何在 System Center Configuration Manager 中监视证书配置文件](monitor-certificate-profiles.md)
