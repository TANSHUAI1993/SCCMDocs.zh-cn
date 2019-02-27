---
title: 配置 Microsoft Edge 设置
titleSuffix: Configuration Manager
description: 在 Windows 10 客户端上配置 Microsoft Edge Web 浏览器设置
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.assetid: 76477b4d-df41-4b25-8318-7d18d46ca2c6
ms.collection: M365-identity-device-management
ms.openlocfilehash: d97a67dd65dd79ba8b47541d0c7a7cad239dca28
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56126019"
---
# <a name="configure-microsoft-edge-settings-in-system-center-configuration-manager"></a>在 System Center Configuration Manager 中配置 Microsoft Edge 设置

适用范围：System Center Configuration Manager (Current Branch)

<!-- 1357310 -->自 1802 版起，如果是在 Windows 10 客户端上使用 [Microsoft Edge](https://technet.microsoft.com/microsoft-edge/bb265256) Web 浏览器的客户，请创建 Configuration Manager 符合性设置策略以配置多个 Microsoft Edge 设置。 

此策略仅适用于 Windows 10 1703 或更高版本上的客户端。 <!--511552-->


## <a name="policy-settings"></a>策略设置
此策略当前包括以下设置：
- 将 Microsoft Edge 浏览器设置为默认浏览器：将 Web 浏览器的 Windows 10 默认应用设置配置为 Microsoft Edge
- **允许使用地址栏下拉列表**：需要 Windows 10 版本 1703 或更高版本。 有关详细信息，请参阅 [AllowAddressBarDropdown 浏览器策略](/windows/client-management/mdm/policy-csp-browser#browser-allowaddressbardropdown)。
- **允许在 Microsoft 浏览器之间同步收藏夹**：需要 Windows 10 版本 1703 或更高版本。 有关详细信息，请参阅 [SyncFavoritesBetweenIEAndMicrosoftEdge 浏览器策略](/windows/client-management/mdm/policy-csp-browser#browser-syncfavoritesbetweenieandmicrosoftedge)。
- **允许在退出时清除浏览数据**：需要 Windows 10 版本 1703 或更高版本。 有关详细信息，请参阅 [ClearBrowsingDataOnExit 浏览器策略](/windows/client-management/mdm/policy-csp-browser#browser-clearbrowsingdataonexit)。
- **允许使用 Do Not Track 标头**：有关详细信息，请参阅 [AllowDoNotTrack 浏览器策略](/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack)。
- **允许自动填充**：有关详细信息，请参阅 [AllowAutofill 浏览器策略](/windows/client-management/mdm/policy-csp-browser#browser-allowautofill)。
- **允许使用 Cookie**：有关详细信息，请参阅 [AllowCookies 浏览器策略](/windows/client-management/mdm/policy-csp-browser#browser-allowcookies)。
- **允许使用弹出窗口阻止程序**：有关详细信息，请参阅 [AllowPopups 浏览器策略](/windows/client-management/mdm/policy-csp-browser#browser-allowpopups)。
- **允许在地址栏中显示搜索建议**：有关详细信息，请参阅 [AllowSearchSuggestionsinAddressBar 浏览器策略](/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar)。
- **允许将 Intranet 流量发送到 Internet Explorer**：有关详细信息，请参阅 [SendIntranetTraffictoInternetExplorer 浏览器策略](/windows/client-management/mdm/policy-csp-browser#browser-sendintranettraffictointernetexplorer)。
- **允许使用密码管理器**：有关详细信息，请参阅 [AllowPasswordManager 浏览器策略](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)。
- **允许使用开发人员工具**：有关详细信息，请参阅 [AllowDeveloperTools 浏览器策略](/windows/client-management/mdm/policy-csp-browser#browser-allowdevelopertools)。
- **允许使用扩展**：有关详细信息，请参阅 [AllowExtensions 浏览器策略](/windows/client-management/mdm/policy-csp-browser#browser-allowextensions)。


### <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge"></a>为 Microsoft Edge 配置 Windows Defender SmartScreen 设置
<!--1353701-->自版本 1806 起，此策略为 [Windows Defender SmartScreen](/windows/security/threat-protection/windows-defender-smartscreen/windows-defender-smartscreen-overview) 添加了 3 个设置。 该策略现在包含“SmartScreen 设置”页上的以下附加设置：

- **允许 SmartScreen**：指定是否允许 Windows Defender SmartScreen。 有关详细信息，请参阅 [AllowSmartScreen 浏览器策略](/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)。
- **用户可以替代站点的 SmartScreen 提示**：指定用户是否可替代有关潜在恶意网站的 Windows Defender SmartScreen 筛选器警告。 有关详细信息，请参阅 [PreventSmartScreenPromptOverride 浏览器策略](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)。
- **用户可以替代文件的 SmartScreen 提示**：指定用户是否可替代有关下载未经认证文件的 Windows Defender SmartScreen 筛选器警告。 有关详细信息，请参阅[PreventSmartScreenPromptOverrideForFiles 浏览器策略](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)。



## <a name="create-the-microsoft-edge-browser-profile"></a>创建 Microsoft Edge 浏览器配置文件

1. 在 Configuration Manager 控制台中，转到“资产和符合性”工作区。 展开“符合性设置”，然后选择“Microsoft Edge 浏览器配置文件”节点。 单击“创建 Microsoft Edge 配置文件”的功能区选项。
2. 指定策略“名称”，根据需要输入“说明”，然后单击“下一步”。
3. 在“常规设置”页上，将值更改为“已配置”，使设置包含在此策略中，然后单击“下一步”。 必须配置“将 Microsoft Edge 浏览器设为默认”设置才能继续操作。
4. 在版本 1806 或更高版本中，请在“SmartScreen 设置”页上配置设置，然后单击“下一步”。 
5. 在“支持的平台”页上，选择此策略要应用到的 OS 版本和体系结构，然后单击“下一步”。 
6. 完成向导。



## <a name="deploy-the-policy"></a>部署策略

1. 选择策略，然后单击功能区选项“部署”。
2. 单击“浏览”以选择要在其中部署策略的用户或设备集合。 
3. 根据需要选择其他选项。  
     a. 当策略不合规时生成警报。  
     b. 设置客户端评估设备与此策略符合性所依据的计划。 
4. 单击“确定”创建部署。



## <a name="next-steps"></a>后续步骤

就像任何符合性设置策略，客户端会修正指定计划的设置。 在 Configuration Manager 控制台中[监视和报告设备合规性](/sccm/compliance/deploy-use/monitor-compliance-settings)。
