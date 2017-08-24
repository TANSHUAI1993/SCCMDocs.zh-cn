---
title: "配置 Endpoint Protection 客户端 | Microsoft Docs"
description: "了解如何配置 Endpoint Protection 的自定义客户端设置，从而将其部署到层次结构中的计算机集合。"
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
caps.latest.revision: "21"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 1488aaa465fb9810bc1b641d41dad95189d37418
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="configure-custom-client-settings-for-endpoint-protection"></a>为 Endpoint Protection 配置自定义客户端设置

*适用范围：System Center Configuration Manager (Current Branch)*

此过程为 Endpoint Protection 配置自定义客户端设置，使其可部署到层次结构中的计算机集合。

> [!IMPORTANT]
>  除非你确信要将这些设置应用于层次结构中的所有计算机，否则请不要配置默认 Endpoint Protection 客户端设置。

## <a name="to-enable-endpoint-protection-and-configure-custom-client-settings"></a>若要启用 Endpoint Protection 并配置自定义客户端设置

1.  在 Configuration Manager 控制台中，单击“管理” 。

2.  在“管理”  工作区中，单击“客户端设置” 。

3.  在“主页”  选项卡上的“创建”  组中，单击“创建自定义客户端设备设置” 。

4.  在“创建自定义客户端设备设置”  对话框中，为设置组提供名称和描述，然后选择“Endpoint Protection” 。

5.  配置所需的 Endpoint Protection 客户端设置。 有关可以配置的 Endpoint Protection 客户端设置的完整列表，请参阅[关于 System Center Configuration Manager 中的客户端设置](../../core/clients/deploy/about-client-settings.md)主题中的 Endpoint Protection 部分。

   > [!IMPORTANT]
   >  必须先安装 Endpoint Protection 站点系统角色，然后才能为 Endpoint Protection 配置客户端设置。

6.  单击“确定”  关闭“创建自定义客户端设备设置”  对话框。 新的客户端设置显示在“管理”  工作区的“客户端设置”  节点中。

7.  在可以使用自定义客户端设置之前，必须将它们部署到集合。 选择你想要部署的自定义客户端设置，然后在“主页”  选项卡的“客户端设置”  组中，单击“部署” 。

8.  在“选择集合”  对话框中，选择你想要将客户端设置部署到的集合，然后单击“确定” 。 新的部署显示在细节窗格的“部署”  选项卡中。

当客户端计算机下一次下载客户端策略时，将使用这些设置对它们进行配置。 若要为单一客户端启动策略检索，请参阅[如何在 System Center Configuration Manager 中管理客户端](../../core/clients/manage/manage-clients.md)中的“为 Configuration Manager 客户端启动策略检索”部分。

## <a name="how-to-provision-the-endpoint-protection-client-in-a-disk-image-in-configuration-manager"></a>如何在 Configuration Manager 中设置磁盘映像中的 Endpoint Protection 客户端
你可以将 Endpoint Protection 客户端安装在打算用作 Configuration Manager 操作系统部署的磁盘映像源的计算机上。 此计算机通常称为引用计算机。 创建操作系统的映像之后，可以随后使用 Configuration Manager 操作系统部署将可能包含软件包（包括 Endpoint Protection）的映像部署到客户端计算机。

本主题介绍了在引用计算机上安装和配置 Endpoint Protection 客户端的相关步骤

### <a name="prerequisites-for-installing-the-endpoint-protection-client-on-the-reference-computer"></a>在引用计算机上安装 Endpoint Protection 客户端的先决条件
下面的列表包含在引用计算机上安装 Endpoint Protection 客户端软件的必需先决条件。

-   必须具有对 Endpoint Protection 客户端安装包 **scepinstall.exe** 的访问权限。 此包位于站点服务器上 System Center Configuration Manager 安装文件夹的“客户端”文件夹中。

-   若要确保使用机构中所需的配置部署 Endpoint Protection 客户端，请创建一个反恶意软件策略，然后导出该策略。 可以随后指定要在手动安装 Endpoint Protection 客户端时使用的反恶意软件策略。 有关详细信息，请参阅[如何在 System Center Configuration Manager 中为 Endpoint Protection 创建和部署反恶意软件策略](endpoint-antimalware-policies.md)。

   > [!NOTE]
   >  无法导出“默认客户端反恶意软件策略”  。

-   如果要使用最新的定义安装 Endpoint Protection 客户端，必须从 [Microsoft 恶意软件防护中心](http://go.microsoft.com/fwlink/?LinkID=200965)下载这些定义。

### <a name="how-to-install-the-endpoint-protection-client-software-on-the-reference-computer"></a>如何在引用计算机上安装 Endpoint Protection 客户端软件
可以通过命令提示符以本地方式在引用计算机上安装 Endpoint Protection 客户端。 为此，你必须首先获取安装文件“scepinstall.exe” 。 你也可以使用预先配置的反恶意软件策略或以前导出的反恶意软件策略来安装客户端。

## <a name="to-install-the-endpoint-protection-client-from-a-command-prompt"></a>通过命令提示符安装 Endpoint Protection 客户端

1.  将 **scepinstall.exe** 从 System Center Configuration Manager 安装媒体上的“Client”文件夹复制到想要安装 Endpoint Protection 客户端软件的计算机上。

2.  使用管理员权限打开命令提示符，导航到“scepinstall.exe”  所在的文件夹，然后运行下列命令，同时添加所需的任何其他命令行属性：

   ```
   scepinstall.exe
   ```

    你可以指定下列命令行属性之一：

   |属性|描述|
   |--------------|-----------------|
   |/s|指定将执行无提示安装。|
   |/q|指定将执行安装程序文件的无提示提取。|
   |/i|指定应执行正常安装。|
   |/noreplace|指定在安装过程中不卸载第三方反恶意软件。|
   |/policy|指定要用于在安装过程中配置客户端的反恶意软件策略文件。|
   |/sqmoptin|指定选择将此客户端软件安装加入 Microsoft 客户体验改善计划。|

3.  请按照屏幕说明进行操作以完成客户端安装。

4.  如果下载了最新的更新定义包，请将该包复制到客户端计算机，然后双击该定义包进行安装。

   > [!NOTE]
   >  Endpoint Protection 客户端安装完成后，客户端将自动执行定义更新检查。 如果此更新检查成功，则你不必手动安装最新的定义更新包。

## <a name="to-install-the-client-software-with-an-antimalware-policy-from-the-command-prompt"></a>通过命令提示符使用反恶意软件策略安装客户端软件

1.  将 **scepinstall.exe** 和导出的或预配置的反恶意软件政策复制到想要安装 Endpoint Protection 客户端软件的计算机上。

2.  使用管理员权限打开命令提示符，导航到“scepinstall.exe”  和反恶意软件策略所在的文件夹，然后运行下列命令：

   ```
   scepinstall.exe /policy <full path>\<policy file>
   ```

3.  请按照屏幕说明进行操作以完成客户端安装。

4.  如果下载了最新的定义包，请将该包复制到客户端计算机，然后双击该定义包进行安装。

   > [!NOTE]
   >  Endpoint Protection 客户端安装完成后，客户端将自动执行定义更新检查。 如果此更新检查成功，则你不必手动安装最新的定义更新包。

## <a name="verify-that-the-endpoint-protection-client-is-installed-correctly"></a>验证是否正确安装了 Endpoint Protection 客户端
在引用计算机上安装 Endpoint Protection 客户端之后，请验证该客户端是否正常工作。

### <a name="to-verify-that-the-endpoint-protection-client-is-installed-correctly"></a>验证是否正确安装了 Endpoint Protection 客户端

1.  在引用计算机上，从 Windows 通知区域中打开“System Center Endpoint Protection” 。

2.  在“System Center Endpoint Protection”对话框的“开始”选项卡上，验证“实时保护” 是否设置为“启用” 。

3.  验证是否为“病毒和间谍软件定义”  显示了“最新” 。

4.  为了确保引用计算机已针对映像做好准备，请在“扫描选项” 下选择“完全” ，然后单击“立即扫描” 。

### <a name="how-to-prepare-the-endpoint-protection-client-for-imaging"></a>如何针对映像准备 Endpoint Protection 客户端
确定 Endpoint Protection 客户端已正确安装在引用计算机上后，可以针对映像准备计算机。 执行下列步骤以针对映像准备 Endpoint Protection 客户端。


有关 Configuration Manager 中操作系统部署的详细信息，请参阅[使用 System Center Configuration Manager 管理操作系统映像](/sccm/osd/get-started/manage-operating-system-images)。

### <a name="to-prepare-the-endpoint-protection-client-for-imaging"></a>针对映像准备 Endpoint Protection 客户端

1.  在引用计算机上，以具有管理权限的用户身份登录。

2.  从 TechNet 上的 **Windows SysInternals 站点** 下载并安装 [PsTools](http://go.microsoft.com/fwlink/?LinkId=215263) 。

3.  打开提升的命令提示符，导航到你在其中安装了 PsTools 的文件夹，然后键入下列命令

   ```
   Psexec.exe -s -i regedit.exe
   ```

   > [!IMPORTANT]
   >  以此方式运行注册表编辑器时请小心；PsExec.exe 中的 –s 选项使用 LocalSystem 权限运行注册表编辑器。

4.  在注册表编辑器中，导航到下列每个注册表项，并将其删除。

   > [!IMPORTANT]
   >  必须在对引用计算机进行映像之前的最后一步骤删除这些注册表项。 Endpoint Protection 客户端启动后，会重新创建注册表项。 如果重启引用计算机，你必须再次删除这些注册表项。

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\InstallTime**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanRun**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanType**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastQuickScanID**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastFullScanID**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\RemovalTools\MRT\GUID**

完成前面的步骤后，即可针对映像准备引用计算机。 有关 Configuration Manager 中操作系统部署的详细信息，请参阅[使用 System Center Configuration Manager 管理操作系统映像](/sccm/osd/get-started/manage-operating-system-images)。

在部署包含 Endpoint Protection 客户端软件的映像时，Endpoint Protection 客户端将自动向计算机所分配到的 Configuration Manager 站点报告信息，并且会下载和应用适用于客户端计算机的策略。
