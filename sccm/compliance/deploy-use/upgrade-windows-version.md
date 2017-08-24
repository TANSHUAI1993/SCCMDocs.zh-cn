---
title: "使用 Configuration Manager 将 Windows 设备升级到不同版本 | Microsoft Docs"
description: "使用 Configuration Manager 将运行 Windows 10 桌面版、Windows 10 移动版或 Windows 10 全息版的设备自动升级到不同版本。"
ms.custom: na
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b0c9db74-841e-46eb-8924-957cde968bf7
caps.latest.revision: "8"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: cd8c644d07dab0010dc211df8ce4f2dc6e1fa7ae
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="upgrade-windows-devices-with-the-edition-upgrade-policy-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中使用版本升级策略升级 Windows 设备

*适用范围：System Center Configuration Manager (Current Branch)*


System Center Configuration Manager **版本升级策略**可以将运行以下任一 Windows 10 版本的设备自动升级至不同版本：

- Windows 10 桌面版
- Windows 10 移动版
<!-- - Windows 10 Holographic -->

支持下列升级路径：

- 从 Windows 10 专业版到 Windows 10 企业版
- 从 Windows 10 家庭版到 Windows 10 教育版
- 从 Windows 10 移动版到 Windows 10 移动企业版
<!-- - From Windows 10 Holographic Pro to Windows 10 Holographic Enterprise -->

设备必须在 Microsoft Intune 中注册或运行 Configuration Manager 客户端软件。 此策略当前不兼容本地 MDM 管理的电脑。

## <a name="before-you-start"></a>开始之前  
 在开始将设备升级至最新版本之前，你将需要以下内容之一：  

-   在该策略针对的所有设备上安装 Windows 新版本使用的有效产品密钥（针对于桌面操作系统）  

-   在该策略针对的所有设备上安装 Windows 新版本使用的包含许可信息的 Microsoft 许可证文件（针对 Windows 10 移动版<!-- and Windows 10 Holographic-->）。

- 若要创建和部署此策略类型，必须分配有 Configuration Manager **完全权限管理员**安全角色。

## <a name="configure-the-edition-upgrade-policy"></a>配置版本升级策略  

1.  在 Configuration Manager 控制台中，单击“资产和符合性” > “符合性设置” > “Windows 10 版本升级”。  

3.  在“主页”  选项卡上的“创建”  组中，单击“创建版本升级策略” 。  

4.  单击“创建策略” 。  

5.  在“创建版本升级策略向导”  的“常规” 页上，指定以下信息：  

    -   **名称** - 输入版本升级策略的名称。  

    -   **描述** （可选）- 根据需要，输入有助于在 Intune 控制台中识别该策略的描述。  

    -   **将设备升级到的 SKU 版本** – 从下拉列表中，选择你想将目标设备升级到的版本：Windows 10 桌面版<!-- Windows 10 Holographic,-->或 Windows 10 移动版。  

    -   **许可证信息** - 选择以下之一：  

        -   **产品密钥** - 输入有效的 Windows 10 产品密钥，该密钥将用于升级运行 Windows 10 桌面版操作系统的目标设备。  

            > [!NOTE]  
            >  在创建包含产品密钥的策略后，将无法对产品密钥进行编辑。 这是因为出于安全考虑，密钥将被遮盖。 若要更改产品密钥，必须重新输入完整的密钥。  

        -   **许可证文件** - 单击“浏览”以选择有效的 XML 格式的许可证文件，该文件将用于升级运行 <!--Windows 10 Holographic and -->Windows 10 移动版操作系统的目标设备。  

6.  完成向导。  

新策略会显示在“资产和符合性”  工作区的“Windows 10 版本升级”  节点中。  

## <a name="deploy-the-edition-upgrade-policy"></a>部署版本升级策略  

1.  在 Configuration Manager 控制台中，单击“资产和符合性” > “符合性设置” > “Windows 10 版本升级”。  

3.  选择你想部署的 Windows 10 版本升级策略，然后在“主页”  选项卡上的“部署”  组中，单击“部署” 。  

4.  在“部署 Windows 10 版本升级”对话框中，选择要为其部署策略的集合和评估该策略的计划，然后单击“确定”。 对于 Configuration Manager 客户端管理的电脑，必须将策略部署到设备集合。 对于已注册 Intune 的电脑，可以将策略部署到用户或设备集合。 



## <a name="next-steps"></a>后续步骤

当监视刚从“监视”工作区的“部署”节点创建的部署时，可能会看到指示部署不成功的错误，如下所示：
- 不适用于此设备
- 数据类型转换失败

这些错误并不表示部署已失败。 在已成功执行升级的目标电脑上进行验证。

该策略应用到目标 Windows 电脑并进行评估后，该电脑将在两小时内重启以应用升级。 确保通知所有要向其部署策略，或计划在其业余时间运行该策略的用户。
