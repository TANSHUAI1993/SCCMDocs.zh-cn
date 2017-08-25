---
title: "注册 iOS 设备 Apple Configurator - Configuration Manager | Microsoft Docs"
descriptions: Pre-enroll iOS devices by using Apple Configurator with Configuration Manager.
ms.custom: na
ms.date: 08/15/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 61a19d95-83ff-4ad8-9a67-f304d2ba54f2
caps.latest.revision: "5"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 403f3b730e24c0f76314b04bcdd1d2f817bcd908
ms.sourcegitcommit: db7b7ec347638efd05cdba474e8a8f8535516116
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2017
---
# <a name="ios-hybrid-enrollment-using-apple-configurator-with-configuration-manager"></a>配合使用 Configuration Manager 和 Apple Configurator 进行的 iOS 混合注册

*适用范围：System Center Configuration Manager (Current Branch)*

购买 iOS 设备供员工使用的公司可以使用Microsoft Intune 管理这些设备。 若要准备公司拥有的 iOS 设备以进行注册，请在 Configuration Manager 控制台中配置注册配置文件，然后导出供 Apple Configurator 使用的配置文件 URL。 准备 iOS 设备以进行注册，具体做法是通过 USB 线缆将设备连接到 Mac 计算机，并通过 Apple Configurator 设置该设备。 Apple Configurator 对该设备进行恢复出厂设置，并添加注册配置文件，以便用户第一次启动该设备并执行设置助理流程时便可注册该设备。

对于其中有单个用户使用该设备访问公司电子邮件和公司资源（如应用和日期）的专用 iOS 设备，建议按照以下过程进行操作。  

## <a name="prerequisites"></a>先决条件  

-   具有 iOS 设备的物理访问权限  

-   设备序列号 - [如何获取 iOS 序列号](https://support.apple.com/en-us/HT204308)  

-   安装了 [Apple Configurator 2.0](http://go.microsoft.com/fwlink/?LinkId=518017) 的 Mac 计算机  

-   用于将设备连接到 Mac 计算机的 USB 线缆  

## <a name="add-a-corporate-owned-device-enrollment-profile"></a>添加公司拥有的设备的注册配置文件

1.  在 Configuration Manager 控制台中，转至“资产和符合性” > “概述” > “公司拥有的所有设备” > “iOS” > “注册配置文件”。 单击“创建配置文件”，打开创建配置文件向导。 在以下页面中配置设置：  

2.  在“常规”  页面上，指定下列信息：  

    -   **名称**（对用户不可见）  

    -   **说明**（对用户不可见）  

    -   **用户关联** - 指定设备的注册方式。 对于大部分设置助理方案，请使用“针对用户相关性进行提示”。  

        -   **用户关联提示**：必须在初始设置过程中将设备与用户相关联，然后允许该用户将其用于访问公司数据和电子邮件。  

        -   “没有用户关联”：该设备不与用户关联。 将此隶属关系用于无需访问本地用户数据即可执行任务的设备。 需要用户关联的应用无法运行。

    单击 **“下一步”** 以继续。  

3.  在“设备注册计划”页面上，保留“为此配置文件配置设备注册计划设置”复选框为未选中，然后单击“下一步”。  

4.  查看摘要，然后单击“下一步”以创建注册配置文件。 单击“关闭”以完成向导。 现已准备好为要注册的设备添加 IMEI 号码或序列号。  

## <a name="predeclare-devices-to-enroll-with-setup-assistant"></a>通过设置助理预声明要注册的设备

在此步骤中，通过提供硬件标识符（IMEI 或序列号）列表，将设备预声明为企业拥有的设备。

有关详细信息，请参阅[通过 IMEI 和 iOS 序列号预声明设备](predeclare-devices-with-hardware-id.md)。 完成该任务后，返回到此页继续进行下一步。

## <a name="export-the-profile-to-deploy-to-ios-devices"></a>导出要部署到 iOS 设备的配置文件

1.  在 Configuration Manager 控制台中，转至“资产和符合性” > “概述” > “公司拥有的所有设备” > “iOS” > “注册配置文件”。

2.  选择要部署到移动设备的注册配置文件，然后单击“导出...”。

3.  在可编辑的文件中复制并保存**配置文件 URL**。   

4.  若要支持 Apple Configurator 2，必须编辑 2.0 配置文件 URL。 替换 URL 的以下部分：  

    ```  
    https://manage.microsoft.com/EnrollmentServer/Discovery.svc/iOS/ESProxy?id=  

    ```  

     替换为：  

    ```  
    https://appleconfigurator2.manage.microsoft.com/MDMServiceConfig?id=  

    ```

5.  保存已编辑的配置文件 URL。 可将其用于[下一节](#step-4-prepare-the-device-with-apple-configurator)中在 Apple Configurator 中添加注册配置文件 URL。  

> [!NOTE]
> 注册配置文件 URL 自其导出之日起两周内有效。 两周后，必须导出新的 URL 以注册 iOS 设备。

## <a name="prepare-the-device-with-apple-configurator"></a>使用 Apple Configurator 准备设备

若要准备 iOS 设备以进行注册，请将每个设备连接到 Mac 计算机，并将注册配置文件上传到设备中。  

> [!WARNING]  
>  Apple Configurator 可擦除设备并将其重置为出厂设置。  

1.  在 Mac 计算机上，打开“Apple Configurator 2”。  

2.  在菜单栏中，单击“Apple Configurator 2” > “偏好设置”。  

2.  在偏好设置窗格中，选择“服务器”，然后单击左窗格下方的“+”符号，以启动 MDM 服务器向导。 单击“下一步” 。  

3.  输入[之前](#step-3-export-the-profile-to-deploy-to-ios-devices)保存的“名称”和“注册 URL”。 单击“下一步” 。  

   > [!NOTE]
   > 如果收到有关 Apple TV 的信任配置文件请求的警告，可通过单击灰色的“X”安全取消“信任配置文件”选项。 也可以安全忽略任何定位证书警告。

   若要继续，请单击“下一步”，直到该向导完成。  

4.  在“服务器”窗格中，单击新服务器的配置文件旁的"编辑"。 确保注册 URL 与之前输入的 URL 完全匹配。 如果不匹配，请重新输入 URL，并单击“保存”。  

5.  通过 USB 线缆将 iOS 设备连接到 Mac 计算机。  

  > [!WARNING]  
  >  此过程会将设备重置为出厂配置。 连接该设备前，请重置并启动设备。 最佳做法是在继续之前设备应显示“你好”屏幕。  

6.  单击“准备”。 在“准备 iOS 设备”窗格中，选择“手动”，然后单击“下一步”。  

7.  在“在 MDM 服务器中注册”窗格中，选择已创建的服务器名称，然后单击“下一步”。  

9. 在“创建组织”窗格中，选择“组织”，或新建一个组织，然后单击“下一步”。  

10. 在“配置 iOS 设置助理”窗格中，选择向用户显示的步骤，然后单击“准备”。 如果出现提示，进行身份验证以更新信任设置。  

11. 完成后，可以断开 USB 线缆的连接。  

对于需要准备以进行注册的所有设备，重复以上步骤。

## <a name="distribute-devices"></a>分发设备

设备现已准备好企业注册。 关闭设备电源，并将它们分发给用户。 开启设备后，设置助理将启动并提示用户输入其工作或学校帐户以便开始注册。
