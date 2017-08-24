---
title: "升级 macOS 客户端 - Configuration Manager | Microsoft Docs"
description: "在 System Center Configuration Manager 中升级 Mac 计算机上的客户端。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 74c60941-5eae-4905-9e58-252bdb39df96
caps.latest.revision: "10"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 502116b66fc14914ca0606ae416e82202824de7a
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-upgrade-clients-on-mac-computers-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中升级 Mac 计算机的客户端

*适用范围：System Center Configuration Manager (Current Branch)*

按照下面的高级步骤，使用 System Center Configuration Manager 应用程序升级 Mac 计算机上的客户端。 或者，你也可以下载 Mac 客户端安装文件，将其复制到 Mac 计算机上的共享网络位置或本地文件夹，然后指示用户手动运行安装。  

> [!NOTE]  
>  在执行这些步骤之前，请确保 Mac 计算机满足先决条件。 请参阅 [Mac 计算机支持的操作系统](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mac-computers)。  

## <a name="step-1-download-the-latest-mac-client-installation-file-from-the-microsoft-download-center"></a>步骤 1：从 Microsoft 下载中心下载最新的 Mac 客户端安装文件  
 Configuration Manager 安装媒体上未提供 Configuration Manager 的 Mac 客户端，必须从 Microsoft 下载中心下载。 Mac 客户端安装文件包含在名为 ConfigmgrMacClient.msi 的 Windows Installer 文件中。  

 可以从 [Microsoft Download Center（Microsoft 下载中心）](http://go.microsoft.com/fwlink/p/?LinkId=525184)下载此文件。  

## <a name="step-2-run-the-downloaded-installation-file-to-create-the-mac-client-installation-file"></a>步骤 2：运行下载的安装文件以创建 Mac 客户端安装文件  
 在运行 Windows 的计算机上，运行下载的“ConfigmgrMacClient.msi”  以解压缩名为“Macclient.dmg” 的 Mac 客户端安装文件。 默认情况下，在你解压缩文件之后，此文件可在 Windows 计算机上的“C:\Program Files (x86)\Microsoft\System Center 2012 Configuration Manager Mac Client”  文件夹中找到。  

## <a name="step-3-extract-the-client-installation-files"></a>步骤 3：提取客户端安装文件  
 将 Macclient.dmg 文件复制到网络共享或 Mac 计算机上的本地文件夹。 然后，从 Mac 计算机中装载并随后打开 Macclient.dmg 文件，并将文件复制到 Mac 计算机上的某个文件夹。  

## <a name="step-4-create-a-cmmac-file-that-can-be-used-to-create-an-application"></a>步骤 4：创建可用于创建应用程序的 .cmmac 文件  

1.  使用“CMAppUtil”  工具（位于 Mac 客户端安装文件的“Tools”  文件夹中）通过客户端安装包创建 .cmmac 文件。 该文件将用于创建 Configuration Manager 应用程序。  

2.  将新文件“CMClient.pkg.cmmac”复制到可供运行 Configuration Manager 控制台的计算机使用的位置。  

 有关详细信息，请参阅[为 Mac 计算机创建和部署应用程序的补充过程](/sccm/apps/get-started/creating-mac-computer-applications#supplemental-procedures-to-create-and-deploy-applications-for-mac-computers)。  

## <a name="step-5-create-and-deploy-an-application-containing-the-mac-client-files"></a>**步骤 5：**创建并部署包含 Mac 客户端文件的应用程序  

1.  在 Configuration Manager 控制台中，从包含客户端安装文件的“CMClient.pkg.cmmac”文件创建应用程序。  

2.  将此应用程序部署到层次结构中的 Mac 计算机。  

 有关详细信息，请参阅[使用 System Center Configuration Manager 创建 Mac 计算机应用程序](../../../../apps/get-started/creating-mac-computer-applications.md)。  

## <a name="step-6-users-install-the-latest-client"></a>步骤 6：用户安装最新的客户端  
 将向 Mac 客户端的用户发出提示，指出 Configuration Manager 客户端的更新可用并且必须安装。 用户安装客户端后，他们必须重启其 Mac 计算机。  

 计算机重启后，“计算机注册向导”将自动运行以请求新用户证书。  

 如果不希望使用 Configuration Manager 注册，而希望从 Configuration Manager 独立安装客户端证书，请参阅[配置已升级客户端以使用现有证书](#BKMK_UpgradingClient_MachineEnrollment)。  

##  <a name="BKMK_UpgradingClient_MachineEnrollment"></a> Configure the upgraded client to use an existing certificate  
 运行下列过程以防止“计算机注册向导”运行，并将升级后的客户端配置为使用现有客户端证书。  

-   在 Configuration Manager 控制台中，创建“Mac OS X”类型的配置项目。  

-   使用设置类型“脚本” 将设置添加到此配置项。  

-   将下列脚本添加到设置：  

    ```  
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

-   将配置项添加到配置基线，然后将该配置基线部署到独立 Configuration Manager 安装证书的所有 Mac 计算机。  

 有关如何为 Mac 计算机创建和部署配置项目的详细信息，请参阅[如何为使用 System Center Configuration Manager 客户端管理的 Mac OS X 设备创建配置项目](../../../../compliance/deploy-use/create-configuration-items-for-mac-os-x-devices-managed-with-the-client.md)和[如何在 System Center Configuration Manager 中部署配置基线](../../../../compliance/deploy-use/deploy-configuration-baselines.md)。  
