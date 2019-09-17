---
title: 升级 macOS 客户端
titleSuffix: Configuration Manager
description: 升级 Mac 计算机上的 Configuration Manager 客户端。
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 74c60941-5eae-4905-9e58-252bdb39df96
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b887a82afce8cf446494e7b9348a0b8c0718e389
ms.sourcegitcommit: cdf2827fb3f44d7522a9b533c115f910aa9c382a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2019
ms.locfileid: "70902571"
---
# <a name="how-to-upgrade-clients-on-mac-computers-in-configuration-manager"></a>如何在 Configuration Manager 中升级 Mac 计算机上的客户端

适用范围：  System Center Configuration Manager (Current Branch)

按照本文中的高级步骤，使用 Configuration Manager 应用程序升级 Mac 计算机上的客户端。 也可以下载 Mac 客户端安装文件，将其复制到 Mac 计算机上的共享网络位置或本地文件夹，然后指示用户手动运行安装。  

> [!NOTE]  
> 在执行这些步骤之前，请确保 Mac 计算机满足先决条件。 请参阅 [Mac 计算机支持的操作系统](/sccm/plan-design/configs/supported-operating-systems-for-clients-and-devices#mac-computers)。  

## <a name="download-the-latest-mac-client"></a>下载最新的 Mac 客户端

Configuration Manager 安装媒体上未提供适用于 Configuration Manager 的 Mac 客户端。 请从 [Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=47719)下载。 Mac 客户端安装文件包含在名为 ConfigmgrMacClient.msi 的 Windows Installer 文件中  。  

## <a name="create-the-mac-client-installation-file"></a>创建 Mac 客户端安装文件

在运行 Windows 的计算机上，运行 ConfigmgrMacClient.msi  。 此安装程序解压缩名为 Macclient.dmg 的 Mac 客户端安装文件  。 此文件默认位于以下文件夹中：C:\Program Files (x86)\Microsoft\System Center 2012 Configuration Manager Mac Client  。  

## <a name="extract-the-client-installation-files"></a>提取客户端安装文件

将 Macclient.dmg 复制到 Mac 计算机上  。 在 macOS 中装载 Macclient.dmg 文件，然后将内容复制到 Mac 计算机上的某个文件夹中。  

## <a name="create-a-cmmac-file"></a>创建 .cmmac 文件

1. 打开 Mac 客户端安装文件的“工具”文件夹  。 使用 CMAppUtil 工具来创建客户端安装包中的 .cmmac 文件  。 需要使用该文件来创建 Configuration Manager 应用程序。  

2. 将新文件“CMClient.pkg.cmmac”复制到可供运行 Configuration Manager 控制台的计算机使用的网络位置  。  

    有关详细信息，请参阅[为 Mac 计算机创建和部署应用程序的补充过程](/sccm/apps/get-started/creating-mac-computer-applications#supplemental-procedures-to-create-and-deploy-applications-for-mac-computers)。  

## <a name="create-and-deploy-the-app"></a>创建并部署应用

1. 在 Configuration Manager 控制台中，从“CMClient.pkg.cmmac”文件[创建应用程序](/sccm/apps/get-started/creating-mac-computer-applications)  。  

2. [将此应用程序部署](/sccm/apps/deploy-use/deploy-applications)到层次结构中的 Mac 计算机。  

## <a name="install-the-updated-client"></a>安装更新后的客户端

Mac 计算机上的现有 Configuration Manager 客户端将提示用户有更新可供安装。 用户安装客户端后，他们必须重启其 Mac 计算机。  

计算机重启后，“计算机注册”向导将自动运行以请求新用户证书  。

如果不使用 Configuration Manager 注册，而是从 Configuration Manager 独立安装客户端证书，请参阅[将客户端配置为使用现有证书](#BKMK_UpgradingClient_MachineEnrollment)。  

## <a name="BKMK_UpgradingClient_MachineEnrollment"></a> 将客户端配置为使用现有证书

使用此过程来防止“计算机注册向导”运行，并将升级后的客户端配置为使用现有客户端证书。  

1. 在 Configuration Manager 控制台中，[创建“Mac OS X”类型的配置项目](/sccm/compliance/deploy-use/create-configuration-items-for-mac-os-x-devices-managed-with-the-client)  。  

1. 使用设置类型“脚本”  将设置添加到此配置项。  

1. 将下列脚本添加到设置：  

  ``` Shell
  #!/bin/sh  
  echo "Starting script\n"  
  echo "Changing directory to MAC Client\n"  
  cd /Users/Administrator/Desktop/'MAC Client'/  
  echo "Import root cert\n"  
  /usr/bin/sudo /usr/bin/security import /Users/Administrator/Desktop/'MAC Client'/Root.pfx -A -k /Library/Keychains/System.Keychain -P ROOT  
  echo "Using openssl to convert pfx to a crt\n"  
  /usr/bin/sudo openssl pkcs12 -in /Users/Administrator/Desktop/'MAC Client'/Root.pfx -out Root1.crt -nokeys -clcerts -passin pass:ROOT  
  echo "Adding trust to root cert\n"  
  /usr/bin/sudo /usr/bin/security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.Keychain Root1.crt  
  echo "Import client cert\n"  
  /usr/bin/sudo /usr/bin/security import /Users/Administrator/Desktop/'MAC Client'/MacClient.pfx -A -k /Library/Keychains/System.Keychain -P MAC  
  echo "Executing ccmclient with MP\n"  
  sudo ./ccmsetup -MP https://SCCM34387.SCCM34387DOM.NET/omadm/cimhandler.ashx  
  echo "Editing Plist file\n"  
  sudo /usr/libexec/Plistbuddy -c 'Add:SubjectName string CMMAC003L' /Library/'Application Support'/Microsoft/CCM/ccmclient.plist  
  echo "Changing directory to CCM\n"  
  cd /Library/'Application Support'/Microsoft/CCM/  
  echo "Making connection to the server\n"  
  sudo open ./CCMClient  
  echo "Ending Script\n"  
  exit  
  ```  

1. 将配置项目添加到[配置基线](/sccm/compliance/deploy-use/create-configuration-baselines)。 然后[将配置基线部署](/sccm/compliance/deploy-use/deploy-configuration-baselines)到独立于 Configuration Manager 安装证书的所有 Mac 计算机。  
