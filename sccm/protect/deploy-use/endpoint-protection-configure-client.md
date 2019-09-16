---
title: Endpoint Protection 客户端设置
titleSuffix: Configuration Manager
description: 了解如何为 Endpoint Protection 配置自定义客户端设置。
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: fadbdaf8dc836e2f468aa0f8a82408d718606bc1
ms.sourcegitcommit: 13ac4f5e600dc1edf69e8566e00968f40e1d1761
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2019
ms.locfileid: "70892338"
---
# <a name="configure-custom-client-settings-for-endpoint-protection"></a>为 Endpoint Protection 配置自定义客户端设置

*适用范围：System Center Configuration Manager (Current Branch)*

此过程为 Endpoint Protection 配置自定义客户端设置，可将其部署到层次结构中的设备集合。

> [!IMPORTANT]  
>  除非确定要将这些设置应用于层次结构中的所有计算机，否则请不要配置默认 Endpoint Protection 客户端设置。 



## <a name="to-enable-endpoint-protection-and-configure-custom-client-settings"></a>若要启用 Endpoint Protection 并配置自定义客户端设置

1. 在 Configuration Manager 控制台中，单击“管理”  。  

2. 在“管理”  工作区中，单击“客户端设置”  。  

3. 在“主页”  选项卡上的“创建”  组中，单击“创建自定义客户端设备设置”  。  

4. 在“创建自定义客户端设备设置”  对话框中，为设置组提供名称和描述，然后选择“Endpoint Protection”  。  

5. 配置所需的 Endpoint Protection 客户端设置。 有关可以配置的 Endpoint Protection 客户端设置的完整列表，请参阅[关于客户端设置](/sccm/core/clients/deploy/about-client-settings#endpoint-protection)中的 Endpoint Protection 部分。  

   > [!IMPORTANT]  
   >  先安装 Endpoint Protection 站点系统角色，然后才能为 Endpoint Protection 配置客户端设置。  

6. 单击“确定”  关闭“创建自定义客户端设备设置”  对话框。 新的客户端设置显示在“管理”  工作区的“客户端设置”  节点中。  

7. 接下来，将自定义客户端设置部署到集合。 选择要部署的自定义客户端设置。 在“主页”选项卡的“客户端设置”组中，单击“部署”    。  

8. 在“选择集合”  对话框中，选择你想要将客户端设置部署到的集合，然后单击“确定”  。 新的部署显示在细节窗格的“部署”  选项卡中。  

当客户端下一次下载客户端策略时，会使用这些设置进行配置。 有关详细信息，请参阅[启动 Configuration Manager 客户端的策略检索](/sccm/core/clients/manage/manage-clients#BKMK_PolicyRetrieval)。  



## <a name="how-to-provision-the-endpoint-protection-client-in-a-disk-image"></a>如何在磁盘映像中预配 Endpoint Protection 客户端

在打算用作 Configuration Manager OS 部署磁盘映像来源的计算机上安装 Endpoint Protection 客户端。 此计算机通常称为引用计算机。 创建 OS 映像后，使用 Configuration Manager OS 部署来部署映像。

> [!Important]  
> 默认情况下，Windows 10 和 Windows Server 2016 已安装 Windows Defender。 这些版本的 Windows 上不需要此过程。  

使用以下相关步骤，可帮助在引用计算机上安装和配置 Endpoint Protection 客户端。


### <a name="prerequisites"></a>先决条件

下面的列表包含在引用计算机上安装 Endpoint Protection 客户端软件的必需先决条件。

- 必须具有对 Endpoint Protection 客户端安装包 **scepinstall.exe** 的访问权限。 可在站点服务器上 Configuration Manager 安装文件夹的“客户端”文件夹中找到此包  。  

- 若要部署 Endpoint Protection 客户端，使其具备组织所需配置，请创建并导出反恶意软件政策。 然后指定要在手动安装 Endpoint Protection 客户端时使用的此政策。 有关详细信息，请参阅[如何创建并部署反恶意软件政策](/sccm/protect/deploy-use/endpoint-antimalware-policies)。  

  > [!NOTE]  
  >  无法导出“默认客户端反恶意软件政策”  。  

- 如果要使用最新定义安装 Endpoint Protection 客户端，请从 [Windows Defender 安全智能](https://www.microsoft.com/wdsi)下载它们。  

> [!NOTE]  
> 从 Configuration Manager 1802 开始，无需在 Windows 10 设备上安装 Endpoint Protection 代理 (SCEPInstall)。 如果已在 Windows 10 设备上安装该代理，Configuration Manager 也不会将其删除。 管理员可在运行最低 1802 客户端版本的 Windows 10 设备上删除 Endpoint Protection 代理。 SCEPInstall.exe 可能仍然存在于某些计算机上的 C:\Windows\ccmsetup 中，但新客户端安装不应下载它。 <!--503654-->


### <a name="how-to-install-the-endpoint-protection-client-on-the-reference-computer"></a>如何在引用计算机上安装 Endpoint Protection 客户端

通过命令提示符以本地方式在引用计算机上安装 Endpoint Protection 客户端。 首先获取安装文件 scepinstall.exe  。 有关详细信息，请参阅[通过命令提示符安装 Endpoint Protection 客户端](#bkmk_manual-install)。

如有必要，还可包含预先配置的或先前导出的反恶意软件政策。 



## <a name="bkmk_manual-install"></a> 通过命令提示符安装 Endpoint Protection 客户端

1. 将 scepinstall.exe 从 Configuration Manager 安装文件夹上的“客户端”文件夹复制到想要安装 Endpoint Protection 客户端软件的计算机上   。  

2. 以管理员身份打开命令提示符。 将目录更改为安装程序所在的文件夹。 然后运行 `scepinstall.exe`，添加所需的任何其他命令行属性：


   |  属性   |                                  说明                                   |
   |-------------|--------------------------------------------------------------------------------|
   |    `/s`     |                           无提示运行安装程序                           |
   |    `/q`     |                        无提示提取安装程序文件                        |
   |    `/i`     |                           正常运行安装程序                           |
   |  `/policy`  | 指定要在安装过程中配置客户端的反恶意软件政策文件 |
   | `/sqmoptin` |     选择 Microsoft 客户体验改善计划 (CEIP)     |


3. 按照屏幕上的说明完成客户端安装。  

4. 如果下载了最新的更新定义包，请将该包复制到客户端计算机，然后双击该定义包进行安装。  

   > [!NOTE]  
   >  Endpoint Protection 客户端安装完成后，客户端将自动执行定义更新检查。 如果此更新检查成功，则无需手动安装最新的定义更新包。  

#### <a name="example-install-the-client-with-an-antimalware-policy"></a>示例：使用反恶意软件政策安装客户端

`scepinstall.exe /policy <full path>\<policy file>`



## <a name="verify-the-endpoint-protection-client-installation"></a>验证 Endpoint Protection 客户端安装

在引用计算机上安装 Endpoint Protection 客户端之后，请验证该客户端是否正常工作。

1.  在引用计算机上，从 Windows 通知区域打开“System Center Endpoint Protection”  。  

2.  在“System Center Endpoint Protection”  对话框的“开始”  选项卡上，验证“实时保护”  是否设置为“启用”  。  

3.  验证“病毒和间谍软件定义”是否显示“最新”   。  

4.  为了确保引用计算机已针对映像做好准备，请在“扫描选项”下选择“完全”，然后单击“立即扫描”    。  



## <a name="prepare-the-endpoint-protection-client-for-imaging"></a>针对映像准备 Endpoint Protection 客户端

执行下列步骤以针对映像准备 Endpoint Protection 客户端：

1. 在引用计算机上，以管理员身份登录。  

2. 从 [Windows SysInternals](https://docs.microsoft.com/sysinternals/downloads/psexec) 下载并安装 **PsExec**。  

3. 以管理员身份运行命令提示符，将目录更改为在其中安装 PsTools 的文件夹，然后键入以下命令：  

   `psexec.exe -s -i regedit.exe`  

   > [!IMPORTANT]  
   >  以这种方式运行注册表编辑器时，请格外小心。 PsExec.exe 在 LocalSystem 上下文中运行它。  

4. 在“注册表编辑器”中，删除以下注册表项：  

   > [!IMPORTANT]  
   >  在对引用计算机进行映像之前的最后一步骤中删除这些注册表项。 Endpoint Protection 客户端会在启动时重新创建这些项。 如果重启引用计算机，将再次删除这些注册表项。  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\InstallTime`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanRun`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanType`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastQuickScanID`   

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastFullScanID`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\RemovalTools\MRT\GUID`

现在，可针对映像准备引用计算机。

部署包含 Endpoint Protection 客户端的 OS 映像时，它会自动将信息报告给设备已分配的 Configuration Manager 站点。 客户端下载并应用任何目标反恶意软件政策。  



## <a name="see-also"></a>另请参阅

有关 Configuration Manager 中的 OS 部署的详细信息，请参阅[管理 OS 映像](/sccm/osd/get-started/manage-operating-system-images)。

