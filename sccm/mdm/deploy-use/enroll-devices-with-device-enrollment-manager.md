---
title: '使用设备注册管理器注册设备 '
titleSuffix: Configuration Manager
description: 使用 System Center Configuration Manager 向设备注册管理器注册企业拥有的设备。
ms.date: 09/08/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 2905f26e-7859-497d-b995-5ff48261efa2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cc1be1d602c3f9f8e65e0523d64c5b6a8e579c90
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2018
ms.locfileid: "53415546"
---
# <a name="enroll-devices-with-device-enrollment-manager-with-configuration-manager"></a>使用 Configuration Manager 向设备注册管理器注册设备

*适用于：System Center Configuration Manager (Current Branch)*

组织可以使用 Intune 来管理大量带有单一用户帐户的移动设备。 设备注册管理器 (DEM) 帐户是用于注册设备的特殊用户帐户。 将现有用户添加到要为其提供专用 DEM 功能的 DEM 帐户。 每个已注册的设备使用单个许可证。 我们建议你将通过此帐户注册的设备作为没有用户关联性的共享设备使用，而不是个人专用设备。  

## <a name="enroll-corporate-owned-devices-with-the-device-enrollment-manager"></a>使用设备注册管理器注册企业自有设备  
 你可以指定存储管理员或主管，例如，允许用户执行下列操作的设备注册管理员用户帐户：  

-   最多可注册 1000 个设备以进行管理  
-   使用公司门户应用安装公司应用  
-   配置对公司数据的访问权限  

以下限制适用于使用设备注册管理器帐户管理的设备：

- 存储管理员无法从公司门户重置设备。  
- 无法加入工作区或已加入 Azure Active Directory 的设备。 这可防止这些设备使用条件性访问。
- 若要将公司应用部署到使用设备注册管理器管理的设备，则需要将公司门户应用作为**必需的安装**到设备注册管理器的用户帐户。 然后，设备注册管理器可以启动公司门户应用来安装其他应用。
- 为了提高性能，公司门户应用仅显示本地设备。 仅管理员可以从 Configuration Manager 控制台远程管理其他的 DEM 设备
- 设备注册管器帐户不能使用公司门户网站。 打开公司门户应用。
- 如果使用 DEM 来注册 iOS 设备，则无法使用 Apple Configurator 或 Apple 设备注册计划 (DEP) 来注册设备。 （仅限 iOS） 

  **设备注册管理器的示例方案：**   
  一家餐厅想为服务员提供销售点平板电脑，为厨房员工提供订单监视器。 员工无需访问公司数据或作为用户登录。 Intune 管理员创建设备注册管理员帐户并使用该帐户注册公司自有设备。 或者，管理员也可以将设备注册管理员凭据交给餐厅经理，允许他或她注册和管理设备。  

  管理员或经理可以将特定于角色的应用部署到餐厅设备。 管理员还可以在控制台中选择一台设备，并从移动设备管理中将其停用。  

#### <a name="add-a-device-enrollment-manager"></a>添加一个设备注册管理器  

1.  在 Configuration Manager 控制台中，单击“管理”。  

2.  在“管理”  工作区中，展开“云服务” ，并单击“Microsoft Intune 订阅” 。 选择要添加设备注册管理器的 Microsoft Intune 订阅，然后单击“属性”。  

3.  在“Microsoft Intune 订阅属性”对话框中，单击“设备注册管理器”选项卡。  

4.  单击“添加/删除”。  

5.  在“设备注册管理器”对话框中，键入想要添加为设备注册管理器的用户的用户名，然后单击“搜索”。 选择想要添加为设备注册管理器的用户，然后单击“添加”。  

6.  确认将成为设备注册管理器的用户帐户并单击“添加/删除”。  每个访问该服务的用户都必须拥有订阅许可证并且“设备注册管理器”不能是 Intune 管理员。 确定是否需要在使用此功能之前添加更多许可证。  

7.  设备注册管理器现在可以使用相同的过程注册移动设备，同最终用户在公司门户中针对“个人携带设备”(BYOD) 方案采用的过程相同。  

#### <a name="delete-a-device-enrollment-manager-from-intune"></a>从 Intune 删除设备注册管理员  
删除设备注册管理器不会影响注册的设备。 删除设备注册管理器时：  
- 不会取消注册任何已注册的设备  
- 仍能够完全管理注册的设备  
- 已删除的设备注册管理员帐户凭据仍有效，能够登录到公司门户来访问应用  
- 已删除的设备注册管理员帐户凭据仍无法擦除或停用设备  
- 已删除的设备注册管理员帐户与注册的设备的关系仍存在，但不可以注册任何其他设备

1.  在 Configuration Manager 控制台中，单击“管理”。  
2.  在“管理”  工作区中，展开“云服务” ，并单击“Microsoft Intune 订阅” 。 选择要添加设备注册管理器的 Microsoft Intune 订阅，然后单击“属性”。  
3.  在“Microsoft Intune 订阅属性”对话框中，单击“设备注册管理器”选项卡。  
4.  “搜索”想要删除的设备注册管理器，单击“删除”，然后单击“确定”。  
