---
title: "通过设备注册计划 (DEP) 注册 iOS 设备 - Configuration Manager | Microsoft Docs"
description: "在 Configuration Manager 中使用 Intune 为混合部署启用 iOS 设备注册计划 (DEP) 注册。"
ms.custom: na
ms.date: 08/15/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 78d44adc-9b1c-4bc6-b72d-e93873916ea6
caps.latest.revision: "9"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: e76e46ce0d6ee0582d5161709ff114b936ac5660
ms.sourcegitcommit: db7b7ec347638efd05cdba474e8a8f8535516116
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2017
---
# <a name="ios-device-enrollment-program-dep-enrollment-for-hybrid-deployments-with-configuration-manager"></a>使用 Configuration Manager 进行混合部署的 iOS 设备注册计划 (DEP) 注册

*适用范围：System Center Configuration Manager (Current Branch)*

公司可以通过 Apple 的设备注册计划购买 iOS 设备，然后使用 Microsoft Intune 管理它们。 要利用 Apple 设备注册计划 (DEP) 管理企业所有的 iOS 设备，公司必须完成 Apple 所要求的步骤以加入该计划并通过该计划获取设备。 该过程的详细信息，可以通过以下网站获得：  [https://deploy.apple.com](https://deploy.apple.com)进行管理。 该程序的优点包括免手动设置设备，无需通过 USB 将每个设备连接到计算机。  

 在你可以通过 DEP 注册企业所有的 iOS 设备之前，你需要从 Apple 获得 DEP 令牌。 此令牌允许 Intune 同步有关你的企业所拥有的且加入了 DEP 的设备的信息。 它还允许 Intune 将注册配置文件上传到 Apple 并将设备分配到这些配置文件。  

## <a name="apple-dep-enrollment-for-ios-devices"></a>适用于 iOS 设备的 Apple DEP 注册  
 以下过程介绍如何将通过 Apple DEP 购买的 iOS 设备指定为 Intune 管理的公司拥有的设备。 用户第一次将设备电源接通时，它会接收 DEP 管理配置文件、运行设置助理并将其纳入管理。  

##  <a name="enable-dep-enrollment-in-configuration-manager-with-intune"></a>使用 Intune 在 Configuration Manager 中启用 DEP 注册  

1.  **开始使用 Configuration Manager 管理 iOS 设备**   
    在能够注册 iOS 设备注册计划 (DEP) 设备之前，必须完成[设置混合移动设备管理](../../mdm/deploy-use/setup-hybrid-mdm.md)的步骤，包括[支持 iOS 注册的步骤](../deploy-use/enroll-hybrid-ios-mac.md)。
2.  **创建 DEP 令牌请求**   
    在 Configuration Manager 控制台中，依次展开“管理”工作区中的“层次结构配置”和“云服务”，然后单击“Microsoft Intune 订阅”。 单击“主页”选项卡上的“创建 DEP 令牌请求”，单击“浏览”指定 DEP 令牌请求的下载位置，然后单击“下载”。 将 DEP 令牌请求 (.pem) 文件保存到本地。 .pem 文件用于从 Apple 设备注册计划门户请求信任令牌 (.p7m)。  
3.  **获取设备注册计划令牌**   
    转到[设备注册计划门户](https://deploy.apple.com) (https://deploy.apple.com) 并使用你的公司 Apple ID 登录。 若要续订 DEP 令牌，必须在将来使用此 Apple ID。  
    1.  在[设备注册计划门户](https://deploy.apple.com)中，转到“设备注册计划” > “管理服务器”，然后单击“添加 MDM 服务器”。  
    2.  输入“MDM 服务器名称”，然后单击“下一步”。 服务器名称供参考，用于识别 MDM 服务器。 它不是名称，也不是 Intune 或 Configuration Manager 服务器的 URL。  
    3.  此时将打开“添加 <ServerName\>”对话框。 单击 **“选择文件...”** ，上载你在上一步中创建的 。pem 文件，然后单击“下一步” **“下一步”**。  
    4.  “添加 <ServerName\>”对话框会显示“你的服务器令牌”链接。 将服务器令牌(.p7m)文件下载到计算机，然后单击“完成”。  

     此证书(.p7m)文件用于在 Intune 和 Apple 的设备注册计划服务器之间建立信任关系。  
4.  **将 DEP 令牌添加到 Configuration Manager**   
    在 Configuration Manager 控制台中，展开“管理”工作区中的“层次结构配置”，然后单击“Microsoft Intune 订阅”。 单击“主页”选项卡上的“配置平台”，然后单击“iOS”。 选择“启用设备注册计划”，浏览到证书 (.p7m) 文件，单击“打开”，再单击“上传”，然后单击“确定”。  

## <a name="add-a-corporate-device-enrollment-policy"></a>添加公司设备注册策略  

1. 在 Configuration Manager 控制台的“资产和符合性”工作区中，依次展开“概述”、“所有公司拥有的设备”和“iOS”，然后单击“注册配置文件”。 单击“主页”选项卡的“创建配置文件”，打开创建配置文件向导。 在以下页面中配置设置：  
2. 在“常规”页上，指定以下信息，然后单击“下一步”。  
  -   名称 – 设备注册配置文件的名称。 （对用户不可见）  
  -   说明 - 设备注册配置文件的说明。 （对用户不可见）  
  -   用户关联 - 指定设备的注册方式。 请参阅 [Configuration Manager 中混合托管设备的用户关联](../../mdm/deploy-use/user-affinity-for-hybrid-managed-devices.md)。  

      -  用户关联提示：必须在初始设置过程中将设备与用户相关联，然后允许该用户将其用于访问公司数据和电子邮件。  应该对属于用户且需要使用公司门户（即需要安装应用）的 DEP 托管设备配置用户关联。  
      > [!NOTE]
      > 具有用户关联的 DEP 要求启用 ADFS WS-Trust 1.3 用户名/混合终结点以请求用户令牌。

      -   无用户关联：该设备不与用户关联。 将此隶属关系用于无需访问本地用户数据即可执行任务的设备。 需要用户关联的应用无法运行。  
    ![DEP 配置文件名称、说明和“用户关联”提示的屏幕截图](../media/dep-general.png)

3. 在“设备注册计划设置”页上，指定以下信息，然后单击“下一步”。  
    -   部门：用户在激活过程中点击“关于配置”时显示此信息。  
    -   支持电话号码：用户在激活过程中单击“需要帮助”按钮时显示。
       ![向 iOS 设备分配 DEP 配置文件的屏幕截图](../media/dep-settings.png)

    - 准备模式：在激活过程中设置此状态，且只能通过恢复设备出厂设置更改：  
        -   无人监督 - 有限的管理功能  
        -   受到监督 - 启用更多的管理选项，并默认禁用激活锁定  
    - **将注册配置文件锁定到设备**：在激活过程中设置此状态，且只能通过恢复出厂设置更改  
      -   禁用 - 允许从“设置”菜单中删除管理配置文件  
      -   启用 -（需要**准备模式** = **受到监督**）禁用可能允许删除管理配置文件的 iOS 设置  

4.  在“设置助理”页上，配置自定义第一次打开设备时启动的 iOS 设置助理的设置，然后单击“下一步”。 这些设置包括：  
  -   密码 - 在激活过程中提示输入密码。 始终需要密码，除非设备将受到保护，或以某种其他方式（即限制设备只可使用一个应用的展台模式）控制访问权限。  
  -   定位服务 - 如果启用，在激活过程中设置助理会提示此服务  
  -   还原 - 如果启用，在激活过程中设置助理会提示进行 iCloud 备份  
  -   Apple ID - 下载 iOS App Store 应用（包括由 Intune 安装的应用）时需要 Apple ID。 如果启用，Intune 在没有 ID 的情况下尝试安装应用时，iOS 将提示用户提供 Apple ID。  
  -   条款和条件 - 如果启用，在激活过程中设置助理会提示用户接受 Apple 的条款和条件  
  -   Touch ID - 如果启用，在激活过程中设置助理会提示此服务
  -   Apple Pay - 如果启用，在激活过程中设置助理会提示此服务
  -   缩放 - 如果启用，在激活过程中设置助理会提示此服务
  -   Siri - 如果启用，在激活过程中设置助理会提示此服务  
  -   向 Apple 发送诊断数据 - 如果启用，在激活过程中设置助理会提示此服务  
    ![向 iOS 设备分配 DEP 配置文件的屏幕截图](../media/dep-setup-assistant.png)
5.  在“附加管理”页上，指定 USB 连接是否可用于附加管理设置。 当选择“需要证书”时，你必须导入 Apple Configurator 管理证书以供此配置文件使用。  设置为“禁止”可阻止通过 Apple Configurator 与 iTunes 或管理同步文件。 Microsoft 建议设置为“禁止”，从 Apple Configurator 中导出任何进一步的配置，然后部署为自定义 iOS 配置文件，而不是使用此设置允许带或不带证书的手动部署。  

  -   禁止 - 阻止设备通过 USB 进行通信（禁止配对）  
  -   允许 - 允许设备通过 USB 连接与任何电脑或 Mac 进行通信  
  -   需要证书 - 允许与具有导入到注册配置文件的证书的 Mac 配对  

## <a name="assign-dep-devices-for-management"></a>分配 DEP 设备以进行管理

1. 转到[设备注册计划门户](https://deploy.apple.com) (https://deploy.apple.com) 并使用你的公司 Apple ID 登录。
2. 转到“部署计划” > “设备注册计划” > “管理设备”。 指定“选择设备”的方式，提供设备信息，并按设备“序列号”、“订单编号”或“上传 CSV 文件”指定详细信息。 接下来，选择“分配到服务器”并选择在步骤 3 中指定的 <*ServerName*>，然后单击“确定”。  

3.  **同步 DEP 管理的设备**   
    在“资产和符合性”工作区中，转到“所有公司拥有的设备” > “预声明设备”。 在“主页”选项卡上，单击“DEP 同步”。 会向 Apple 发送同步请求。 同步完成后，将显示 DEP 管理的设备。

    > [!NOTE]
    > 在混合配置中，DEP 同步操作通过在 Configuration Manager 控制台中单击“DEP 同步”手动触发。

4.  **分配 DEP 配置文件**<br>在“资产和符合性”工作区中，转到“公司拥有的所有设备” > “iOS” > “注册配置文件”。 选择 DEP 注册配置文件，然后在“主页”选项卡中单击“分配给设备”。 选择要使用此注册配置文件的设备，单击“添加”，然后单击“确定”。   
     ![向 iOS 设备分配 DEP 配置文件的屏幕截图](../media/dep-assign-profile.png)

## <a name="distribute-devices-to-users"></a>将设备分发给用户
现在可以将你的企业拥有的设备给予用户。 在打开设备并运行设置助理以注册设备之前，托管设备的“注册状态”将一直显示为“未连接”。 打开 iOS 设备时，它将注册为由 Intune 管理。
