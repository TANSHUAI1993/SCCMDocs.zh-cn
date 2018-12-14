---
title: 自定义支持中心
titleSuffix: Configuration Manager
description: 自定义支持中心配置文件。
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a6f7f6b7-9ef3-4ffa-a3cf-d877ac55983b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ca7dfce7b96747e46247cb290b4fc0d7e0df41ff
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52458029"
---
# <a name="customize-support-center"></a>自定义支持中心

*适用范围：System Center Configuration Manager (Current Branch)*

[支持中心](/sccm/core/support/support-center)工具包括可自定义的配置文件。 默认情况下，安装支持中心时，此文件位于以下路径：`C:\Program Files (x86)\Configuration Manager Support Center\ConfigMgrSupportCenter.exe.config`。 配置文件会更改程序的行为：

  - [自定义数据收集：](#bkmk_datacoll)：编辑数据收集期间包含的注册表项和 WMI 命名空间集  

  - [自定义日志组](#bkmk_loggroups)：使用正则表达式定义新的日志文件组。 也向日志组添加其他日志文件。  

  - [使用通配符收集其他日志文件](#bkmk_wildcards)：使用通配符搜索功能收集其他日志文件  

要进行这些更改，你需要在安装支持中心的客户端上具有本地管理权限。 使用文本编辑器或 XML 编辑器（如 Notepad 或 Visual Studio）进行这些自定义设置。

> [!Important]  
> 支持中心配置文件是 XML 格式的文件。 这对支持中心的运行至关重要。 仅建议熟悉 XML 和正则表达式的用户修改此文件。  

在自定义支持中心配置文件之前，请保存原始文件的备份。 如果在编辑文件时出错，你可以通过此备份恢复原始的支持中心功能。 如果未创建备份，并且在修改配置文件后支持中心无法正常运行，请重新安装支持中心。 还可以在支持中心的其他安装过程中复制配置文件。



## <a name="bkmk_datacoll"></a> 自定义数据收集

要自定义客户端上的数据收集，请使用 `<dataCollectorSettings>` 元素中包含的 XML 元素来修改支持中心配置文件。


### <a name="wmi-data-collection"></a>WMI 数据收集

`<CcmWmiDataCollector>` 元素包含 `<collectionScopes>` 元素。 使用此元素更改供支持中心收集数据的 WMI 命名空间。 它还包含 `<ignoreScopes>` 元素。 使用此元素从 `<collectionScopes>` 元素中定义的命名空间部分筛选出数据收集。  
    
#### <a name="example"></a>示例
默认配置文件从 `root\ccm` 命名空间收集数据。 它在 `<collectionScopes>` 中的 `<add/>` 元素中包含此路径。 

还忽略此命名空间的 `\cimodels`、`\invagt`、 `\events` 和 `\policy` 路径下的所有内容。 它在 `<ignoreScopes>` 内所含的 `<add/>` 元素中包含这些路径。

```XML
<CcmWmiDataCollector>
  <collectionScopes>
    <!-- Collect these namespaces (ignoring the sub-scopes in the ignoreScopes block) -->
    <add key="root\ccm"/>
    <add key="root\cimv2\sms"/>
  </collectionScopes>
  <ignoreScopes>
    <!-- Collecting these namespaces is known to be problematic/unnecessary -->
    <add key="root\ccm\cimodels"/>
    <add key="root\ccm\invagt"/>
    <add key="root\ccm\events"/>
    <!-- Do not collect policy, there's already a separate policy collector.-->
    <add key="root\ccm\policy"/>
  </ignoreScopes>
</CcmWmiDataCollector>
```


### <a name="registry-data-collection"></a>注册表数据收集

`<RegistryDataCollector>` 元素包含 `<registryKeys>` 元素。 使用此元素更改支持中心在 `HKEY_LOCAL_MACHINE` 路径下收集的注册表项和子项。 支持中心不支持从其他根注册表路径收集注册表数据。

#### <a name="example"></a>示例
要收集设备上安装的经典程序的注册表项，请在 `<registryKeys>` 元素中添加以下 `<add/>` 元素：`<add key="software\\microsoft\\windows\\currentversion\\uninstall"/>`

```XML
<RegistryDataCollector>
  <registryKeys>
    <!-- Registry keys (and all subkeys) to collect -->
    <add key="software\\microsoft\\ccm"/>
    <add key="software\\microsoft\\sms"/>
    <add key="software\\microsoft\\ccmsetup"/>
    <add key="software\\microsoft\\windows\\currentversion\\uninstall"/>
  </registryKeys>
</RegistryDataCollector>
```



## <a name="bkmk_loggroups"></a> 自定义日志文件组

要自定义支持中心收集的日志文件及其在“日志组”列表中的显示方式，请使用 `<logGroups>` 元素中的元素。 启动支持中心时，它会扫描配置文件的此部分。 然后，它会在日志组列表中为 `<logGroups>` 元素中包含的 `<add/>` 元素中找到的每个唯一键属性值创建组。

  - **组件日志组**：`<componentLogGroup>` 元素使用键属性定义显示在列表中的日志组的名称。 它还使用包含正则表达式 (regex) 的值属性。 它使用此正则表达式来收集一组相关的日志文件。  

  - **静态日志组**：`<staticLogGroup>` 元素使用键属性定义显示在列表中的日志组的名称。 它还使用定义日志文件名的值属性。  

如果 `<componentLogGroup>` 元素和 `<staticLogGroup>` 元素内的 `<add/>` 元素中使用了相同的键属性值，则支持中心会创建一个组。 该组包括由使用相同键的两个元素定义的日志文件。

#### <a name="example"></a>示例
```XML
<logGroups>
  <componentLogGroup>
    <add key="Application Management" value="^(app.*|ci.*|contentaccess|contenttransfermanager|datatransferservice|dcm.*|execmgr.*|UserAffinity.*|.*Handler$|.*Provider$)"/>
    <add key="Client Registration" value="^(clientregistration|locationservices|ccmmessaging|ccmexec)"/>
    <add key="Inventory" value="^(ccmmessaging|inventoryagent|mtrmgr|swmtrreportgen|virtualapp|mtr.*|filesystemfile)"/>
    <add key="Policy" value="^(ccmmessaging|policyagent_.*|policyevaluator_.*)"/>
    <add key="Software Updates" value="^(ci.*|contentaccess|contenttransfermanager|datatransferservice|dcm.*|update.*|wuahandler|xmlstore|scanagent)"/>
    <add key="Software Distribution" value="^(datatransferservice|execmgr.*|contenttransfermanager|locationservices|contentaccess|filebits)"/>
    <add key="Desired Configuration Management" value="^(ci.*|dcm.*)"/>
    <add key="Operating System Deployment" value="^(ts.*)"/>
  </componentLogGroup>
  <staticLogGroup>
    <add key="Application Management" value="ccmsdkprovider.log"/>
    <add key="Desired Configuration Management" value="ccmsdkprovider.log"/>
    <add key="Software Updates" value="ccmsdkprovider.log"/>
  </staticLogGroup>
</logGroups>
```



## <a name="bkmk_wildcards"></a> 使用通配符收集额外的日志文件

要收集额外的日志文件，请在文件路径或文件名中使用通配符。 这些通配符包括系统范围的环境变量（如 `%WINDIR%`），但不包括用户范围的环境变量（如 `%USERPROFILE%`）。 若要使用非递归日志文件搜索收集额外的日志文件，请在 `<add/>` 元素中使用 `<additionalLogFiles>` 元素。 

以下示例演示支持中心如何在默认配置文件中使用此功能。

#### <a name="example-1-collect-all-windows-update-log-files-in-the-windows-directory"></a>示例 1：收集 Windows 目录中的所有 Windows 更新日志文件
以下元素收集在 Windows 目录中找到的任何名为 `WindowsUpdate.log` 的文件： 

`<add key="%WINDIR%\WindowsUpdate.log" />`

#### <a name="example-2-collect-all-log-files-in-the-windows-logs-directory"></a>示例 2：收集 Windows 日志目录中的所有日志文件
以下元素收集在 Windows 日志目录中找到的任何以 `.log` 结尾的文件： 

`<add key="%WINDIR%\logs\*.log" />`

#### <a name="full-example-xml"></a>完整的示例 XML
```XML
<CcmLogDataCollector>
  <additionalLogFiles>
    <!-- Collect these additional log files. Can pass in a wildcard for the filename. System variables are also supported. -->
    <!--
    <add key="%WINDIR%\WindowsUpdate.log" />
    <add key="%WINDIR%\logs\*.log" />
    -->
  </additionalLogFiles>
</CcmLogDataCollector>
```