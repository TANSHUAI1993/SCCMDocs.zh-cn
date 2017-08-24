---
title: "Windows Hello 企业版设置 | Microsoft Docs"
description: "了解如何将 Windows Hello 企业版与 System Center Configuration Manager 集成。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c0593c07-5dd7-4d23-a0d8-d30165f49ef7
caps.latest.revision: "17"
author: lleonard-msft
ms.author: alleonar
manager: angrobe
ms.openlocfilehash: a97b3d97eb302e4133b0a79a8c7e27004872c8b1
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="windows-hello-for-business-settings-in-system-center-configuration-manager-hybrid"></a>System Center Configuration Manager 中的 Windows Hello 企业版设置（混合）

*适用范围：System Center Configuration Manager (Current Branch)*

通过 System Center Configuration Manager，可与 Windows Hello 企业版（以前为 Microsoft Passport for Windows）集成，其为 Windows 10 设备的替代登录方法。 Hello 企业版使用 Active Directory 或 Azure Active Directory 帐户来替代密码、智能卡或虚拟智能卡。  

在 Hello 企业版中，可以使用“用户手势”取代密码进行登录。 用户手势可以是简单的 PIN、生物识别身份验证或指纹读取器等外部设备。  

 Configuration Manager 通过两种方式与 Windows Hello 企业版集成：  

-   可以使用 Configuration Manager 来控制用户能够和不能用于登录的手势。  

-   可在 Windows Hello 企业版密钥存储提供程序 (KSP) 中存储身份验证证书。 有关详细信息，请参阅[证书配置文件](create-pfx-certificate-profiles.md)。  

- 可将 Windows Hello 企业版策略部署到运行 Configuration Manager 客户端的已加入域的 Windows 10 设备。 [在已加入域的 Windows 10 设备上配置 Windows Hello 企业版](../../protect/deploy-use/windows-hello-for-business-settings.md#configure-windows-hello-for-business-on-domain-joined-windows-10-devices)中介绍了此配置。 搭配使用 Configuration Manager 和 Intune（混合）时，可在 Windows 10 和 Windows 10 移动设备上配置这些设置，但不能在运行 Configuration Manager 客户端的已加入域的设备上进行配置。   

有关配置 Windows Hello 企业版设置的一般信息，请参阅 [System Center Configuration Manager 中的 Windows Hello 企业版设置](../../protect/deploy-use/windows-hello-for-business-settings.md)。

## <a name="configure-windows-hello-for-business-settings-hybrid"></a>配置 Windows Hello 企业版设置（混合）  

1.  在 Configuration Manager 控制台中，单击“管理” > “云服务” > “Microsoft Intune 订阅”。  

3.  从列表中选择你的 Microsoft Intune 订阅，然后在“主页”选项卡的“订阅”组中，单击“配置平台” > “Windows (MDM)”。  

4.  在“Microsoft Intune 订阅属性”对话框的“Windows Hello 企业版”选项卡上，从以下值中选择将影响所有已注册的 Windows 10 和 Windows 10 移动版设备的项：  

    -   **禁用已注册设备上的 Windows Hello 企业版**或**启用已注册设备上的 Windows Hello 企业版** - 启用或禁用所有已注册的 Windows 10 和 Windows 10 移动版设备上的 Windows Hello 企业版。  

    -   **使用受信任的平台模块 (TPM)** - 受信任的平台模块 (TPM) 芯片提供了一层额外的数据安全保障。 选择下列值之一：  

        -   **必须** （默认）- 仅具有可访问 TPM 的设备可预配 Windows Hello 企业版。  

        -   **首选** - 首次尝试使用 TPM 的设备。 如果这不可用，他们可以使用软件加密  

    -   **要求的最小 PIN 长度** - 指定 Windows Hello 企业版 PIN 所需的最小字符数。 必须使用至少 4 个字符（默认值为 6 个字符）。  

    -   **要求的最大 PIN 长度** - 指定 Windows Hello 企业版 PIN 允许的最大字符数。 最多可以使用 127 个字符。  

    -   **要求在 PIN 中使用小写字母** - 指定是否必须在 Windows Hello 企业版 PIN 中使用小写字母。 选择：  

        -   **允许** - 用户可以在其 PIN 中使用小写字母。  

        -   **必须** - 用户必须在其 PIN 中包含至少一个小写字母。  

        -   **不允许** （默认）- 用户不得在其 PIN 中使用小写字母。  

    -   **要求在 PIN 中使用大写字母** - 指定是否必须在 Windows Hello 企业版 PIN 中使用大写字母。 选择：  

        -   **允许** - 用户可以在其 PIN 中使用大写字母。  

        -   **必须** - 用户必须在其 PIN 中包含至少一个大写字母。  

        -   **不允许** （默认）- 用户不得在其 PIN 中使用大写字母。  

    -   **要求含有特殊字符** - 指定 PIN 中使用特殊字符。 选择：  

        -   **允许** - 用户可以在其 PIN 中使用特殊字符。  

        -   **必须** - 用户必须在其 PIN 中包含至少一个特殊字符。  

        -   **不允许** （默认）- 用户必须在其 PIN 中使用特殊字符（这也是不配置此设置时的行为）。  

         特殊字符包括：**! " # $ % & ' ( ) \* + , - . / : ; < = > ? @ [ \ ] ^ _ ` { &#124; } ~**。  

    -   **需要 PIN 有效期（天）** - 指定必须更改设备 PIN 前的天数。 默认值为 41 天。  

    -   **防止重用以前的 PIN** - 使用此设置来限制重用以前使用过的 PIN。 默认设置为不能重用最近使用的 5 个 PIN。  

    -   **启用生物识别手势** - 启用如面部识别或指纹等生物识别身份验证作为 Windows Hello 企业版的 PIN 的替代方法。 如果生物识别身份验证失败，则用户仍必须配置工作 PIN。  

         如果设置为“启用”，Windows Hello 企业版则允许生物识别身份验证。  如果设置为“禁用”，Windows Hello 企业版将阻止生物识别身份验证（对于所有帐户类型）。  

    -   **在可用时，使用增强型反欺骗程序** - 配置是否在支持增强型反欺骗程序的设备上使用该程序。  

         如果设置为“已启用” ，则 Windows 将在支持反电子欺骗技术时要求所有用户对面部识别功能使用此技术。  

    -   **使用远程 Passport** - 如果此选项设置为“启用”，则用户可以使用远程 Hello 企业版充当台式计算机身份验证的便携伴侣设备。 台式计算机必须加入 Azure Active Directory，并且伴侣设备必须配置 Windows Hello 企业版 PIN。  

5.  完成后单击“确定” 。  

### <a name="see-also"></a>另请参阅  
 [使用 System Center Configuration Manager 保护数据和站点基础结构](../../protect/understand/protect-data-and-site-infrastructure.md)

 [使用 Windows Hello 企业版管理身份验证](https://technet.microsoft.com/itpro/windows/keep-secure/manage-identity-verification-using-microsoft-passport)。  
