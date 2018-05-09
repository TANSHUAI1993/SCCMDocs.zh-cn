---
title: 将 Windows 设备升级到另一版本
titleSuffix: Configuration Manager
description: 使用 Configuration Manager 将运行 Windows 10 桌面版或 indows 10 移动版的设备自动升级为其他版本。
ms.date: 01/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: b0c9db74-841e-46eb-8924-957cde968bf7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0c15e919978ae8458f426511dd9a0e6d7c311b4b
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="upgrade-windows-devices-with-the-edition-upgrade-policy-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中使用版本升级策略升级 Windows 设备

*适用范围：System Center Configuration Manager (Current Branch)*


“版本升级策略”可以将运行以下任一 Windows 10 版本的设备自动升级为其他版本：

- Windows 10 桌面版
- Windows 10 移动版

支持下列升级路径：

- 从 Windows 10 专业版到 Windows 10 企业版
- 从 Windows 10 家庭版到 Windows 10 教育版
- 从 Windows 10 移动版到 Windows 10 移动企业版

设备必须在 Microsoft Intune 中注册或运行 Configuration Manager 客户端软件。 此策略当前不兼容本地 MDM 管理的电脑。

## <a name="before-you-start"></a>开始之前  
 开始将设备升级为最新版本之前，请先查看以下先决条件：  

-   针对 Windows 10 桌面版：在使用该策略的所有目标设备上的新版 Windows 的有效产品密钥。 此产品密钥可以是多次激活密钥 (MAK) 或通用批量授权密钥 (GVLK)。 GVLK 也叫密钥管理服务 (KMS) 客户端安装密钥。 有关详细信息，请参阅[规划批量激活](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client)。 如需 KMS 客户端设置密钥的列表，请参阅 Windows Server 激活指南的[附录 A](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys)。 <!--496871-->  

-   针对 Windows 10 移动版：Microsoft 批量许可服务中心 (VLSC) 的 XML 许可证文件。 此文件包含在使用该策略的所有目标设备上的新版 Windows 的许可信息。

- 若要管理此策略类型，必须使用 Configuration Manager 完全权限管理员安全角色。

## <a name="configure-the-edition-upgrade-policy"></a>配置版本升级策略  

1.  在 Configuration Manager 控制台中，单击“资产和符合性” > “符合性设置” > “Windows 10 版本升级”。  

3.  在“主页”  选项卡上的“创建”  组中，单击“创建版本升级策略” 。  

4.  单击“创建策略” 。  

5.  在“创建版本升级策略向导”  的“常规” 页上，指定以下信息：  

    -   **名称** - 输入版本升级策略的名称  

    -   **描述**（可选）- 根据需要，输入有助于在 Intune 控制台中识别该策略的描述  

    -   将设备升级到的 SKU 版本 – 从下拉列表中，选择 Windows 10 桌面版或 Windows 10 移动版的目标版本  

    -   **许可证信息** - 选择以下之一：  

        -   **产品密钥** - 输入 Windows 10 桌面版目标版本的有效产品密钥  

            > [!NOTE]  
            >  在创建包含产品密钥的策略后，将无法对产品密钥进行编辑。 出于安全原因，Configuration Manager 会遮盖密钥。 若要更改产品密钥，必须重新输入完整的密钥。  

        -   **许可证文件** - 单击“浏览”，然后选择 XML 格式的有效许可证文件。 Configuration Manager 使用此许可证文件来升级 Windows 10 移动版设备。  

6.  完成向导。  


## <a name="deploy-the-edition-upgrade-policy"></a>部署版本升级策略  

1.  在 Configuration Manager 控制台中，单击“资产和符合性” > “符合性设置” > “Windows 10 版本升级”。  

3.  选择你想部署的 Windows 10 版本升级策略，然后在“主页”  选项卡上的“部署”  组中，单击“部署” 。  

4.  在“部署 Windows 10 版本升级”对话框中，首先选择要将此策略部署到的集合。 选择客户端用于评估策略的计划，然后单击“确定”。 对于 Configuration Manager 客户端管理的电脑，必须将策略部署到设备集合。 对于已注册 Intune 的电脑，可以将策略部署到用户或设备集合。 



## <a name="next-steps"></a>后续步骤

从“监视”工作区的“部署”节点监视此部署。 如果看到表示部署失败的错误，例如：
- 不适用于此设备
- 数据类型转换失败

这些错误并不表示部署已失败。 在已成功执行升级的目标电脑上进行验证。

客户端评估目标策略之后，会在两小时内重新启动，以便应用升级。 确保通知所有要向其部署策略，或计划在其业余时间运行该策略的用户。

如果客户端上的 DcmWmiProvider.log 中出现以下错误，请检查激活方案中使用的密钥是否正确。 有关详细信息，请参阅[准备工作](#before-you-start)部分。 如果使用密钥管理服务进行激活，请务必使用 [KMS 客户端安装密钥](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys)。  <!-- 496871 -->   

`Failed to execute CheckApplicabilityMethod with error = 0x80041001 OsEditionUpgradeProvider`
