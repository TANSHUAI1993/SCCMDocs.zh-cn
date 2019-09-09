---
title: 将 Windows 设备升级到另一版本
titleSuffix: Configuration Manager
description: 使用 Configuration Manager 将 Windows 10 设备自动升级到不同的 Windows 版本。
ms.date: 09/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: b0c9db74-841e-46eb-8924-957cde968bf7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 643ba6189743d4e3d465fa369811867ebcd32e83
ms.sourcegitcommit: b28a97e22a9a56c5ce3367c750ea2bb4d50449c3
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2019
ms.locfileid: "70243616"
---
# <a name="upgrade-windows-devices-to-a-new-edition-with-configuration-manager"></a>使用 Configuration Manager 将 Windows 设备升级到新版本

*适用范围：System Center Configuration Manager (Current Branch)*

通过版本升级策略，可将 Windows 10 设备自动升级到其他版本  。

支持下列升级路径：

- 从 Windows 10 专业版到 Windows 10 企业版
- 从 Windows 10 家庭版到 Windows 10 教育版
- 从 Windows 10 移动版到 Windows 10 移动企业版

设备必须运行 Configuration Manager 客户端软件。 不支持[本地 MDM](/sccm/mdm/understand/manage-mobile-devices-with-on-premises-infrastructure)管理的设备。

## <a name="before-you-start"></a>开始之前

开始将设备升级为最新版本之前，请先查看以下先决条件：  

- 针对 Windows 10 桌面版：在使用该策略的所有目标设备上的新版 Windows 的有效产品密钥。 此产品密钥可以是多次激活密钥 (MAK) 或通用批量授权密钥 (GVLK)。 GVLK 也叫密钥管理服务 (KMS) 客户端安装密钥。 有关详细信息，请参阅[规划批量激活](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client)。 如需 KMS 客户端设置密钥的列表，请参阅 Windows Server 激活指南的[附录 A](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys)。 <!--496871-->  

- 针对 Windows 10 移动版：Microsoft 批量许可服务中心 (VLSC) 的 XML 许可证文件。 此文件包含在使用该策略的所有目标设备上的新版 Windows 的许可信息。

- 若要管理此策略类型，必须使用 Configuration Manager 完全权限管理员安全角色  。

## <a name="configure-the-policy"></a>配置策略  

1. 在 Configuration Manager 控制台中，转到“资产和符合性”工作区，展开“符合性设置”，然后选择“Windows 10 版本升级”节点    。  

2. 在功能区的 "**主页**" 选项卡上的 "**创建**" 组中，选择 "**创建版本升级策略**"。  

3. 选择 "**创建策略**"。  

4. 在“创建版本升级策略向导”  的“常规”  页上，指定以下信息：  

    - **名称** - 输入版本升级策略的名称  

    - **说明**（可选）- 可选择输入此策略的说明，帮助你在 Configuration Manager 控制台中识别它  

    - 将设备升级到的 SKU 版本  – 从下拉列表中，选择 Windows 10 桌面版或 Windows 10 移动版的目标版本  

    - **许可证信息**-选择以下选项之一：  

        - **产品密钥** - 输入 Windows 10 桌面版目标版本的有效产品密钥  

            > [!NOTE]  
            > 创建包含产品密钥的策略后，就无法再编辑该产品密钥。 出于安全原因，Configuration Manager 会遮盖密钥。 要更改产品密钥，请重新输入完整的密钥。  

        - **许可证文件**-选择 "**浏览**" 以选择 XML 格式的有效许可证文件。 Configuration Manager 使用此许可证文件来升级 Windows 10 移动版设备。  

5. 完成向导。  

## <a name="deploy-the-policy"></a>部署策略  

1. 在 Configuration Manager 控制台中，转到“资产和符合性”工作区，展开“符合性设置”，然后选择“Windows 10 版本升级”节点    。  

2. 选择要部署的 Windows 10 版本升级策略。 在功能区的“主页”  选项卡上，在“部署”  组中，选择“部署”  。  

3. 选择要将策略部署到的设备集合。

4. 选择客户端用于评估策略的计划。

5. 完成向导。

## <a name="next-steps"></a>后续步骤

从“监视”工作区的“部署”节点监视此部署   。 如果看到表示部署失败的错误，例如：

- 不适用于此设备 
- 数据类型转换失败 

这些错误并不表示部署失败。 在目标设备上验证是否已成功运行升级。

客户端在评估目标策略后，会在两小时内应用升级。 [某些版本的 Windows](https://docs.microsoft.com/windows/deployment/upgrade/windows-10-edition-upgrades)可能需要在此时重启。 请务必通知要将策略部署到的所有用户，或者进行策略计划，使其在用户工作时间外运行。

如果客户端上的 DcmWmiProvider.log  中出现以下错误，请检查对激活方案使用的密钥是否正确。 有关详细信息，请参阅[准备工作](#before-you-start)部分。 如果使用密钥管理服务 (KMS) 进行激活，请务必使用 [KMS 客户端安装密钥](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys)。  <!-- 496871 -->

`Failed to execute CheckApplicabilityMethod with error = 0x80041001 OsEditionUpgradeProvider`

## <a name="see-also"></a>另请参阅

- [批量激活计划](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client)

- [Windows 10 版本升级](https://docs.microsoft.com/windows/deployment/upgrade/windows-10-edition-upgrades)

- [使用 Microsoft Intune 升级 Windows 10 版本或在设备上切换出 S 模式](https://docs.microsoft.com/intune/edition-upgrade-configure-windows-10)
