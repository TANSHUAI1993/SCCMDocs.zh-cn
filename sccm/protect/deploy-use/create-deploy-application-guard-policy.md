---
title: 创建和部署 Windows Defender 应用程序防护策略
titleSuffix: Configuration Manager
description: 创建和部署 Windows Defender 应用程序防护策略。
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 33a6c1d9-4dd8-411c-a748-693a5bd2ea5a
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: a21ef053cbd5f0a57d7688d69f29bc6f8871484a
ms.sourcegitcommit: b5c7496ca408803046acc8403858aafd5dca8808
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/05/2019
ms.locfileid: "68794734"
---
# <a name="create-and-deploy-windows-defender-application-guard-policy"></a>创建和部署 Windows Defender 应用程序防护策略

*适用范围：System Center Configuration Manager (Current Branch)*
<!-- 1351960 -->  
可以使用 Configuration Manager Endpoint Potection 创建和部署 [Windows Defender 应用程序防护（应用程序防护）](https://docs.microsoft.com/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview)策略。 这些策略通过在操作系统的其他部分无法访问的安全隔离容器中打开不受信任的网站来帮助保护用户安全。

## <a name="prerequisites"></a>先决条件

若要创建和部署 Windows Defender 应用程序防护策略，必须使用 Windows 10 Fall Creator’s Update (1709)。 必须使用网络隔离策略配置要部署此策略的 Windows 10 设备。 有关详细信息，请参阅 [Windows Defender 应用程序防护概述](https://docs.microsoft.com/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview)。

## <a name="create-a-policy-and-to-browse-the-available-settings"></a>若要创建策略，并浏览可用设置，请执行以下操作：

1. 在 Configuration Manager 控制台中，选择“资产和符合性”  。
2. 在“资产和符合性”  工作区中，选择“概述”   > “终结点保护”   > “Windows Defender 应用程序防护”  。
3. 在“主页”  选项卡的“创建”  组中，单击“创建 Windows Defender 应用程序防护策略”  。
4. 将此[文章](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/configure-wd-app-guard)用作参考，浏览和配置可用的设置。 Configuration Manager 允许设置某些策略设置:
   - [主机交互设置](#bkmk_HIS)
   - [应用程序行为](#bkmk_ABS)
   - [文件管理](#bkmk_FM)
5. 在“网络定义”页上，可指定公司标识并定义企业网络边界  。

    > [!NOTE]
    > Windows 10 电脑仅在客户端上存储一个网络隔离列表。 可以创建两种不同的网络隔离列表，并将它们部署到客户端：
    >
    >  - 一个来自 Windows 信息保护
    >  - 一个来自 Windows Defender 应用程序防护
    >
    > 如果部署两个策略，两个网络隔离列表必须匹配。 如果部署的列表与同一个客户端不匹配，则部署失败。 有关详细信息，请参阅 [Windows 信息保护文档](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/create-wip-policy-using-sccm)。

6. 结束后，完成向导操作，并将策略部署到一个或多个 Windows 10 1709 设备。

### <a name="bkmk_HIS"></a> 主机交互设置

配置主机设备和应用程序防护容器之间的交互。 在 Configuration Manager 1802 之前的版本中，应用程序行为和主机交互都位于“设置”  选项卡下。

- **剪贴板** - 在 Configuration Manager 1802 之前的版本中，位于“设置”下
  - 允许的内容类型
    - 文本
    - 映像
- **打印：**
  - 启用打印为 XPS
  - 启用打印为 PDF
  - 启用打印到本地打印机
  - 启用打印到网络打印机
- **图形：** （从 Configuration Manager 1802 版开始）
  - 虚拟图形处理器访问
- **文件：** （从 Configuration Manager 1802 版开始）
  - 将下载的文件保存到主机

### <a name="bkmk_ABS"></a> 应用程序行为设置

在应用程序防护会话内配置应用程序行为。 在 Configuration Manager 1802 之前的版本中，应用程序行为和主机交互都位于“设置”  选项卡下。

- **内容：**
  - 企业网站可以加载非企业内容，如第三方插件。
- **其他：**
  - 保留用户生成的浏览器数据
  - 在独立的应用程序防护会话中审核安全性事件

### <a name="bkmk_FM"></a> 文件管理
<!--3555858-->
从 Configuration Manager 版本1906开始, 有一个允许用户信任通常在应用程序防护中打开的文件的策略设置。 成功完成后，文件将在主机设备上打开，而不是在应用程序防护中打开。 有关应用程序防护策略的详细信息，请参阅[配置 Windows Defender 应用程序防护策略设置](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/configure-wd-app-guard)。

- **允许用户信任在 Windows Defender 应用程序防护中打开的文件**-使用户能够将文件标记为受信任。 当文件受信任时, 它会在主机而不是应用程序防护中打开。 适用于 Windows 10 版本1809或更高版本的客户端。
  - **禁止：** 不允许用户将文件标记为可信（默认）。
  - **文件由防病毒软件检查:** 允许用户在防病毒检查后将文件标记为受信任。
  - **所有文件：** 允许用户将任何文件标记为可信。

启用文件管理时, 可能会看到客户端的 DCMReporting 中记录的错误。 以下错误通常不会影响功能: <!--4619457-->

- 在兼容的设备上：
  - 找不到 FileTrustCriteria_condition
- 在不兼容的设备上：
  - 找不到 FileTrustCriteria_condition
  - FileTrustCriteria_condition 不能位于映射中
  - 在摘要中找不到 FileTrustCriteria_condition

若要编辑应用程序防护设置, 请在 "**资产和符合性**" 工作区中展开**Endpoint Protection** , 然后单击 " **Windows Defender 应用程序防护**" 节点。 右键单击要编辑的策略，然后选择“属性”  。

## <a name="next-steps"></a>后续步骤

若要了解有关 Windows Defender 应用程序防护的详细信息：[Windows Defender 应用程序防护概述](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/wd-app-guard-overview)。
[Windows Defender 应用程序防护常见问题解答](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/faq-wd-app-guard)。
